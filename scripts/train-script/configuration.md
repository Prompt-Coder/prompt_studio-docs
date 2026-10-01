---
description: >-
  All top-level settings live in config/config.lua. The file returns a plain Lua
  table — every key is explained below.
icon: gear-code
---

# Configuration

{% hint style="info" %}
**Version 2** (2.0.0-beta) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

All top-level settings live in `config/config.lua`. The file returns a plain Lua table, grouped into numbered sections. **Lines and stations are not configured here** — see [Lines & Stations](lines-and-stations.md).

```lua
debug = true   -- verbose logging; turn off in production
```

***

### 1. Integrations

```lua
integrations = {
    interaction = 'auto',   -- 'auto' | 'ox_target' | 'qb-target' | 'textui' | 'none'
    framework   = 'auto',   -- 'auto' | 'qbx' | 'qb' | 'esx' | 'none'
    inventory   = 'auto',   -- 'auto' | 'ox_inventory' | 'qb-inventory' | 'esx' | 'none'
    payment     = 'cash',   -- 'cash' | 'bank'
}
```

`'auto'` checks which resources are running and picks the first match. `interaction = 'textui'` needs nothing but `ox_lib` — it's the automatic fallback when no target resource is found, so most servers never have to set it explicitly. `inventory = 'none'` doesn't disable tickets; the script keeps its own ticket store instead. See [Frameworks](frameworks.md) and [Tickets](tickets.md).

***

### 2. Route overrides

```lua
routes = {}   -- e.g. routes.metro = { label = 'Subway' }
```

Empty by default. A line's real settings (label, fleet, track, stops…) live in its own file under `prompt_train_script-assets/lines/`. This table only overrides a field on top of that, for a value you want pinned by hand regardless of what the line file or the [web editor](https://train-editor.prompt-mods.com/) writes. Any field a line accepts can go here, keyed by the line's id.

***

### 3. NPC-driven trains

```lua
npcDriven = {
    enable = true,
    trainsPerRoute = {},   -- overrides a line's own `fleet`

    keepTrainsOnOwnerChange = false,
    autoRebuild   = true,
    ghostCleanup  = true,
    autoReconcile = true,
}
```

| Field                     | Effect                                                                                                                                                                                              |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `enable`                  | `false` = no NPC trains at all                                                                                                                                                                      |
| `trainsPerRoute`          | Overrides a line's `fleet` value, keyed by line id                                                                                                                                                  |
| `keepTrainsOnOwnerChange` | One-sync `OrphanMode`. Left off: it stops the server's own cleanup but not the client's, and it exempts delinked carriages from cleanup — trading occasional respawns for permanent ghost carriages |
| `autoRebuild`             | Rebuild (despawn + respawn) a consist confirmed genuinely broken — a missing carriage, or one stopped and left behind while the loco moves on                                                       |
| `ghostCleanup`            | Delete carriages not linked to any tracked loco                                                                                                                                                     |
| `autoReconcile`           | Top a short-staffed line back up to its fleet size, one train per pass                                                                                                                              |

***

### 4. Spawning

```lua
spawning = {
    mode = 'predictive',   -- 'always' | 'predictive'
    bucket = 0,
    entityLockdown = GetConvar('sv_entityLockdown', 'inactive'),
    trackScanRange = 25,
    configScanWindow = 40,

    predictive = {
        spawnDistance   = 400.0,
        despawnDistance = 450.0,
        checkInterval   = 1000,
        cruiseSpeed     = 20.0,
        acceleration    = 1.5,
        braking         = 2.0,
        brakingDistance = 100.0,
        stationDwellMs  = 20000,
        maxConcurrentSpawns = 2,
        minSpawnSeparation  = 250.0,
    },
}
```

`'predictive'` keeps every train as a server-side virtual position until a player gets within `predictive.spawnDistance`, then materialises the real entity — this is what most servers should run. `'always'` spawns every NPC train at startup and keeps it alive, entities and all.

A line can override any `predictive.*` field for itself — see [Lines & Stations](lines-and-stations.md).

***

### 5. Anti-collision

```lua
collision = {
    enable           = true,
    checkInterval    = 500,
    stopDistance     = 720.0,
    resumeDistance   = 1040.0,
    sameRailLateral  = 8.0,
    sameRailVertical = nil,
    sameDirectionDot = 0.3,
}
```

GTA does no train-vs-train spacing on its own; this is scripted. A follower holds below `stopDistance` to the train ahead on the same rail and resumes past `resumeDistance`. `sameRailVertical` stays `nil` (a 2D check) except for lines stacked over each other, like an elevated line crossing a tunnel — set it per line to add a height gate.

***

### 6. Train blips

```lua
blips = {
    enable     = true,
    interval   = 2000,
    sprite     = 795,
    color      = 0,
    scale      = 0.8,
    shortRange = true,
    label      = 'Train #{id} - {routeLabel}',

    group         = true,
    groupLabels   = { freight = 'Train',         metro = 'Metro'         },
    stationLabels = { freight = 'Train Station', metro = 'Metro Station' },
    stationScale  = 0.8,   -- station blips; a station's own blip.scale wins
}
```

