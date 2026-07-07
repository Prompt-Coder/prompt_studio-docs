# 🏭 Bilgeco HQ & Warehouse

### Logistics & Warehouse (+ warehouse script)

{% embed url="https://portal.cfx.re/assets/granted-assets?direction=asc&page=1&search=Prompt%27s+-+Bilgeco+Corporation&sort=asset.updated_at" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**
{% endembed %}

{% embed url="https://youtu.be/Wbptp_lOSr4" %}

{% embed url="https://youtu.be/naf0o4BcGXI" %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### <i class="fa-download" style="color:$warning;">:download:</i> Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Bilgeco+Corporatio).

After downloading, **you will get a folder named:**

```
prompt_logistics_corp
```

Drag and drop the downloaded folder inside your resources directory.\
When done, the full path should look like this:

<pre><code><strong>resources/prompt_logistics_corp
</strong></code></pre>
{% endstep %}

{% step %}
#### <i class="fa-folder-open" style="color:$warning;">:folder-open:</i> Open your `server.cfg` and add this line:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_logistics_corp
</strong></code></pre>

Save the file once done.
{% endstep %}

{% step %}
#### <i class="fa-gear-code" style="color:$warning;">:gear-code:</i> Config

**Open `config.lua`** and adjust settings to your liking [#configuration](bilgeco-hq-and-warehouse.md#configuration "mention").  Framework is **auto-detected** (QBCore, QBox, ESX). No extra setup needed unless you use a custom money system.
{% endstep %}

{% step %}
#### <i class="fa-bottle-baby" style="color:$warning;">:bottle-baby:</i> Install Depencencies



| Dependency          | Required | Notes                                                                                           |
| ------------------- | -------- | ----------------------------------------------------------------------------------------------- |
| `ox_lib`            | Yes      | Required in `shared_scripts`. Powers elevators, text UI, and interaction zones.                 |
| `ox_target`         | No       | Optional targeting system. Auto-detected. Falls back to E-key / `lib.zones.box` if not present. |
| `qb-target`         | No       | Alternative targeting system. Auto-detected via `Config.interactionMode`.                       |
| QBCore / QBox / ESX | No       | For payment and job restriction. Auto-detected. Standalone also supported.                      |
{% endstep %}

{% step %}
#### <i class="fa-repeat" style="color:$warning;">:repeat:</i>  **Restart your server** and verify both locations:

| Location          | Coordinates                 |
| ----------------- | --------------------------- |
| **Main Building** | `-1015.06, -2145.97, 13.42` |
| **Warehouse**     | `-1098.4, -2068.99, 15.59`  |

If both interiors appear, installation is complete ✅\
[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***



### <i class="fa-gear-code" style="color:blue;">:gear-code:</i> Configuration

<details>

<summary>Payment &#x26; Framework</summary>

Framework is auto-detected on startup. Force one manually if needed.

```lua
Config.framework       = 'auto'       -- 'auto' | 'qbcore' | 'qbox' | 'esx' | 'standalone'
Config.moneyType       = 'bank'       -- 'bank' | 'cash'
Config.currencySymbol  = '$'
Config.moneySystem     = 'auto'       -- 'auto' | 'bigdaddy' | 'custom'
Config.okokBankingLogs = 'auto'       -- 'auto' | true | false

Config.money = {
    enabled           = true,
    payPerBoxPackaged = 10,       -- paid per box packed
    payPerPalletMoved = 75,       -- paid per forklift delivery
}
```

</details>

<details>

<summary>Job Restriction</summary>

Gate the job behind a framework job check. Disabled by default.

```lua
Config.jobRestriction = {
    enabled       = false,        -- set true to require a job
    jobName       = 'logistics',  -- must match your framework's job name
    requireOnDuty = false,        -- QBCore/QBox only
}
```

</details>

<details>

<summary>Box Economy</summary>

```lua
Config.economy = {
    mode            = 'infinite', -- 'infinite' | 'limited'
    maxStockPerType = 20,         -- cap per product type (limited only)
}
```

| Mode       | Behaviour                                                                                                |
| ---------- | -------------------------------------------------------------------------------------------------------- |
| `infinite` | Workers can always pack. No cap. Default.                                                                |
| `limited`  | Each product type caps at `maxStockPerType`. Packing blocked when full. Frees up as boxes are collected. |

</details>

<details>

<summary>Interaction &#x26; UI</summary>

```lua
Config.interactionMode = 'auto'    -- 'auto' | 'ox_lib' | 'ox_target' | 'qb-target'
Config.textUI          = 'default' -- 'default' | 'ox_lib' | 'qb-drawtext' | 'custom'
```

| Setting           | Effect                                                                                                                                |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `interactionMode` | How players interact with job start points, platform buttons, etc. `auto` detects ox\_target or qb-target, falls back to E-key zones. |
| `textUI`          | Which text notification system to use for prompts.                                                                                    |

The resource includes a **target wrapper** (`client/target_wrapper.lua`) that provides a unified API for both `ox_target` and `qb-target`. It auto-detects which system is installed and exposes:

* `TargetAddLocalEntity(entity, options)` / `TargetRemoveLocalEntity(entity, name)`
* `TargetAddSphereZone(data)` / `TargetAddBoxZone(data)` / `TargetRemoveZone(name)`

The platform interaction system can be configured separately:

```lua
Config.elevator.platformInteraction = 'ox_lib' -- 'auto' | 'ox_lib' | 'ox_target' | 'qb-target'
```

</details>

<details>

<summary>Map Blip</summary>

```lua
Config.blip       = true    -- show blip on map
Config.blipSprite = 473     -- blip icon
```

</details>

<details>

<summary>Standalone Payment</summary>

If no framework is detected (or you set `Config.framework = 'standalone'`), open `prompt_logistics_corp_script/dist/server/money.lua` and fill in the `-- STANDALONE` block inside `AddMoney()`:

```lua
-- Examples:
exports['okokBanking']:AddMoney(source, amount, reason)
exports['ox_economy']:addBalance(source, { amount = amount })
TriggerEvent('my_money:add', source, amount)
```

`source`, `amount`, and `reason` are already in scope.

</details>

<details>

<summary>Vehicle Keys (Forklift &#x26; Truck)</summary>

Automatically gives vehicle keys when a job starts and removes them when it ends. Supports popular key-lock scripts out of the box.

```lua
Config.vehicleKeys = {
    enabled = true,
    system  = 'auto',  -- 'auto' | 'qbx_vehiclekeys' | 'wasabi_carlock' | 'custom' | 'none'
}
```

| System            | Notes                                                |
| ----------------- | ---------------------------------------------------- |
| `auto`            | Detects installed key script automatically (default) |
| `qbx_vehiclekeys` | Force QBox vehicle keys                              |
| `wasabi_carlock`  | Force Wasabi Car Lock                                |
| `custom`          | Define your own logic in `dist/server/keys.lua`      |
| `none`            | Disable key management entirely                      |

For `custom`, open `prompt_logistics_corp_script/dist/server/keys.lua` and fill in the `-- CUSTOM` blocks inside `GiveVehicleKey()` and `RemoveVehicleKey()`. Variables `src` (player id), `vehicle` (entity handle), and `plate` (license plate string) are already in scope.

</details>

<details>

<summary>Leaderboard</summary>

```lua
Config.leaderboard = {
    enabled   = true,
    topCount  = 20,        -- how many players to show
    oxLib     = true,      -- enable ox_lib menu display
    dui       = true,      -- enable physical whiteboard with DUI texture
    resetDays = false,     -- auto-reset every N days (false = never)
    board = {
        coords = vector4(-1092.431, -2103.217, 15.192, -135),
        radius = 1.5,
    },
}
```

See Leaderboard System for full details.

</details>

***

#### <i class="fa-warehouse">:warehouse:</i> Warehouse Jobs

<i class="fa-box">:box:</i> **Packing Job**

<details>

<summary>How it works</summary>

1. Walk up to a packing station and press **E** to claim it.
2. A random product type is chosen (Impotent Rage, Pisswasser, or Phones).
3. Place items into the box using the mouse, press **E** to seal.
4. The box rides the conveyor out — payment fires when it leaves.
5.  The box is added to warehouse stock (visible on pickup pallets).

    **Economy flow:**

```
Pack box → conveyor → submitPackage → stock +1
                                          ↓
                              Player picks up → takePackage → stock -1
```

Boxes must be **produced before they can be collected**. Stock starts at 0 each server boot and increases only when workers pack boxes. Counts survive `/restart` but reset on full server reboot.

</details>

<details>

<summary>Server Exports (Stock)</summary>

All exports are **server-side only**.

**`getBoxCount(packageName) → number`**

```lua
local count = exports['prompt_logistics_corp']:getBoxCount('beer_package')
```

**`getAvailableStock() → table`**

```lua
local stock = exports['prompt_logistics_corp']:getAvailableStock()
-- { impotent_rage_package = 5, beer_package = 12, phone_package = 3 }
```

**`takeBoxes(packageName, amount) → boolean`**\
Atomically removes boxes from stock. Returns `false` if not enough (nothing removed).

```lua
local ok = exports['prompt_logistics_corp']:takeBoxes('beer_package', 5)
```

**`addBoxes(packageName, amount) → boolean`**\
Adds boxes back to stock. Returns `false` if it would exceed the cap in `limited` mode.

```lua
exports['prompt_logistics_corp']:addBoxes('beer_package', 5)
```

**Valid package names:**

```
'impotent_rage_package'
'beer_package'
'phone_package'
```

</details>

<details>

<summary>Server Events (Stock)</summary>

```lua
-- Submit a box externally
TriggerEvent("prompt_logistics:submitPackage", "beer_package")

-- Remove a box externally
TriggerEvent("prompt_logistics:takePackage", "beer_package")
```

</details>

<details>

<summary>GlobalState Keys</summary>

Readable from any resource, client or server side:

```lua
GlobalState.impotentBoxCount  -- number
GlobalState.beerBoxCount      -- number
GlobalState.phoneBoxCount     -- number
```

</details>

<details>

<summary>Integration Example</summary>

A trucking script that picks up boxes from the warehouse:

````lua
-- server.lua of your trucking script
RegisterNetEvent('mytrucking:loadCargo', function(packageName, amount)
    local src = source
    local ok = exports['prompt_logistics_corp']:takeBoxes(packageName, amount)
    if not ok then
        TriggerClientEvent('mytrucking:notify', src, 'Not enough stock.')
        return
    end
    TruckCargo[src] = { package = packageName, amount = amount }
    TriggerClientEvent('mytrucking:notify', src, 'Loaded ' .. amount .. ' boxes.')
end)

-- Return boxes on cancel
RegisterNetEvent('mytrucking:cancelDelivery', function()
    local src = source
    local cargo = TruckCargo[src]
    if cargo then
        exports['prompt_logistics_corp']:addBoxes(cargo.package, cargo.amount)
        TruckCargo[src] = nil
    end
end)
```<div data-gb-custom-block data-tag="hint" data-style='info'>`takeBoxes` is atomic. If two scripts try to grab the last 5 boxes at the same time, only one succeeds. The other gets `false`.</div></details>

***

#### <i class="fa-forklift">:forklift:</i> Forklift Job

<details>

<summary>How it works</summary>

1. Walk to a forklift start marker and press **E** to begin. A forklift spawns automatically.
2. Drive to a **pickup pallet** (orange marker), align the forks, and attach it.
3. Transport the pallet to the **drop zone** (green marker, visible from distance).
4. Payment of `payPerPalletMoved` fires on each successful delivery.
5. Return to the start marker and press **X** to end the job and despawn the forklift.<div data-gb-custom-block data-tag="embed" data-url='<https://youtu.be/852uZEKE1V0>'></div></details>

<details>

<summary>Job Variants</summary>

There are two separate forklift jobs, each with its own start marker:

| Variant             | What you do                         | Pickup                           | Drop-off                                |
| ------------------- | ----------------------------------- | -------------------------------- | --------------------------------------- |
| **Load Deliveries** | Move pallets from shelves to trucks | Upstairs shelving (20 locations) | Loading zone downstairs (4 locations)   |
| **Stock Storage**   | Move pallets from ground to shelves | Ground floor (4 locations)       | Upstairs shelf locations (20 locations) |

Both variants pay the same amount per delivery (`Config.money.payPerPalletMoved`).

</details>

<details>

<summary>Forklift Pallets vs Box Economy</summary><div data-gb-custom-block data-tag="hint" data-style='info'>Forklift pallets are **completely independent** from the box packing economy. They are static warehouse props placed at fixed shelf and floor locations — not tied to `GlobalState` stock counts.

The packing job produces boxes → the forklift job moves pallets. They are two separate gameplay loops that happen to exist in the same warehouse.</div></details>

<details>

<summary>Custom Forklifts</summary>

The resource ships with a default forklift model. To add your own custom forklift vehicles:

```lua
Config.customForklifts = {
    { modelName = `myforklift`, forksAttachBoneName = 'forks_attach' }
}
````

* `modelName` — the hashed model name of your custom vehicle
* `forksAttachBoneName` — the bone on your vehicle model where pallets attach (use OpenIV or CodeWalker to find the bone name)

</details>

<details>

<summary>Forklift Shift Config</summary>

```lua
Config.forkliftShift = {
    enabled          = true,
    npcModel         = 's_m_m_warehouse_01',
    npcCoords        = vector4(-1096.149, -2104.999, 14.672, 1.816),
    maxDistance       = 300,
    parkingSpots     = { vector4(...), ... },  -- forklift spawn/park locations
    workOutfit       = { [8] = { d = 182, t = 0 } },
    workOutfitFemale = { [8] = { d = 220, t = 0 } },
    workProps        = { [0] = { d = 145, t = 0 } },
}
```

Outfit keys are GTA component IDs (e.g. `8` = undershirt). `d` = drawable, `t` = texture.

</details>

***

#### <i class="fa-truck">:truck:</i> Truck Delivery

<details>

<summary>How it works</summary>

1. Talk to the **delivery NPC** at the warehouse staging area.
2. Select a product type (Impotent Rage, Pisswasser, or Phones) — stock must have enough full pallets.
3. A **truck** spawns at one of the garage bays. The garage door opens automatically.
4. Use a **loading forklift** to move pallets from the staging columns onto the truck (3 pallets per truck).
5. Once the truck is fully loaded, get in and **drive to the destination**.
6. Park at the delivery zone, unload, and get paid.
7.  Return the truck to the warehouse to complete the job.

    <div data-gb-custom-block data-tag="hint" data-style="info" class="hint hint-info"><p>Truck delivery is tied to the <strong>box economy</strong>. Each pallet requires <code>boxesPerPallet</code> boxes (default: 20) from stock. Stock is deducted when the delivery starts and restored if the delivery fails (<code>restoreStockOnFail = true</code>).</p></div>

</details>

<details>

<summary>Trailer Mode</summary>

When `useTrailer = true`, the delivery system switches to **flatbed trailer mode**:

* A **flatbed trailer** (default: `trailers3`) spawns in the garage bay instead of a box truck.
* Pallets are loaded onto the trailer using the same forklift workflow.
* After loading, a **cab truck** (default: `hauler`) spawns at a separate location for the driving leg.
* Players can also use their own truck instead of the job cab.
* Garage doors open/close automatically and can be toggled manually via wall buttons.
* Trailer doors open/close during loading/unloading (configurable indices).

```lua
Config.truckDelivery.useTrailer         = true
Config.truckDelivery.flatbedModel       = { 'trailers3' }
Config.truckDelivery.cabModel           = 'hauler'
Config.truckDelivery.cabSpawnSpots      = { vector4(...), ... }
Config.truckDelivery.trailerDoors       = true
Config.truckDelivery.trailerDoorIndices = { 4, 5 }
Config.truckDelivery.trailerPalletSlots = { vector3(...), vector3(...), vector3(...) }
```

</details>

<details>

<summary>Destinations &#x26; Payment</summary>

Each product type has its own set of delivery destinations with different payouts. Longer trips pay more.

```lua
Config.truckDelivery.destinations = {
    impotent_rage_package = {
        { coords = vector3(289.669, -998.869, 29.281), label = 'Dark Alley Drop', payment = 1700 },
        { coords = vector3(1978.426, 3037.496, 47.124), label = 'Yellow Jack Bar', payment = 3500 },
        { coords = vector3(41.259, 6450.312, 31.484), label = 'Paleto Bay', payment = 4500 },
        -- ...more destinations
    },
    beer_package = { ... },
    phone_package = { ... },
}
```

Players choose from available destinations when starting a delivery. Payment fires on successful delivery completion.

</details>

<details>

<summary>Truck Delivery Config</summary>

```lua
Config.truckDelivery = {
    enabled            = true,
    boxesPerPallet     = 20,           -- boxes consumed per pallet
    maxPalletsPerType  = 6,            -- max pallets per product type in staging
    palletsPerTruck    = 3,            -- pallets loaded per delivery
    palletLabelMode    = 'floating',   -- 'floating' | 'proximity'
    restoreStockOnFail = true,         -- return boxes to stock on failed delivery
    truckModel         = 'pounder2',   -- truck model (non-trailer mode)
    requireLicense     = false,        -- require driving license
    licenseType        = 'drive',      -- license type to check
    maxLoadingDistance  = 300,          -- max distance from warehouse during loading
}
```

</details>

<details>

<summary>Garage Doors</summary>

The warehouse has **7 automated garage doors** that open/close for truck deliveries.

* Doors open automatically when a delivery spawns a truck at that bay.
* Doors close automatically when the truck leaves.
* Players can manually toggle doors using **wall-mounted buttons** near each bay.
*   Door state is server-authoritative — all players see the same state.

    <div data-gb-custom-block data-tag="hint" data-style="warning" class="hint hint-warning"><p>Manually toggling a door while a delivery is active at that bay is blocked to prevent issues.</p></div>

</details>

***

#### <i class="fa-trophy">:trophy:</i> Leaderboard System

<details>

<summary>How it works</summary>

The leaderboard tracks three categories:

| Category          | Incremented when           |
| ----------------- | -------------------------- |
| `boxesPacked`     | A player seals a box       |
| `palletsMoved`    | A forklift delivery lands  |
| `trucksDelivered` | A truck delivery completes |

**Display modes** (all can be enabled simultaneously):

1. **Console** — always available via server print
2. **ox\_lib menu** — players interact near the board to open a menu (`Config.leaderboard.oxLib`)
3. **Physical DUI board** — a whiteboard prop in the warehouse with a live-updating HTML texture (`Config.leaderboard.dui`)

The DUI board auto-refreshes every 60 seconds. Leaderboard data is persisted to `logistics_leaderboards.json` every 5 minutes and survives restarts.

</details>

<details>

<summary>Auto-Reset</summary>

Set `Config.leaderboard.resetDays` to a number to automatically reset leaderboards on a recurring schedule:

```lua
Config.leaderboard.resetDays = 7  -- reset weekly
Config.leaderboard.resetDays = false  -- never reset (default)
```

</details>

<details>

<summary>Leaderboard Export</summary>

```lua
-- Get all categories
local all = exports['prompt_logistics_corp']:getLeaderboard()

-- Get a specific category
local boxers = exports['prompt_logistics_corp']:getLeaderboard('boxesPacked')
local movers = exports['prompt_logistics_corp']:getLeaderboard('palletsMoved')
local drivers = exports['prompt_logistics_corp']:getLeaderboard('trucksDelivered')

-- Returns: { { rank = 1, identifier = 'char1:abc', name = 'Player', count = 42 }, ... }
```

</details>

***

#### <i class="fa-elevator">:elevator:</i> Freight Platform & Elevators

<details>

<summary>Freight Platform</summary>

The warehouse freight platform moves pallets and vehicles between ground level and the upper floor.

* Press **E** (or use target) near one of the **two platform buttons** to toggle up/down.
* Server-authoritative — all players see the platform move in sync.
* Vehicles on the platform are carried with it (physics cache fix applied automatically).
* Platform state is synced via `GlobalState.logistics_corp_platform_up`.

```lua
Config.elevator.platformInteraction = 'ox_lib'  -- 'auto' | 'ox_lib' | 'ox_target' | 'qb-target'
```

</details>

<details>

<summary>Elevators (requires ox_lib)</summary>

Four elevators across three floors. Press **E** inside to select a floor, or **E** outside to call it.

```lua
Config.elevator = {
    enabled             = true,
    interaction         = 'auto',      -- elevator interaction mode
    platformInteraction = 'ox_lib',    -- platform button interaction mode
    moveSpeed           = 0.1,
    floorWaitTime       = 3000,        -- ms to wait at each floor
    timePerFloor        = 8000,        -- ms travel time per floor
    bezierCurve         = 'easeInOut', -- animation easing
    floorHeights        = { 13.002, 18.982, 25.248 },
}
```

</details>

***

#### <i class="fa-plug">:plug:</i> API & Integration

The resource exposes a comprehensive API for external scripts. All API exports and events can be individually toggled in `Config.api`.

<details>

<summary>API Configuration</summary>

```lua
Config.api = {
    enableAll = true,  -- master toggle (overrides individual toggles)
    exports = {
        isPlayerWorking     = true,
        getActiveDeliveries = true,
        getDoorStates       = true,
        getStationStates    = true,
        setDoorState        = true,
        cancelPlayerJob     = true,
        setStockCount       = true,
    },
    events = {
        paymentProcessed     = true,
        doorStateChanged     = true,
        palletStockFull      = true,
        playerStartedPacking = true,
        playerStoppedPacking = true,
    },
    clientExports = {
        isWorking      = true,
        getDeliveryPhase = true,
    },
}
```

</details>

<details>

<summary>Server Exports (API)</summary>

**`isPlayerWorking(serverId)`** — Check if a player is currently working any logistics job.

```lua
local info = exports['prompt_logistics_corp']:isPlayerWorking(source)
-- Returns: false | { job = 'packing'|'forklift'|'delivery', startedAt = os.time(), product = '...', state = '...' }
```

**`getActiveDeliveries()`** — Get all active truck deliveries.

```lua
local deliveries = exports['prompt_logistics_corp']:getActiveDeliveries()
-- Returns: { [serverId] = { product, destination, phase, spotIndex, startedAt } }
```

**`getDoorStates()`** — Get the open/closed state of all garage doors.

```lua
local doors = exports['prompt_logistics_corp']:getDoorStates()
-- Returns: { [spotIdx] = true|false }
```

**`getStationStates()`** — Get packing station occupancy.

```lua
local stations = exports['prompt_logistics_corp']:getStationStates()
-- Returns: { [stationName] = { inUse = bool, owner = serverId } }
```

**`setDoorState(spotIdx, isOpen)`** — Programmatically open or close a garage door.

```lua
local ok = exports['prompt_logistics_corp']:setDoorState(1, true)  -- open door 1
```

**`cancelPlayerJob(serverId, reason)`** — Force-cancel a player's active job.

```lua
local ok = exports['prompt_logistics_corp']:cancelPlayerJob(source, 'Admin cancelled')
```

**`setStockCount(packageName, count)`** — Directly set stock for a product type.

```lua
local ok = exports['prompt_logistics_corp']:setStockCount('beer_package', 50)
```

</details>

<details>

<summary>Client Exports</summary>

**`isWorking()`** — Check if the local player is working.

```lua
local job = exports['prompt_logistics_corp']:isWorking()
-- Returns: false | 'packing' | 'forklift' | 'delivery'
```

**`getDeliveryPhase()`** — Get the current delivery phase.

```lua
local phase = exports['prompt_logistics_corp']:getDeliveryPhase()
-- Returns: nil | 'loading' | 'hitching' | 'driving' | 'dropping' | 'returning'
```

</details>

<details>

<summary>Server Events</summary>

When `Config.serverEvents = true`, the resource fires these events that other server scripts can listen to:

```lua
-- Payment processed
AddEventHandler('prompt_logistics:paymentProcessed', function(src, amount, reason, method)
    -- src: player server ID
    -- amount: payment amount
    -- reason: 'boxPackaged' | 'palletMoved' | 'truckDelivered'
    -- method: payment framework used
end)

-- Garage door state changed
AddEventHandler('prompt_logistics:doorStateChanged', function(spotIdx, isOpen, triggeredBy)
    -- spotIdx: door index (1-7)
    -- isOpen: true/false
    -- triggeredBy: 'delivery' | 'button' | 'api'
end)

-- Product stock is full
AddEventHandler('prompt_logistics:palletStockFull', function(packageName)
end)

-- Player started packing
AddEventHandler('prompt_logistics:playerStartedPacking', function(src, stationName)
end)

-- Player stopped packing
AddEventHandler('prompt_logistics:playerStoppedPacking', function(src, stationName, reason)
    -- reason: 'completed' | 'cancelled' | 'timeout' | 'disconnect'
end)

-- Delivery started
AddEventHandler('prompt_logistics:deliveryStarted', function(src, productType, destination)
end)

-- Delivery completed
AddEventHandler('prompt_logistics:deliveryCompleted', function(src, productType, destination, payment)
end)

-- Delivery cancelled or failed
AddEventHandler('prompt_logistics:deliveryCancelled', function(src, productType, reason)
end)

-- Stock count changed
AddEventHandler('prompt_logistics:stockChanged', function(packageName, newCount)
end)
```

</details>

<details>

<summary>Integration Example — Admin Panel</summary>

```lua
-- server.lua of your admin panel
RegisterCommand('logistics-status', function(src)
    local stock = exports['prompt_logistics_corp']:getAvailableStock()
    local deliveries = exports['prompt_logistics_corp']:getActiveDeliveries()
    local doors = exports['prompt_logistics_corp']:getDoorStates()

    print('--- Stock ---')
    for name, count in pairs(stock) do
        print(name .. ': ' .. count)
    end

    print('--- Active Deliveries ---')
    for playerId, info in pairs(deliveries) do
        print(('Player %d: %s → %s (%s)'):format(playerId, info.product, info.destination, info.phase))
    end

    print('--- Doors ---')
    for idx, isOpen in pairs(doors) do
        print(('Door %d: %s'):format(idx, isOpen and 'OPEN' or 'CLOSED'))
    end
end, true) -- admin only
```

</details>

***

#### <i class="fa-chair">:chair:</i> Custom Props

<details>

<summary>Main Building</summary>

| Prop Name                                |
| ---------------------------------------- |
| `prompt_dlclogistic_prop_desk1`          |
| `prompt_dlclogistic_prop_meetingtable01` |
| `prompt_dlclogistic_prop_meetingtable02` |
| `prompt_dlclogistic_prop_table_03`       |
| `prompt_dlclogistic_prop_coftable01`     |
| `prompt_dlclogistic_prop_safedoor`       |
| `prompt_dlclogistic_prop_chair1`         |

</details>

<details>

<summary>Warehouse</summary>

| Prop Name                               |
| --------------------------------------- |
| `prompt_dlclogistic_int2_prop_desk01_a` |
| `prompt_dlclogistic_int2_prop_desk01_b` |
| `prompt_bcorp_prop_boxpile_02b`         |
| `prompt_bcorp_prop_boxpile_02c`         |
| `prompt_bcorp_prop_boxpile_02d`         |
| `prompt_bcorp_prop_boxpile_03a`         |
| `prompt_bcorp_prop_boxpile_04a`         |
| `prompt_bcorp_prop_boxpile_05a`         |
| `prompt_bcorp_prop_boxpile_06a`         |
| `prompt_bcorp_prop_boxpile_06b`         |
| `prompt_bcorp_prop_boxpile_07d`         |
| `prompt_bcorp_prop_boxpile_08a`         |
| `prompt_bcorp_prop_rub_cage01a`         |
| `prompt_bcorp_prop_rub_cage01b`         |
| `prompt_bcorp_prop_rub_cage01c`         |
| `prompt_bcorp_prop_rub_cage01d`         |

</details>

<details>

<summary><strong>Doorlock SQL</strong></summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(2793, 'Bilgeco HQ E-1', '{"doors":[{"model":-791930759,"coords":{"x":-1006.2828369140625,"y":-2166.29150390625,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1008.155029296875,"y":-2164.419189453125,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1007.2189331054688,"y":-2165.35546875,"z":12.8707046508789},"maxDistance":2}'),
	(2794, 'Bilgeco HQ E-2', '{"doors":[{"model":-791930759,"coords":{"x":-1008.3624267578125,"y":-2164.211669921875,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1010.234619140625,"y":-2162.339599609375,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1009.2985229492188,"y":-2163.275634765625,"z":12.8707046508789},"maxDistance":2}'),
	(2795, 'Bilgeco HQ E-3', '{"doors":[{"model":-791930759,"coords":{"x":-1010.4417724609375,"y":-2162.13232421875,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1012.31396484375,"y":-2160.26025390625,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1011.3778686523438,"y":-2161.1962890625,"z":12.8707046508789},"maxDistance":2}'),
	(2796, 'Bilgeco HQ E-4', '{"doors":[{"model":-791930759,"coords":{"x":-1012.521484375,"y":-2160.052734375,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1014.3936767578125,"y":-2158.180419921875,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1013.4575805664063,"y":-2159.11669921875,"z":12.8707046508789},"maxDistance":2}'),
	(2797, 'Bilgeco HQ E-5', '{"doors":[{"model":-791930759,"coords":{"x":-1016.0777587890625,"y":-2156.496337890625,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1017.949951171875,"y":-2154.624267578125,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1017.0138549804688,"y":-2155.560302734375,"z":12.8707046508789},"maxDistance":2}'),
	(2798, 'Bilgeco HQ E-6', '{"doors":[{"model":-791930759,"coords":{"x":-1018.1573486328125,"y":-2154.416748046875,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1020.0296020507813,"y":-2152.544677734375,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1019.093505859375,"y":-2153.480712890625,"z":12.8707046508789},"maxDistance":2}'),
	(2799, 'Bilgeco HQ E-7', '{"doors":[{"model":-791930759,"coords":{"x":-1020.2366943359375,"y":-2152.33740234375,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1022.10888671875,"y":-2150.46533203125,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1021.1727905273438,"y":-2151.4013671875,"z":12.8707046508789},"maxDistance":2}'),
	(2800, 'Bilgeco HQ E-8', '{"doors":[{"model":-791930759,"coords":{"x":-1022.3164672851563,"y":-2150.2578125,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1024.1885986328126,"y":-2148.385498046875,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1023.2525634765625,"y":-2149.32177734375,"z":12.8707046508789},"maxDistance":2}'),
	(2801, 'Bilgeco HQ E-9', '{"doors":[{"model":-791930759,"coords":{"x":-1019.0076293945313,"y":-2136.622314453125,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1020.8798217773438,"y":-2134.75,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1019.9437255859375,"y":-2135.68603515625,"z":12.8707046508789},"maxDistance":2}'),
	(2802, 'Bilgeco HQ E-10', '{"doors":[{"model":-1508031716,"coords":{"x":-1022.95947265625,"y":-2132.67041015625,"z":12.8707046508789},"heading":135},{"model":-791930759,"coords":{"x":-1021.0872192382813,"y":-2134.542724609375,"z":12.8707046508789},"heading":315}],"state":0,"coords":{"x":-1022.0233154296875,"y":-2133.6064453125,"z":12.8707046508789},"maxDistance":2}'),
	(2803, 'Bilgeco HQ E-11', '{"doors":[{"model":-791930759,"coords":{"x":-1023.1665649414063,"y":-2132.46337890625,"z":12.8707046508789},"heading":315},{"model":-1508031716,"coords":{"x":-1025.038818359375,"y":-2130.591064453125,"z":12.8707046508789},"heading":135}],"state":0,"coords":{"x":-1024.1026611328126,"y":-2131.52734375,"z":12.8707046508789},"maxDistance":2}'),
	(2804, 'Bilgeco HQ E-12', '{"doors":[{"model":-1508031716,"coords":{"x":-1027.1185302734376,"y":-2128.51123046875,"z":12.8707046508789},"heading":135},{"model":-791930759,"coords":{"x":-1025.246337890625,"y":-2130.383544921875,"z":12.8707046508789},"heading":315}],"state":0,"coords":{"x":-1026.182373046875,"y":-2129.447265625,"z":12.8707046508789},"maxDistance":2}'),
	(2805, 'Bilgeco HQ E-13', '{"doors":[{"model":-1966586148,"coords":{"x":-1042.9149169921876,"y":-2208.51513671875,"z":9.22123146057128},"heading":45},{"model":1978178845,"coords":{"x":-1041.076904296875,"y":-2206.67724609375,"z":9.22123146057128},"heading":45}],"state":1,"coords":{"x":-1041.995849609375,"y":-2207.59619140625,"z":9.22123146057128},"maxDistance":2}'),
	(2806, 'Bilgeco HQ 1-1', '{"doors":false,"state":1,"heading":315,"coords":{"x":-1021.3955688476563,"y":-2175.222412109375,"z":12.86267471313476},"model":634417522,"maxDistance":2}'),
	(2807, 'Bilgeco HQ 1-2', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1029.3680419921876,"y":-2180.267578125,"z":12.8621826171875},"model":634417522,"maxDistance":2}'),
	(2808, 'Bilgeco HQ 1-3', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1021.0541381835938,"y":-2178.380859375,"z":12.86120891571045},"model":-35610440,"maxDistance":2}'),
	(2809, 'Bilgeco HQ 1-4', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1029.181640625,"y":-2184.45166015625,"z":12.86267375946045},"model":634417522,"maxDistance":2}'),
	(2810, 'Bilgeco HQ 1-5', '{"doors":[{"model":634417522,"coords":{"x":-1039.096435546875,"y":-2185.674072265625,"z":12.86218452453613},"heading":135},{"model":634417522,"coords":{"x":-1040.9345703125,"y":-2183.835693359375,"z":12.86218452453613},"heading":315}],"state":1,"coords":{"x":-1040.0155029296876,"y":-2184.7548828125,"z":12.86218452453613},"maxDistance":2}'),
	(2811, 'Bilgeco HQ 1-6', '{"doors":false,"state":1,"heading":225,"coords":{"x":-1045.9073486328126,"y":-2188.214599609375,"z":12.86218738555908},"model":520256171,"maxDistance":2}'),
	(2812, 'Bilgeco HQ 1-7', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1046.4483642578126,"y":-2188.755615234375,"z":12.86218643188476},"model":520256171,"maxDistance":2}'),
	(2813, 'Bilgeco HQ 1-8', '{"doors":false,"state":1,"heading":225,"coords":{"x":-1046.2867431640626,"y":-2193.502685546875,"z":12.86218643188476},"model":520256171,"maxDistance":2}'),
	(2814, 'Bilgeco HQ 1-9', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1046.843994140625,"y":-2194.059814453125,"z":12.86218643188476},"model":520256171,"maxDistance":2}'),
	(2815, 'Bilgeco HQ 1-10', '{"doors":false,"state":1,"heading":225,"coords":{"x":-1051.5908203125,"y":-2193.89794921875,"z":12.86218738555908},"model":520256171,"maxDistance":2}'),
	(2816, 'Bilgeco HQ 1-11', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1052.1319580078126,"y":-2194.439208984375,"z":12.86218643188476},"model":520256171,"maxDistance":2}'),
	(2817, 'Bilgeco HQ 1-12', '{"doors":[{"model":-35610440,"coords":{"x":-1051.249267578125,"y":-2200.18017578125,"z":12.86120796203613},"heading":45},{"model":-35610440,"coords":{"x":-1049.410888671875,"y":-2198.341552734375,"z":12.86120796203613},"heading":225}],"state":1,"coords":{"x":-1050.330078125,"y":-2199.2607421875,"z":12.86120796203613},"maxDistance":2}'),
	(2818, 'Bilgeco HQ 1-13', '{"doors":[{"heading":225,"model":-35610440,"coords":{"x":-1032.3748779296876,"y":-2123.972412109375,"z":12.86215114593505}},{"heading":45,"model":-35610440,"coords":{"x":-1034.212890625,"y":-2125.810302734375,"z":12.86215114593505}}],"coords":{"x":-1033.2939453125,"y":-2124.891357421875,"z":12.86215114593505},"maxDistance":2,"state":1}'),
	(2819, 'Bilgeco HQ 1-14', '{"doors":[{"heading":315,"model":-35610440,"coords":{"x":-1077.5201416015626,"y":-2094.585693359375,"z":14.82245349884033}},{"heading":135,"model":-35610440,"coords":{"x":-1075.68212890625,"y":-2096.423583984375,"z":14.82245349884033}}],"coords":{"x":-1076.60107421875,"y":-2095.504638671875,"z":14.82245349884033},"maxDistance":2,"state":1}'),
	(2820, 'Bilgeco HQ 1-15', '{"doors":[{"heading":225,"model":-35610440,"coords":{"x":-1078.489990234375,"y":-2089.426513671875,"z":14.82245349884033}},{"heading":45,"model":-35610440,"coords":{"x":-1080.328125,"y":-2091.26513671875,"z":14.82245349884033}}],"coords":{"x":-1079.4090576171876,"y":-2090.345703125,"z":14.82245349884033},"maxDistance":2,"state":1}'),
	(2821, 'Bilgeco HQ 2-1', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1029.2991943359376,"y":-2180.3701171875,"z":18.83972549438476},"model":634417522,"maxDistance":2}'),
	(2822, 'Bilgeco HQ 2-2', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1021.0541381835938,"y":-2178.380859375,"z":18.83826065063476},"model":-35610440,"maxDistance":2}'),
	(2823, 'Bilgeco HQ 2-3', '{"doors":false,"state":1,"heading":315,"coords":{"x":-1021.3955688476563,"y":-2175.222412109375,"z":18.83972549438476},"model":634417522,"maxDistance":2}'),
	(2824, 'Bilgeco HQ 2-4', '{"doors":false,"state":1,"heading":225,"coords":{"x":-1046.0360107421876,"y":-2197.0869140625,"z":18.85225677490234},"model":-1967709362,"maxDistance":2}'),
	(2825, 'Bilgeco HQ 2-5', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1049.1279296875,"y":-2193.909423828125,"z":18.85225677490234},"model":-1967709362,"maxDistance":2}'),
	(2826, 'Bilgeco HQ 2-6', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1048.1466064453126,"y":-2199.197509765625,"z":18.85225677490234},"model":-1967709362,"maxDistance":2}'),
	(2827, 'Bilgeco HQ 2-7', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1059.599365234375,"y":-2183.43798828125,"z":18.85225677490234},"model":-1967709362,"maxDistance":2}'),
	(2828, 'Bilgeco HQ 3-1', '{"doors":false,"state":1,"heading":135,"coords":{"x":-1048.94970703125,"y":-2166.313720703125,"z":25.14712524414062},"model":-1967709362,"maxDistance":2}'),
	(2829, 'Bilgeco HQ 3-2', '{"doors":false,"state":1,"heading":315,"coords":{"x":-1056.5902099609376,"y":-2174.75341796875,"z":25.13459587097168},"model":-972688951,"maxDistance":2}'),
	(2830, 'Bilgeco HQ 3-3', '{"doors":false,"state":1,"heading":135,"coords":{"x":-1049.444580078125,"y":-2155.281494140625,"z":25.14712524414062},"model":-1967709362,"maxDistance":2}'),
	(2831, 'Bilgeco HQ 3-4', '{"doors":false,"state":1,"heading":315,"coords":{"x":-1052.1890869140626,"y":-2152.536865234375,"z":25.14712524414062},"model":-1967709362,"maxDistance":2}'),
	(2832, 'Bilgeco HQ 3-5', '{"doors":false,"state":1,"heading":225,"coords":{"x":-1058.190185546875,"y":-2143.920166015625,"z":25.14712524414062},"model":-1967709362,"maxDistance":2}'),
	(2833, 'Bilgeco HQ 3-6', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1049.7257080078126,"y":-2135.455810546875,"z":25.14712524414062},"model":-1967709362,"maxDistance":2}'),
	(2834, 'Bilgeco HQ 3-7', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1042.4713134765626,"y":-2128.201416015625,"z":25.14712524414062},"model":-1967709362,"maxDistance":2}'),
	(2835, 'Bilgeco HQ 3-8', '{"doors":false,"state":1,"heading":225,"coords":{"x":-1039.7266845703126,"y":-2125.456787109375,"z":25.14712524414062},"model":-1967709362,"maxDistance":2}'),
	(2836, 'Bilgeco HQ 3-9', '{"doors":false,"state":1,"heading":315,"coords":{"x":-1021.3955688476563,"y":-2175.222412109375,"z":25.13459587097168},"model":634417522,"maxDistance":2}'),
	(2837, 'Bilgeco HQ 3-10', '{"doors":false,"state":1,"heading":45,"coords":{"x":-1020.9649047851563,"y":-2178.29150390625,"z":25.13313102722168},"model":-35610440,"maxDistance":2}'),
	(2838, 'Bilgeco Warehouse E-1', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1078.0491943359376,"y":-2080.02978515625,"z":13.74787330627441},"model":1563234809,"maxDistance":6}'),
	(2839, 'Bilgeco Warehouse E-2', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1083.4053955078126,"y":-2074.673828125,"z":13.73957252502441},"model":1563234809,"maxDistance":6}'),
	(2840, 'Bilgeco Warehouse E-3', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1088.7611083984376,"y":-2069.31787109375,"z":13.76008033752441},"model":1563234809,"maxDistance":6}'),
	(2841, 'Bilgeco Warehouse E-4', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1094.1173095703126,"y":-2063.96142578125,"z":13.76008033752441},"model":1563234809,"maxDistance":6}'),
	(2842, 'Bilgeco Warehouse E-5', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1099.47314453125,"y":-2058.60546875,"z":13.76008033752441},"model":1563234809,"maxDistance":6}'),
	(2843, 'Bilgeco Warehouse E-6', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1104.8294677734376,"y":-2053.2490234375,"z":13.76008033752441},"model":1563234809,"maxDistance":6}'),
	(2844, 'Bilgeco Warehouse E-7', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1110.1851806640626,"y":-2047.89306640625,"z":13.76008033752441},"model":1563234809,"maxDistance":6}'),
	(2845, 'Bilgeco Warehouse E-8', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1186.4951171875,"y":-2134.86865234375,"z":14.07837295532226},"model":384370034,"maxDistance":6}'),
	(2846, 'Bilgeco Warehouse E-9', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1181.13916015625,"y":-2140.224853515625,"z":14.07837295532226},"model":384370034,"maxDistance":6}'),
	(2847, 'Bilgeco Warehouse E-10', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1175.7830810546876,"y":-2145.5810546875,"z":14.07837295532226},"model":384370034,"maxDistance":6}'),
	(2848, 'Bilgeco Warehouse E-11', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1170.4271240234376,"y":-2150.937255859375,"z":14.07837295532226},"model":384370034,"maxDistance":6}'),
	(2849, 'Bilgeco Warehouse E-12', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1165.071044921875,"y":-2156.29345703125,"z":14.07837295532226},"model":384370034,"maxDistance":6}'),
	(2850, 'Bilgeco Warehouse E-13', '{"auto":true,"doors":false,"state":1,"heading":315,"coords":{"x":-1159.108154296875,"y":-2162.256591796875,"z":14.07837295532226},"model":-676234388,"maxDistance":6}'),
	(2851, 'Bilgeco Warehouse E-14', '{"doors":[{"heading":135,"model":1978178845,"coords":{"x":-1071.0579833984376,"y":-2083.08203125,"z":14.52606773376464}},{"heading":135,"model":-1966586148,"coords":{"x":-1069.219970703125,"y":-2084.920166015625,"z":14.52606773376464}}],"coords":{"x":-1070.138916015625,"y":-2084.0009765625,"z":14.52606773376464},"maxDistance":2,"state":1}');
