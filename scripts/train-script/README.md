---
description: by adaz
icon: train
---

# Train Script

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
