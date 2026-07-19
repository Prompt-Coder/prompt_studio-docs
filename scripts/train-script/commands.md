---
icon: terminal
---

# Commands

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
