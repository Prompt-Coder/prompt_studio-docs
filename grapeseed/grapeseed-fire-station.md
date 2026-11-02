---
description: Grapeseed Fire Station — a 4-bay drive-through station with a full crew floor, gym and native interior audio.
---

# 🚒 Grapeseed Fire Station

<figure><img src="../.gitbook/assets/banner-grapeseed-fire-station.jpg" alt="GRAPESEED FIRE STATION"><figcaption></figcaption></figure>

{% embed url="https://store.prompt-mods.com/store/package/7277536" %}
**Official asset for FiveM — available on CFX Portal and Prompt's Mods Store**
{% endembed %}

{% embed url="https://youtu.be/5hHh8ag99Rc" %}

The **Grapeseed Fire Station** gives the north of the map a real, working fire house. It is built as a single MLO — four **drive-through** apparatus bays with roller doors at both ends, a crew floor with offices, a meeting room, a kitchen, a hangout area, lockers and bathrooms, and a full gym that can run animated equipment. It ships with native interior audio (occlusion, per-room reverb and door sounds) and an interior LOD, so it holds up from the road as well as it does from inside.

***

### 🗺️ Map Location

The station sits on the north-west edge of Grapeseed:

* **Main pedestrian entrance**: `1965.04, 4625.70, 41.23`
* **Upper-floor entrances**: `1967.67, 4626.72, 44.94` and `1970.73, 4634.49, 44.94`
* **Interior placement**: `1951.02, 4626.86, 45.38`

The four bays are drive-through — each has a door on the forecourt side and a matching door at the rear:

| Bay | Forecourt door | Rear door |
| --- | --- | --- |
| 1 | `1957.84, 4621.30, 41.59` | `1952.35, 4635.35, 41.59` |
| 2 | `1952.18, 4619.09, 41.59` | `1946.70, 4633.14, 41.59` |
| 3 | `1946.34, 4616.81, 41.59` | `1940.86, 4630.86, 41.59` |
| 4 | `1940.69, 4614.60, 41.59` | `1935.21, 4628.65, 41.59` |

***

### 🛠️ Features

#### 🚒 Apparatus bay

Four drive-through bays, eight roller doors, a workshop corner with tool boxes, gas cylinders and spray cans, and five full sets of turnout gear (jacket, pants, helmet) on the racks. The bay is the largest volume in the building and is tuned as such in the interior audio.

#### 🏠 Crew floor

* Hallway and reception
* Two offices (desks, phones, fax, folders)
* Meeting room
* Kitchen
* Hangout area — sofas, armchairs and a TV
* Locker room
* Bathrooms

#### 🏋️ Gym

What you get depends on which core is installed, and the station works it out on its own:

* **With [Animations Core 2.0](../scripts/animations-core-2.0.md)** — the equipment is replaced with animated machines your players can actually use. Thirteen pieces: two flat benches, two bench presses, two exercise bikes, two cable/pull stations, a lat pull, a row pull, a leg press, a speed bag and a wall-mounted speed bag.
* **With the limited core** — the same eleven pieces it can animate; the two bench presses are not spawned, because that core has no bench-press animation.
* **With no core at all** — every machine is the baked static prop. This is also what you get running the map on its own with the scripts deleted, since the `gym` entity set is on by default in the ymap.

The tyre, the dumbbell racks and the food table have no animated counterpart, so they stay in the interior permanently and are never part of the entity set.

{% hint style="info" %}
The animated machines are fitted onto the **footprints** of the baked props, so the gym layout stays the same either way — nothing moves when a core is added or removed.
{% endhint %}

#### 🔊 Interior audio

Native GTA audio, provided through the shared `prompt_audio` resource:

* **Occlusion** — sound is muffled correctly through walls and doors. Glazing is sealed, the bay doors and every interior door occlude when shut, and the hatches and over-wall vents between the bay and the corridor stay open on purpose.
* **Room reverb** — the apparatus bay gets a large hall tail, the gym and the tiled rooms a shorter one, the carpeted offices stay dry.
* **Door sounds** — all eleven door models have open/close audio, with the roller-door family on the eight bay doors.

#### 🚪 Door behaviour

All eleven door models are registered in `prompt_doortuning` as standard latching doors, the same tuning used by the other Prompt fire stations.

#### 📦 LOD

The interior has its own LOD drawable that draws out to **200 m**, taking over from the MLO at 80 m. Textures come from the station's own shared dictionaries, so the LOD costs almost nothing.

***

### 🪑 Chairs and Props

The seating used throughout the station:

* `tuco_gr_fire_chair`
* `tuco_gr_fire_bar_chair`
* `tuco_gr_fire_armchair`
* `tuco_gr_fire_hall_chair`
* `tuco_gr_fire_sofa_1`
* `tuco_gr_fire_sofa_2`
* `prop_off_chair_01`
* `p_clb_officechair_s`

The TV in the day room is `prop_tv_flat_02`.

***

### 📦 Entity Sets

The set is listed in the ymap's `defaultEntitySets`, so it is **on out of the box** — the gym is furnished even with no scripts running. The gym script's only job is to switch it off once a core has taken over.

| Entity set | Contents | Switched off when |
| --- | --- | --- |
| `gym` | The thirteen swappable machines | An Animations Core is running |

See [Entity Sets](../extra-content/entity-sets.md) for how to toggle an entity set by hand.

***

### 🚀 Installation Guide

{% stepper %}
{% step %}
#### Download the resource

Grab `prompt_grapeseed_firestation` from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Grapeseed+Fire+Station) and drop it into your `resources` folder.
{% endstep %}

{% step %}
#### Add it to `server.cfg`

```
ensure prompt_grapeseed_firestation
```
{% endstep %}

{% step %}
#### Add the shared audio resource

The interior audio lives in our free shared `prompt_audio` resource, which comes with the map as a separate package on the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Audio). Ensure it **before** the map:

```
ensure prompt_audio
ensure prompt_grapeseed_firestation
```

Without it the station still loads, but you lose occlusion, room reverb and door sounds.
{% endstep %}

{% step %}
#### Add the shared door tuning

```
ensure prompt_doortuning
```
{% endstep %}

{% step %}
#### (Optional) Animated gym

If you own Animations Core 2.0 (or the limited core), ensure it anywhere in your config — the station finds it on its own and switches the gym over. Nothing to configure.
{% endstep %}

{% step %}
#### Restart and test

Restart the server — a full restart, not `restart <resource>`, because the audio data is cached — then head to `1965.04, 4625.70, 41.23`.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Audio and occlusion only load on a **full server restart**. Restarting just the resource, or rejoining, is not enough.
{% endhint %}

***

### ⚙️ Configuration

The only configurable part is the gym, in `gym/config.lua`:

{% code title="gym/config.lua" %}
```lua
Config.GSFireGym = {
    mode  = 'auto',   -- 'auto' = animated if a core is present, else the static set
                      -- 'static' = always the baked props, ignore the core
    debug = false,
}
```
{% endcode %}

In-game, `/gsfiregymcheck` prints which mode is live and whether the entity set resolved — the first thing to run if the gym ever looks wrong.

***

### 🚪 Doorlocks

{% hint style="info" %}
ox_doorlock entries for this station are not shipped yet — ask support and we will add them.
{% endhint %}

***

For further assistance, contact support. Enjoy using the Grapeseed Fire Station on your FiveM server! 🚀
