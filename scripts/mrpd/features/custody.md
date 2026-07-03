---
description: Briefing room, interactive briefing TV, and memorial
icon: gavel
---

# Custody

The briefing and memorial wing — a reconfigurable briefing room, an interactive briefing screen, and a memorial.

***

### Briefing room layout

Flip the room between **classroom** and **briefing** layouts. The toggle is an `ox_target` point in the room; the new layout is **synced to everyone** instantly.

* **Who:** instructor tier (`Config.Custody.InstructorAccess`).
* Interaction reach is capped at **1.5 m** so you can't flip it through a wall.

***

### Briefing TV / laptop

An interactive screen an instructor drives from the laptop control point:

* Put an **image URL** on the TV — **Discord CDN only** (`cdn.discordapp.com`, `media.discordapp.net`); YouTube/Twitch are blocked by the browser context.
* A **whiteboard** mode with drawing and text objects (anti-spam limits apply).

**Who:** instructor tier. Without it, the control interaction shows a "no access" notify.

***

### Memorial

A quiet memorial — press **F** on the memorial marker to *Pay Respect* (salute).

***

{% hint style="info" %}
The briefing TV only accepts **Discord CDN** links by design — host your briefing images on Discord and paste the direct file URL. Other domains are rejected.
{% endhint %}
