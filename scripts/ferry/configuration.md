---
description: config.lua and config/*.lua — modules, access, helm rules, speeds, keys, ramps, cars on deck, seats, interior, languages
icon: sliders
---

# Configuration

| File | What it controls |
| --- | --- |
| `config.lua` | Modules, language, framework / target / notify / fuel / keys selection, who counts as staff, debug |
| `config/helm.lua` | Who may take the helm, top speed, acceleration, docking |
| `config/captain.lua` | The captain panel: keys, position, cruise speeds |
| `config/ramps.lua` | Ramp speed, the speed limit while a ramp is open, ramp keys, cables, sounds |
| `config/carry.lua` | Which cars ride along on the car deck, and when |
| `config/seats.lua` | Seat prompt or target, distances |
| `config/interior.lua` | Interior distance, doors, lights |
| `config/spawn.lua` | `/ferry`: ACE, water check, plates, ferries from spawn menus |
| `config/core.lua` | Scan rate and the interact key |
| `config/watchdog.lua` | When a ferry counts as sunk or capsized |
| `config/calmwater.lua` | Still water near a ferry (off by default) |
| `localization/<lang>.lua` | Every text players see |
| `hooks/*.lua` | Your own rules and reactions (see [For Developers](developers.md#hooks)) |
| `bridge/*.lua` | Framework, target, notify, text UI, fuel and keys adapters, with the `custom` functions |

All of these stay open under escrow. `data/*.json` is readable too, but it is built from the ferry's model: do not edit it. Restart `prompt_ferry` after editing (this removes the ferries in the world).

***

### Main settings

{% code title="config.lua" %}
```lua
Config.Modules = {
    spawn     = true,
    helm      = true,
    captain   = true,
    ramps     = true,
    carry     = true,
    seats     = true,
    interior  = true,
    aboard    = true,
    watchdog  = true,
    calmwater = false,
}
Config.language    = 'auto'
Config.framework   = 'auto'
Config.target      = 'auto'
Config.notify      = 'auto'
Config.textUI      = 'auto'
Config.fuel        = 'auto'
Config.vehiclekeys = 'auto'
Config.debug       = false
```
{% endcode %}

| Setting | Values |
| --- | --- |
| `Config.Modules.spawn` | `/ferry`, `/ferry_delete`, `ferry_del_all` and the `SpawnFerry` export |
| `Config.Modules.helm` | Taking the helm, the speed limit, docking |
| `Config.Modules.captain` | The captain panel and its cruise control |
| `Config.Modules.ramps` | The bow and stern ramps, their cables and sounds |
| `Config.Modules.carry` | Empty cars on the car deck ride along held in place |
| `Config.Modules.seats` | The 94 seats |
| `Config.Modules.interior` | The bridge, lounge and cabins, the doors, the lights |
| `Config.Modules.aboard` | Players standing on the ferry are not knocked over by its motion |
| `Config.Modules.watchdog` | A sunk or capsized ferry is put back upright, a damaged one repaired |
| `Config.Modules.calmwater` | Still sea for players near a ferry. Off: it calms the whole sea for that player, which looks wrong away from the ferry |
| `Config.language` | `auto` (follows `setr ox:locale "xx"`) or `en` `de` `es` `fr` `ru` `pt` `sv` `no` `fi` `ar` `ko` `zh` |
| `Config.framework` | `auto` \| `qbox` \| `qbcore` \| `esx` \| `standalone` \| `custom`. `auto` checks `qbx_core`, `qb-core`, `es_extended` |
| `Config.target` | `auto` \| `ox_target` \| `qb-target` \| `none` \| `custom`. Only the seats use it, and only with `Config.Seats.interaction = 'auto'` and `ox_target` |
| `Config.notify` | `auto` \| `ox_lib` \| `qb` \| `esx` \| `native` \| `custom`. `auto` uses qb-core's notify on qb-core and qbox, ESX's on ESX, else `ox_lib` if it runs, else the GTA feed |
| `Config.textUI` | `auto` \| `ox_lib` \| `qb` \| `native` \| `custom`. The `Take the helm` and `Sit down` prompts |
| `Config.fuel` | `auto` \| `ox_fuel` \| `LegacyFuel` \| `cdn-fuel` \| `ps-fuel` \| `lc_fuel` \| `none` \| `custom`. The ferry is kept full through it; `none` = only the game's own fuel level |
| `Config.vehiclekeys` | `auto` \| `qbx_vehiclekeys` \| `qb-vehiclekeys` \| `qs-vehiclekeys` \| `wasabi_carlock` \| `MrNewbVehicleKeys` \| `Renewed-Vehiclekeys` \| `vehicles_keys` \| `cd_garage` \| `okokGarage` \| `none` \| `custom` |
| `Config.debug` | Verbose console for every module, plus `/ferry_test`. Keep `false` on a live server |
| `Config.Debug` | Console logging for one module (`core`, `spawn`, `helm`, `captain`, `ramps`, `carry`, `seats`, `interior`, `aboard`, `watchdog`, `calmwater`) without turning on `Config.debug` |
| `Config.debugZones` | Draws target zone outlines in the world. Keep `false` |

A module that is off registers nothing: no prompts, no threads, and its exports do not exist.

***

### Access

Two settings decide who may do what: `Config.access` says who counts as **staff**, and `Config.Helm.access` says who may take a ferry's **helm**.

{% code title="config.lua" %}
```lua
Config.access = {
    jobs          = {},              -- jobs that count as staff, e.g. { 'ferry' }
    minGrade      = 0,
    requireOnDuty = false,           -- qbox / qb-core
    ace           = 'ferry.access',  -- this ACE makes a player staff on every framework
    showcase      = false,
}
```
{% endcode %}

{% code title="config/helm.lua" %}
```lua
Config.Helm = {
    access   = 'keys',               -- 'keys' | 'staff' | 'everyone'
    giveKeys = true,
    ...
}
```
{% endcode %}

| `Config.Helm.access` | Who may take the helm |
| --- | --- |
| `keys` | Players with keys to that ferry, when a keys script runs. Without one: the player who spawned that ferry. Staff always may |
| `staff` | Staff only |
| `everyone` | Any player who walks up to the wheel |

* **Staff** are players with one of `jobs` at `minGrade` or higher (and on duty, with `requireOnDuty`), or players with the ACE `ferry.access`. On a standalone server only the ACE counts.
* **`giveKeys = true`** gives keys to a player who takes the helm and to the player who spawns a ferry, when a keys script runs.
* **Spawning** has its own ACE: `command.ferry` for `/ferry` and `/ferry_delete`, `command.ferry_del_all` for `ferry_del_all` (see [Spawn](#spawn)).
* **`showcase = true`** lets everyone do everything: spawn and delete ferries, take any helm, run `ferry_debugdump`. For filming and demos only. The server console warns about it at every start.
* Your own rules go into the hooks (see [For Developers](developers.md#hooks)), and another script can set the rule for one ferry with the `SetHelmAccess` export.

{% code title="server.cfg — examples" %}
```
add_ace group.admin ferry.access allow          # admins may take any helm
add_ace group.admin command.ferry allow         # admins may use /ferry and /ferry_delete
add_ace group.admin command.ferry_del_all allow
add_ace group.admin command.ferry_debugdump allow
```
{% endcode %}

***

### Helm

{% code title="config/helm.lua" %}
```lua
Config.Helm = {
    access        = 'keys',
    giveKeys      = true,
    checkMs       = 2000,
    parkMaxSpeed  = 1.0,
    distance      = 1.6,
    maxSpeed      = 15.0,
    acceleration  = 1.7,
    parkDeckDelay = 500,
}
```
{% endcode %}

| Setting | Default | What |
| --- | --- | --- |
| `checkMs` | `2000` | How often the server checks who sits at each helm. A driver who may not steer is put out of the seat |
| `parkMaxSpeed` | `1.0` | Docking is refused above this speed, m/s |
| `distance` | `1.6` | Metres from the helm seat for the `Take the helm` prompt |
| `maxSpeed` | `15.0` | Top speed, m/s (15 = 54 km/h). Turning circle at full speed: 194 m |
| `acceleration` | `1.7` | Most the ferry speeds up per second, m/s (standstill to 15 m/s in about 9 s) |
| `parkDeckDelay` | `500` | Docking and undocking first hold the cars on the car deck, then switch the ferry this many ms later |

***

### Captain panel

{% code title="config/captain.lua" %}
```lua
Config.Captain = {
    panelKey  = 'G',
    cursorKey = 'GRAVE',          -- the ~ key
    position  = 'top',            -- 'top' or 'bottom' middle of the screen
    offset    = 22,               -- px from that edge
    ahead     = { 5.0, 10.0, 15.0 },
    astern    = { 2.0, 3.5, 5.0 },
}
```
{% endcode %}

* `ahead` and `astern` are the cruise speeds in m/s for SLOW, HALF and FULL. `Config.Helm.maxSpeed` still caps them.
* Move the panel with `position` and `offset` if your HUD has something in that spot.

***

### Keys

The defaults below are what a player gets the first time they join. After that the binding is theirs: players change it in **Settings > Key Bindings > FiveM**, and changing a default here does not change it for players who already have it.

| Setting | Default | What |
| --- | --- | --- |
| `Config.Core.interactKey` | `E` | Take the helm, sit, stand up |
| `Config.Captain.panelKey` | `G` | Show / hide the captain panel |
| `Config.Captain.cursorKey` | `GRAVE` (~) | The panel's mouse |
| `Config.Ramps.keys.bowDown` / `bowUp` | `LBRACKET` / `RBRACKET` | Lower / raise the bow ramp (hold) |
| `Config.Ramps.keys.sternDown` / `sternUp` | `END` / `HOME` | Lower / raise the stern ramp (hold) |

{% hint style="warning" %}
For the ramp keys, pick keys GTA has an icon for, or the help box shows a blank: letters, digits, `[` `]` `.`, the arrows, Home and End work. Page Up / Down, Insert, Delete and the comma show nothing.
{% endhint %}

***

### Ramps

{% code title="config/ramps.lua" %}
```lua
Config.Ramps = {
    speed            = 12.0,
    rateMs           = 100,
    maxDroop         = 10.0,
    maxSpeed         = 2.0,
    drawDistance     = 400.0,
    fullRateDistance = 150.0,
    soundDistance    = 80.0,
    moveSound = { ambientBank = 'Crane', set = 'CRANE_SOUNDS', name = 'Move_U_D', speed = 0.9 },
    keys = { bowDown = 'LBRACKET', bowUp = 'RBRACKET', sternDown = 'END', sternUp = 'HOME' },
    cables = { enabled = true, distance = 150.0, detailDistance = 30.0 },
}
```
{% endcode %}

| Setting | Default | What |
| --- | --- | --- |
| `speed` | `12.0` | How fast a ramp moves, degrees per second |
| `maxDroop` | `10.0` | Lowest position, degrees below level. The ground usually stops the ramp first |
| `maxSpeed` | `2.0` | The ferry's speed limit while any ramp is open, m/s. Lowering needs the ferry below this + 0.5 |
| `drawDistance` | `400.0` | Players farther away get no ramp prop |
| `fullRateDistance` | `150.0` | A moving ramp updates every frame within this, 4 times a second beyond it |
| `soundDistance` | `80.0` | Players within this hear the ramp motor and the stop clunk |
| `moveSound` | the dock crane hoist | The game sound played while a ramp moves |
| `cables.enabled` | `true` | The steel ropes from the posts to the ramp ends. `false` = no ropes |
| `cables.distance` | `150.0` | Players within this see the ropes |
| `cables.detailDistance` | `30.0` | Within this the detailed rope is used, farther a lighter one that looks the same at that range |
| `rateMs` | `100` | Server: one ramp request per player and ramp every this many ms |

***

### Cars on the car deck

{% code title="config/carry.lua" %}
```lua
Config.Carry = {
    stillSpeed      = 0.5,
    stillChecks     = 2,
    deck            = { halfWidth = 8.0, halfLength = 33.0, zMin = 0.5, zMax = 3.5 },
    checkRadius     = 50.0,
    recarryBlockMs  = 10000,
    seatReach       = 4.5,
    settleMs        = 750,
    releaseReach    = 10.0,
    offsetTolerance = 2.0,
    offsetLag       = 0.25,
    types = { automobile = true, bike = true, trailer = true, amphibious_automobile = true, amphibious_quadbike = true },
    rateMs          = 1000,
    retryMs         = 10000,
}
```
{% endcode %}

| Setting | Default | What |
| --- | --- | --- |
| `stillSpeed`, `stillChecks` | `0.5`, `2` | A car is held once it moves slower than 0.5 m/s against the ferry for 2 seconds in a row |
| `deck` | | The car deck in metres from the ferry's centre. The ramps are not part of it |
| `types` | cars, bikes, trailers, amphibious | Vehicle types that may be held. Set one to `false` to leave that type loose |
| `recarryBlockMs` | `10000` | A car someone got into is not held again for this long, so the get-in animation can finish |
| `seatReach` | `4.5` | Scripted ferries only: how close a player must be for **F** to put them straight into a held car. On a ferry a player steers, **F** lets the car go as usual |
| `settleMs` | `750` | A car that was just let go is kept moving with the deck for this many ms (or until its driver gives gas or brakes) |
| `checkRadius`, `releaseReach` | `50.0`, `10.0` | Server checks: how far a held car may be from its ferry, and how close a player must be to let one go |
| `offsetTolerance`, `offsetLag` | `2.0`, `0.25` | Server check on where a car is held: metres of tolerance, plus this many seconds of the ferry's travel |
| `rateMs`, `retryMs` | `1000`, `10000` | Request limits |

***

### Seats

{% code title="config/seats.lua" %}
```lua
Config.Seats = {
    interaction   = 'prompt',     -- 'prompt' | 'auto'
    distance      = 1.2,
    scanDistance  = 60.0,
    standOffset   = 0.6,
    claimReach    = 4.0,
    rateMs        = 500,
    sweepMs       = 5000,
    sweepDistance = 5.0,
    anim = { dict = 'amb@prop_human_seat_chair@male@generic@base', clip = 'base' },
}
```
{% endcode %}

| Setting | Default | What |
| --- | --- | --- |
| `interaction` | `'prompt'` | `prompt` = a `Sit down` prompt at the nearest free seat. `auto` = `ox_target` options on the seats when `ox_target` runs, else the prompt. `qb-target` cannot place options on a moving ship's seats |
| `distance` | `1.2` | Metres from a seat for the prompt |
| `scanDistance` | `60.0` | Players within this of a ferry look for seats |
| `standOffset` | `0.6` | Metres in front of the seat where a player stands up |
| `claimReach`, `sweepMs`, `sweepDistance` | `4.0`, `5000`, `5.0` | Server checks: a player must be within 4 m to sit, and a seat whose player left or is more than 5 m away is freed every 5 s |
| `anim` | the chair sit | The sitting clip. The seat positions were made for this clip: another one sits players off the seat |

***

### Interior

{% code title="config/interior.lua" %}
```lua
Config.Interior = {
    distance = 150.0,
    props = { 'prompt_ferry_int1', 'prompt_ferry_int2', 'prompt_ferry_int3', 'prompt_ferry_int4', 'prompt_ferry_lights' },
    doors = { openDistance = 2.0, swingTime = 0.6 },
    lights = {
        models = { 'prompt_ferry_lights' },
        astern = { prompt_ferry_lights = 'prompt_ferry_lights_astern' },
        intervalMs = 100,
    },
}
```
{% endcode %}

| Setting | Default | What |
| --- | --- | --- |
| `distance` | `150.0` | Players within this of a ferry get the interior and the detailed model |
| `props` | | The interior pieces. Leave the list as it is |
| `doors.openDistance` | `2.0` | A door opens while a player is within this many metres of it |
| `doors.swingTime` | `0.6` | Seconds a door takes to open or close |
| `lights.intervalMs` | `100` | On a moving ferry the lights are kept up with the ferry this often, for players near it. Without it, lights you looked away from stay behind and are dark when you look back |
| `lights.astern` | | The light set used while a script runs the ferry stern-first (`SetLightsAstern`). A ferry players drive keeps the normal lights |

The hours the lights are on are built into the light model.

***

### Spawn

{% code title="config/spawn.lua" %}
```lua
Config.Spawn = {
    model             = 'prompt_ferry',
    ace               = 'command.ferry',
    spawnTimeout      = 5000,
    deleteDistance    = 100.0,
    waterCheck        = true,
    minDepth          = 4.0,
    adoptClientSpawns = true,
    plate             = 'FERRY%03d',
}
```
{% endcode %}

| Setting | Default | What |
| --- | --- | --- |
| `ace` | `command.ferry` | Who may run `/ferry` and `/ferry_delete`. The server console always may |
| `deleteDistance` | `100.0` | `/ferry_delete` removes the nearest ferry within this many metres |
| `waterCheck`, `minDepth` | `true`, `4.0` | A player's `/ferry` needs this many metres of water under the spot. The console is not checked |
| `adoptClientSpawns` | `true` | Ferries spawned by client-side scripts (spawn menus) are taken over like any ferry. `false` removes them at once. Garages that spawn on the server always work |
| `plate` | `FERRY%03d` | Plate of ferries from `/ferry` and `SpawnFerry`: `FERRY001`, `FERRY002` … (8 characters, no spaces). The number carries on across restarts, so a new ferry never gets the plate of an old one someone still holds keys to |
| `spawnTimeout` | `5000` | ms to wait for the spawn before giving up |
| `model` | `prompt_ferry` | The ferry's vehicle model. Leave it |

***

### Watchdog, core and calm water

| Setting | Default | What |
| --- | --- | --- |
| `Config.Watchdog.belowWater` | `3.0` | The ferry counts as sunk when it is this many metres under the water level… |
| `Config.Watchdog.sinkChecks` | `10` | …for this many seconds in a row (a storm wave passing over the hull is not sinking) |
| `Config.Watchdog.capsize` | `60.0` | Pitch or roll beyond this many degrees: the ferry is put upright |
| `Config.Core.scanMs` | `1000` | How often each player's game looks for ferries near it, ms |
| `Config.Core.idleScanMs` | `2000` | The same while no ferry is near |
| `Config.CalmWater.distance` | `500.0` | With the `calmwater` module on: players within this of a ferry get still water |

***

### Languages

Twelve languages ship in `localization/`: English, German, Spanish, French, Russian, Portuguese, Swedish, Norwegian, Finnish, Arabic, Korean and Chinese. `Config.language = 'auto'` follows your `ox:locale` convar; any key missing from a language falls back to English.

To change a text, edit it in `localization/<language>.lua`. To add a language, copy `en.lua` to `<code>.lua`, translate the values and set `Config.language` to that code. Save the files as UTF-8. Debug output in the console is always English.
