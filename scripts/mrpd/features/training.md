---
description: Shooting range, killhouse, and CQB team match
icon: crosshairs
---

# Training

A full firearms-training wing: a **shooting range** with a live DUI scoreboard, a **killhouse** with weapon-selector props, and a **CQB team match** (red vs blue).

***

### What officers do

* **Pick a weapon** — walk up to a weapon-selector prop in the killhouse and select it. Presets: Combat Pistol, SMG, Carbine Rifle, Pump Shotgun.
* **Shoot the range** — hits register on the **DUI scoreboard** above the arena.
* **Join a team** — walk into the **red** or **blue** team zone to spawn in for a CQB match.
* **Instructor panel** — an interactive screen on the training desk control center (ox_target) to drive modes and presets.

***

### Access

| Action | Who |
| --- | --- |
| Join team · claim stall · switch preset | any officer (`Config.access`) |
| Instructor panel + instructor commands | **instructor tier** (`Config.Training.InstructorAccess`) |

See [Configuration → Instructor tier](../configuration.md) to set who instructs. By default any officer (grade 0+) can; raise `minGrade` for supervisors only.

***

### Weapons — native or inventory

By default training weapons are given **natively** on the client. Inventory / weapon-anticheat servers flip one switch and route them through their own system:

```lua
-- config/training.lua
Config.Weapons = { custom = true, give = ..., remove = ... }
```

A ready-to-use `ox_inventory` example ships in the file. See [Providers](../developers/providers.md).

***

### Downed players (CQB)

Override what happens to a downed match player — e.g. tell your ambulance script it isn't a real death:

```lua
-- config/training.lua
Config.Training.Callbacks.onDowned = function(src) ... end
```

***

{% hint style="warning" %}
The instructor panel and commands are **silent** without the instructor tier — grant the job + grade (or the `mrpd.training.instructor` ACE). This is intended: only instructors run drills.
{% endhint %}
