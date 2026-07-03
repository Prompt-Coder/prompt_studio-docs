---
description: >-
  All top-level settings live in config/config.lua. The file returns a plain Lua
  table — every key is explained below.
icon: gear-code
---

# Configuration

### General

```lua
debug = false
```

Enables verbose console logging. Useful while setting up; disable in production.

```lua
interaction = 'auto'   -- 'auto' | 'ox_target' | 'qb-target' | 'none'
framework   = 'auto'   -- 'auto' | 'qbx' | 'qb' | 'esx' | 'none'
inventory   = 'auto'   -- 'auto' | 'ox_inventory' | 'qb-inventory' | 'ps-inventory' | 'esx' | 'none'
paymentMethod = 'cash' -- 'cash' | 'bank'
```

`'auto'` checks which resources are running and picks automatically. Set a specific value if auto-detection fails or you want to lock a choice.

```lua
lightRenderingMode = 'nearby' -- 'nearby' | 'inside'
```

* `'nearby'` — wagon lights render for all tracked wagons within sensor range.
* `'inside'` — lights render only when the local player is sitting inside a wagon.

***

### Routes

```lua
routes = {
    lossantos = { id = 25, label = 'Los Santos'   },
    sandy     = { id = 24, label = 'Sandy Shores' },
}
```

Each key is an internal route name used throughout the script. The fields are:

| Field   | Type      | Description                                   |
| ------- | --------- | --------------------------------------------- |
| `id`    | `integer` | GTA V track ID passed to `CreateMissionTrain` |
| `label` | `string`  | Human-readable name shown on departure boards |

> If you add a new route, you must also add its waypoints to `routes.json`. See the Route Converter page for how to generate that data.

***

### Train Models

```lua
trainModels = { 'sloco', 'rest', 'scab', 'coal' }
```

The list of model names the script recognises as train entities. The **first entry is always the locomotive**. If `sv_entityLockdown` is active, the script uses this list to block unauthorized train spawns from clients.

***

### Additive Trains

```lua
additiveTrains = {
    polar = { signature = 'rest', expectedIndex = 28 },
}
defaultTrain = 'polar'
trainConfigScanWindow = 40
```

GTA V's `CreateMissionTrain` takes a numeric index into the global train config pool. When a third-party resource appends a new train config (via its own `trains.xml`), that index shifts depending on load order.

The script resolves the index at runtime by spawning a test consist and reading which carriage model it produced:

* `signature` — a unique carriage model name that only this consist uses (e.g. `'rest'` for the polar express).
* `expectedIndex` — the index to try first as a fast path (1 spawn). If the carriage model matches, the index is cached and reused.
* `trainConfigScanWindow` — if `expectedIndex` is wrong, how many indices past it to scan before giving up.

You do not need to touch this unless you are adding a custom train set. See Advanced Topics.

***

### Stations

```lua
stations = {
    paletobay = {
        nodes    = { lossantos = 667, sandy = 667 },
        resource = 'prompt_trainstation_paleto',
    },
    lossantos1 = {
        nodes    = { lossantos = 2348 },
        resource = 'prompt_trainstation_ls',
    },
}
```

| Field      | Type                       | Description                                                                                                                                                             |
| ---------- | -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `nodes`    | `table<routeKey, integer>` | Nearest rail node index on each route — used for ETA calculations                                                                                                       |
| `resource` | `string?`                  | Optional: name of a companion resource that owns the station's departure board textures/props. The zone anchor will be read from that resource's board zone if present. |

Node indices are looked up from `routes.json`. You can find the right value by running the debug command and watching which node the train is on when it reaches the platform.

***

### NPC Trains

```lua
npcDriven = {
    enable = true,
    trainsPerRoute = {
        lossantos = 5,
        sandy     = 2,
    },
}
```

| Field            | Description                                                                        |
| ---------------- | ---------------------------------------------------------------------------------- |
| `enable`         | Set to `false` to disable all NPC trains entirely                                  |
| `trainsPerRoute` | How many trains to spawn on each route. Must match route keys defined in `routes`. |

Trains are spawned on the first player join and cleaned up when the last player disconnects.

***

### PA (Public Announcement) Zones

```lua
paStations = {
    {
        id       = 'pa_los_santos',
        stations = { 'lossantos1', 'lossantos2' },
        coords   = vec3(716.97, -532.14, 28.46),
        range    = 150.0,
    },
}
```

| Field      | Type               | Description                                                                                   |
| ---------- | ------------------ | --------------------------------------------------------------------------------------------- |
| `id`       | `string`           | Unique identifier for this PA zone                                                            |
| `stations` | `string[]`         | Station IDs that trigger announcements for this PA zone                                       |
| `coords`   | `vec3` or `vec3[]` | Speaker position(s). Multiple positions play the announcement simultaneously from each point. |
| `range`    | `number`           | Audio range in metres                                                                         |

See Public Announcements for more detail.

***

### Tickets

```lua
tickets = {
    defaultPrice = 50,
    prices = {
        -- ['paletobay'] = 30,
    },
    machines = { ... }
}
```

See Ticket System for the full reference.

***

### Trains Command

```lua
trainsCommand = {
    enable      = true,
    restriction = false,  -- false = all players | 'group.admin' = ace permission
}
```

Registers the `/trains` chat command that opens a staff management menu. See Trains Command & Blips.

***

### Train Blips

```lua
trainBlips = {
    enable     = true,
    interval   = 2000,
    sprite     = 795,
    color      = 0,
    scale      = 0.8,
    shortRange = false,
    label      = 'Train #{id} - {routeLabel}',
}
```

| Field        | Description                                                                                                |
| ------------ | ---------------------------------------------------------------------------------------------------------- |
| `enable`     | Toggle all train blips                                                                                     |
| `interval`   | Milliseconds between position updates pushed to GlobalState                                                |
| `sprite`     | Blip sprite ID — see [FiveM blip reference](https://docs.fivem.net/docs/game-references/blips/#blips)      |
| `color`      | Blip colour — see [FiveM colour reference](https://docs.fivem.net/docs/game-references/blips/#blip-colors) |
| `scale`      | Blip size on the minimap                                                                                   |
| `shortRange` | `true` = only visible when zoomed in; `false` = always visible                                             |
| `label`      | Blip name template. Placeholders: `{id}`, `{route}`, `{routeLabel}`                                        |

See Trains Command & Blips for examples.
