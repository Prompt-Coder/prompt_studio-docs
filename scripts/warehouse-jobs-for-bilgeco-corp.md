---
icon: shelves
---

# Warehouse Jobs (for Bilgeco Corp)

> The logistics jobs let players earn money in the warehouse through two main activities. Box packing has players build and fold boxes at stations, place them on the conveyor, and get paid per box. Forklift delivery has players pick up pallets, move them to delivery points, and get paid per pallet. The packed boxes and pallets feed a shared box economy that other scripts (trucking, deliveries, etc.) can use for loading and deliveries.
>
> Part of the [bilgeco-hq-and-warehouse.md](../civilian-maps/bilgeco-hq-and-warehouse.md "mention")

{% embed url="https://youtu.be/naf0o4BcGXI" %}

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

#### <i class="fa-warehouse" style="color:$primary;">:warehouse:</i> Warehouse Jobs

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
