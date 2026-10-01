---
description: by adaz
icon: train
---

# Train Script

{% hint style="info" %}
**Version 2** (2.0.0-beta) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

### Requirements

* FiveM server (artifact 6683 or newer recommended)
* [`ox_lib`](https://github.com/overextended/ox_lib) started **before** either resource below
* `prompt_train_polar_express` — the model pack for the default consist
* `prompt_train_script-assets` — ships with the script. Holds every station, line, `.dat` and streamed asset. `prompt_train_script` has no data of its own; it will not start without this resource running first.

***

### Installation

1. Copy `prompt_train_script`, `prompt_train_script-assets`, and `prompt_train_polar_express` into your `resources` folder.
2. Add the following to your `server.cfg` **in this order**:

```
ensure ox_lib
ensure prompt_train_polar_express
ensure prompt_train_script-assets
ensure prompt_train_script
```

3. Open `config/config.lua` and adjust settings for your server (interaction, framework, inventory, ticket prices, etc.). See [Configuration](configuration.md).
4. If you're running with an inventory resource, register the `train_ticket` item. See [Tickets → Inventory Item](tickets.md#inventory-item). If `integrations.inventory` is `'none'`, skip this — the script keeps tickets itself.

***

### First Boot Checklist

In the server console:

```
train_assets_validate
train_routes
```

| Check                           | What to look for                                                                            |
| ------------------------------- | ------------------------------------------------------------------------------------------- |
| Assets resource loaded first    | Console should **not** say `cannot read stations and lines from prompt_train_script-assets` |
| `train_assets_validate` passes  | Reports every line's track id, stop count, and point count, ending in `validation passed`   |
| `train_routes` shows every line | Lists each line with its track id, fleet, and stations — no unexplained gaps                |
| Trains spawn                    | After the first player joins you should see trains appear on the map                        |

If a line shows as **dormant** in `train_routes`, either its `traintracks.xml` entry hasn't been built yet (run `train_build` in the assets resource, then restart) or a resource it depends on (`requires`) isn't running.

***

### The two resources, in one sentence

`prompt_train_script-assets` is data: every station and every line, as plain files you can add, edit, or delete without touching a line of runtime logic. `prompt_train_script` is the engine that reads that data and runs it. See [Lines & Stations](lines-and-stations.md) for how to add your own, or build them in the browser with the [Train Editor](https://train-editor.prompt-mods.com/).

***

## Version 1

Everything below applies to **1.0.x** (latest: 1.0.4.1).

### Requirements

* FiveM server (artifact 6683 or newer recommended)
* [`ox_lib`](https://github.com/overextended/ox_lib) started **before** this resource
* `prompt_train_polar_express` — the model pack that ships alongside the script

Everything else is **optional** — the script runs fully standalone:

* **Framework** (QBx / QBCore / ESX) — used only to charge for tickets. Without one, tickets are free.
* **Inventory** (`ox_inventory` / `qb-inventory` / `ps-inventory` / ESX) — used only to hold the ticket item. Without one, the script stores tickets itself: they survive restarts, stay valid for 24 hours, and `/trainticket` re-displays them. See [tickets.md](tickets.md "mention").
* **Targeting** (`ox_target` / `qb-target`) — used only for the ticket machine and seat interactions. Without one, the script automatically falls back to built-in `[E]` proximity prompts (no extra setup).

***

### Installation

1. Copy `prompt_train_script` and `prompt_train_polar_express` into your `resources` folder.
2. Add the following to your `server.cfg` **in this order**:

```
ensure ox_lib
ensure prompt_train_polar_express
ensure prompt_train_script
```

3. Open `config/config.lua` and adjust settings for your server (framework, inventory, routes, etc.). See Configuration for a full reference.
   1. If you want to use train tickets, register the `train_ticket` item in your inventory resource. See [tickets.md](tickets.md "mention") for the exact snippets.

***

### First Boot Checklist

| Check                      | What to look for                                                        |
| -------------------------- | ----------------------------------------------------------------------- |
| No `resource name` warning | Console should **not** say `Resource name is not "prompt_train_script"` |
| Framework detected         | Console prints the detected framework (`qbx`, `qb`, `esx`, or `none`)   |
| Trains spawn               | After the first player joins you should see trains appear on the map    |
