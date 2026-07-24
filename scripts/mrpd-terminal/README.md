---
description: A physical in-world police MDT — the station's monitors become working computers
icon: desktop
---

# MRPD Terminal (In-World MDT)

## Prompt MRPD Terminal

***

<details>

<summary><strong>Overview</strong></summary>

<br>

A physical, in-world police computer. Officers walk up to a monitor or laptop inside the station and the **screen itself** lights up with a working MDT — no fullscreen takeover, no tablet item. The UI is rendered onto the monitor's glass (DUI) and driven with the mouse while your character stands at the desk.

* **Dashboard** — identity, callsign, duty, on-duty roster, live dispatch feed
* **Registries** — citizens, vehicles, weapons (per backend)
* **Records** — warrants, BOLOs, incidents, evidence, charges (per backend)
* **Enforcement** — fines, licenses, jail, impound (per backend)
* **Fleet kiosk** — a second screen kind in the garage: grade-filtered vehicle list + spawn

**The terminal does not replace your police script — it renders it.** All data comes from the MDT/police backend your server already runs, through an adapter. Your existing MDT stays the source of truth; the terminal is an in-world screen for it.

</details>

***

{% hint style="info" %}
The terminal pairs with the [**Mission Row Police Department** map](../../government-maps/mission-row-police-department.md) (the shipped monitors live in its interiors), and works alongside the [MRPD Police Feature Pack](../mrpd/README.md) — each runs independently.
{% endhint %}

### Requirements

* [`ox_lib`](https://github.com/overextended/ox_lib) — **required**
* [`ox_target`](https://github.com/overextended/ox_target) — **required** (the walk-up interaction)
* `oxmysql` — recommended; without it the terminal runs in a data-less standalone mode
* **A supported backend** — one of:
  * [Wasabi Advanced MDT](https://wasabiscripts.com)
  * [pscripts](https://pscripts.tebex.io/) **p\_mdt** (+ optional p\_policejob for the enforcement pages)
  * [LB Tablet](https://lbscripts.com) (MDT app)
  * stock **qb-policejob**

{% hint style="success" %}
**Big thanks to [Wasabi](https://wasabiscripts.com) and [pscripts](https://pscripts.tebex.io/)** for working with us and providing the exports that make these integrations possible ❤️
{% endhint %}

Framework — `qb-core`, `qbx_core`, or `es_extended`, **auto-detected**.

{% hint style="warning" %}
No backend installed? The terminal still runs: the `null` adapter shows an honest empty state, and `Config.showcase = true` serves full scripted demo data for previews. See [Adapters](adapters.md).
{% endhint %}

***

### Installation

{% stepper %}
{% step %}
#### Add the resource

Place the folder inside your `resources` directory and ensure it **after** its dependencies and your backend:

{% code title="server.cfg" %}
```
ensure ox_lib
ensure ox_target
ensure oxmysql
ensure wasabi_mdt              # or p_mdt / lb-tablet / qb-policejob
ensure prompt_mrpd_terminal
```
{% endcode %}
{% endstep %}

{% step %}
#### Check the selection banner

On boot the terminal picks the first detected backend from `Config.adapterPriority` and prints it:

```
[MRPD Terminal] Adapter loaded: Wasabi MDT — Advanced MDT & Dispatch (wasabi_mdt)
```

Wrong backend picked (several installed)? Reorder `Config.adapterPriority` — see [Configuration](configuration.md).
{% endstep %}

{% step %}
#### Use it in-game

Walk up to a terminal monitor at Mission Row as an **on-duty officer** and use the target option (*"Use terminal"*). The garage kiosk (*"Use fleet kiosk"*) works the same way.
{% endstep %}
{% endstepper %}

***

### Who can open it

All configurable in `Config.access`:

* a police job (`police`, `lspd`, `sasp`, `bcso` by default), **and**
* being **on duty**, — or
* the ACE permission `mrpd_terminal.use` (admin bypass).

Individual features are then gated twice more:

1. **By grade** — `Config.features` maps every action to a minimum rank (flag a plate ≥ 2, grant licenses ≥ 4, …).
2. **By backend** — the UI only renders what the active adapter genuinely supports. Different backends produce visibly different terminals, with **no dead buttons**. See the capability matrix in [Adapters](adapters.md).

***

### The two screen kinds

| Kind | What it opens |
| ---------- | ------------------------------------------------------------------ |
| `terminal` | The full MDT — dashboard, registries, records, enforcement |
| `fleet` | The garage kiosk — grade-filtered vehicle list + spawn |

Both are placements in `Config.targets`. Interactions attach to the **prop model**, so every instance of a known monitor model — baked into an MLO, spawned by a script, placed by hand — is automatically interactive. Adding screens elsewhere is a config entry + one in-game calibration; see [Configuration](configuration.md).

***

### Diagnostics

* `Config.debug = true` — verbose logs, capability dump on boot, dev commands (`/termcam`, `/termtest_*`)
* `Config.showcase = true` — demo mode: permission bypass + scripted data (videos/previews)
* `/termtest` (admin, in-game) — self-check battery

{% hint style="success" %}
Building an adapter for a backend we don't ship? That's a supported extension point — start at [For Developers](developers/README.md).
{% endhint %}
