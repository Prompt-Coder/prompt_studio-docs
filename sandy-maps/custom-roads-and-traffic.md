# 🌴 Custom Roads & Traffic

A full road network rework for Sandy Shores. Includes new road geometry with editable textures, new AI traffic with optional bridge routing, a reworked entrance sign, palms with lights, a roundabout food-truck area, a rural walkway to the bus stop, and additional vegetation. Every optional feature is a separate folder under `stream/`, so server owners can keep only what they want.

{% embed url="https://youtu.be/hNyPQzAY80o" %}

{% hint style="info" %}
Pure map resource — no framework, no scripts, no dependencies. Both `stream/` and `mapdata/` folders are required (the resource ships its own base road file replacements).
{% endhint %}

## <i class="fa-toolbox">:toolbox:</i> Installation Instructions

{% stepper %}
{% step %}
Place the `prompt_sandy_roads` folder inside your `resources` directory.
{% endstep %}

{% step %}
Insert the following line to ensure the map loads automatically: `start prompt_sandy_roads`
{% endstep %}

{% step %}
Make sure you have the correct Sandy MapData installed.
{% endstep %}

{% step %}
Restart your server and drive around Sandy Shores. If the new roads, signs, palms, and AI traffic load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

## Modular components

Every optional feature is a separate folder inside `stream/`. **Delete any folder to disable that feature** — no other changes required.

| Folder                   | What it adds                                                             |
| ------------------------ | ------------------------------------------------------------------------ |
| `roads/`                 | New road geometry, textures, LODs, traffic lights, distant lights        |
| `traffic/`               | New AI traffic across Sandy Shores (includes bridge routing — see below) |
| `entrance_sign/`         | Reworked Sandy Shores entrance sign                                      |
| `palms/`                 | Curvy palms with custom lights along the front-side road                 |
| `round_stop/`            | Roundabout food-truck area with big tree and lighting                    |
| `rural_walkway/`         | Pedestrian walkway from the front of Sandy Shores to the bus stop        |
| `additional_vegetation/` | Extra vegetation on the front side of Sandy Shores                       |

{% hint style="danger" %}
Do not delete the `mapdata/` folder at the resource root, or the `_manifest.ymf` and `prompt_sandy_addons_toroad.ytyp` files at the top of `stream/`. These are required for the resource to load. Modular removal applies only to subfolders inside `stream/`.
{% endhint %}

## Editable road textures

Open these YTDs in OpenIV or RPF Explorer to customize the road textures:

* `stream/roads/prompt_sandy_roads.ytd` — main road textures
* `stream/roads/prompt_sandy_roads_lod.ytd` — LOD textures

Replace any texture inside and the corresponding road surface updates in-game on next resource start.

## Bridge AI traffic & GPS routing

By default, AI traffic uses the bridge and the in-game GPS routes players across the bridge when it's the shortest path.

To **disable** bridge AI + GPS routing while keeping AI traffic on the rest of the map:

1. Delete the `stream/traffic/withbridge/` folder entirely.
2. Move the `nobridge/` folder (located at the resource root) into `stream/traffic/`, so the resulting path is `stream/traffic/nobridge/`.
3. Restart the resource.

To disable AI traffic completely, delete `stream/traffic/` entirely.

## Location

Sandy Shores — full town road network. Recommended viewing point: `1624.34, 3685.44, 34.7`

## Notes

* Fully compatible with other Sandy Shores maps and the Sandy MapData system.
* Modular folder structure lets server owners disable any individual feature by deleting its folder under `stream/`.
* Optimized with LODs, distant lights, and night-lighting for performance.
* Designed to work alongside the Prompt Studios Sandy Shores map collection.

For bug reports, support, or feedback, join the [Prompt Studios Discord](https://discord.gg/promptstudios).
