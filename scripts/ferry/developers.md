---
description: Hooks (gate and react), server exports, scripted ferries, events, state bags, commands and the custom bridges
icon: code
---

# For Developers

Everything here works without touching the protected files. Rules and reactions go into the open hook files, other resources spawn and drive ferries through the exports, and your own framework, keys, fuel, notify or text UI plugs in through the open `bridge/` files.

***

### Hooks

Hook files live in `hooks/`. They are created from the `.example.lua` templates on the first start and are never overwritten by updates. Each file returns a Lua table. Restart the resource after editing.

| File | Role |
| --- | --- |
| `hooks_server.lua` | Decides. Every ferry gate and reaction runs on the server |
| `hooks_shared.lua` | Loaded on both sides and checked together with `hooks_server.lua`. Only use data both sides can see (statebags, the `ctx` fields) |
| `hooks_client.lua` | Loaded on each player's game. The ferry runs no hooks on the client, so leave it empty and put your rules in `hooks_server.lua` |

* Gates (`can*`) return `false` to block; `nil` or `true` allows. They come on top of the ferry's own checks: a gate can take a permission away, never give one.
* Handlers go under `global` (every id) or `entries['<id>']` (one id). The `global` handler, the `entries` handler and the shared file must all allow an action.
* Every handler runs in `pcall` and fails open: a broken hook prints `hook error in <feature>.<id>.<event>` in the console and never blocks or stops the resource.

| Feature | id | Gates | Reactions | ctx |
| --- | --- | --- | --- | --- |
| `spawn` | `spawn` | `canSpawn` | `onSpawn` | `source, coords` (+ `ferry` in `onSpawn`) |
| `spawn` | `delete` | `canDelete` | `onDelete` | `source, ferry` |
| `helm` | the ferry's id (state bag `ferryId`) | `canOperate` | `onStart`, `onEnd` | `source, ferry` |
| `helm` | `park` | `canPark` | `onPark`, `onSail` | `source, ferry` |
| `ramps` | `bow`, `stern` | `canOperate` | `onStart`, `onEnd` | `source, ferry, ramp, dir` |
| `seats` | the seat number, `1` … `94` | `canUse` | `onStart`, `onEnd` | `source, ferry, seat` |
| `carry` | the ferry's id (state bag `ferryId`) | `canCarry` | `onStart`, `onEnd` | `source, ferry, car` |

`ferry` and `car` are vehicle entities on the server. `source` is the player, or `0` for the server console and for the exports.

#### When they fire

