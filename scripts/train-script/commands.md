---
icon: terminal
---

# Commands

{% hint style="info" %}
**Version 2** (2.1.0) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

### `/trains` (player command)

Opens an `ox_lib` context menu listing every currently spawned train, with speed, carriage count, node, network id, and position. Selecting a train offers **Teleport to Train**. The menu text comes from the locale files (`admin.*` keys).

```lua
-- config/config.lua
commands = {
    trains = {
        enable      = true,
        restriction = 'group.admin',   -- false = everyone | a principal, e.g. a group
    },
}
```

`enable = false` unregisters the command entirely — nothing is wired up client or server. `restriction` goes to `ox_lib`'s command system (`lib.addCommand`), which lets that principal use the command (`add_ace <restriction> command.trains allow`). Use a group such as `'group.admin'`. To let more players in, add `add_ace <principal> command.trains allow` to `server.cfg`.

***

### `/trainticket` (player command)

Shows the player's latest ticket on screen again. It only exists in standalone mode (`integrations.inventory = 'none'`); with an inventory resource, players use the `train_ticket` item instead. See [Tickets](tickets.md#standalone-mode-integrations-inventory-none).

***

### Key bindings (player)

These are FiveM key bindings, so each player can change them in **Settings > Key Bindings > FiveM**.

| Default key | Key binding                  | What it does                                                                               |
| ----------- | ---------------------------- | ------------------------------------------------------------------------------------------ |
| `G`         | Train: release / close doors | While driving: releases the doors at a platform, or closes them. Only when stopped         |
| `R`         | Train: change direction      | While driving: switches between forward and reverse. Only when stopped, with the controller at N or braking |
| `Q`         | Train: acknowledge vigilance | While driving: answers the vigilance device                                                |
| `X`         | Train: stand up from a seat  | Stands up from a train seat                                                                |

`driving.keys` in `config/config.lua` sets the defaults of the three driving keys. The other cab controls are the game's own vehicle keys, see [Driving](driving.md#controls). Who may drive is not a command permission: it is set by `driving.jobs` and the `prompt_train.drive` ace, see [Driving](driving.md#who-may-drive).

***

### Setup commands

Run these from the **server console** while setting up or changing lines.

