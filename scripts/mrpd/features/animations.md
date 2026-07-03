---
description: Animated props, coffee carry, and prisoner escort
icon: person-running
---

# Animations

Job-gated animated interactions around the station — plus a coffee carry and a two-officer prisoner escort.

***

### Animated prop spots

Walk up to a spot (lockers, evidence, and more) and interact to play the tied animation with its prop. Spots are **police-gated** and defined in the anims config.

### Coffee carry

Grab a coffee from a vend point and carry it. A persistent on-screen hint shows the controls:

* **G** — take a sip
* **X** — drop the cup

### Prisoner escort

A synced **two-officer escort** for a cuffed suspect: walk them along, and hand off to a holding bench to retrieve later. Requires a **cuffed target**.

***

### For other scripts

The escort and busy-state are exposed as exports so your death / arrest / admin scripts can see and cleanly cancel MRPD animations — see [Exports & Commands](../developers/exports-and-commands.md) (`IsPlayerAnimated`, `StopPlayerAnim`, `IsCarrying`, `StopCarry`, `StartConvoy`).

***

{% hint style="info" %}
Prop animations run **locally per client** by design (the ped is the clock) — there are no networked props to desync. Want to restrict a spot further? Add a rule in [Hooks](../developers/hooks.md) (`anims` · `canUse`).
{% endhint %}
