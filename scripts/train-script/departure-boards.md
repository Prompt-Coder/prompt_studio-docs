---
description: >-
  Departure boards display real-time train information (ETA, destination,
  status, track number) at station locations. They are configured in
  config/boards.lua.
icon: chalkboard-user
---

# Departure Boards

There are two board types:

| Type             | Description                                                     |
| ---------------- | --------------------------------------------------------------- |
| **Built-in**     | Replaces an existing in-world texture with a live display       |
| **Spawned prop** | Spawns a new prop at a given location and renders a board on it |

***

### How It Works

1. When a player enters a **zone** defined in `config/boards.lua`, the client subscribes to train sync data for the stations in that zone.
2. The server pushes ETA data to subscribed players.
3. The client renders the board via a DUI.
4. The DUI updates as train positions change.

***

### Zone Structure

Each entry in `config/boards.lua` represents one station zone:

```lua
{
    id       = 'my_station',          -- unique identifier
    stations = { 'mystation' },       -- station IDs from config/config.lua

    stationTracks = {
        mystation = 1,                -- track number shown on the board
    },

    stationDestinations = {
        mystation = {
            lossantos = 'Los Santos', -- route key → label shown on the board
            sandy     = 'Sandy Shores',
        },
    },

    blip = {
        enable = true,
        label  = 'My Station',
        coords = vec3(x, y, z),
    },

    zone = {
        points    = { vec3(...), vec3(...), vec3(...), vec3(...) },
        thickness = 22.0,
    },

    boards = { ... },  -- see below
}
```

#### `stationTracks`

Maps each station ID to a track number. This number appears in the **Track** column on boards that have it. If your station has only one platform you can omit this entirely (it defaults to `1`).

#### `stationDestinations`

Maps each station ID + route key to a human-readable destination string shown on the board. Without this the raw route label from `config.routes` is used.

#### `zone`

A polygon (at least 3 points) that defines the area where boards activate. `thickness` is the vertical height of the zone in metres.

***

### Adding a Board

#### Step 1 — Add the station to `config/config.lua`

```lua
stations = {
    -- existing entries ...
    mystation = {
        nodes = { lossantos = 1234 },  -- nearest rail node index
    },
},
```

> **Finding the node index:** run `/train_debug` in the console while a train is near your platform. Note the `node=` value when the train is at the stop, and use that.

#### Step 2 — Add the zone to `config/boards.lua`

Append a new entry to the returned table:

```lua
{
    id       = 'my_station',
    stations = { 'mystation' },

    stationDestinations = {
        mystation = {
            lossantos = 'Los Santos',
        },
    },

    blip = {
        enable = true,
        label  = 'My Station',
        coords = vec3(100.0, 200.0, 30.0),
    },

    zone = {
        points = {
            vec3(90.0,  190.0, 30.0),
            vec3(110.0, 190.0, 30.0),
            vec3(110.0, 210.0, 30.0),
            vec3(90.0,  210.0, 30.0),
        },
        thickness = 20.0,
    },

    boards = {
        -- choose one of the board types below
    },
},
```

#### Step 3 — Define the boards

**Option A: Built-in texture replacement (DUI)**

Use this when the station already has a board-like object in GTA V whose texture you want to replace.

```lua
boards = {
    {
        id  = 'my_board',
        img = 'txt/default.png',   -- fallback image shown before DUI loads

        dui = {
            width  = 1024,
            height = 1024,
            txd    = 'TEXTURE_DICT_NAME',  -- GTA V texture dictionary
            txn    = 'TEXTURE_NAME',       -- texture name inside the dict
        },

        elements = {
            CLOCK_ELEMENT,           -- shared clock (top-right)
            DEFAULT_BOARD_TABLE,     -- standard departures table
            stationLabel('MY STATION'),
        },
    },
},
```

The `txd` / `txn` values come from the game's asset files. Tools like CodeWalker can help you find them by inspecting the board prop at the station.

**Custom fallback texture (`img`)**

The `img` field points to a static PNG image shown on the board before the DUI finishes loading (or as a permanent background layer). If you want to use your own design:

1. Export your image as a **PNG** (recommended size: match the `dui.width` × `dui.height`, e.g. 1024×1024).
2. Place it in `web/dui/txt/` inside the resource.
3. Reference it in the board definition:

```lua
img = 'txt/my_board_bg.png',
```

This path is relative to the `web/dui/` folder — do not include that prefix.

**Option B: Spawned prop**

Use this when there is no existing board at the location. The script spawns a prop and renders the DUI onto it.

```lua
boards = {
    {
        id = 'my_board',

        spawn = {
            {
                type   = 'hanging',   -- 'hanging' or 'standing'
                coords = {
                    vec4(x1, y1, z1, heading1),
                    vec4(x2, y2, z2, heading2),  -- add as many as needed
                },
            },
        },

        elements = {
            CLOCK_ELEMENT,
            DEFAULT_BOARD_TABLE,
            stationLabel('MY STATION'),
        },
    },
},
```

* `'hanging'` — an overhead board (hangs from ceiling or poles).
* `'standing'` — a floor-standing kiosk.

The fourth component of `vec4` is the heading in degrees.

***

### Board Elements

Elements define what is rendered on the board canvas. Every board gets its own 1024×1024 canvas by default.

#### Clock

```lua
{
    type          = 'text',
    key           = 'currentTime',   -- filled automatically by the sync
    x = 800, y = 560, width = 200, height = 40,
    align         = 'right',
    fontSize      = 48,
    fontWeight    = 700,
    letterSpacing = 1.0,
    color         = '#F3F6FB',
}
```

Use the shared `CLOCK_ELEMENT` constant to avoid repeating this.

#### Station Name Label

```lua
stationLabel('PALETO BAY')
```

This helper creates a static text element placed at the bottom-left of the board.

#### Departures Table

The standard table shows up to 6 rows with ETA, destination, and status columns:

```lua
DEFAULT_BOARD_TABLE
```

For stations with multiple tracks, override the table with a `track` column:

```lua
{
    type    = 'table',
    key     = 'departures',
    orderBy = { 'time', 'eta', 'track', 'destination', 'status' },
    maxRows = 6,
    x = 22, y = 664, width = 980, height = 350,
    row = { ... },     -- copy from DEFAULT_BOARD_TABLE if needed
    columns = {
        { key = 'eta',         ... },
        { key = 'destination', ... },
        { key = 'track',       ... },  -- add this column
        { key = 'status',      ... },
    },
}
```

***

### Multi-Track Stations

For stations like Los Santos that have two platforms on the same zone:

```lua
stations = { 'lossantos1', 'lossantos2' },

stationTracks = {
    lossantos1 = 1,
    lossantos2 = 2,
},

stationDestinations = {
    lossantos1 = { lossantos = 'Sandy Shores', sandy = 'Paleto Bay' },
    lossantos2 = { lossantos = 'Sandy Shores', sandy = 'Paleto Bay' },
},
```

Both station IDs need their own entry in `config.stations` with the correct node index for each platform.

***

### Station Blips

Each zone can show a map blip for the station:

```lua
blip = {
    enable = true,
    label  = 'Paleto Bay Train Station',
    coords = vec3(162.98, 6371.36, 31.59),
},
```

Set `enable = false` to hide the blip.