| Command                 | Resource                                            | What it does                                                                                                                                                                                                                                                |
| ----------------------- | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `train_build`           | `prompt_train_script-assets`                        | Rebuilds `traintracks.xml` from the line folders. For a line whose active variant takes a stretch of rails from another resource, it also writes the spliced rails (`track.<variant>.dat` + `points.<variant>.json`). A line's own `track.dat`/`points.json` are left alone; those come from `train_convert`. Run after adding or editing a line, then restart the server: GTA only reads the track list at startup. |
| `train_assets_validate` | `prompt_train_script-assets`                        | Checks every line's track id, stop flags, and point count against `traintracks.xml`; reports mismatches and ends with `validation passed` if clean. It also runs by itself when the assets resource starts. Run this first when anything looks wrong.      |
| `train_convert`         | `prompt_train_script`                               | Converts a legacy/manually-captured route into a line's `track.dat` + `points.json` and prints a ready-to-paste `Line{}` snippet. See [Converter](converter.md).                                                                |
| `train_routes`          | `prompt_train_script`                               | Lists every line with its resolved track id, train, fleet size, and stations, then every registered train and any problems found. **Dormant** lines are listed with what they need: a map, a train, a station, or `traintracks.xml` (see [First Boot Checklist](README.md#dormant-lines)). |
| `train_findtrack <line>` | `prompt_train_script` (client, `debug = true` only) | Spawns test trains at four points of a line and prints the track id each one lands on, plus the id to use. Handy when a line's track id is in doubt.                                                                                                       |
| `toggletrainnodes`      | `prompt_train_script` (client)                      | Toggles debug spheres + labels over every rail node within 120m, showing each line and node index at that point. Use it to find a node number for a variant's remapped station. See [Lines & Stations](lines-and-stations.md). |

***

### Diagnostics

These are for troubleshooting spawn/despawn, orphaned carriages, and door desync — not needed for normal operation. Server commands run in the **server console**, client commands in **F8**. Most of them only exist with `debug = true` in `config/config.lua`; the **Needs `debug`** column says which.

| Command                                              | File                                                   | Needs `debug`                         | Purpose                                                                                                                                                                                                       |
| ---------------------------------------------------- | ------------------------------------------------------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `train_debug`                                        | `debug.lua`                                            | yes                                   | Full state dump: spawned trains, subscribed players, station route points, spawner state                                                                                                                     |
| `train_diag`                                         | `debug.lua`                                            | yes                                   | Tracked trains, plus every train vehicle that no tracked train owns (orphan candidates)                                                                                                                       |
| `train_sweep`                                        | `debug.lua`                                            | yes                                   | Force an orphan cleanup pass over stray train entities                                                                                                                                                        |
| `train_orphan_test`                                  | `debug.lua`                                            | yes                                   | Simulate an orphaned carriage to test cleanup                                                                                                                                                                 |
| `train_kill <index>`                                 | `debug.lua`                                            | yes                                   | Force-despawn one tracked train (index from `train_debug`); it respawns                                                                                                                                       |
| `train_rebuild <netId>`                              | `debug.lua`                                            | yes                                   | Despawn one train's whole set and respawn it (network id from `train_debug`)                                                                                                                                  |
| `train_orphanmode <on\|off>`                         | `debug.lua`                                            | yes                                   | Toggle `keepTrainsOnOwnerChange` at runtime                                                                                                                                                                   |
| `train_carriages`                                    | `debug.lua`                                            | yes                                   | List every tracked carriage and its owning locomotive                                                                                                                                                         |
| `train_clientprobe`                                  | `debug.lua`                                            | yes                                   | Measure each client's FPS and frame time for about a second. A client running at very low FPS slows the trains it owns                                                                                       |
| `train_spawnon <playerId> [line]`                    | `debug.lua`                                            | yes                                   | Force-spawn a train on a line, at the rail point nearest that player and owned by them                                                                                                                       |
| `train_census`                                       | `diag.lua`                                             | yes                                   | One-line census: tracked and held trains, ghost carriages, runtime toggles                                                                                                                                    |
| `train_watch on [seconds]` / `train_watch off`       | `diag.lua`                                             | yes                                   | Print the census every few seconds (default 2) until `train_watch off`                                                                                                                                        |
| `train_toggle <collision\|orphan\|respawn> [on\|off]` | `diag.lua`                                             | yes                                   | Switch a runtime system on or off. Without `on`/`off` it flips                                                                                                                                               |
| `train_doctor`                                       | `doctor.lua`                                           | no                                    | Runs a battery of sanity checks and reports anything broken                                                                                                                                                   |
| `train_wagon_doors [playerId]`                       | `doors_diag.lua` (server) / `doors.lua` (client, `F8`) | no                                    | Wagon door report with a diagnosis, from every client or from one player. In `F8` it reports your own client                                                                                                 |
| `train_predict`                                      | `predict.lua`                                          | yes                                   | List every virtual (predicted) train: state, node, speed, dwell, hold                                                                                                                                         |
| `train_stage <0-5>` / `train_popwatch`               | `staging.lua`                                          | yes, or the `prompt_train_staging` convar | `train_stage` steps the train system up stage by stage. It needs `setr prompt_train_staging 1` in `server.cfg`, and trains then don't spawn by themselves. `train_popwatch` reports the vehicle pool and population per client |
| `train_spacing`                                      | `collision.lua`                                        | yes                                   | Dumps current anti-collision pair distances                                                                                                                                                                   |
| `train_closest` / `getclosesttrain`                  | `train_closest.lua` (client)                           | no                                    | Prints the nearest train to the local player                                                                                                                                                                  |
| `train_config_index [train] [refresh]`               | `train_config.lua` (client)                            | no                                    | Prints the train-config index found for a train from `config/trains.lua` (default: the default train). `refresh` searches again                                                                              |
| `train_doors [left\|right\|close\|flip]`             | `train_doors.lua` (client, `F8`)                       | no                                    | Door state of the nearest metro-type train (doors built into the model) within 200 m. `left` / `right` / `close` force its doors; `flip` swaps the door sides until the next restart                         |
| `train_cab <x> <y> <z> [heading]`                    | `driving.lua` (client, `F8`)                           | yes                                   | While driving, moves your seat on the locomotive and prints the `cab = { ... }` line for that train. Without numbers it prints the current `cab` offset. See [Driving](driving.md#which-trains-can-be-driven)      |

***

## Version 1

Everything below applies to **1.0.x** (latest: 1.0.4.1).

### `/trains` Command

Opens an ox\_lib context menu showing all currently spawned trains.

#### Enabling / Disabling

```lua
-- config/config.lua
trainsCommand = {
    enable      = true,
    restriction = false,   -- who can use the command
}
```

| Value              | Effect                                                            |
| ------------------ | ----------------------------------------------------------------- |
| `false`            | All players can use `/trains`                                     |
| `'group.admin'`    | Only players with that ace permission (uses ox\_lib's AddCommand) |
| `'command.trains'` | Any valid ace group string works                                  |

Setting `enable = false` disables the command entirely — neither the command nor its callbacks are registered.

#### Menu Structure

```
Active Trains (7)
├── Train #1 - Los Santos          Speed: 44 mph | Carriages: 6
│   ├── Teleport to Train
│   └── Train Information
│       ├── Route: Los Santos
│       ├── Speed: 44 mph
│       ├── Carriages: 6
│       ├── Node: 2348
│       ├── Network ID: 37
│       └── Position: 217, -2500, 7
├── Train #2 - Sandy Shores        ...
└── ...
```

#### Teleport

Selecting **Teleport to Train** teleports the player to the train's current position (server-side, 2 metres above the locomotive). A success/error notification confirms the result.

***

### `/trainticket` Command

Only available on standalone servers (`inventory = 'none'`). Re-displays the player's latest purchased ticket on screen — the standalone replacement for using the `train_ticket` inventory item. See [tickets.md](tickets.md "mention").

***

### Debug Commands

These commands are only available from the **server console** (not in-game chat) and require `debug = true` in config.

#### `/train_debug`

Prints a full snapshot of the train system state:

```
==== SPAWNED TRAINS (7) ====
  [1] route=lossantos | netId=37 | node=2348 | dir=1 | carriages=6 | coords=(217.5, -2500.7, 14.2)
  ...
==== SUBSCRIBED PLAYERS ====
  player=4 | stations=lossantos1, lossantos2
==== STATION ROUTE POINTS ====
  station=lossantos1 | lossantos=1126
==== STATE ====
  isSpawningTrains=false | cleanupSource=4
```