Placeholders in `label`: `{id}` train index, `{route}` line id, `{routeLabel}` its label.

`group = true` collapses the pause-map legend to one entry per kind ("Train" / "Metro") instead of one per train and one per station — with it on, `label` above and any per-line or per-station blip label are ignored in favour of `groupLabels` / `stationLabels`. Set it `false` to name every train and station apart.

`scale` sizes the **train** blips and `stationScale` sizes the **station** blips. A station that sets its own `blip.scale` in its station file keeps that value.

***

### 7. Wagons

```lua
wagons = {
    doorsAlwaysOpen = false,
    lightRenderingMode = 'nearby',   -- 'nearby' | 'inside'

    doors = {
        spawnDistance   = 80.0,
        cleanupDistance = 120.0,
        triggerDistance = 2.2,
        notifyDistance  = 1.0,
        loopWait        = 300,
        scanEveryLoops  = 8,
        animation       = { duration = 900, steps = 30 },
    },
}
```

`doorsAlwaysOpen = true` also bypasses the ticket check — useful for RP scenes or screenshots. The wagon models and door/seat/light fittings themselves are defined per consist in `config/trains.lua`, not here.

***

### 8. Departure boards

```lua
boards = {
    propDistance = 150.0,
    props = {
        hanging  = { model = `prompt_trainscreen`,          txd = '...', txn = '...' },
        standing = { model = `prompt_trainscreen_standing`, txd = '...', txn = '...' },
        side     = { model = `prompt_trainscreen_side`,     txd = '...', txn = '...' },
    },
}
```

The prop models a station can spawn a board onto. The board's actual layout — what it looks like, which columns it shows — is a **preset** in `config/boards.lua`, picked by name from a station file (`board = { preset = 'default' }`). See [Departure Boards](departure-boards.md).

***

### 9. Tickets

```lua
tickets = {
    defaultPrice = 50,
    requireForDoors = true,
    defaultMachine = { model = `prompt_train_ticketmachine_prop`, txd = '...', txn = '...' },
    machineSpawnDistance = 100.0,
    prices   = {},   -- destination label -> price, overrides a station's own `price`
    machines = {},   -- added on top of each station's own `machines`
}
```

`requireForDoors = true` means a player needs a `train_ticket` to open wagon doors. Prices and ticket machines are normally set per station (see [Lines & Stations](lines-and-stations.md)); `prices` and `machines` here only add to or override that. See [Tickets](tickets.md).

***

### 10. PA (Public Announcement)

```lua
pa = {
    enable       = true,
    audioBank    = 'audiodirectory/prompt_train',
    soundSet     = 'prompt_train',
    entityModel  = `prop_pool_ball_01`,
    defaultRange = 120.0,
    clips   = { intro = 'pa_intro_chime', train = 'pa_train', ... },
    numbers = { 'pa_num_1', ... },
    tracks  = { 'pa_num_1', 'pa_num_2', 'pa_num_3', 'pa_num_4' },
    routes = {}, destinations = {}, stations = {}, zones = {},
}
```

`routes` / `destinations` / `stations` map a key to an audio clip name; a missing entry just drops that word from the announcement. A line's own `pa` clip and a station's own `pa` block already provide these — the tables here only override or add to them. `zones` works the same way for speaker positions. See [Audio Announcements](audio-announcements.md).

***

### 11. Commands

```lua
commands = {
    trains = {
        enable      = true,
        restriction = 'group.admin',   -- false = everyone | an ace permission string
    },
}
```

Controls the player-facing `/trains` command. Server console commands (`train_build`, `train_routes`, …) are always available regardless of this setting — see [Commands](commands.md).

***

## Version 1

Everything below applies to **1.0.x** (latest: 1.0.4.1).

### General

```lua
debug = false
```

Enables verbose console logging. Useful while setting up; disable in production.

```lua
interaction = 'auto'   -- 'auto' | 'ox_target' | 'qb-target' | 'textui' | 'none'
framework   = 'auto'   -- 'auto' | 'qbx' | 'qb' | 'esx' | 'none'
inventory   = 'auto'   -- 'auto' | 'ox_inventory' | 'qb-inventory' | 'ps-inventory' | 'esx' | 'none'
paymentMethod = 'cash' -- 'cash' | 'bank'
```

`'auto'` checks which resources are running and picks automatically. Set a specific value if auto-detection fails or you want to lock a choice.

{% hint style="info" %}
None of these are hard requirements. With no target resource, `interaction = 'auto'` falls back to `'textui'` — built-in `[E]` proximity prompts. With `inventory = 'none'`, tickets are stored by the script itself (see [tickets.md](tickets.md "mention")).
{% endhint %}

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
