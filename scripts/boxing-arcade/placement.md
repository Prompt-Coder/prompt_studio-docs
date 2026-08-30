---
description: The /boxarcade creator — panel, ghost placement, per-machine price, map marks & binding machines to map resources
icon: location-dot
---

# Placing Machines

Everything is done **in-game** with `/boxarcade`. No coordinates to copy, no config editing
required — though everything you place can be exported to config with one click.

### Who can place

`/boxarcade` is gated behind an ACE permission:

```
add_ace group.admin prompt_boxing.creator allow
```

On a dev server you can skip the ACE with `Config.devMode = true` in `config.lua`.
The two are deliberately independent: `devMode` bypasses **only** the creator permission
(it never enables debug commands), and `Config.debug` never grants creator access.

{% hint style="info" %}
**Playing** a machine needs no permission at all — the ACE only controls who can place,
move, remove and re-price cabinets.
{% endhint %}

***

### The creator panel

Run `/boxarcade` with no arguments to open the panel. It lists **every machine on the
server** — nearest first — with its id, distance, price and resource binding.

Per row:

| Button | What it does |
| --- | --- |
| **Set** | Set or clear that machine's per-play price (overrides the global `Config.Payment.price`) |
| **Move** | Re-enter ghost placement for that machine — walk it somewhere else and confirm |
| **Remove** | Deletes the machine — asks for a second click (**Confirm**) so a mis-click costs nothing |
| **Mark / Unmark** | Drops a temporary map blip on that machine so you can find it. Self-clears after 90 s, clears when the machine is removed, and **Unmark** clears it early |
| **Copy line** | Copies a ready-to-paste config line to your clipboard — for moving a placement into `config/machines.lua` or a [map pack](#map-packs-ship-machines-with-your-maps) |

The **bind** box on each row ties the machine to a map resource — see
[Binding](#bind-a-machine-to-a-map-resource) below. Type to filter; every started resource
on the server is offered.

New machines: the **Place** button at the top (with an optional price) drops you into ghost
placement, and the panel re-opens when you're done.

***

### Ghost placement controls

While placing (or moving) a machine you steer a transparent ghost cabinet:

| Control | Action |
| --- | --- |
| **Mouse scroll** | Rotate (±5° per notch) |
| **Arrow Up / Down** | Raise / lower — smooth while held (0.5 m per second), turns ground-snap off |
| **G** | Snap back to the ground |
| **Enter** | Confirm placement |
| **Backspace** | Cancel |

Ground snap rests the cabinet flush on its feet (the snap offset is pre-tuned — no floating,
no clipping). All rates live in `Config.Creator` if you want different steps.

{% hint style="warning" %}
The server rejects placements farther than `Config.Creator.maxDistance` (default **50 m**)
from the player — a safety net against misclicks into the void.
{% endhint %}

***

### Command reference

The panel is the comfortable way; every action also exists as a subcommand:

| Command | Action |
| --- | --- |
| `/boxarcade` | Open the creator panel |
| `/boxarcade <price>` | Place a new machine with that per-play price |
| `/boxarcade move` | Move the nearest placed machine (within 3 m) |
| `/boxarcade remove` | Remove the nearest placed machine — repeat within 5 s to confirm |
| `/boxarcade price <n>` | Set / clear the price on the nearest placed machine |
| `/boxarcade list` | Print ids, distances and prices to F8 — including a ready-to-paste config line per machine |
| `/boxarcade dump` | Print a full diagnostics block to the **server console** — paste this when asking for support |

***

### The three kinds of machines

Every machine has a **stable id** — hooks, exports and support all key on it:

| Kind | Id looks like | Defined in | Editable in-game? |
| --- | --- | --- | --- |
| **Placed** | `a3f21c` (6 characters) | `data/machines.json` (runtime file) | ✅ move / remove / price / bind |
| **Config** | `cfg_1`, `cfg_2`, … | `config/machines.lua` | 🔒 price only — move/remove refuse by design; edit the file and restart |
| **Map pack** | `map_prompt_sandy_bar_1` | `config/mappacks.lua` | 🔒 same — edit the file and restart |

{% hint style="warning" %}
`cfg_N` ids follow **array position** in `config/machines.lua` — inserting or reordering
entries re-keys every machine after the change point (and any hooks keyed on those ids).
Append at the end, or use placed machines instead.
{% endhint %}

`data/machines.json` and the leaderboard are **runtime files** — updates to the resource
never touch them, so your placements and scores survive every update.

***

### Bind a machine to a map resource

If a cabinet stands inside a custom map, bind it to that map's resource with the **bind box**
on its panel row. A bound machine only exists while that resource is **started**:

* Map running → machine spawns as normal.
* Map not running → the machine stays saved but **dormant** — no prop, no target, shown
  dimmed with a `dormant` badge in the panel (where you can still re-bind or unbind it).

This makes placements safe to keep while you toggle maps on and off — remove the map and the
cabinet silently steps aside instead of floating in the void.

{% hint style="info" %}
Bindings are checked once the server has finished starting resources. A map started **later
by hand** is picked up on the next `restart prompt_boxing_machine`.
{% endhint %}

***

### Map packs — ship machines with your maps

`config/mappacks.lua` holds **preset machines per map resource** — the config-file version of
binding. The same file ships safely everywhere: machines only register when their map is
actually running.

```lua
Config.MapPacks = {
    {
        resource = 'prompt_sandy_bar',
        machines = {
            { coords = vec3(1986.42, 3054.18, 47.22), heading = 120.0 },
            { coords = vec3(1988.10, 3054.90, 47.22), heading = 120.0, price = 20 },
        },
    },
}
```

Authoring flow: place the machine in-game where you want it, then hit **Copy line** on its
panel row (or `/boxarcade list`) and paste the line into the pack. Ids are stable
(`map_<resource>_<index>`), so hooks can target them.

***

### Permanent map blips

The Mark button is for you, temporarily. To show **all players** every machine on the map,
enable the blip block in `config/machines.lua`:

```lua
blip = { enabled = false, sprite = 740, colour = 5, scale = 0.8 },
```

Off by default — placed machines can live in rooms you may not want advertised.