| Event | Fires |
| --- | --- |
| `spawn.canSpawn` / `onSpawn` | `/ferry`, before the water check / after the ferry is in the world. Not for the `SpawnFerry` export |
| `spawn.canDelete` / `onDelete` | `/ferry_delete`, for each ferry it would remove / after removing it (`ctx.ferry` no longer exists then). Not for `ferry_del_all` or `DeleteFerry` |
| `helm.canOperate` | When a player takes the helm, and when a player turns up in the driver seat some other way. `false` = the prompt does not show, and a seated driver is put out. Not asked in showcase mode or for a ferry with `SetHelmAccess(ferry, 'none')` |
| `helm.onStart` / `onEnd` | A player took the helm at the wheel / is no longer at it (noticed within `Config.Helm.checkMs`) |
| `helm.canPark` | Docking or undocking, from the panel, `/ferry_park` or the `SetParked` export |
| `helm.onPark` / `onSail` | The ferry is now docked / free to sail |
| `ramps.canOperate` | Every ramp move: `dir` = `down`, `up` or `stop`. Also for the `SetRamp` export |
| `ramps.onStart` / `onEnd` | A move was accepted / the ramp reached the end of its move |
| `seats.canUse` / `onStart` / `onEnd` | Sitting down / sat down / stood up or left |
| `carry.canCarry` / `onStart` | A car is about to be held / is now held. `source` is the player whose game found the car (the ferry's owner) |
| `carry.onEnd` | A player's game let a held car go: someone got in, or a scripted ferry docked. `source` is that player. Not for the `ReleaseCar` export, or a car let go because it or its ferry is gone |

#### Examples

{% tabs %}
{% tab title="Dock only in the harbour" %}
```lua
-- hooks/hooks_server.lua
return {
    helm = {
        global = {},
        entries = {
            ['park'] = {
                canPark = function(ctx)
                    local c = GetEntityCoords(ctx.ferry)
                    return c.x > -1000.0 and c.x < -700.0 and c.y > -3000.0 and c.y < -2600.0
                end,
            },
        },
    },
}
```
{% endtab %}

{% tab title="Ramps for on-duty crew" %}
```lua
-- hooks/hooks_server.lua
return {
    ramps = {
        global = {
            canOperate = function(ctx)
                if ctx.source == 0 then return true end      -- scripts (SetRamp) always may
                return Player(ctx.source).state.onDuty == true
            end,
        },
    },
}
```
{% endtab %}

{% tab title="Log the crossings" %}
```lua
-- hooks/hooks_server.lua
return {
    helm = {
        global = {
            onStart = function(ctx)
                print(('%s took the helm of ferry %s'):format(GetPlayerName(ctx.source), Entity(ctx.ferry).state.ferryId))
            end,
        },
        entries = {
            ['park'] = {
                onPark = function(ctx) print(('ferry docked at %s'):format(GetEntityCoords(ctx.ferry))) end,
            },
        },
    },
}
```
{% endtab %}
{% endtabs %}

***

### Exports

Server, `exports.prompt_ferry`. An export exists only while its module is on (see [Main settings](configuration.md#main-settings)).

| Export | Returns / does |
| --- | --- |
| `SpawnFerry(x, y, z, heading, opts)` | Spawns a ferry and returns `vehicle, netId`, or `nil`. `opts.owner` = a server id: that player may take the helm under the `keys` rule and gets keys when `Config.Helm.giveKeys` is on; `opts.bucket` = a routing bucket. No water check, no hooks |
| `DeleteFerry(ferry)` | Removes a ferry. `true` when it was one. No hooks |
| `GetFerries()` | Every ferry in the world: `{ vehicle, ... }` |
| `IsFerry(vehicle)` | `true` for a ferry |
| `GetFerryId(ferry)` | The ferry's own id (state bag `ferryId`), a string. Unlike the network id it is never reused |
| `SetHelmAccess(ferry, policy)` | The helm rule for this ferry: `'everyone'`, `'keys'`, `'staff'`, or `'none'` (nobody, see [Scripted ferries](#scripted-ferries)). `nil` = `Config.Helm.access` again |
| `CanOperate(src, ferry)` | `ok, reasonKey`: may this player take that ferry's helm |
| `SetParked(ferry, parked)` | `ok, reasonKey`: docks (`true`) or undocks (`false`), like the panel's Dock button. Refused above `Config.Helm.parkMaxSpeed` (`'helm_too_fast_dock'`) and while a dock or undock is already under way. Takes effect `Config.Helm.parkDeckDelay` ms later |
| `IsParked(ferry)` | `true` while docked |
| `SetSpeedCap(ferry, mps)` | This ferry's top speed, 1 to 60 m/s, instead of `Config.Helm.maxSpeed`. `nil` = the config value again. The ramp limit and the cruise control still apply on top |
| `SetRamp(ferry, which, dir)` | `'bow'` or `'stern'`, `'down'` (stops on the ground) or `'up'`, from where the ramp is now. `false` when refused (lowering above `Config.Ramps.maxSpeed` + 0.5, or a `canOperate` hook) |
| `SetLightsAstern(ferry, astern)` | `true` turns the bridge projector to shine astern, for a ferry that sails stern-first. `false` puts it back |
| `SetDoorsLocked(ferry, names, locked)` | The named interior doors stay shut for everyone on this ferry (`true`), or open for players again (`false`). `names` is a list of door names (below) |
| `GetSeatOccupant(ferry, seat)` | The server id of the player in that seat, or `nil` |
| `IsCarried(car)` | `true` while a car is held on a car deck |
| `GetCarriedCars(ferry)` | The cars held on that ferry: `{ vehicle, ... }` |
| `ReleaseCar(car)` | Lets a held car go. `false` when it was not held |

`reasonKey` is a key in `localization/<lang>.lua`: show it with your own notify, or ignore it.

<details>
<summary>Door names for SetDoorsLocked (data/doors.json, field source)</summary>

* Toilet doors: `Prop_Ch_Toilet_Door_Flat`, `Prop_Ch_Toilet_Door_Flat.002`, `Prop_Ch_Toilet_Door_Flat.003`, `Prop_Ch_Toilet_Door_Flat.004`
* Roof doors: `Prop_VW_Roof_Door_01a.001`, `Prop_VW_Roof_Door_01a.002`
* Ship doors, left leaves: `SM_dima_ship_door_l`, `SM_dima_ship_door_l.001`, `SM_dima_ship_door_l.002`
* Ship doors, right leaves: `SM_dima_ship_door_r`, `SM_dima_ship_door_r.001`, `SM_dima_ship_door_r.002`

</details>

```lua
-- server: spawn a ferry for a player in their routing bucket, at most 10 m/s
local ferry = exports.prompt_ferry:SpawnFerry(-1800.0, -1250.0, 0.0, 140.0, { owner = src, bucket = GetPlayerRoutingBucket(src) })
if ferry then exports.prompt_ferry:SetSpeedCap(ferry, 10.0) end
```

The ferry has no client exports.

***

### Scripted ferries

A ferry your own script sails (an automatic ferry line, a tour, an event) should not be taken over by players. `SetHelmAccess(ferry, 'none')` marks it as scripted:

* Nobody may take its helm: not staff, not in showcase mode. The `helm.canOperate` hook is not asked.
* Held cars stay held until the ferry has docked, also with people in them. **F** within `Config.Carry.seatReach` of a held car puts a player straight into a free seat, and **F** inside puts them out beside it. GTA's own get-in pushes a car around on a moving deck, and a car let go before the ferry is docked can be thrown.
* With nobody at the helm, the game of the player who owns the ferry stops a lowering ramp where it touches the ground, and a rising one on a car.
* The state bag `ferryScripted` is `true`.

prompt_ferry does not move a ferry by itself: steering it is your script's job. The exports do the rest:

```lua
local ferry = exports.prompt_ferry:SpawnFerry(x, y, 0.0, heading)
exports.prompt_ferry:SetHelmAccess(ferry, 'none')

-- at the quay (the ferry slower than 1 m/s)
exports.prompt_ferry:SetParked(ferry, true)
exports.prompt_ferry:SetRamp(ferry, 'bow', 'down')

-- before leaving
exports.prompt_ferry:SetRamp(ferry, 'bow', 'up')
exports.prompt_ferry:SetParked(ferry, false)

-- a leg sailed stern-first
exports.prompt_ferry:SetLightsAstern(ferry, true)
```

***

### Events

Server, local events (listen with `AddEventHandler` in another server resource):

| Event | Arguments | When |
| --- | --- | --- |
| `ferry:spawned` | `ferry, netId, ferryId` | A ferry was taken over, however it was spawned (`/ferry`, `SpawnFerry`, a garage, a spawn menu) |
| `ferry:removed` | `ferry, ferryId` | A ferry left the world (deleted, put in a garage, despawned) |

```lua
AddEventHandler('ferry:spawned', function(ferry, netId, ferryId)
    print(('ferry %s is in the world (net %d, plate %s)'):format(ferryId, netId, GetVehicleNumberPlateText(ferry)))
end)
```

***

### State bags

Read them with `Entity(ferry).state.<name>` on either side. They are set by the ferry: do not write them.

| On | State bag | Value |
| --- | --- | --- |
| ferry | `ferryId` | The ferry's own id (`GetFerryId`) |
| ferry | `ferryParked` | `true` while docked |
| ferry | `ferryRamps` | `{ bow = { a, to, id }, stern = { ... } }`: the angle a move started at and its target, degrees down from closed (`0` = closed) |
| ferry | `ferrySeats` | `{ ['<seat>'] = server id }` |
| ferry | `ferryScripted` | `true` after `SetHelmAccess(ferry, 'none')` |
| ferry | `ferrySpeedCap` | The `SetSpeedCap` value, m/s |
| ferry | `ferryAstern` | `true` after `SetLightsAstern(ferry, true)` |
| ferry | `ferryDoorsLocked` | `{ ['<door name>'] = true }` |
| car | `ferryCarry` | Set while the car is held on a car deck |

***

### Commands

| Command | Who | What |
| --- | --- | --- |
| `/ferry [x y z [heading]]` | Server console, ACE `command.ferry` | Spawns a ferry where you stand, or at the coordinates |
| `/ferry_delete` | Server console, ACE `command.ferry` | Removes the nearest ferry within `Config.Spawn.deleteDistance`. From the console: every ferry |
| `ferry_del_all` | Server console, ACE `command.ferry_del_all` | Removes every ferry |
| `/ferry_ramp bow` \| `stern` | The player at the helm | Sends that ramp all the way down, or up when it is open |
| `/ferry_park` | The player at the helm | Docks or undocks, like the panel's Dock button |
| `/ferry_info` | Everyone | Bridge, module and language report: your side in F8, the server side in the server console |
| `ferry_debugdump` | Server console, ACE `command.ferry_debugdump` | The support snapshot (see [Troubleshooting](troubleshooting.md#support-dump)) |
| `/ferry_test notify` \| `ui` \| `target` | `Config.debug = true` | Bridge self-tests: a notification, a text UI line, a target zone at your feet |

With `Config.access.showcase = true` every player may run the ACE commands.

***

### Custom bridges

Each `custom` value calls functions you define in the open `bridge/` files.

**Framework** (`Config.framework = 'custom'`), in `bridge/framework.lua`:

```lua
-- server: used for Config.access (staff by job)
function CustomGetJob(src) return { name = 'police', grade = 0, onDuty = true } end
function CustomGetName(src) return 'John Doe' end
-- client: shown by /ferry_info
function CustomGetJobClient() return { name = 'police', grade = 0, onDuty = true } end
```

**Vehicle keys** (`Config.vehiclekeys = 'custom'`), in `bridge/vehiclekeys.lua` (server):

```lua
function CustomHasKeys(src, veh, plate) return exports['my_keys']:HasKey(src, plate) end
function CustomGiveKeys(src, veh, plate) exports['my_keys']:GiveKey(src, plate) end
```

**Fuel** (`Config.fuel = 'custom'`), in `bridge/fuel.lua` (client):

```lua
function CustomSetFuel(veh, level) exports['my_fuel']:SetFuel(veh, level) end
```

**Notifications** (`Config.notify = 'custom'`), in `bridge/notify.lua` (client):

```lua
-- opts = { title?, description, type = 'inform' | 'success' | 'error', duration? }
function CustomNotify(opts) exports['my_hud']:Notify(opts.description, opts.type) end
```

**Text UI** (`Config.textUI = 'custom'`), in `bridge/textui.lua` (client), for the `Take the helm` and `Sit down` prompts:

```lua
function CustomShowUI(text) exports['my_ui']:Show(text) end
function CustomHideUI() exports['my_ui']:Hide() end
```
