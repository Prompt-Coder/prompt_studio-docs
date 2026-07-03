---
description: Prompt's Mission Row Police Department — Full (scripts) tier
icon: shield-halved
---

# MRPD Police Feature Pack

## Prompt MRPD

***

<details>

<summary><strong>Overview</strong></summary>

<br>

The **Full** tier for Mission Row Police Department — the interactive layer that turns the MRPD map into a working police station.

* **Training** — shooting range, killhouse, and CQB team match
* **Custody** — mugshot board, briefing room + interactive TV/whiteboard, memorial
* **Gym** — animated workout equipment
* **Elevator** — multi-floor access
* **Animations** — lockers, evidence, coffee carry, and 2-officer prisoner escort
* **Audio** — hallway PA and holding-cell ambience
* **Banners** — toggleable exterior banners

Multi-framework, multi-target, and fully localizable (12 languages). Runs on a bare server with sensible defaults — no framework required.

</details>

***

{% hint style="info" %}
This pack is the **Full tier**. It pairs with the [**Mission Row Police Department** map](../../government-maps/mission-row-police-department.md) — the map runs on its own; add this pack on top for the interactive features. When this resource runs, the map's standalone layer steps aside automatically.
{% endhint %}

### Requirements

* [`ox_lib`](https://github.com/overextended/ox_lib) — **required**, started **before** this resource.
* Optional, all **auto-detected** (nothing to wire up):
  * Framework — `qbx_core`, `qb-core`, or `es_extended`
  * Target — `ox_target` or `qb-target`
  * `screenshot-basic` — only for the mugshot board

***

### Installation

{% stepper %}
{% step %}
#### Step 1 — Add the resources

Place both folders inside your `resources` directory:

```
resources/prompt_mrpd            # the map (Base tier)
resources/prompt_mrpd_scripts    # this pack (Full tier)
```
{% endstep %}

{% step %}
#### Step 2 — Start order (server.cfg)

Add to your `server.cfg`, **in this order**:

```
ensure ox_lib
ensure prompt_mrpd
ensure prompt_mrpd_scripts
```

If you use a framework or target system, make sure it starts **before** `prompt_mrpd_scripts`.
{% endstep %}

{% step %}
#### Step 3 — Set your police jobs

Open `config.lua` and list the job names that count as police:

```lua
Config.access = {
    jobs          = { 'police', 'lspd', 'bcso', 'sasp' },
    minGrade      = 0,
    requireOnDuty = false,
}
```

This is the one setting most servers change. See [Configuration](configuration.md) for the full picture.
{% endstep %}

{% step %}
#### Step 4 — Restart & verify

Restart the server (or `ensure prompt_mrpd_scripts`) and watch the console:

* No red `SCRIPT ERROR` lines on boot
* With `Config.debug = true`, the detected framework is printed

Walk into MRPD and confirm the training, gym, and briefing interactions appear ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

### First Boot Checklist

| Check | What to look for |
| --- | --- |
| No boot errors | Console shows **no** red `SCRIPT ERROR` from `prompt_mrpd_scripts` |
| Framework detected | With `Config.debug = true`, console prints `framework = qbox / qbcore / esx / standalone` |
| Access works | An officer (a job in `Config.access.jobs`) can use training/gym; a civilian cannot |
| Interactions appear | Range, gym, elevator, and briefing targets show when you look at them |

{% hint style="warning" %}
Adding a **new file** to the resource later (not just editing one) needs players to **rejoin** — `restart prompt_mrpd_scripts` alone won't stream new manifest entries to already-connected clients.
{% endhint %}

***

### Next steps

* [**Configuration**](configuration.md) — access, modules, language, and framework bridges
* [**Features**](features/README.md) — every module and its in-game controls
* [**For Developers**](developers/README.md) — hooks, providers, and exports
* [**Troubleshooting**](troubleshooting.md) — `/mrpd_debugdump` and common fixes
