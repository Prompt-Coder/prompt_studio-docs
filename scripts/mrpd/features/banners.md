---
description: Toggleable exterior banners
icon: flag
---

# Banners

Exterior banners on the MRPD building that can be raised or lowered — **synced to everyone** and **remembered across restarts**.

***

### How it works

* Interact with the banner toggle point (`ox_target`) to raise or lower the banners.
* The state is synced to all players (GlobalState) and **persisted** (KVP), so it survives a restart.
* Interaction reach is capped at **1.5 m** so you can't flip it through a wall.

***

### Access

Toggling is limited to authorized officers — normal police access **or** the `mrpd.banners` ACE (for admins). See [Configuration](../configuration.md) and [Hooks](../developers/hooks.md) (`banners` · `canToggle`) to customize.

***

{% hint style="info" %}
Because the state is persisted, whatever you set stays that way until someone toggles it again — set it once for an event and forget it.
{% endhint %}
