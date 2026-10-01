---
description: >-
  train_convert turns a captured .dat route file into a ready-to-use line in
  prompt_train_script-assets.
icon: conveyor-belt-boxes
---

# Converter

{% hint style="info" %}
**Version 2** (2.0.0-beta) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

`train_convert` turns a captured `.dat` route file into a ready-to-use line — no manual `routes.json`/`points.json` bookkeeping.

### 1. Capture a route

Record the rail as a `.dat` file (first line = point count, then one `x y z flag` row per node — the same format GTA itself uses for `traintracks.xml` entries). Drop it in:

```
prompt_train_script/routes_convert/<file>.dat
```

### 2. Run the converter

From the **server console**:

```
train_convert <file.dat> <line_id> [unused] [label]
```

```
train_convert trains13.dat sandy - "Sandy Shores"
```

This:

1. Parses every `x y z flag` row from the file.
2. Writes `prompt_train_script-assets/lines/<line_id>/points.json` (the point list, used for predictive spawning and geometry lookups) and `.../track.dat` (the raw rail rows GTA reads at runtime).
3. If `lines/<line_id>/line.lua` **doesn't exist yet**, prints a ready-to-paste `Line{}` snippet to the console, pre-filled with one `stops` entry per node whose flag bit marks it as a station stop (bit 1 or 2). You fill in each stop's `station = '<station id>'` with an id from `stations/`.
4. If `line.lua` **already exists**, leaves it untouched — only the geometry files are refreshed. Restart to pick up new geometry against the existing line definition.

### 3. Finish the line

Paste the printed snippet into `lines/<line_id>/line.lua`, fill in station ids (create new [Station](lines-and-stations.md) entries first if needed), then:

```
train_build
```

restart both resources, and:

```
train_assets_validate
```

to confirm the line, its track id, and its stops are all consistent.

***

### Notes

* The line id may only contain letters, digits, `_`, and `-`.
* `train_convert` only ever writes into `lines/<line_id>/`; it never touches `config/config.lua` or any other line. Legacy `routes.json`/`config.routes` registration from older versions of the script no longer exists.
* Re-running the converter against the same `line_id` after edits just refreshes `points.json`/`track.dat` — safe to do repeatedly while tuning a captured route.

***

## Version 1

Everything below applies to **1.0.x** (latest: 1.0.4.1).

### Why a Converter?

Train routes in GTA V are defined as sequences of 3D waypoints stored in `.dat` files (`trains13.dat`, `trains14.dat`). The script needs those waypoints in JSON form so it can:

* Calculate the distance between a train and each station node.
* Estimate arrival times (ETAs).
* Determine the train's direction of travel.

The converter reads the raw `.dat` format and writes the result directly into `routes.json` — no manual editing required.

***

### How the `.dat` Format Works

A train route `.dat` file looks like this:

```
4096
-538.93 4669.99 90.46
-534.21 4663.12 89.87
...
```

* **Line 1** — the total number of points (used as a sanity check).
* **Subsequent lines** — one point per line: `x y z` separated by spaces.

The converter reads every line, parses the coordinates, and stores them as a JSON array:

```json
{
  "routes": {
    "lossantos": {
      "points": [
        { "x": -538.93, "y": 4669.99, "z": 90.46 },
        { "x": -534.21, "y": 4663.12, "z": 89.87 }
      ]
    }
  }
}
```

***

### Step-by-Step Usage

#### Step 1 — Place the file

Create the folder `routes_convert/` inside the resource root (if it doesn't exist) and copy your `.dat` file into it:

```
prompt_train_script/
└── routes_convert/
    └── myroute.dat
```

#### Step 2 — Run the command (server console)

```
train_convert myroute.dat myroute
```

Arguments:

1. **filename** — the `.dat` file inside `routes_convert/`. The `.dat` extension is optional.
2. **route name** — the internal key for this route (letters, digits, `_`, `-` only). This key must match what you use in `config.routes`.

Example output:

```
[prompt_train_script] Parsed 4096 points (expected 4096) from myroute.dat
[prompt_train_script] Added route "myroute" -> 4096 points. routes.json saved.
[prompt_train_script] Remember to add "myroute" to config.routes in config/config.lua (id + label).
```

#### Step 3 — Register the route in config

```lua
-- config/config.lua
routes = {
    lossantos = { id = 25, label = 'Los Santos'  },
    sandy     = { id = 24, label = 'Sandy Shores' },
    myroute   = { id = 26, label = 'My Route'    },  -- add this
},
```

The `id` here is the GTA V `CreateMissionTrain` track ID for this route — it must match the `.dat` file's actual track.

#### Step 4 — Add trains for the route

```lua
npcDriven = {
    trainsPerRoute = {
        lossantos = 5,
        sandy     = 2,
        myroute   = 3,   -- add this
    },
},
```

#### Step 5 — Restart the resource

The new route is immediately usable after `routes.json` is saved (the in-memory `NpcDriven.routes` table is updated live, but a restart is needed for the NPC spawn configuration to take effect).

***

### Updating an Existing Route

Running `train_convert` with an existing route name **overwrites** it in `routes.json`:

```
train_convert myroute_v2.dat myroute
```

```
[prompt_train_script] Updated route "myroute" -> 4098 points. routes.json saved.
```

***

### Troubleshooting

| Error                                | Cause                                   | Fix                                                           |
| ------------------------------------ | --------------------------------------- | ------------------------------------------------------------- |
| `File not found`                     | `.dat` file is not in `routes_convert/` | Move it to the correct folder and retry                       |
| `First line must be the point count` | The file is not in the expected format  | Verify the file starts with an integer on the first line      |
| `Failed to parse any points`         | No valid `x y z` lines found            | Check the file encoding (should be UTF-8 or ASCII)            |
| `Failed to save routes.json`         | File permissions                        | Make sure the server process can write to the resource folder |

***

### routes.json Structure

You can also edit `routes.json` manually if needed. The full structure is:

```json
{
  "routes": {
    "lossantos": {
      "points": [
        { "x": 100.0, "y": 200.0, "z": 30.0 },
        { "x": 101.5, "y": 201.0, "z": 30.1 }
      ]
    },
    "sandy": {
      "points": [ ... ]
    }
  }
}
```

Keep the file valid JSON — a syntax error will prevent the resource from starting.
