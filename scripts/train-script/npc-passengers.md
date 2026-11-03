---
description: >-
  Metro trains carry NPC passengers. They wait on the platforms, ride in the
  carriages, and get on and off at every stop.
icon: people-group
---

# NPC Passengers

{% hint style="info" %}
New in **2.1.0**. All settings are in section 13 of `config/config.lua` (`passengers`). Passengers need NPC trains (`npcDriven.enable = true`).
{% endhint %}

Metro trains carry NPC passengers. People wait on the platforms and ride in the carriages, sitting or standing. At every stop some riders get off, and the people waiting get on.

***

### Which trains and lines

Passengers ride every train that has a `passengers` block in `config/trains.lua` (see [The passengers block](#the-passengers-block)). In the shipped config only the `metro` train has one. You see them on the **Metro** line, and on the **Monorail** line if you run its map (see [Integrating Another Map Resource](integrating-another-map-resource.md)). The Polar Express has no NPC passengers.

A platform gets waiting passengers when a line that runs such a train stops there.

Passengers also use a metro that a player drives: they get on and off when the driver releases the doors at a platform. See [Driving](driving.md).

***

### How they behave

* **Riders.** When a carriage first comes within `range` of you, it gets 1 to 5 riders (`perCarriage`). About 7 in 10 sit while there are free seats; the rest stand.
* **Waiting.** Each platform near you gets 3 to 7 waiting passengers (`waiting`), standing around, on their phone or with a coffee. They appear where you can't see them, and the platform is topped up every `refillMs` (15 s).
* **Getting off.** When the train stops and its doors open, about 40% (`alightShare`) of each carriage's riders step out on the platform side, walk off along the platform and wander away.
* **Getting on.** Waiting passengers within `boardRange` (22 m) of an open door walk to it and board, as long as the train is still standing there.

Passengers only get on and off through the carriage's own train doors, the doors built into the model like the metro's.

***

### Options

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
        -- ... 16 models in total
    },
},
```

| Option        | Default       | What it does                                                                                                 |
| ------------- | ------------- | ------------------------------------------------------------------------------------------------------------ |
| `enable`      | `true`        | Turns NPC passengers on or off                                                                               |
| `range`       | `150.0`       | Distance (m) around the player. Carriages and platforms inside it get passengers; passengers outside it are removed |
| `maxPeds`     | `40`          | Most passengers one player's game spawns at once: riders, waiting and walking together                      |
| `perCarriage` | `{ 1, 5 }`    | Riders in a carriage when it first comes in range, from min to max                                           |
| `waiting`     | `{ 3, 7 }`    | Passengers waiting on a platform, from min to max                                                            |
| `alightShare` | `0.4`         | Share of each carriage's riders that get off at a stop                                                       |
| `boardRange`  | `22.0`        | Waiting passengers this close (m) to an open door get on                                                     |
| `refillMs`    | `15000`       | How often (ms) a platform near the player is topped up                                                       |
| `models`      | 16 ped models | Ped models passengers are picked from at random                                                              |

***

### Turning them off

* Everywhere: set `passengers.enable = false`.
* For one train: remove the `passengers` block from that train in `config/trains.lua`.
* Fewer of them: lower `maxPeds`, `perCarriage`, `waiting` or `range`.

***

### Performance

* Passengers are local peds. Each player's game spawns its own and they are not networked, so they add no network traffic or server work. Two players on the same platform see different people.
* Only carriages and platforms within `range` get passengers. Anything further away is deleted.
* `maxPeds` caps how many one player's game spawns.
* The script looks for new carriages every 2 seconds and handles the ones in range twice a second.
* Passengers who got off are deleted after 40 seconds once you can't see them, or as soon as they are out of range.

***

### The passengers block

Each train sets its own in `config/trains.lua`. The metro's:

```lua
metro = {
    -- ...
    passengers = { -- door bones, standing area, seats (x, y, z, heading)
        doors = { 'door_dside_f', 'door_dside_r', 'door_pside_f', 'door_pside_r' },
        stand = { z = 1.55, x = 0.55, yMin = -4.2, yMax = 4.2 },
        seats = {
            vec4( 1.04,  2.27, 1.54, 0.0), vec4( 1.04,  1.39, 1.54, 0.0), vec4( 1.04, -0.08, 1.54, 0.0),
            vec4( 1.04, -0.82, 1.54, 0.0), vec4( 1.04, -4.85, 1.54, 0.0),
            vec4(-1.04,  2.28, 1.54, 180.0), vec4(-1.04,  0.71, 1.54, 180.0),
            vec4(-1.04, -1.61, 1.54, 180.0), vec4(-1.04, -3.74, 1.54, 180.0),
        },
    },
},
```

| Field   | Meaning                                                                                                                                  |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `doors` | Bone names of the carriage's doors. Passengers get off and on next to these, on the platform side                                        |
| `stand` | Where standing riders go, as offsets from the carriage: height `z`, up to `x` either side of the centre line, and from `yMin` to `yMax` along it |
| `seats` | One `vec4(x, y, z, heading)` per seat, as an offset from the carriage                                                                    |

The block applies to every carriage of that train (all of its `models`). A [train pack](train-packs.md) can bring its own `passengers` block. To give another train passengers, its carriages need those door bones and their own train doors, like the metro.
