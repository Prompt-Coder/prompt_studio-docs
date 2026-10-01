---
icon: route
---

# Lines & Stations

{% hint style="info" %}
This page applies to **version 2** (2.0.0-beta) only.
{% endhint %}

All map data — every station and every line — lives in `prompt_train_script-assets`, as plain Lua files. `prompt_train_script` has none of its own; it only reads what this resource declares. Add, edit, or delete a station or line here and restart both resources to pick it up.

```
prompt_train_script-assets/
├── stations/
│   ├── metro/       -- e.g. burton.lua, davis.lua
│   └── freight/      -- e.g. lossantos_prompt.lua, sandy_prompt.lua
└── lines/
    └── <line id>/
        ├── line.lua
        ├── track.dat        -- raw rail rows GTA reads at runtime
        └── points.json       -- point list used for predictive spawning
```

{% hint style="success" %}
You don't have to write these files by hand. The [**Train Editor**](https://train-editor.prompt-mods.com/) builds stations and lines in your browser: import your `.dat` track files, place stations, draw lines, then export the `stations/` and `lines/` folders for this resource.
{% endhint %}

<a href="https://train-editor.prompt-mods.com/" class="button primary">Open the Train Editor</a>

A station's id is taken from its filename; a line's id is taken from its folder name. Subfolders under `stations/` (`metro/`, `freight/`) are purely organisational — a line can reference a station in either one.

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

A single-platform station skips `platforms` and puts `coords` directly on the station (see the `paletobay_prompt` example in [Tickets](tickets.md)). Other optional fields: `resource` (this station only exists while a named resource is running — see Variants below), `machines` ([Tickets](tickets.md)), `board` ([Departure Boards](departure-boards.md)), `pa` ([Audio Announcements](audio-announcements.md)).

***

### Lines

A line is a route: rolling stock, a loop of rails, and the stops along it.

```lua
-- lines/sandy/line.lua
Line {
    label = 'Sandy Shores',
    type  = 'freight',    -- 'freight' | 'metro' -- also groups blips, see Configuration § 6
    fleet = 2,
    loop  = true,

    speed           = 20,     -- optional per-line predictive.cruiseSpeed override
    brakingDistance = 50,
    pa              = 'pa_route_sandy',

    stops = {
        { station = 'paletobay_prompt', node = 667  },
        { station = 'sandy_prompt',     node = 1511 },
    },
}
```

| Field                               | Meaning                                                                                                                                                                                                                                              |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `stops[].station`                   | A station id from `stations/`                                                                                                                                                                                                                        |
| `stops[].node`                      | The rail node index (0-based) where the train stops for that station — find it with `/toggletrainnodes`                                                                                                                                              |
| `stops[].platform`                  | Which of the station's `platforms` entries this stop uses (omit for a single-platform station)                                                                                                                                                       |
| `stops[].destination`               | Overrides the label shown on departure boards for that stop, if different from the line's usual direction                                                                                                                                            |
| `track`                             | Usually left unset (defaults to this line's own `track.dat`); a table `{ resource, file }` points at another resource's rail file instead — see [Integrating Another Map Resource](integrating-another-map-resource.md) |
| `requires`                          | A resource name (or list) that must be running for this line to be active at all                                                                                                                                                                     |
| `predictive` / `collision` / `blip` | Any field from [Configuration](configuration.md) §4/§5/§6 can be overridden per line here                                                                                                                               |

A line that references a station id which doesn't exist, or whose `requires` isn't met, shows as **dormant** in `train_routes` rather than crashing.

***

### Track files

`track.dat` and `points.json` describe the physical rail. You almost never hand-write these:

* **New line from a captured route** — use `train_convert`, see [Converter](converter.md).
* **Everything else** — run `train_build` (server console) after editing any line or variant; it regenerates `traintracks.xml`, every line's `track.dat`, and `points.json` from the line definitions.
* `train_assets_validate` checks the result matches what's mounted, and is safe to run any time.

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
