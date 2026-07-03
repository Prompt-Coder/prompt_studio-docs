# 🚓 Mission Row Police Department

<!-- TODO: replace with the real store package embed, e.g. {% embed url="https://fivem.prompt-mods.com/package/PACKAGE_ID" %} -->

<!-- TODO: add a showcase video, e.g. {% embed url="https://youtu.be/VIDEO_ID" %} -->

The **Mission Row Police Department** is a fully detailed MLO for FiveM — a complete police station with a reworked interior and exterior, built for roleplay, law enforcement, and emergency-response scenarios. It ships as a standalone map and pairs with the **MRPD Police Feature Pack** for interactive features.

***

### 🧩 Base vs Full

| Tier | Resource | What you get |
| --- | --- | --- |
| **Base** | `prompt_mrpd` | The map — interiors, exterior, garage, elevator shell. Runs on its own. |
| **Full** | `+ prompt_mrpd_scripts` | Adds training, custody, gym, animations, audio, and banners. |

When the **Full** pack runs, the map's standalone layer steps aside automatically. → [**MRPD Police Feature Pack**](../scripts/mrpd/README.md)

***

### 📍 Map Location

Mission Row Police Department. Teleport inside the station to verify the load:\
**455.91, -999.01, 27.47**

***

### 🛠️ Features

* Detailed **interior** — briefing room, holding cells, garage, gym area, and offices
* Reworked **exterior** building, decals, and signage
* Scripted **garage** door
* Multi-floor **elevator** shell
* Animated props, PA audio, and banners *(with the [Full pack](../scripts/mrpd/README.md))*

***

### 🚪 Doorlock System (optional)

The station is compatible with [`ox_doorlock`](https://github.com/overextended/ox_doorlock). If you use it, import the provided SQL to enable the door setup.

<!-- TODO: paste the MRPD ox_doorlock SQL INSERT block here (same format as the other map pages) -->

***

### 🚀 Installation

{% stepper %}
{% step %}
#### Step 1 — Add the resource

Place `prompt_mrpd` inside your `resources` folder:

```
resources/prompt_mrpd
```
{% endstep %}

{% step %}
#### Step 2 — Add to server.cfg

```
ensure prompt_mrpd
```

Adding the Full pack too? Start it **after** the map (and after `ox_lib`):

```
ensure ox_lib
ensure prompt_mrpd
ensure prompt_mrpd_scripts
```
{% endstep %}

{% step %}
#### Step 3 — Doorlocks (optional)

If you use `ox_doorlock`, import the SQL above into your database.
{% endstep %}

{% step %}
#### Step 4 — Restart & verify

Restart the server and teleport to **455.91, -999.01, 27.47** to confirm the interior loads ✅
{% endstep %}
{% endstepper %}

***

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
