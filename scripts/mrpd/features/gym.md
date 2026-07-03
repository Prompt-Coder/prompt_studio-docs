---
description: Animated workout equipment
icon: dumbbell
---

# Gym

A furnished gym in the garage interior — benches, exercise bikes, leg press, speed bags, and pull/lat/row machines.

***

### How it works

The gym is set up **once, at server start** — there's no runtime toggle:

* With an **anim core** running (`prompt_anim_core`), the equipment is animated and interactive.
* Without one, it **falls back** to a static entity set so the gym still looks furnished.

```lua
-- config/gym.lua
Config.Gym.Mode = 'auto'   -- 'auto' = anim core if present, else static · 'static' = always static
```

***

### Requirements

* Animated equipment needs a compatible **anim core** resource started before MRPD.
* No anim core? Leave `Mode = 'auto'` — you get the static furnished gym automatically.

***

{% hint style="info" %}
The gym is **not** a runtime feature — it's placed at boot based on whether an anim core is present. To change it, change `Config.Gym` and restart the server.
{% endhint %}
