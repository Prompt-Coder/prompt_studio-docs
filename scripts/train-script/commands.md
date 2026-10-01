---
icon: terminal
---

# Commands

{% hint style="info" %}
**Version 2** (2.0.0-beta) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

### `/trains` (player command)

Opens an `ox_lib` context menu listing every currently spawned train, with speed, carriage count, node, network id, and position. Selecting a train offers **Teleport to Train**.

```lua
-- config/config.lua
commands = {
    trains = {
        enable      = true,
        restriction = 'group.admin',   -- false = everyone | an ace permission string
    },
}
```

`enable = false` unregisters the command entirely — nothing is wired up client or server. `restriction` is checked by `ox_lib`'s own command system (`lib.addCommand`), so any ace permission string works, not just group names.

***

### `/trainticket` (player command)

Shows the player's latest ticket on screen again. It only exists in standalone mode (`integrations.inventory = 'none'`); with an inventory resource, players use the `train_ticket` item instead. See [Tickets](tickets.md#standalone-mode-integrations-inventory-none).

***

### Setup commands

Run these from the **server console** while setting up or changing lines.

| Command                 | Resource                                            | What it does                                                                                                                                                                                                                                                |
| ----------------------- | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `train_build`           | `prompt_train_script-assets`                        | Rebuilds `traintracks.xml` and per-line `.dat`/`points.json` from every line's own geometry and active variants. Run after adding or editing a line, then restart both resources.                                                                           |
| `train_assets_validate` | `prompt_train_script-assets`                        | Checks every line's track id, stop flags, and point count against `traintracks.xml`; reports mismatches and ends with `validation passed` if clean. Run this first when anything looks wrong.                                                               |
| `train_convert`         | `prompt_train_script`                               | Converts a legacy/manually-captured route into a line's `track.dat` + `points.json` and prints a ready-to-paste `Line{}` snippet. See [Converter](converter.md).                                                                |
| `train_routes`          | `prompt_train_script`                               | Lists every line with its resolved track id, fleet size, and stations — including whether a line is currently **dormant** (its variant/resource requirement isn't met).                                                                                     |
| `train_findtrack`       | `prompt_train_script` (client, `debug = true` only) | Prints the track id and node the local player is currently nearest to — handy for filling in a station's `node` by hand.                                                                                                                                    |
| `toggletrainnodes`      | `prompt_train_script` (client)                      | Toggles debug spheres + labels over every rail node within 120m, showing each line and node index at that point. Use it to find a node number for a variant's remapped station. See [Lines & Stations](lines-and-stations.md). |

***

### Diagnostics (server console, `debug = true`)

These are for troubleshooting spawn/despawn, orphaned carriages, and door desync — not needed for normal operation.

| Command                             | File                                                   | Purpose                                                                                                         |
| ----------------------------------- | ------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| `train_debug`                       | `debug.lua`                                            | Full state dump: spawned trains, subscribed players, station route points, spawner state                        |
| `train_diag`                        | `debug.lua`                                            | Condensed health summary                                                                                        |
| `train_sweep`                       | `debug.lua`                                            | Force a cleanup pass over all tracked trains                                                                    |
| `train_orphan_test`                 | `debug.lua`                                            | Simulate an orphaned carriage to test cleanup                                                                   |
| `train_kill <index>`                | `debug.lua`                                            | Force-despawn one tracked train                                                                                 |
| `train_rebuild <route>`             | `debug.lua`                                            | Force despawn + respawn every train on a line                                                                   |
| `train_orphanmode <on\|off>`        | `debug.lua`                                            | Toggle `keepTrainsOnOwnerChange` at runtime                                                                     |
| `train_carriages`                   | `debug.lua`                                            | List every tracked carriage and its owning locomotive                                                           |
| `train_clientprobe`                 | `debug.lua`                                            | Ask all clients to report their local train state                                                               |
| `train_spawnon <route>`             | `debug.lua`                                            | Force-spawn a train on a specific line regardless of predictive distance                                        |
| `train_census`                      | `diag.lua`                                             | Count of spawned trains per line                                                                                |
| `train_watch <route>`               | `diag.lua`                                             | Log spawn/despawn events for one line                                                                           |
| `train_toggle <flag>`               | `diag.lua`                                             | Flip a runtime diagnostic flag                                                                                  |
| `train_doctor`                      | `doctor.lua`                                           | Runs a battery of sanity checks and reports anything broken                                                     |
| `train_wagon_doors`                 | `doors_diag.lua` (server) / `doors.lua` (client, `F8`) | Aggregates per-client wagon door state; the client-side `F8` bind reports the local player's nearest door state |
| `train_predict`                     | `predict.lua`                                          | Dumps the current predictive-spawn queue and its timers                                                         |
| `train_stage` / `train_popwatch`    | `staging.lua`                                          | Inspect the staging/despawn queue                                                                               |
| `train_spacing`                     | `collision.lua`                                        | Dumps current anti-collision pair distances                                                                     |
| `train_closest` / `getclosesttrain` | `train_closest.lua` (client)                           | Prints the nearest train to the local player                                                                    |
| `train_config_index`                | `train_config.lua` (client)                            | Prints the resolved consist index for the train the player is on                                                |
| `train_doors`                       | `train_doors.lua` (client, `F8`)                       | Manually trigger the local engine/metro door animation, for testing smoothness                                  |

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
