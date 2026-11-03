---
description: >-
  Trains are separate resources called train packs. How the script finds them,
  how to put them on a line, and how to convert trains from GTA5-Mods.
icon: train-subway
---

# Train Packs

{% hint style="info" %}
This page applies to **version 2** (2.1.0) only.
{% endhint %}

Trains are not part of the script. The metro, the monorail and the freight fallback use the game's own trains; every other train is a separate resource called a **train pack**, such as the Polar Express (`prompt_train_polar_express`). You don't register a pack anywhere: when the script starts, it finds every train pack that is already running. You only choose which lines it runs on.

***

### Installing a train pack

1. Copy the pack into your `resources` folder.
2. In `server.cfg`, start it **above** `prompt_train_script` (the full order is in [Installation](README.md#installation)):

```
ensure prompt_train_polar_express
ensure prompt_train_script-assets
ensure prompt_train_script
```

3. Put its train on the lines you want with `fleet` in `config/trains.lua` — see [Which trains run on a line](#which-trains-run-on-a-line). The Polar Express already is.
4. Restart the server.

{% hint style="warning" %}
The script reads the installed trains **once, when it starts**. A pack that starts later isn't used, and the server console says `train pack <name> (<file>) started after prompt_train_script -- restart prompt_train_script to use it`.
{% endhint %}

***

### The Polar Express

`prompt_train_polar_express` is the Polar Express, the script's `default` train. `config/trains.lua` has a built-in `polar` entry for it, so it works without a `train_pack.lua` of its own. The version on the Cfx.re portal needs no update for 2.1.0; it only has to start before the script.

***

### Which trains run on a line

`fleet` in `prompt_train_script/config/trains.lua` sets which trains run on each line, keyed by line id. The shipped values:

{% code title="config/trains.lua" %}
```lua
fleet = {
    default   = { polar = 50, bullet = 50 },
    sandy     = { polar = 100 },
    lossantos = { bullet = 100 },
    roxwood   = { polar = 60, bullet = 40 },
},
```
{% endcode %}

* The numbers are chances. Every new train on the line picks one at random by weight: `{ polar = 60, mytrain = 40 }` runs about 60% Polar Express. They don't have to add up to 100.
* An entry here wins over the `train` in the line's own `line.lua`. A line with neither runs `metro` if it is a metro line, or `fleet.default` if it is a freight line.
* `bullet` is the AERION bullet train pack (`prompt_train_bullet`, coming soon). Until it is installed, the lines that list it run the Polar Express.
* A train pack that isn't installed or running is left out. If nothing is left, the line runs the `default` train (`default = 'polar'`, the Polar Express). If that can't run either, the line goes [dormant](lines-and-stations.md#dormant-lines): `line "<id>" is dormant: none of its trains is installed (needs <resource>)`.

This `fleet` sets **which** trains run. The `fleet` number in a line's `line.lua` sets **how many**. See also [Configuration → Fleet mix](configuration.md#fleet-mix). To give a train its own blip colour and legend name, add its key to `blips.consistColors` and `blips.consistLabels` ([Configuration § 6](configuration.md#6-train-blips)).

***

### What a train pack contains

A train pack is an ordinary resource with the train's models, its vehicle data, a `trains.xml` and a `train_pack.lua`. Its `fxmanifest.lua` needs:

| Line                                                                                                        | Why                                                                                                          |
| ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| `prompt_train_pack 'train_pack.lua'`                                                                        | How the script finds the pack. It names the pack's settings file                                             |
| `train_pack.lua` in `files { }`                                                                             | Every player's game reads it too                                                                             |
| `data_file 'TRAINCONFIGS_FILE' 'trains.xml'`                                                                | The train itself: its carriages, locomotive first. GTA adds it to the end of its list of train configs       |
| The vehicle `data_file` lines (`VEHICLE_METADATA_FILE`, `HANDLING_FILE`, `CARCOLS_FILE`, `VEHICLE_VARIATION_FILE`, …) | The models' vehicle data, as in any vehicle resource. The models go in `stream/`                 |
| `escrow_ignore { 'train_pack.lua' }`                                                                        | Needed if the pack is escrowed. The script reads `train_pack.lua` as plain Lua text, so an encrypted copy can't be read |

{% code title="fxmanifest.lua" %}
```lua
fx_version 'cerulean'
game 'gta5'
lua54 'yes'

prompt_train_pack 'train_pack.lua'   -- prompt_train_script finds the train by this line

files {
    'trains.xml',
    'train_pack.lua',
    'data/**/vehicles.meta',
    'data/**/carvariations.meta',
    'data/**/carcols.meta',
    'data/**/handling.meta',
}

data_file 'HANDLING_FILE'          'data/**/handling.meta'
data_file 'VEHICLE_METADATA_FILE'  'data/**/vehicles.meta'
data_file 'CARCOLS_FILE'           'data/**/carcols.meta'
data_file 'VEHICLE_VARIATION_FILE' 'data/**/carvariations.meta'
data_file 'TRAINCONFIGS_FILE'      'trains.xml'

escrow_ignore { 'train_pack.lua' }
```
{% endcode %}

`trains.xml` holds one `train_config` (the carriages, locomotive first) and a `train_config_group` that names it; the Polar Express's `trains.xml` is a good starting point. Where the train lands in GTA's list depends on load order, so each player's game finds it by its `signature` model (below). Like any custom prop, door panels or a ramp that the pack streams need their `.ytyp`, loaded with `data_file 'DLC_ITYP_REQUEST'`.

***

### `train_pack.lua`

`train_pack.lua` returns one table: the train's settings, with the same fields as an entry in `registry` in `config/trains.lua` ([Configuration → Train registry](configuration.md#train-registry)), plus a `key`. One pack holds one train. Positions on a carriage are offsets from its origin, in metres: `+X` right, `+Y` forward, `+Z` up.

{% code title="train_pack.lua" %}
```lua
return {
    key           = 'mytrain',          -- the name lines and fleet use
    label         = 'My Train',
    signature     = 'mytrain_dining',   -- a carriage model only this train uses
    expectedIndex = 28,
    models        = { 'mytrain_loco', 'mytrain_dining', 'mytrain_coach' }, -- locomotive first

    wagons = {
        mytrain_coach = {
            doors  = { doorModel = 'mytrain_door', sides = { ... } },
            seats  = {
                anim       = { dict = 'timetable@ron@ig_5_p3', clip = 'ig_5_p3_base' },
                animOffset = vec3(0.0, 0.5, 0.47),
                offsets    = { vec4(-1.07, 6.13, 1.88, 0.0), vec4(1.07, 6.27, 1.88, 0.0) },
            },
            lights = {
                { position = vec3(0.0, 0.0, 3.4), colour = { r = 255, g = 116, b = 24 }, intensity = 1.0, falloff = 3.7 },
            },
        },
    },
}
```
{% endcode %}

| Field             | Meaning                                                                                                                              |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `key`             | **Required.** The train's name, used by `fleet` and a line's `train`. Give every pack its own key                                   |
| `label`           | Name shown on blips and in the depot menu                                                                                            |
| `signature`       | A carriage model only this train uses. The script finds the train in GTA's list of train configs by it                              |
| `expectedIndex`   | The config number tried first. If the train isn't there, the script searches the numbers around it and remembers the result         |
| `consistSize`     | Vehicles including the locomotive. Only needed when several configs use the same models                                              |
| `index`           | Skip the search and use this config number as it is                                                                                  |
| `models`          | Every model of the train, **locomotive first**                                                                                       |
| `smoke`           | A smoke plume from the locomotive (`asset`, `effect`, `offset`, `rotation`, `bone`, `scale`, `colour`), as in the `polar` entry. Leave it out for none |
| `wagons`          | Per carriage model: `doors`, `seats` and `lights`, and for a car carrier `ramp` and `carry` (below)                                  |
| `cab` / `driving` | The player driver's seat and physics — see [Driving](driving.md#which-trains-can-be-driven)                                          |
| `passengers`      | NPC passengers — see [NPC Passengers](npc-passengers.md#the-passengers-block)                                                       |

`resource` is filled in for you with the pack's own name. The other fields of the [registry](configuration.md#train-registry) (`ambient`, `blockAmbient`, `engineDoors`, `autoCloseDoors`) work too; they are meant for trains the game also spawns by itself, or with doors built into the model, like the `metro` entry.

**A pack with the same key as an entry in `config/trains.lua`.** The two are merged: a field set in `config/trains.lua` wins, and the pack fills in the fields left out there. Whole fields are swapped, not merged inside — set `wagons` in `config/trains.lua` and the pack's `wagons` is ignored. Use this to change a pack's train without editing the pack. An entry with a `resource` but no `models`, like the shipped `bullet` one (it sets only the driver's `cab`), waits for its pack: while that pack isn't running, the entry is skipped, and each line that lists it prints `line "<id>": consist "<key>" left out, <resource> is not running`.

#### Doors, seats and lights

| Field    | Format                                                                                                                                                                                                                                                                                  |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `doors`  | `doorModel` (the door prop) and `sides`, one per doorway. A side is either a fixed spot — `trigger` (where the player opens it) and `panels = { { base, slide, rot } }` (each panel's closed position, how far it slides, its rotation) — or a bone on the carriage model: `bone` (where the closed door panel sits), `triggerHeight` (default 1.0 m above it) and `panels = { { prop, slide } }` |
| `seats`  | `anim = { dict, clip }`, `animOffset` (`vec3`), and `offsets`: one `vec4(x, y, z, heading)` per seat                                                                                                                                                                                  |
| `lights` | A list of `{ position = vec3, colour = { r, g, b }, intensity, falloff }`                                                                                                                                                                                                              |

The built-in `polar` entry in `config/trains.lua` is a complete example of all three.

#### Car carrier

A carriage can carry cars. Give it a `ramp` and a `carry` box:

{% code title="train_pack.lua" %}
```lua
wagons = {
    mytrain_carrier = {
        ramp  = { prop = 'mytrain_ramp', hinge = vec3(0.0, -7.4, 1.3), maxAngle = 135.0, speed = 25.0 },
        carry = { halfWidth = 1.6, yMin = -7.4, yMax = 6.8, zMin = 1.0, zMax = 3.2 },
    },
},
```
{% endcode %}

| Field           | Meaning                                                                                                                       |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `ramp.prop`     | The ramp model, streamed by the pack                                                                                          |
| `ramp.hinge`    | Where the ramp turns on the carriage (`vec3`). Opening, it swings out over the carriage's rear                                |
| `ramp.maxAngle` | How far it can open, in degrees. It stops earlier where its far edge meets the ground or a platform                           |
| `ramp.speed`    | How fast it turns, in degrees per second (default 25)                                                                         |
| `carry`         | The deck, in metres from the carriage's origin: `halfWidth` to each side, `yMin` to `yMax` along it, `zMin` to `zMax` in height |

Players open and close the ramp from the ramp itself: **Open ramp** / **Close ramp**, with your target resource or `[E]`, whether the train is moving or not. It doesn't close while a vehicle stands on it. An empty car that stands still on the deck for about two seconds is fixed in place, so it can't slide while the train moves. It is let go as soon as someone starts getting in.

***

### Checking a pack

| Where                    | What                                                                                                        | What it tells you                                                                                                                                                                             |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Server console           | `train_routes`                                                                                              | Every line with its train or mix (`sandy (polar)`, `myline (polar x60 / mytrain x40)`), every dormant line and what it needs, and under **registered consists** each train's models, `signature`, resource state and the lines that use it |
| Game console (F8)        | `train_config_index <key>`                                                                                  | The train's config number: `[train_config] "<key>" = <number>`. Add `refresh` to check it again. Without a key, it checks the `default` train                                                 |
| Server console, at start | `train pack @<resource>/<file> could not be read: <error>`                                                  | `train_pack.lua` failed to load, or it doesn't return a table with a `key` — for example, an escrowed file that isn't in `escrow_ignore`                                                     |
| Server console, at start | `line "<id>" asks for consist "<key>", which neither config/trains.lua nor a train pack has -- left out`    | A `fleet` entry or a line's `train` names a train that isn't installed or isn't running, or has a typo                                                                                       |
| Game console (F8)        | `[train_config] FAILED to resolve "<key>" (signature "<model>")`                                            | None of the train configs searched holds the `signature` model. Check `trains.xml`, `signature`, and that the pack is started                                                               |

***

### Trains from GTA5-Mods (Kitsune Trains 7)

**Kitsune Trains 7** by Foxunitone, on gta5-mods.com, is a pack of trains for singleplayer GTA V. Our free [Kitsune converter](https://github.com/Prompt-Coder/prompt_train_kitsune_converter) turns the trains you pick into train packs for the script. You don't need OpenIV, CodeWalker or a GTA install.

1. Download Kitsune Trains 7 from gta5-mods.com. You get a `.zip`; don't unzip it.
2. Download the latest `PromptTrainConverter_KitsuneTrains_v*.zip` from the converter's [Releases](https://github.com/Prompt-Coder/prompt_train_kitsune_converter/releases) and unzip it.
3. Put the Kitsune Trains `.zip` next to `PromptTrainConverter_KitsuneTrains.exe`. You can also leave it in your Downloads folder (the converter looks there too), or drag the zip onto the exe.
4. Double-click the exe, type the numbers of the trains you want (for example `22, 25`) and press Enter.
5. A `[kt_trains]` folder appears next to the zip. Follow the `HOW_TO_INSTALL.txt` inside it (summary below).

{% hint style="info" %}
Windows may show **Windows protected your PC**, because the exe isn't signed. Click **More info**, then **Run anyway**.
{% endhint %}

The `[kt_trains]` folder holds:

| Item                 | What it is                                                         |
| -------------------- | ------------------------------------------------------------------ |
| `kt_models`          | The models and vehicle data of every train you picked              |
| `kt_<train>`         | One small folder per train, with its `trains.xml` and `train_pack.lua` |
| `HOW_TO_INSTALL.txt` | The install steps, and the names of your trains                    |

To install them:

1. Copy the whole `[kt_trains]` folder into your server's `resources`.
2. In `server.cfg`, add `ensure [kt_trains]` **above** the line that starts `prompt_train_script`.
3. Put the trains on a line in `prompt_train_script/config/trains.lua` → `fleet`. Their names are `kt_` + the train's config name; `HOW_TO_INSTALL.txt` lists them. Replace `kt_example` below with one of yours:

{% code title="config/trains.lua" %}
```lua
fleet = {
    -- ...
    lossantos = { kt_example = 100 },             -- only this train
    sandy     = { polar = 50, kt_example = 50 },  -- mixed: the numbers are chances
},
```
{% endcode %}

4. Restart the whole server.

**Limits**

* Trains marked `*` in the converter's list had their wheels animated by the mod's singleplayer script, so in FiveM their wheels may not turn.
* Trains longer than 12 vehicles are shortened (the end car is kept).
* The trains have no doors, seats or interior, so tickets, boarding and seats do nothing on them.

{% hint style="info" %}
Please don't re-upload converted trains. Point people to the mod on gta5-mods.com and to the converter instead. Credit: Kitsune Trains 7 by Foxunitone.
{% endhint %}