```

</details>

***

#### <i class="fa-comment-question">:comment-question:</i> Troubleshooting

<details>

<summary>Interior not spawning</summary>

* Ensure `prompt_logistics_corp` is started in `server.cfg`.
* Verify `stream` folders aren't missing or renamed.
* Check the server console for errors on startup.

</details>

<details>

<summary>Elevator not working</summary>

Confirm `ox_lib` is installed and started **before** this resource.

</details>

<details>

<summary>Payment not working</summary>

* Check `Config.money.enabled` is `true`.
* If using `standalone`, make sure you filled in the standalone block in `money.lua`.
* Enable `Config.debug = true` and check server console for `[Logistics Money]` messages.

</details>

<details>

<summary>Box count doubling</summary>

Make sure `prompt_logistics_corp_script/dist/server/*.lua` is **not** listed in both `shared_scripts` and `server_scripts` in `fxmanifest.lua`.

</details>

<details>

<summary>Truck not spawning</summary>

* Check `Config.truckDelivery.enabled` is `true`.
* Ensure there's enough stock for a full delivery (`boxesPerPallet * palletsPerTruck` boxes).
* Verify `truckSpawnSpots` or `trailerSpawnSpots` coordinates aren't blocked by other vehicles.
* Check server console with `Config.debug = true`.

</details>

<details>

<summary>Garage doors not opening</summary>

* Doors require the delivery system to register them on first use. A player must be near the door.
* If using trailer mode, ensure `trailerGarageDoors` coordinates match the prop positions.
* The GTA door system requires all same-model doors to be registered in batch — this is handled automatically but may fail if props aren't streamed in.

</details>

<details>

<summary>Leaderboard not showing</summary>

* Ensure `Config.leaderboard.enabled` is `true`.
* For the DUI board: `Config.leaderboard.dui` must be `true` and the whiteboard prop must be streamed in.
* For the ox\_lib menu: `Config.leaderboard.oxLib` must be `true` and `ox_lib` must be running.
* Check that `logistics_leaderboards.json` exists and isn't corrupted (delete it to reset).

</details>

<details>

<summary>Target system not working</summary>

* Check `Config.interactionMode` — set to `'auto'` to detect, or force `'ox_target'` / `'qb-target'`.
* Ensure your target resource is started **before** this resource.
* The target wrapper (`client/target_wrapper.lua`) only supports `ox_target` and `qb-target`.

</details>

***

#### <i class="fa-globe">:globe:</i> Locale / Translations

All player-facing strings are defined in `Config.Locale` at the bottom of `config.lua`. Edit these values to translate or customize text:

```lua
Config.Locale = {
    paymentReceived         = 'Payment Received',
    boxPackaged             = 'Box packaged',
    palletDelivered         = 'Pallet delivered',
    shiftStarted            = 'Shift started. Get in your forklift!',
    shiftEnded              = 'Shift ended.',
    truckDeliveryStart      = 'Start Delivery',
    truckDeliveryLoading    = 'Load pallets into the truck using the forklift.',
    truckDeliveryFull       = 'Truck loaded! Get in to deliver.',
    truckDeliveryDriving    = 'Deliver to %s.',
    truckDeliveryComplete   = 'Delivery complete! Payment: %s%d',
    truckDeliveryFailed     = 'Delivery failed.',
    -- ... 40+ more strings, see config.lua for the full list
}
```

***

**Need help?** Open a ticket on our support Discord with the resource name, console errors, and a screenshot.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
