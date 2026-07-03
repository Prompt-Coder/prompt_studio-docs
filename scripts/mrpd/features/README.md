---
description: Every module, its settings, and its in-game controls
icon: puzzle-piece
---

# Features

Each module is independent — toggle any of them in `Config.Modules` (see [Configuration](../configuration.md)). The three substantial modules have their own pages; the lighter ones are covered right here.

<table data-view="cards"><thead><tr><th></th><th></th><th data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Training</strong></td><td>Shooting range, killhouse &#x26; CQB team match</td><td><a href="training.md">training.md</a></td></tr><tr><td><strong>Custody</strong></td><td>Briefing room, interactive TV &#x26; memorial</td><td><a href="custody.md">custody.md</a></td></tr><tr><td><strong>Animations</strong></td><td>60+ props, coffee carry, interrogation &#x26; escort</td><td><a href="animations.md">animations.md</a></td></tr></tbody></table>

***

## Gym

A furnished gym in the garage interior — benches, bikes, leg press, speed bags, and pull/lat/row machines. It's set up **once, at server start**:

* With an **anim core** running (`prompt_anim_core`), the equipment is animated and interactive.
* Without one, it **falls back** to a static entity set so the gym still looks furnished.

```lua
-- config/gym.lua
Config.Gym.Mode = 'auto'   -- 'auto' = anim core if present, else static · 'static' = always static
```

There's no runtime toggle — to change it, edit `Config.Gym` and restart.

***

## Elevator

A working multi-floor elevator connecting MRPD's levels. Interact with the elevator panel to pick a floor. Enable/disable with `Config.Modules.elevator`; floor definitions live in the elevator module's config.

***

## Audio

Two ambient layers: a **hallway PA** with periodic announcements, and a **sanctuary / holding-cell** ambient bed. Tune them in `config.lua`'s `Config.Audio` block.

{% hint style="info" %}
The sound files live in the shared **`prompt_audio`** resource — install and start it, or there's nothing to play.
{% endhint %}

***

## Banners

Exterior banners on the building that can be raised or lowered — **synced to everyone** and **remembered across restarts** (GlobalState + KVP). Interact with the banner toggle point (reach capped at **1.5 m** so you can't flip it through a wall).

**Access:** normal police access **or** the `mrpd.banners` ACE (for admins). Customize via [Hooks](../developers/hooks.md) (`banners` · `canToggle`).
