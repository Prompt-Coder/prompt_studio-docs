---
description: >-
  Run a line on rails that ship inside another resource, such as the
  cfx-nteam-monorail-map monorail, with two fields on a line file.
icon: map-location-dot
---

# Integrating Another Map Resource

{% hint style="info" %}
This page applies to **version 2** (2.0.0-beta) only.
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
| `requires`                   | A resource name (or list) that must be running for this line to be active. If it isn't, the line stays **dormant** — reported as such by `train_routes`, not an error. |
| `track = { resource, file }` | Points at the `.dat` file *inside that resource* instead of this line's own `track.dat`.                                                                               |

***

### Setting one up

1. Find the `.dat` file the target resource ships (check its own `traintracks.xml` for the filename it declares) and the node range/config you want to use.
2. Create `lines/<id>/line.lua` with `requires` and `track = { resource, file }` as above.
3. Add `stops`, pointing at existing or new stations (see [Lines & Stations](lines-and-stations.md)). Use `/toggletrainnodes` in-game to read off node numbers if you don't already have them.
4. Run `train_build` (server console, in the assets resource), then restart both resources so `traintracks.xml` picks up the new rail file.
5. `train_routes` should list the line as active; `train_assets_validate` confirms everything lines up.

No code changes are ever required for a new dependency — only a new line file. The same `requires` + `track` shape is also what powers per-map [variants](lines-and-stations.md#variants) on an *existing* line, when you want one line to switch rails depending on what's running rather than adding a whole new line.

***

### Example: an elevated overlay line (`cfx-nteam-monorail-map`)

```lua
Line {
    label    = 'Monorail',
    type     = 'metro',
    fleet    = 4,
    loop     = true,
    requires = 'cfx-nteam-monorail-map',
    track    = { resource = 'cfx-nteam-monorail-map', file = 'trains13.dat' },
    stops = {
        { station = 'milehigh', node = 21 },
        { station = 'mrpd',     node = 85 },
        ...
    },
}
```
