---
description: by adaz
icon: train
---

# Train Script

{% hint style="info" %}
**Version 2** (2.1.0) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

### What's new in 2.1.0

* **Drive the trains yourself.** Take over a line's train in its cab, or take out a service train from a depot dispatcher at Sandy Shores, Los Santos or Davis (metro). The cab has a power/brake controller, curve speed limits, signals and train protection, and drivers are paid for every stop they serve ($150 by default). See [Driving](driving.md).
* **NPC passengers on the metro.** They wait on the platforms and get on and off at stops. See [NPC Passengers](npc-passengers.md).
* **Train packs.** A train resource is picked up automatically, with no config edits. A line can run several trains side by side (`fleet` in `config/trains.lua`), and blips show each train type in its own colour. Train packs can add car carriers, with a ramp and cars that ride on the deck. You can also convert trains from GTA5-Mods. See [Train Packs](train-packs.md).
* **One-way lines** and a new **Roxwood line** (Los Santos > Sandy Shores > Paleto Bay > Roxwood), which needs the `amb-roxwood` map. Templates for your own lines and stations are in `prompt_train_script-assets/templates`. See [Lines & Stations](lines-and-stations.md).
* **Freight fallback.** When no other freight line runs, the `freight` line runs the game's own freight train.
* **Doors.** Side doors only open while the train is stopped at a station. Doors between carriages always work. See [Tickets](tickets.md#doors-and-tickets).
* **Who may drive.** By default, players with the `train` job, on duty. Change `driving.jobs` in `config/config.lua`, or give players the `prompt_train.drive` ace. See [Driving](driving.md#who-may-drive).
* **Text.** All text is in the locale files now, including the admin `/trains` menu and the seat prompts, translated into all 14 languages.
* **Fixes.** The default lines no longer use the RTX Paleto rails on servers without RTX Paleto. The Paleto Bay platform height is fixed. Track ids are detected in game, so other resources that add tracks no longer mix up the lines. Client config warnings only show in F8 with `debug` on.

{% hint style="warning" %}
**Updating from 2.0.0-beta**

* Replace the `prompt_train_script` and `prompt_train_script-assets` folders completely. `config/config.lua` has two new sections (12. PLAYER DRIVING and 13. NPC PASSENGERS), and the locale keys were renamed. If you edited either, redo your edits on the new files.
* Add `prompt_sandy_traintunnel` from the zip. The Sandy Shores line needs it now.
* Start your trains before the script (see [Installation](#installation)).
* The track list changed (new Roxwood track), so restart the whole server, not just the resources.
{% endhint %}

***

### Requirements

* FiveM server (artifact 6683 or newer recommended)
* [`ox_lib`](https://github.com/overextended/ox_lib) started **before** every resource below
* `prompt_train_script-assets`: ships with the script. Holds every station, line, `.dat` and streamed asset. `prompt_train_script` has no data of its own; it will not start without this resource running first.
* `prompt_sandy_traintunnel`: ships with the script. The Sandy Shores train tunnel map. The Sandy Shores line runs through the tunnel, so it stays dormant without it.
* A train. Trains are separate resources, not part of the script:
  * `prompt_train_polar_express`, the **Polar Express**, runs the Sandy Shores, Los Santos and Roxwood lines. The version on the Cfx.re portal needs no update for 2.1.0. It only has to start before the script.
  * Optional: trains from GTA5-Mods (Kitsune Trains 7 by Foxunitone), converted with our free [Kitsune converter](https://github.com/Prompt-Coder/prompt_train_kitsune_converter). Converted trains have no doors, seats or interior. See [Train Packs](train-packs.md).

The metro, the monorail and the freight fallback use the game's own trains.

***

### Installation

1. Copy the three folders from the zip, `prompt_train_script`, `prompt_train_script-assets` and `prompt_sandy_traintunnel`, into your `resources` folder. Add `prompt_train_polar_express` too, if it isn't there yet.
2. Add the following to your `server.cfg` **in this order**:

```
ensure ox_lib
ensure prompt_train_polar_express
# only if you converted GTA5-Mods trains (see Train Packs):
# ensure [kt_trains]
ensure prompt_sandy_traintunnel
ensure prompt_train_script-assets
ensure prompt_train_script
```

{% hint style="warning" %}
Trains must start **before** `prompt_train_script`. The script reads the installed trains once, when it starts. A line whose trains start later stays dormant, and a train pack that starts later makes the console say `train pack <name> (...) started after prompt_train_script -- restart prompt_train_script to use it`. Fix the order in `server.cfg` and restart the server.
{% endhint %}

3. Open `config/config.lua` and adjust settings for your server (interaction, framework, inventory, ticket prices, etc.). See [Configuration](configuration.md).
4. If you're running with an inventory resource, register the `train_ticket` item. See [Tickets → Inventory Item](tickets.md#inventory-item). If `integrations.inventory` is `'none'`, skip this — the script keeps tickets itself.

***

### First Boot Checklist

In the server console:

```
train_assets_validate
train_routes
```

| Check                           | What to look for                                                                                                                                                                            |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Assets resource loaded first    | Console should **not** say `cannot read stations and lines from prompt_train_script-assets`                                                                                                 |
| Trains loaded first             | Console should **not** say `started after prompt_train_script` or `none of its trains is installed`                                                                                         |
| `train_assets_validate` passes  | Reports every line's track id, stop count, and point count, ending in `validation passed`. It also runs by itself when the assets resource starts. A line that needs a map you don't run shows as `skipped, needs <resource>` |
| `train_routes` shows every line | Lists each line with its track id, train, fleet, and stations — no unexplained gaps. Dormant lines are listed with what they need                                                          |
| Trains spawn                    | After the first player joins you should see trains appear on the map                                                                                                                        |

#### Dormant lines

A **dormant** line runs no trains. `train_routes` lists it as `dormant line : <id> -- needs <what>`, and the server console says why when the script starts:

| Console says                                                                 | What to do                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `line "<id>" is dormant: <resource> (<state>) not running`                   | The line needs a map (its `requires`) that isn't running: `prompt_sandy_traintunnel` for Sandy Shores, `amb-roxwood` for Roxwood, `cfx-nteam-monorail-map` for the monorail. Start the map before the script. If you don't use that map, the line just stays off |
| `line "<id>" is dormant: none of its trains is installed (needs <resource>)` | None of the line's trains is running. Start the named train before `prompt_train_script`                                                                                                                                                                           |
| `line "<id>" is dormant: none of its stations is available`                  | A station only exists while the map in its `resource` field runs (for example `prompt_sandy_train_station`, `prompt_trainstation_paleto`, `prompt_trainstation_ls`), and none of this line's stations is up. Start those maps before the script                   |
| `line "<id>" is not mounted yet -- run train_build ...`                      | The line isn't in `traintracks.xml` yet. Run `train_build` in the server console, then restart the server                                                                                                                                                         |
| nothing, and `train_routes` says `freight -- needs no other freight line running` | Normal. `freight` is a fallback line: it runs the game's own freight train (2 trains of 14 vehicles, on the game's track 0) only when no other freight line runs. Freight cars have no doors or seats, so tickets and boarding do nothing on it                |

{% hint style="info" %}
`line "lossantos": consist "bullet" left out, prompt_train_bullet is not running` is normal (and the same for `roxwood`, if you run Roxwood). These lines are set up for the AERION bullet train pack (`prompt_train_bullet`, coming soon); until it is installed they run the Polar Express. If the Polar Express isn't running either, the dormant message for the Los Santos line names `prompt_train_bullet`: start `prompt_train_polar_express` before the script.
{% endhint %}

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
