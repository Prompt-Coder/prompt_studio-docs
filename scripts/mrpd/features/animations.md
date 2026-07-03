---
description: 60+ animated props, coffee carry, interrogation, and prisoner escort
icon: person-running
---

# Animations

The largest module — **60+ animated interaction points** across the station, from lockers and evidence shelves to a coffee machine, a two-officer interrogation, and a walk-along prisoner escort. Everything is **job-gated** and routed through your target system.

<!-- TODO: showcase video. Repo file limit is 100 MB (the raw preview is 249 MB), so upload to YouTube and embed here like the other pages, e.g. {% embed url="https://youtu.be/VIDEO_ID" %} — or ask us to compress + self-host. -->

***

### Interaction types

| Type | Behaviour |
| --- | --- |
| **Looped** | Interact to start a looping animation; interact again to stop. |
| **Phased** | Plays an **enter → loop → exit** sequence (doors, chairs, cart). |
| **Single-shot** | Plays once, then does something — the coffee machine hands you a coffee. |
| **Carried** | A prop pinned to your hand you can **walk around with** (coffee cup). |
| **Duo** | A **two-player synced** scene (interrogation). |
| **Convoy** | Walk a cuffed suspect along, **attached** to you. |

***

### Animated props

Grouped by prop; every placement shares the same animation. Counts are the number of spots in the MLO.

| Prop | Count | Type | Model | Pack |
| --- | --- | --- | --- | --- |
| Armory gun locker | 2 | looped | `prompt_mrpd_armorygunlocker` | mrpd1 |
| Change locker | 10 | phased | `prompt_mrpd_changelocker1_door` | mrpd1 |
| Evidence locker | 1 | looped | `prompt_mrpd_evdlocker` | mrpd1 |
| Evidence plan table | 1 | looped | `prompt_mrpd_evdplantable` | mrpd1 |
| Evidence shelf (2 / 4 / 5) | 26 | looped | `prompt_mrpd_evdshelf2/4/5` | mrpd1 |
| Body cam shelf | 2 | looped | `prompt_mrpd_techbodycshelf` | mrpd1 |
| Tech desk | 1 | looped | `prompt_mrpd_techdesk` | mrpd1 |
| Drone wall | 1 | looped | `promtp_mrpd_footdronewall` | mrpd1 |
| Listening chair (L / R) | 4 | phased | `prompt_mrpd_listeninganimprop1/2` | mrpd2 |
| Weapon cleaning table | 4 | looped | `d1n_mrpd_garage_large_cleaning_weapons_table_equip_01` | mrpd2 |
| Vend coffee | 6 | single-shot → carried | `prop_vend_coffe_01` | mrpd2 |
| Mug cart | 1 | phased (root-motion) | `prompt_mrpd_mugcart` | mrpd2 |
| Interrogation table | 4 | duo | `apa_mp_h_din_chair_12` | mrpd2 |
| Prison bench | 2 | duo (park) | `prompt_mrpd_custbench` | mrpd2 |

Each spot has its own `id` and a `jobs` list in `config/anims.lua`; an empty list falls back to `Config.Anims.DefaultJobs` (`police`, `lspd`, `bcso`). Set `enabled = false` on any spot to hide it.

***

### Coffee carry

Get a coffee from a vend machine and carry it while you walk. A persistent hint shows the controls:

* **G** — take a sip
* **X** — drop the cup

Uses base-game dicts: hold `amb@world_human_drinking@coffee@male@base`, sip `amb@world_human_drinking@coffee@male@idle_a`. The system is data-driven (`Config.Anims.CarriedItems`) so more items can be added later.

***

### Interrogation (duo)

A synced two-officer scene at the interrogation table: the officer (lead) and a compliant suspect sit, with an **E-menu of "beats"** (`assault1/2/3`) and a shared cinematic camera. Both clients drive both peds locally off a network-time rendezvous.

### Prisoner escort (convoy)

Walk a **cuffed** suspect along, attached at your side with an arm-IK grip and a stock cuffed gait. Start it from a target option on the suspect **or** from exports:

```lua
exports.prompt_mrpd_scripts:StartConvoy(targetServerId)   -- client
exports.prompt_mrpd_scripts:StopConvoy()                  -- client
exports.prompt_mrpd_scripts:IsConvoying()                 -- client
```

The **park** flow ties the two together: seat an inmate on a holding bench (they loop there indefinitely), any officer picks them up later, and the pickup chains straight back into a convoy.

{% hint style="info" %}
Convoy requires the target to be **cuffed**. That's enforced by the `canPartner` hook (the server can't read a ped's animation, so cuffed-authority lives in your hook) — see [Hooks](../developers/hooks.md).
{% endhint %}

***

### For developers — `.ycd` dictionaries

All animation data is in `config/anims.lua` (`Config.Anims.Spots`, `.CarriedItems`, `.Duo`, `.Convoy`). The custom clips ship in these dicts:

| Dict | Contains |
| --- | --- |
| `prompt@mrpd@prop` | mrpd1 **prop** clips (lockers, evidence shelves, tech, drone) |
| `prompt@mrpd@ped` | mrpd1 **ped** clips |
| `prompt@mrpd2` | mrpd2 **prop** clips (chairs, cleaning, vend, mug cart, interrogation) — note the `prompt@…` clip-name prefix |
| `prompt@mrpd@ped2` | mrpd2 **ped** clips (incl. convoy `police_follow` / `zek_follow`, bench pairs) |

Base-game dicts used: `amb@world_human_drinking@coffee@male@base` / `…@idle_a` (coffee), `anim@move_m@prisoner_cuffed` (escort legs — idle/walk), `mp_arresting` (cuff idle preserved across a convoy).

Naming: prop clips are `prompt_mrpd_<name>_animation` (mrpd1) or `prompt@<name>` (mrpd2); ped clips are `<name>_ped`. Phased spots use `openPropAnim`/`propAnim`/`closePropAnim` (+ the matching `*PedAnim`); looped spots use just `propAnim`/`pedAnim` with `flag = 1`; single-shot uses `flag = 0` + `carriedItem`.

Extend behaviour per spot via [Hooks](../developers/hooks.md) (`anims` feature — `canUse`, `canPartner`, `onStart`, `onEnd`, keyed by spot `id`) and integrate with [Exports](../developers/exports-and-commands.md) (`IsPlayerAnimated`, `StopPlayerAnim`, `StartConvoy`, …).

***

{% hint style="info" %}
Prop animations run **locally per client** by design (the ped is the clock) — there are no networked props to desync.
{% endhint %}
