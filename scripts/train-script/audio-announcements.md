---
description: >-
  The PA system plays spatial audio announcements at stations when trains
  arrive, stop, or depart. Announcements are assembled from a library of
  pre-recorded audio clips that are combined at runtime.
icon: circle-waveform-lines
---

# Audio Announcements

### How It Works

1. The server pushes train ETA data to subscribed players.
2. On the client, a state machine tracks each train's status at each station (approaching / on station / departed).
3. When a state transition is confirmed (3 consecutive matching ticks — prevents false triggers), the matching announcement clips are assembled and played from the configured speaker coordinates.
4. Clips play sequentially from a single queue per PA zone, so overlapping announcements on the same zone are blocked until the current one finishes.

#### State Machine

| Transition                             | Announcement clips                                                 |
| -------------------------------------- | ------------------------------------------------------------------ |
| Train approaches → arrives at platform | `"Train [route] to [dest] via [station] is arriving on track [n]"` |
| 12 seconds after arriving              | `"… has arrived on track [n]"`                                     |
| Train leaves station                   | `"… has departed on track [n]"`                                    |

***

### Configuration

PA zones are defined in `config/config.lua` under `paStations`:

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

| Field      | Type               | Description                                                     |
| ---------- | ------------------ | --------------------------------------------------------------- |
| `id`       | `string`           | Unique PA zone identifier                                       |
| `stations` | `string[]`         | Station IDs (from `config.stations`) that this zone announces   |
| `coords`   | `vec3` or `vec3[]` | Speaker location(s) — see below                                 |
| `range`    | `number`           | Maximum distance in metres at which the announcement is audible |

***

### Multiple Speaker Positions

You can pass an array of `vec3` values to `coords` to broadcast the same announcement from several speakers simultaneously:

```lua
{
    id       = 'pa_los_santos',
    stations = { 'lossantos1', 'lossantos2' },
    coords   = {
        vec3(716.97, -532.14, 28.46),   -- platform A speaker
        vec3(730.00, -550.00, 28.46),   -- platform B speaker
        vec3(745.00, -570.00, 28.46),   -- concourse speaker
    },
    range = 150.0,
},
```

All speakers play in sync — each clip starts on all positions at the same time and the system waits for all to finish before moving to the next clip.

A single `vec3` (old format) is still accepted — it is automatically wrapped into a one-element table internally, so existing configs do not need updating.

***

### Adding a New PA Zone

#### Step 1 — Add the station to `config.stations`

If not already present:

```lua
stations = {
    mystation = {
        nodes = { lossantos = 1234 },
    },
},
```

#### Step 2 — Add the PA zone

```lua
paStations = {
    -- existing entries ...
    {
        id       = 'pa_my_station',
        stations = { 'mystation' },
        coords   = vec3(x, y, z),
        range    = 120.0,
    },
},
```

That is all that is needed. The announcement content (route name, destination, track number) is assembled automatically from the train sync data.

***

### Audio Clips

Clips are defined in `client/pa.lua` and reference sounds from the custom audio bank (`audiodirectory/prompt_train.awc`).

#### Route clips

```lua
ROUTE_CLIPS = {
    lossantos = 'pa_route_lossantos',
    sandy     = 'pa_route_sandy',
}
```

#### Destination clips

```lua
DEST_CLIPS = {
    ['Los Santos']   = 'pa_dest_los_santos',
    ['Sandy Shores'] = 'pa_dest_sandy_shores',
    ['Paleto Bay']   = 'pa_dest_paleto_bay',
}
```

#### Station name clips

```lua
STATION_CLIPS = {
    paletobay  = 'pa_station_paleto_bay',
    lossantos1 = 'pa_station_los_santos_track_1',
    lossantos2 = 'pa_station_los_santos_track_2',
}
```

If a station or destination has no clip mapped (value is `nil`), that segment is simply skipped — the announcement still plays but without that piece of audio.

#### Adding clips for a new route or station

1. Record or obtain the audio file (any common format — WAV or MP3 work well).
2. Pack it into `audiodirectory/prompt_train.awc`. The recommended tool for this is [**Audiotool by Renewed-Scripts**](https://github.com/Renewed-Scripts/Audiotool) — it handles AWC packing and the required files without needing to touch OpenIV or RPF files manually.
3. Add the entry to the corresponding table in `client/pa.lua`:

```lua
ROUTE_CLIPS = {
    lossantos = 'pa_route_lossantos',
    sandy     = 'pa_route_sandy',
    myroute   = 'pa_route_myroute',   -- new
}

STATION_CLIPS = {
    mystation = 'pa_station_my_station',   -- new
}
```

***

### Tuning

#### Confirmation threshold

The PA system requires **3 consecutive ticks** in the new state before playing an announcement. This prevents false triggers from momentary sync glitches. The constant is `STABLE_TICKS_REQUIRED = 3` at the top of `client/pa.lua`. Increasing it makes the system more conservative; decreasing it makes it more reactive.

#### Arrived delay

After the "arriving" announcement, a "has arrived" announcement plays **12 seconds later** (hardcoded in `client/pa.lua`). This gives passengers time to hear both messages.
