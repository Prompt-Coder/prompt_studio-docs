---
description: One page to install any Sandy Shores map — start lines, load order, and what each map needs
icon: rocket
---

# 🚀 Sandy Shores — Installation

Every Sandy Shores map installs the same way. This page is the short version for all of them — the per-map pages only add location, features and doorlock data.

{% hint style="info" %}
Sandy Shores is split into **one resource per map** on purpose. Install only the maps you own; nothing here requires you to run the full set.
{% endhint %}

***

## Quick install (any Sandy map)

{% stepper %}
{% step %}
#### Step 1 — Add the resource

Drop the map folder into your `resources` directory. We recommend grouping them so load order is easy to manage:

<pre><code><strong>resources/[promptsandy]/prompt_sandy_bank
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Add it to server.cfg

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_bank
</strong></code></pre>

Using a folder like `[promptsandy]`? A single `ensure [promptsandy]` starts everything inside it.
{% endstep %}

{% step %}
#### Step 3 — Install the Sandy MapData

**This is the step people miss.** Almost every Sandy map needs the matching [**Sandy MapData**](sandy-mapdata.md) or it will load wrong — floating props, missing ground, or no interior at all.
{% endstep %}

{% step %}
#### Step 4 — Restart and check

Restart the server, travel to the map, and confirm the exterior and interior load ✅
{% endstep %}
{% endstepper %}

***

## Load order

Order matters in three places only:

```cfg
ensure ox_lib                  # before any map that uses it
start cfx_prompt_sandy_mapdata # MapData before the maps
start [promptsandy]            # all your Sandy maps
start prompt_sandy_shared      # needed for Sandy Houses interiors
```

{% hint style="warning" %}
`ox_lib` must start **before** the maps that depend on it. Everything else is a pure map resource and is order-independent.
{% endhint %}

***

## All Sandy resources

Resource names are exact — copy them straight into `server.cfg`.

| Map | Resource | Also needs | Exterior-Only |
| --- | --- | --- | :---: |
| [Sandy MapData](sandy-mapdata.md) | `cfx_prompt_sandy_mapdata` | — | — |
| [Sandy Shores Downtown](sandy-downtown.md) | `prompt_sandy_downtown` | — | ✓ |
| [Custom Roads & Traffic](custom-roads-and-traffic.md) | `prompt_sandy_roads` | — | — |
| [The Corner](the-corner.md) | `prompt_sandy_corner` | `ox_lib` | ✓ |
| [University](university.md) | `prompt_sandy_university` | — | ✓ |
| [Sandy Fire Station V2](sandy-fire-station-v2.md) | `prompt_sandy_fire2` | — | ✓ |
| [Sandy Hospital V2](sandy-hospital-v2.md) | `prompt_sandy_hospital2` | `ox_lib` | ✓ |
| [Sandy Apartments](sandy-apartments.md) | `prompt_sandy_apts` | — | ✓ |
| [Sandy Bank](sandy-bank.md) | `prompt_sandy_bank` | — | ✓ |
| [Sandy Market](sandy-market.md) | `prompt_sandy_market` | — | ✓ |
| [Sandy Motel](sandy-motel.md) | `prompt_sandy_motel` | — | ✓ |
| [Sandy Mechanic](sandy-mechanic.md) | `prompt_sandy_mechanic` | `ox_lib` | ✓ |
| [Illegal Garage & Gas Station](sandy-illegal-garage-and-gas-station-with-carwash.md) | `prompt_sandy_illegal_garage` | `ox_lib` | ✓ |
| [Sandy Church](sandy-church.md) | `prompt_sandy_church` | — | ✓ |
| [Sandy Car Dealership](sandy-car-dealership.md) | `prompt_sandy_classic_car_dealership` | — | ✓ |
| [Sandy City Hall](sandy-city-hall.md) | `prompt_sandy_cityhall` | `ox_lib` | ✓ |
| [Sandy Houses](sandy-houses.md) | `prompt_sandy_houses_part1` | `prompt_sandy_shared` | ✓ |
| [Sandy Train Station](sandy-train-station.md) | `prompt_sandy_train_station` | — | ✓ |
| [Sandy Sheriff](sandy-sheriff.md) | `prompt_sandy_sheriff` | — | ✓ |
| [Sandy Airport](sandy-airport.md) | `prompt_sandy_airfield` | — | — |
| [Sandy Hospital](sandy-hospital.md) | `prompt_sandy_hospital` | — | ✓ |
| [Sandy Fire Department](sandy-fire-department.md) | `cfx_prompt_sandy_shores_fire_department` | — | ✓ |
| [Sandy Marina](sandy-marina.md) | `cfx_prompt_sandy_marina` | — | — |
| [Boat House](boat-house.md) | `cfx_chuz_sandy_shores_boat_house` | — | — |
| [\[FREE\] Construction Zones](free-construction-zones.md) | `prompt_sandy_corner_construction`<br>`prompt_sandy_downtown_construction` | — | — |

***

## Add-ons

{% tabs %}
{% tab title="Sandy Shared Files" %}
Required for **Sandy Houses interiors**. The house interiors ship in their own resource:

```cfg
start prompt_sandy_shared
start prompt_sandy_houses_part1
```

Without it the houses still load — as exteriors only, with no interiors. Download it from the CFX Portal (*Prompt's - Sandy Shared Files*).
{% endtab %}

{% tab title="Exterior-Only Add-On" %}
Free drag-and-drop patch that strips interiors from the maps marked ✓ above, keeping the exteriors fully intact. Useful for lower-end servers.

→ [**Exterior-Only Add-On**](exterior-only-add-on.md)
{% endtab %}

{% tab title="Doorlocks" %}
Most Sandy maps ship community-submitted [`ox_doorlock`](https://github.com/overextended/ox_doorlock) SQL on their own page — import it and restart `ox_doorlock`.

{% hint style="success" %}
All our doorlock SQL uses `DEFAULT` for the `id` column, so your database assigns free IDs on import. It will never collide with doorlocks you already have, no matter how many of our maps you install.
{% endhint %}
{% endtab %}
{% endtabs %}

***

## Troubleshooting

<details>

<summary>The map doesn't appear at all</summary>

1. Check the resource is actually started — look for it in the server console on boot.
2. Confirm the folder name matches the `start` line exactly (they're case-sensitive on Linux).
3. Clear your client cache: `%localappdata%\FiveM\FiveM Application Data\data\cache`, then rejoin.

</details>

<details>

<summary>Exterior loads but the interior is missing or floating</summary>

Almost always the **MapData**. Make sure you have the correct [Sandy MapData](sandy-mapdata.md) installed and started **before** the maps.

For Sandy Houses specifically, missing interiors usually means `prompt_sandy_shared` isn't installed.

</details>

<details>

<summary>Props or ground are in the wrong place after an update</summary>

Update the MapData too. MapData and maps are versioned together — a new map release can expect a newer MapData.

</details>

<details>

<summary>Doorlocks didn't import</summary>

Import the SQL from the map's own page, then `restart ox_doorlock`. If a query fails, check you copied the full statement including the closing `;`.

</details>

***

Still stuck? Join the [Prompt Studio Discord](https://discord.gg/rKbHHdfZFU) with your resource name, console errors, and a screenshot — that's usually enough for us to spot it straight away.
