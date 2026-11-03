---
description: >-
  Run a line on rails that ship inside another resource, such as the
  cfx-nteam-monorail-map monorail, with two fields on a line file.
icon: map-location-dot
---

# Integrating Another Map Resource

{% hint style="info" %}
This page applies to **version 2** (2.1.0) only.
{% endhint %}

Any line can run on rails that ship inside a *different* resource — an elevated monorail overlay, a rebuilt Paleto Bay, a custom map pack, anything that carries its own `.dat` rail file. There is no manual `traintracks.xml` editing, no `fxmanifest.lua` change, and no central route table to maintain — it's just two fields on an ordinary line.

```lua
-- prompt_train_script-assets/lines/<id>/line.lua
Line {
    label    = 'My Overlay Line',
    type     = 'metro',
    fleet    = 4,
    loop     = true,
    requires = 'some-map-resource',
    track    = { resource = 'some-map-resource', file = 'trains13.dat' },
    stops = {
        { station = 'somestation', node = 21 },
        ...
    },
}
```

| Field                        | Meaning                                                                                                                                                                |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requires`                   | A resource name (or list) that must be running for this line to be active. If it isn't, the line stays [**dormant**](lines-and-stations.md#dormant-lines) — reported as such by `train_routes`, not an error. |
| `track = { resource, file }` | Points at the `.dat` file *inside that resource* instead of this line's own `track.dat`.                                                                               |
| `conflicts`                  | Optional. A resource name (or list) that is stopped while the `requires` resource runs — for example a train script that ships with the map and would control the same trains. |

***

### Setting one up

1. Find the `.dat` file the target resource ships (check its own `traintracks.xml` for the filename it declares) and the node range/config you want to use.
2. Create `lines/<id>/line.lua` with `requires` and `track = { resource, file }` as above.
3. Add `stops`, pointing at existing or new stations (see [Lines & Stations](lines-and-stations.md)). Use `/toggletrainnodes` in-game to read off node numbers if you don't already have them.
4. Run `train_build` (server console, in the assets resource), then restart the server so `traintracks.xml` picks up the new rail file. GTA reads the track list only at startup, so restarting the resources is not enough.
5. `train_routes` should list the line as active; `train_assets_validate` confirms everything lines up.

{% hint style="warning" %}
If the map resource registers a track list of its own (`data_file 'TRAINTRACK_FILE'` in its `fxmanifest.lua`), the server console prints a **PROMPT TRAIN CONFLICT** box: the tracks come from `prompt_train_script-assets/traintracks.xml`, so the two clash. In the map's `fxmanifest.lua`, remove or comment out every `data_file 'TRAINTRACK_FILE'` line and the track list file it names in `files { }` (keep the `.dat` rail files), then restart the server.
{% endhint %}

Other resources that register track files no longer shift your lines onto the wrong rails: the script finds the real track numbers in game (see [Track files](lines-and-stations.md#track-files)).

No code changes are ever required for a new dependency — only a new line file. The same `requires` + `track` shape is also what powers per-map [variants](lines-and-stations.md#variants) on an *existing* line, when you want one line to switch rails depending on what's running rather than adding a whole new line.

***

### Example: an elevated overlay line (`cfx-nteam-monorail-map`)

```lua
Line {
    label     = 'Monorail',
    type      = 'metro',
    fleet     = 4,
    loop      = true,
    requires  = 'cfx-nteam-monorail-map',
    conflicts = 'cfx-nteam-monorail-script',
    track     = { resource = 'cfx-nteam-monorail-map', file = 'trains13.dat' },
    stops = {
        { station = 'milehigh', node = 21 },
        { station = 'mrpd',     node = 85 },
        ...
    },
}
```
