---
description: >-
  All top-level settings live in config/config.lua. The file returns a plain Lua
  table — every key is explained below.
icon: gear-code
---

# Configuration

{% hint style="info" %}
**Version 2** (2.1.0) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

All top-level settings live in `config/config.lua`. The file returns a plain Lua table, grouped into numbered sections. **Lines and stations are not configured here** — see [Lines & Stations](lines-and-stations.md). The trains themselves, and which ones run on each line, are in `config/trains.lua`, covered at the end of this part.

```lua
debug = false   -- verbose logging; turn on while setting up
```

All player-facing text (notifications, menus, the ticket and driver screens) is in `locales/*.json`, in 14 languages. The script uses `ox_lib`'s language, set with `setr ox:locale de` in `server.cfg`. Missing text falls back to English. To change a wording, edit its key in the JSON file.

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

The framework is also used by [player driving](driving.md) (§ 12): the job and grade check, on-duty status, and driver pay.

***

### 2. Route overrides

```lua
routes = {}   -- e.g. routes.metro = { label = 'Subway' }
```

Empty by default. A line's real settings (label, fleet, track, stops…) live in its own file under `prompt_train_script-assets/lines/`. This table only overrides a field on top of that, for a value you want pinned by hand regardless of what the line file or the [web editor](https://train-editor.prompt-mods.com/) writes. Use it for fields such as `label`, `blip`, `predictive`, `collision` and `speedZones`, keyed by the line's id.

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
| `enable`                  | `false` = no NPC trains at all. This also turns off player driving (§ 12) and NPC passengers (§ 13)                                                                                                 |
| `trainsPerRoute`          | Overrides how many trains a line runs (the `fleet` number in its `line.lua`), keyed by line id. Which trains run is set in `config/trains.lua`                                                      |
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

`'predictive'` keeps every train as a server-side virtual position until a player gets within `predictive.spawnDistance`, then materialises the real entity — this is what most servers should run. `'always'` spawns every NPC train at startup and keeps it alive, entities and all. One-way lines, such as Roxwood, need `'predictive'`; under `'always'` they stay dormant.

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

    consistColors = { bullet = 3, polar = 1, metro = 5 },   -- consist key -> blip colour, over the line's own
    consistLabels = { bullet = 'Bullet Train', polar = 'Polar Express', metro = 'Metro' },   -- legend names with `group`
}
```

Placeholders in `label`: `{id}` train index, `{route}` line id, `{routeLabel}` its label, `{train}` the train type (its `consistLabels` name, else its `label` in `config/trains.lua`).

`group = true` collapses the pause-map legend instead of listing every train and station apart. Stations get one entry per kind (`stationLabels`). Trains get one entry per train type, named from `consistLabels`, or the train's `label` in `config/trains.lua` when it has no entry there. With `group` on, `label` above and any per-line or per-station blip label are ignored. Set it `false` to name every train and station apart.

`consistColors` gives each train type its own [blip colour](https://docs.fivem.net/docs/game-references/blips/#blip-colors), keyed by its name in `config/trains.lua`. It wins over the colour a line sets for itself. If you empty it (`consistColors = {}`), grouped train blips go back to one entry per kind from `groupLabels` ("Train" / "Metro"). The `bullet` entries are for the AERION bullet train pack (`prompt_train_bullet`, coming soon).

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

        exterior = {              -- side doors; gangway doors always work
            stationOnly  = true,  -- open only when stopped at a station
            minOffsetX   = 1.0,   -- door trigger this far off the centre line = exterior (m)
            stoppedSpeed = 0.5,   -- m/s
            stationRange = 150.0, -- from a station's stop point (m)
        },
    },
}
```

