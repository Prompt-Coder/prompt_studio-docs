---
description: Hallway PA and holding-cell ambience
icon: volume-high
---

# Audio

Two ambient layers that make the station feel alive: a **hallway PA** and a **holding-cell / sanctuary** ambient bed.

***

### What it adds

* **Hallway PA** — periodic public-address announcements through the station.
* **Sanctuary bed** — a low ambient loop in the holding-cell area.

Tune behaviour in `config.lua`'s `Config.Audio` block (toggles, timing, volume).

***

### Requirements

The actual sound files live in the shared **`prompt_audio`** resource — make sure it's installed and started. The audio module here just triggers those sounds; without the data resource there's nothing to play.

***

{% hint style="info" %}
Enable or disable the whole layer with `Config.Modules.audio` in `config.lua`.
{% endhint %}
