---
icon: route
---

# Lines & Stations

{% hint style="info" %}
This page applies to **version 2** (2.1.0) only.
{% endhint %}

All map data — every station and every line — lives in `prompt_train_script-assets`, as plain Lua files. `prompt_train_script` has none of its own; it only reads what this resource declares. Add, edit, or delete a station or line here and restart both resources to pick it up. A change that touches `traintracks.xml` (a new line, new rails, or a line's `type`, `mode`, `speed` or `brakingDistance`) also needs `train_build` and a full server restart — see [Track files](#track-files).

```
prompt_train_script-assets/
├── stations/
│   ├── metro/       -- e.g. burton.lua, davis.lua
│   └── freight/      -- e.g. lossantos_prompt.lua, sandy_prompt.lua
├── lines/
│   └── <line id>/
│       ├── line.lua
│       ├── track.dat        -- raw rail rows GTA reads at runtime
│       └── points.json       -- point list used for predictive spawning
├── templates/        -- line.lua and station.lua to copy from (not loaded)
└── traintracks.xml   -- the track list, written by train_build
```

{% hint style="success" %}
You don't have to write these files by hand. The [**Train Editor**](https://train-editor.prompt-mods.com/) builds stations and lines in your browser: import your `.dat` track files, place stations, draw lines, then export the `stations/` and `lines/` folders for this resource.
{% endhint %}

<a href="https://train-editor.prompt-mods.com/" class="button primary">Open the Train Editor</a>

A station's id is taken from its filename; a line's id is taken from its folder name. Subfolders under `stations/` (`metro/`, `freight/`) are purely organisational — a line can reference a station in either one.

***

### Templates

`prompt_train_script-assets/templates/` holds two files with the main fields explained in comments: `line.lua` and `station.lua`. The folder is not loaded, so nothing in it runs.

* **New line:** copy `templates/line.lua` to `lines/<id>/line.lua`, next to the line's `track.dat` and `points.json` (`train_convert <file.dat> <id>` makes both, see [Converter](converter.md)). Run `train_build`, restart the server, then run `train_assets_validate`.
* **New station:** copy `templates/station.lua` to `stations/<type>/<id>.lua`. The file name is the station id that lines refer to. Only `label` and `coords` (or `platforms`) are needed; delete what you don't use. Restart both resources, then run `train_assets_validate`.

***

### Stations

A station is a physical place trains stop — the prop board, ticket machine, blip, and PA speakers all attach to it. **Stations are reusable across lines**: `burton.lua` is referenced by both the metro loop and (if you add one) any other line passing through it.

```lua
-- stations/metro/burton.lua
Station {
    label  = 'Burton',
    centre = vec3(-294.680, -323.400, 8.150),
    worldTolerance = 12.0,   -- platforms 25-60m apart need a wider match radius

    platforms = {
        { coords = vec3(-287.121, -301.918, 8.149), track = 1 },
        { coords = vec3(-302.231, -344.879, 8.150), track = 2 },
    },

    blip  = { label = 'Burton Metro Station', sprite = 79, colour = 5 },
    zone  = { radius = 55.0, thickness = 30.0 },
    board = { preset = 'tracks' },
}
```

A single-platform station skips `platforms` and puts `coords` directly on the station (see the `paletobay_prompt` example in [Tickets](tickets.md)). Other optional fields: `resource` (this station only exists while a named resource is running; otherwise lines pass through without stopping — see Variants below), `machines` ([Tickets](tickets.md)), `board` ([Departure Boards](departure-boards.md)), `pa` ([Audio Announcements](audio-announcements.md)), and `alight`. `templates/station.lua` has an example of each.

`alight = vec4(x, y, z, heading)` is only for the last stop of a [one-way line](#one-way-lines): it is where players still aboard are put when the train leaves for the depot. Without it, a spot next to the rails at the stop's node is found automatically. The shipped `roxwood` station sets one.

***

### Lines

A line is a route: its trains, its rails, and the stops along it.

```lua
-- lines/sandy/line.lua
Line {
    label    = 'Sandy Shores',
    type     = 'freight',    -- 'freight' | 'metro' -- also groups blips, see Configuration § 6
    fleet    = 2,
    loop     = true,
    requires = 'prompt_sandy_traintunnel',

    speed           = 20,     -- GTA's own track speed, written into traintracks.xml
    brakingDistance = 50,
    pa              = 'pa_route_sandy',

    stops = {
        { station = 'paletobay_prompt', node = 667  },
        { station = 'sandy_prompt',     node = 1511 },
    },
}
```

The Sandy Shores line `requires` the Sandy Shores train tunnel map (`prompt_sandy_traintunnel`, in the release zip), because its rails run through the tunnel east of Sandy Shores.

| Field                               | Meaning                                                                                                                                                                                                                                              |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `stops[].station`                   | A station id from `stations/`                                                                                                                                                                                                                        |
| `stops[].node`                      | The rail node index (0-based) where the train stops for that station — find it with `/toggletrainnodes`                                                                                                                                              |
| `stops[].platform`                  | Which of the station's `platforms` entries this stop uses (omit for a single-platform station)                                                                                                                                                       |
| `stops[].destination`               | Overrides the label shown on departure boards for that stop, if different from the line's usual direction                                                                                                                                            |
| `type`                              | `'freight'` (default) or `'metro'`. A metro line runs GTA's metro train unless told otherwise; a freight line takes its trains from `fleet` in `config/trains.lua` — see [Train Packs](train-packs.md)                                              |
| `fleet`                             | How many trains run on this line (default 1). `npcDriven.trainsPerRoute` in `config/config.lua` wins. Not the same as `fleet` in `config/trains.lua`, which picks *which* trains run                                                               |
| `mode`                              | `'loop'` (default): round its track for ever. `'pingpong'`: back and forth between the two ends of its track. `'oneway'`: see [One-way lines](#one-way-lines)                                                                                       |
| `loop`                              | The older way to set the mode: `loop = false` is `mode = 'pingpong'`. Use one or the other                                                                                                                                                          |
| `train`                             | Which train runs here: a train key (`'polar'`) or a weighted mix (`{ polar = 80, mytrain = 20 }`). An entry for this line in `fleet` in `config/trains.lua` wins — see [Train Packs](train-packs.md)                                               |
| `track`                             | Usually left unset (defaults to this line's own `track.dat`, listed in `traintracks.xml` by `train_build`). `{ id = 3 }` runs on one of the game's own tracks instead — the shipped `metro` line uses track 3 and `freight` uses track 0; such a line isn't listed in `traintracks.xml`, but its folder still holds a `points.json` and a `track.dat` copy of the rails. A table `{ resource, file }` points at another resource's rail file — see [Integrating Another Map Resource](integrating-another-map-resource.md) |
| `requires`                          | A resource name (or list) that must be running for this line to be active at all. Otherwise the line is [dormant](#dormant-lines)                                                                                                                   |
| `conflicts`                         | A resource name (or list) that is stopped while this line's `requires` are running, because both would control the same trains. The console shows a `PROMPT TRAIN CONFLICT` box; remove that resource's `ensure` line from `server.cfg` to silence it |
| `fallback`                          | `true` = the line runs only while no other line of the same `type` runs — see [Fallback lines](#fallback-lines)                                                                                                                                     |
| `speed` / `brakingDistance`         | GTA's own track speed and braking distance, written into `traintracks.xml` (default 20 / 50, metro 8 / 10). They don't set how fast trains run: NPC trains cruise at `predictive.cruiseSpeed`, and a player driver's line limit is that times `driving.controls.speedLimitFactor` |
| `speedZones`                        | Speed limits for player drivers on stretches of the line: `{ { from = <node>, to = <node>, limit = <km/h> }, ... }` — see [Driving](driving.md#speed-limits-and-signals)                                                                           |
| `oneway`                            | Settings for `mode = 'oneway'` — see [One-way lines](#one-way-lines)                                                                                                                                                                                 |
| `predictive` / `collision` / `blip` | Any field from [Configuration](configuration.md) §4/§5/§6 can be overridden per line here                                                                                                                               |

A stop whose station file doesn't exist is skipped with a console warning; the rest of the line still runs. A line that can't run at all shows as **dormant** in `train_routes` rather than crashing — see [Dormant lines](#dormant-lines).

Lines may share rails: the Roxwood line shares stretches of rail with the Los Santos and Sandy Shores lines. The anti-collision spacing ([Configuration](configuration.md) §5) also applies between trains of different lines.

***

### Shipped lines

| Line        | Route                                                                                    | Trains                                                                                                                                       | Needs                                           |
| ----------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| `lossantos` | Paleto Bay, Power Station, Los Santos (both platforms), Sandy Shores — loop              | 5 — the AERION bullet train pack (`prompt_train_bullet`, coming soon); until it is installed, the line runs the Polar Express                | —                                               |
| `sandy`     | Paleto Bay and Sandy Shores — loop                                                       | 2 — the Polar Express                                                                                                                        | `prompt_sandy_traintunnel` (in the release zip) |
| `roxwood`   | Los Santos > Sandy Shores > Paleto Bay > Roxwood — [one-way](#one-way-lines)            | 3 — a 60/40 mix of the Polar Express and the AERION bullet train pack (`prompt_train_bullet`, coming soon); until it is installed, the Polar Express | `amb-roxwood`                                   |
| `metro`     | Los Santos Transit metro, on the game's own track 3 — loop                              | 8 — GTA's metro train                                                                                                                        | —                                               |
| `monorail`  | The elevated loop of `cfx-nteam-monorail-map` — loop                                     | 4 — GTA's metro train                                                                                                                        | `cfx-nteam-monorail-map`                        |
| `freight`   | GTA's own freight loop (track 0), no stations — [fallback](#fallback-lines)              | 2 — GTA's freight train                                                                                                                      | —                                               |

The number of trains is each line's `fleet`. Which trains run is set by `fleet` in `config/trains.lua` — see [Train Packs](train-packs.md#which-trains-run-on-a-line).

***

### One-way lines

A one-way line doesn't loop. Its trains enter near the start of the line, call at every stop, and terminate at the **last** stop. There they wait, then run empty to a depot point further along the rails, fade out and are removed. A new train then enters at the start. The shipped Roxwood line works this way:

```lua
-- lines/roxwood/line.lua
Line {
    label     = 'Roxwood',
    type      = 'freight',
    fleet     = 3,
    mode      = 'oneway',
    requires  = 'amb-roxwood',
    conflicts = 'amb-roxwood-trains',

    speed           = 20,
    brakingDistance = 50,

    oneway = {
        spawn      = { from = 0, to = 470 },
        spawnClear = 150.0,
        dwellMs    = 45000,
        depotNode  = 2992,
        depotSpeed = 8.0,
        fadeMs     = 2500,
    },

    stops = {
        { station = 'lossantos_prompt', node = 563,  platform = 2, destination = 'Roxwood' },
        { station = 'sandy_prompt',     node = 1789, destination = 'Roxwood' },
        { station = 'paletobay_prompt', node = 2531, destination = 'Roxwood' },
        { station = 'roxwood',          node = 2922, destination = 'Terminus' },
    },
}
```

| Field               | Default                             | Meaning                                                                                         |
| ------------------- | ----------------------------------- | ----------------------------------------------------------------------------------------------- |
| `oneway.spawn`      | `from = 0`, `to` = about the first fifth of the line | The node range where new trains may enter                                          |
| `oneway.spawnClear` | `150.0`                             | Extra metres, beyond `predictive.spawnDistance`, that no player may be within where a train enters |
| `oneway.dwellMs`    | `45000`                             | How long a train waits at the terminus (ms)                                                     |
| `oneway.depotNode`  | near the end of the rails           | The node past the terminus where the train is removed                                           |
| `oneway.depotSpeed` | `8.0`                               | Speed (m/s) of the empty run to the depot                                                       |
| `oneway.fadeMs`     | `2500`                              | How long the train fades out before it is removed (ms)                                          |

* A one-way line needs `spawning.mode = 'predictive'` in `config/config.lua` (the shipped setting). With `'always'`, the line stays [dormant](#dormant-lines).
* The line's `track.dat` must run in the direction of travel: from where trains enter, past the terminus, to the depot. If it runs the other way, the console says `one-way line "<id>" is running BACKWARDS along its track.dat -- reverse the node order`.
* At the terminus, players near or on the train are told it terminates here, and 10 seconds before it leaves that its doors are closing. Anyone still aboard when it is removed is put on the platform, at the terminus station's `alight` point if it has one.
* Departure boards show the terminus as the destination at every stop, unless a stop sets its own `destination`.

**The Roxwood line** runs Los Santos > Sandy Shores > Paleto Bay > Roxwood. It needs the `amb-roxwood` map (`requires`) and stays dormant without it. While it runs, `amb-roxwood-trains` is stopped (`conflicts`), because both would control the same trains.

***

### Fallback lines

`fallback = true` makes a line a stand-in: it runs only while no other line of the same `type` runs. The shipped `freight` line is one:

```lua
-- lines/freight/line.lua
Line {
    label    = 'Freight',
    type     = 'freight',
    fleet    = 2,
    loop     = true,
    fallback = true,
    track    = { id = 0 },
    train    = 'freight',
}
```

It runs GTA's own freight train on the game's own freight loop (track 0), with no stations, so a server where no other freight line can run — for example, with no train pack installed — still has trains. As soon as another freight line runs, `train_routes` lists this one as `dormant line : freight -- needs no other freight line running`. That is normal. The freight cars have no doors or seats, so there is nothing to board.

***

### Dormant lines

A line that can't run is **dormant**: it is skipped, and every other line keeps running. When the script starts, the server console says why, and `train_routes` lists it as `dormant line : <id> -- needs <...>`. The first reason that applies is shown:

| `needs …`                            | Why                                                                                                                                                                                               | Fix                                                                                     |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `no other <type> line running`       | A [fallback line](#fallback-lines), set aside because another line of its `type` runs. No console warning                                                                                         | Nothing — this is normal                                                                |
| `<resource> (<state>)`               | A resource in `requires` (or the `when` of the line's mounted [variant](#variants)) isn't running. Console: `line "<id>" is dormant: <resource> (<state>) not running`                          | Start it before `prompt_train_script`. If you don't use that map, the line just stays off |
| `traintracks.xml`                    | The line's rails aren't in `traintracks.xml` yet. Console: `line "<id>" is not mounted yet -- run train_build in the server console and restart`                                                 | Run `train_build`, then restart the server                                              |
| `config.spawning.mode = 'predictive'` | A [one-way line](#one-way-lines), but `spawning.mode` is `'always'`. Console: `line "<id>" is one-way, which needs config.spawning.mode = 'predictive' -- dormant`                               | Set `spawning.mode = 'predictive'` in `config/config.lua`                               |
| `one of its stations`                | None of its stops can be used — for example, every station on it is off because its `resource` isn't running. Console: `line "<id>" is dormant: none of its stations is available`              | Start the stations' map resources before `prompt_train_script`                          |
| a train pack resource, or `a train`  | None of its trains is installed, not even the `default` train. Console: `line "<id>" is dormant: none of its trains is installed (needs <resource>)`                                            | Install the train pack and start it before `prompt_train_script` — see [Train Packs](train-packs.md) |

***

### Track files

`track.dat` and `points.json` describe the physical rail. You almost never hand-write these:

* **New line from a captured route** — use `train_convert`, see [Converter](converter.md).
* **Everything else** — run `train_build` (server console) after adding or editing any line or variant. It rewrites `traintracks.xml` from the line folders, and the spliced rails of any active variant. GTA reads the track list only at startup, so **restart the server** afterwards — restarting the resources is not enough.
* `train_assets_validate` checks the result matches what's mounted, and is safe to run any time.

Lines on the game's own tracks (`track = { id = ... }`) are not listed in `traintracks.xml`. A line whose rails come from a resource that isn't installed is left out, and `train_build` says `left out: <id> (needs <resource>)`.

**Track numbers are found in game.** `train_build` lists the lines in `traintracks.xml` from track 12 up, but another resource that registers its own track file can shift GTA's numbering. Before it spawns any train, each player's game checks which track each line really landed on (it test-spawns a train on each one), so lines don't get mixed up. If the numbers shifted, the game console (F8) shows `[track_ids] track numbering shifted by <n> -- check for a resource with its own TRAINTRACK_FILE`, and trains still run. `[track_ids] FAILED to find our tracks` usually means `traintracks.xml` isn't mounted yet: run `train_build` and restart the server.

***

### Variants

A variant lets the *same line* run on different rails or stop at different stations depending on which map resource is active — e.g. the base Prompt map's Paleto Bay platform vs. an RTX Paleto Bay overhaul.

```lua
-- lines/sandy/line.lua
Line {
    label = 'Sandy Shores',
    ...
    stops = {
        { station = 'paletobay_prompt', node = 667  },
        { station = 'sandy_prompt',     node = 1511 },
    },

    variants = {
        {
            when     = 'rtx_paleto_project_data',
            rails    = { from = 546, to = 711, resource = 'rtx_paleto_project_data', file = 'trains1.dat' },
            stations = { paletobay_prompt = { station = 'paletobay_rtx', node = 653 } },
        },
    },
}
```

| Field                           | Meaning                                                                                                                                                                                           |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `when`                          | A resource name (or list) — this variant applies while it's running                                                                                                                               |
| `rails.from` / `rails.to`       | The node range in the variant's own rail file to splice into this line's geometry                                                                                                                 |
| `rails.resource` / `rails.file` | Where that rail range comes from                                                                                                                                                                  |
| `stations`                      | Maps a base stop's station id to its variant replacement — a station id string (auto-detects the nearest node on the spliced rail), or a table `{ station, node, platform }` for an explicit node |

**Explicit vs. auto-detected node:** giving just a station id (`stations = { paletobay_prompt = 'paletobay_rtx' }`) makes the build step guess the nearest matching node on the spliced-in rail. If that guess is wrong, or you already know the number, give it explicitly:

```lua
stations = { paletobay_prompt = { station = 'paletobay_rtx', node = 653 } },   -- node: /toggletrainnodes
```

Use `/toggletrainnodes` in-game to find that number: it draws a debug sphere and label over every rail node within 120m of the player, for every line, so you can walk up to the platform you want and read off its node index.

**Resolution consistency:** which variant is active is decided the same way on client and server — from what `traintracks.xml` actually has mounted, not from a live resource-state check (a data-only resource like `rtx_paleto_project_data` isn't visible to `GetResourceState` on the client, so checking that directly would disagree between the two sides). This means a variant only takes effect after `train_build` + a restart, never instantly when you `ensure`/`stop` its resource.

While a variant is mounted, its `when` resource also counts as one of the line's `requires`: if that resource stops running, the line goes [dormant](#dormant-lines) until you run `train_build` and restart the server.