`doorsAlwaysOpen = true` also bypasses the ticket check — useful for RP scenes or screenshots. Side doors still follow `exterior.stationOnly` below. The wagon models and door/seat/light fittings themselves are defined per consist in `config/trains.lua` (see [Train registry](#train-registry) below), not here.

**Side doors only open at stations.** A door counts as a side door when its trigger sits at least `minOffsetX` metres off the carriage's centre line, unless the train's own door settings say otherwise. With `stationOnly = true`, side doors stay shut until the train has slowed below `stoppedSpeed` (m/s) within `stationRange` metres of a station's stop point. Then the doors on the platform side open by themselves; on a player-driven train, they open when the driver releases them. Gangway doors work anywhere. `stationOnly = false` lets side doors open anywhere, by walking up to them.

This matters for train packs with side doors. The Polar Express's doors sit on the centre line, so they count as gangway doors.

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

`requireForDoors = true` means a player needs a `train_ticket` to open a wagon door by walking up to it. Prices and ticket machines are normally set per station (see [Lines & Stations](lines-and-stations.md)); `prices` and `machines` here only add to or override that. See [Tickets](tickets.md).

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
        restriction = 'group.admin',   -- false = everyone | a principal, e.g. a group
    },
}
```

Controls the player-facing `/trains` command. Server console commands (`train_build`, `train_routes`, …) are always available regardless of this setting — see [Commands](commands.md).

***

### 12. Player driving

Players can take over a line's train from its cab, or take a service train out of a depot. This section lists the settings; the full guide is [Driving](driving.md).

```lua
driving = {
    enable        = true,
    jobs          = { train = 0 }, -- job -> minimum grade; {} = anyone
    requireDuty   = true,
    ace           = 'prompt_train.drive', -- used instead of jobs without a framework
    lines         = {},    -- line ids allowed; {} = all
    units         = 'mph', -- 'kmh' | 'mph'
    sounds        = true,  -- cab sounds
    stopTolerance = 8.0,   -- stop point tolerance (m)

    takeover = {
        enable        = true,
        maxSpeed      = nil,    -- m/s; nil = also a moving train
        range         = 25.0,   -- from the loco (m)
        idleReleaseMs = 180000, -- standing off a station this long -> autopilot
    },

    service = {
        enable    = true,
        perLine   = 1,     -- service trains per line at once
        abandonMs = 60000, -- driver out of the cab this long -> train removed
        train     = nil,   -- consist key; nil = the driver picks one of the line's trains
        dispatcher = { model = `s_m_m_lsmetro_01`, scenario = 'WORLD_HUMAN_CLIPBOARD', range = 100.0 },

        -- station = registry platform key; ped = dispatcher spot on the platform (vec4)
        depots = {
            { line = 'sandy',     station = 'sandy_prompt',       ped = vec4(1878.8, 3554.5, 37.82, 210.0) },
            { line = 'lossantos', station = 'lossantos_prompt_1', ped = vec4(692.4, -606.6, 25.07, 74.0) },
            { line = 'metro',     station = 'davis_1',            ped = vec4(122.7, -1733.2, 29.11, 150.0) },
        },
    },

    controls = {
        powerNotches     = 4,
        brakeNotches     = 4,
        notchRepeatMs    = 250,
        reverseMaxSpeed  = 4.0, -- m/s
        speedLimitFactor = 1.2, -- line limit = predictive.cruiseSpeed x this
    },

    physics = { -- m/s²; a consist's own `driving` wins
        accel     = 1.0,
        brake     = 1.4,
        emergency = 3.0,
        coast     = 0.04,
    },

    speedProfile = { -- curve limits; a line adds `speedZones` = { from, to, limit (km/h) }
        enable       = true,
        lateralAccel = 0.8,    -- m/s² allowed in a curve
        minSpeed     = 30,     -- km/h
        step         = 5,      -- km/h
        smoothing    = 25.0,   -- m a lower limit is widened by
        lookahead    = 1500.0, -- m ahead the driver is warned
    },

    vigilance = { -- acknowledge every intervalMs within warnMs, else emergency brake
        enable     = true,
        intervalMs = 60000,
        warnMs     = 5000,
        minSpeed   = 1.0, -- m/s
    },

    signals = {
        cautionFactor      = 0.5,  -- yellow: limit x this
        redSpeed           = 8.0,  -- red: m/s
        atpGap             = 80.0, -- m to the train ahead -> emergency brake
        overspeedMs        = 5000, -- over the limit this long -> service brake
        interventionMargin = 10,   -- km/h over the limit -> service brake at once
    },

    pay = {
        enable                = true,
        perStop               = 150,
        account               = 'bank', -- 'cash' | 'bank'
        minDwellMs            = 8000,   -- doors open this long at a stop
        sameStationCooldownMs = 300000,
    },

    keys = { doors = 'G', reverser = 'R', vigilance = 'Q' }, -- defaults, rebindable; horn: E
    horn = { name = 'Horn', set = 'DLC_Apt_Yacht_Ambient_Soundset', bank = nil }, -- bank: custom audio bank
}
```

**Who may drive.** A player needs one of the `jobs` (job name → lowest grade) and, with `requireDuty`, must be on duty. Players with the `ace` may drive whatever their job, with or without a framework. Without a framework, grant it (`add_ace group.admin prompt_train.drive allow`) or set `jobs = {}` to let everyone drive. `lines` limits takeovers and depots to the listed line ids. Driving also needs `npcDriven.enable`.

| Block                              | What it sets                                                                                                                                                                                                                                                                                                       |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `units`, `sounds`, `stopTolerance` | Speed units in the cab, cab sound effects, and how far (m) from the stop marker a train still counts as berthed                                                                                                                                                                                                    |
| `takeover`                         | Taking over a line's own train: `maxSpeed` (m/s; `nil` = moving trains too) and `range` (m from the train). A taken-over train left standing away from a station for `idleReleaseMs` goes back to the autopilot                                                                                                    |
| `service`                          | Service trains. The player talks to the `dispatcher` ped at one of the `depots`, and the train starts at that platform. `perLine` caps service trains per line, `abandonMs` removes one whose driver has been out of the cab that long, and `train` fixes the train type (`nil` = the driver picks from the line's trains). A depot whose line isn't running is skipped |
| `controls`                         | Power and brake notches, `notchRepeatMs` while a key is held, `reverseMaxSpeed` (m/s), and `speedLimitFactor`: the line's limit is its `predictive.cruiseSpeed` × this                                                                                                                                             |
| `physics`                          | Full power, service brake, emergency brake and coasting drag, in m/s². A train's own `driving` block in `config/trains.lua` wins                                                                                                                                                                                   |
| `speedProfile`                     | Curve limits worked out from the track. A line can add fixed limits in its `line.lua`: `speedZones = { { from = 120, to = 180, limit = 60 } }` (0-based nodes, km/h)                                                                                                                                               |
| `vigilance`                        | Above `minSpeed` (m/s), the driver must acknowledge every `intervalMs`, within `warnMs`, or the emergency brake trips. Moving the controller, the doors key or the horn also counts                                                                                                                                 |
| `signals`                          | The cab signal turns yellow, then red, as the gap to the train ahead drops below the line's `collision.resumeDistance` and `stopDistance` (§ 5). Yellow cuts the limit to `cautionFactor` × limit, red to `redSpeed` (m/s). Closer than `atpGap` (m), the ATP trips the emergency brake. Staying over the limit for `overspeedMs`, or going `interventionMargin` km/h over it, applies the service brake |
| `pay`                              | `perStop` is paid into `account` once the doors have been open `minDwellMs` at a stop, and not again at the same station within `sameStationCooldownMs`. Needs a framework                                                                                                                                          |
| `keys`, `horn`                     | Default keys for doors, reverser and vigilance; players can rebind them in GTA's key bindings (FiveM section). The horn is always E. `horn.bank` loads a custom audio bank for the horn sound                                                                                                                       |

A depot's `station` is the platform key of one of the line's stops: the station id, plus `_1`, `_2`… for a station with several platforms (`lossantos_prompt_1`).

***

### 13. NPC passengers

NPC riders in the carriages and crowds waiting on the platforms. They only ride trains whose entry in `config/trains.lua` has a `passengers` block; out of the box, that is the metro. Passengers are local peds: each player's game spawns its own, and nothing is synced. Full guide: [NPC Passengers](npc-passengers.md).

```lua
passengers = {
    enable      = true,
    range       = 150.0,    -- around the player (m)
    maxPeds     = 40,
    perCarriage = { 1, 5 }, -- riders in a carriage when first seen
    waiting     = { 3, 7 }, -- peds waiting on a platform
    alightShare = 0.4,      -- share of riders leaving at each stop
    boardRange  = 22.0,     -- from an open door (m)
    refillMs    = 15000,
    models = {
        `a_m_y_business_01`, `a_m_y_business_02`, `a_m_m_business_01`, `a_m_y_hipster_01`,
        ...                 -- 16 models in total
    },
}
```

| Field         | Effect                                                                                                    |
| ------------- | --------------------------------------------------------------------------------------------------------- |
| `enable`      | `false` = no NPC passengers. Also needs `npcDriven.enable`                                                |
| `range`       | Carriages and platforms within this distance (m) of the player get passengers; peds further away are removed |
| `maxPeds`     | Most passenger peds at once on each player's game                                                         |
| `perCarriage` | `{ min, max }` riders placed in a carriage when it first comes into range                                 |
| `waiting`     | `{ min, max }` peds waiting on each platform                                                              |
| `alightShare` | Share of riders that get off at each stop (`0.4` = 40 %)                                                  |
| `boardRange`  | Waiting peds within this distance (m) of an open door board the train                                     |
| `refillMs`    | How often (ms) a platform's crowd is topped back up                                                       |
| `models`      | Ped models, picked at random                                                                              |

***

### Trains (config/trains.lua)

Every train type the script can run is an entry in `registry`, and `fleet` sets which ones run on each line. New trains come as train packs, which add their own entry when they start — see [Train Packs](train-packs.md).

{% hint style="warning" %}
Start every train pack **before** `prompt_train_script` in `server.cfg`. The script reads the installed trains once, when it starts.
{% endhint %}

{% code title="config/trains.lua" %}
```lua
return {
    default       = 'polar',
    defaultModels = DEFAULT_MODELS, -- { 'sloco', 'rest', 'scab', 'coal' }
    maxCarriages  = 14,

    fleet = {
        default   = { polar = 50, bullet = 50 },
        sandy     = { polar = 100 }, -- Sandy Shores <-> Paleto Bay: Polar Express only
        lossantos = { bullet = 100 }, -- Los Santos <-> Sandy Shores: AERION bullet train only (Polar Express if prompt_train_bullet is not running)
        roxwood   = { polar = 60, bullet = 40 }, -- Los Santos -> Roxwood
    },

    -- Live screens: kind 'passenger' = next stop, 'cab' = driver's desk
    screens = {
        bullet = {
            { kind = 'passenger', txd = 'prompt_bt_shared', txn = 'img_5664', image = 'atlas/img_5664.png' },
            { kind = 'cab', txd = { 'prompt_bt_head', 'prompt_bt_head_hi' }, txn = 'img_5940', image = 'atlas/img_5940.png' },
        },
    },

    registry = {
        polar = {
            label         = 'Polar Express',
            signature     = 'rest',
            expectedIndex = 28,
            resource      = 'prompt_train_polar_express',
            models        = DEFAULT_MODELS,
            driving       = { accel = 0.7, brake = 1.2 },
            smoke         = { ... },
            wagons        = { scab = { doors = ..., seats = ..., lights = ... }, ... },
        },

        bullet = {
            resource = 'prompt_train_bullet',
            cab      = { offset = vec3(0.0, 3.2, 2.0), heading = 0.0, anim = { ... }, exit = vec3(-0.2, -4.17, 1.8) },
        },

        freight = {
            label         = 'Freight',
            signature     = 'freight',
            expectedIndex = 23,
            consistSize   = 14, -- flatcars and containers; game config 0 is only 2 cars
            models        = { 'freight', 'freightcar', 'freightcar2', 'freightcont1', 'freightcont2', 'freightgrain', 'tankercar' },
            ambient       = true,
        },

        metro = {
            label         = 'Metro',
            signature     = 'metrotrain',
            models        = { 'metrotrain' },
            expectedIndex = 24,
            consistSize   = 2,
            driving       = { accel = 1.3, brake = 1.6 },
            passengers    = { doors = { ... }, stand = { ... }, seats = { ... } },
            ambient       = true,
            blockAmbient  = true,
            engineDoors   = { manual = true, ... },
        },
    },
}
```
{% endcode %}

| Key             | Effect                                                                                                      |
| --------------- | ----------------------------------------------------------------------------------------------------------- |
| `default`       | The fallback train. A line runs it when none of the train packs it lists is installed                       |
| `defaultModels` | Model list for an entry without `models` of its own. Leave it as is                                         |
| `maxCarriages`  | The most carriages the script reads behind one locomotive. Raise it only for a train pack with longer trains |
| `fleet`         | Which trains run on each line — see [Fleet mix](#fleet-mix)                                                 |
| `screens`       | Live screens drawn onto a train's own textures (below)                                                      |
| `registry`      | One entry per train type — see [Train registry](#train-registry)                                            |

`screens` turns a texture on the train into a live display: `kind = 'passenger'` shows the next stop, `kind = 'cab'` the driver's desk. `txd` and `txn` name the model texture to draw over (`txd` can be a list), and `image` is the background picture in `web/trainscreen/`. `screens.bullet` is for the AERION bullet train pack (`prompt_train_bullet`, coming soon) and does nothing until it is installed.

***

### Fleet mix

`fleet` is keyed by line id. Each value lists train keys with weights, and every new train on that line picks its type at random by weight: `{ polar = 60, bullet = 40 }` runs about 60 % Polar Express. `bullet` is the AERION bullet train pack (`prompt_train_bullet`, coming soon); until it is installed, the lines that list it run the Polar Express.

* An entry here wins over the `train` set in a line's own `line.lua`. Freight lines with neither use `fleet.default`; metro lines run `metro`.
* Keys are entries from `registry` below or from an installed train pack. Trains converted from GTA5-Mods (Kitsune Trains 7) with the free [Kitsune converter](https://github.com/Prompt-Coder/prompt_train_kitsune_converter) have keys like `kt_<name>` — see [Train Packs](train-packs.md).
* A train pack that is not running is left out of the mix. If none is left, the line runs `default`. If no train can run at all, the line goes dormant and the server console names the resource it needs.

{% hint style="info" %}
This `fleet` sets **which** trains run. The `fleet` number in a line's `line.lua` (or `npcDriven.trainsPerRoute`) sets **how many** run.
{% endhint %}

***

### Train registry

One entry per train type. The key (`polar`, `metro`, …) is the name lines, `fleet` and the blip settings use. When a train pack has the same key as an entry here, the fields set here win and the pack fills in the rest. That is why the `bullet` entry here only sets the driver's cab.

| Field            | Meaning                                                                                                                 |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `label`          | Name shown on blips and in the depot menu                                                                               |
| `signature`      | A carriage model only this train uses; it identifies the train's slot in the game's train-config pool                   |
| `expectedIndex`  | The pool slot tried first                                                                                               |
| `consistSize`    | Vehicles including the loco. Only needed when the pool holds several configs built from the same models                 |
| `index`          | Skip the search and use this pool slot as is                                                                            |
| `models`         | The train's models, **locomotive first**                                                                                |
| `resource`       | The resource that streams the models. The train is left out while it isn't running                                      |
| `smoke`          | Smoke plume from the loco, or `nil` for none                                                                            |
| `ambient`        | The game also spawns this train by itself. Those copies are turned away so only the script's own trains run            |
| `blockAmbient`   | `false` = leave the game's own copies alone                                                                             |
| `autoCloseDoors` | Safety net that closes doors left open on departure                                                                     |
| `engineDoors`    | Doors built into the model; `manual = true` = the script opens and closes them at stations                              |
| `wagons`         | Per carriage model: prop `doors`, `seats` and `lights`. Car carriers add `ramp` (the loading ramp) and `carry` (the deck area that holds parked cars) |
| `driving`        | Player-driver physics for this train, over `driving.physics` (§ 12)                                                     |
| `cab`            | Where a player driver sits: `{ offset, heading, anim, exit }`. `nil` = the model's own driver seat                      |
| `passengers`     | NPC passenger layout: door bones, a standing area and seats. `nil` = no NPC passengers (§ 13)                           |

**How a train's pool slot is found.** Each player's game spawns test trains to find it: first the slot that worked last time on that client, then `expectedIndex`, then the slots around it, up to `spawning.configScanWindow` past it, until one holds the `signature` model (with `consistSize` vehicles, if set). If none of the train's models is in the game, the search is skipped and the game console (F8) asks whether its resource is started. A failed search is retried at most once a minute.

The shipped entries:

* `polar` — the Polar Express, from `prompt_train_polar_express`. It is the `default` train.
* `bullet` — the AERION bullet train pack (`prompt_train_bullet`, coming soon). Only its driver's cab is set here. Until the pack is installed, this entry is skipped and the lines that list `bullet` run the Polar Express.
* `freight` — GTA's own freight train, 14 cars. It runs on the fallback line `lines/freight` (in `prompt_train_script-assets`) on the game's track 0, and only while no other freight line runs. Because it is `ambient`, the game's own freight trains are turned away while NPC trains are enabled.
* `metro` — GTA's metro train. It runs every metro line (the Los Santos metro and the monorail) and carries NPC passengers.

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
