---
description: Modules, access, language, and framework bridges
icon: gear
---

# Configuration

Everything owner-facing lives in the **open** files — you never need to touch protected logic:

* `config.lua` — modules, access, debug
* `config/*.lua` — per-feature settings
* `bridge/*.lua` — framework / target / notify / textUI adapters
* `localization/*.lua` — every on-screen string
* `hooks/*.lua` — your own allow/deny rules (see [For Developers](developers/README.md))

***

### Modules

Turn features on or off in `config.lua`. A disabled module registers nothing — no targets, no threads, no commands.

```lua
Config.Modules = {
    training = true,   -- shooting range, killhouse, CQB team match
    custody  = true,   -- mugshot, briefing room + TV, memorial
    gym      = true,   -- animated workout equipment
    elevator = true,   -- multi-floor access
    anims    = true,   -- lockers, evidence, coffee carry, prisoner escort
    audio    = true,   -- hallway PA, cell ambience
    banners  = true,   -- exterior banners
}
```

***

### Access — who may use police features

This is the setting **most servers change**. List the job names that count as police:

```lua
Config.access = {
    jobs          = { 'police', 'lspd', 'bcso', 'sasp' },  -- any of these passes
    minGrade      = 0,               -- minimum rank
    requireOnDuty = false,           -- true = must be clocked in
    ace           = 'mrpd.access',   -- standalone (no framework): this ACE unlocks it
    showcase      = false,           -- true = EVERYONE, everything (demo/dev only)
}
```

{% hint style="info" %}
**To open a feature to more players, add your job to `Config.access.jobs`.** That is the intended way to "loosen" access. `showcase = true` is a blanket bypass for demos and screenshots — leave it `false` in production.
{% endhint %}

#### Instructor tier

A stricter tier gates the **briefing TV / layout toggle** and the **training instructor panel**. Access = **jobs + `minGrade`** (the primary control), OR the `ace`, OR global `showcase`.

```lua
-- config/custody.lua  and  config/training.lua
Config.Custody.InstructorAccess  = { minGrade = 0, ace = 'mrpd.briefing.instructor' }
Config.Training.InstructorAccess = { minGrade = 0, ace = 'mrpd.training.instructor' }
```

* **Jobs default to `Config.access.jobs`** — list your departments **once** in `config.lua` and the instructor tier reuses them.
* **`minGrade` defaults to `0`** (any officer instructs — works on every grade ladder). Raise it to restrict to supervisors, using whatever number matches *your* rank ladder.
* To restrict by job too, add `jobs = { 'police', 'lspd' }` (list) or `job = 'police'` (single).
* The `ace` is an optional bypass — handy for admins or standalone (no-framework) servers.

***

### Language

```lua
Config.language = 'auto'   -- follows  setr ox:locale "xx"
```

Auto-follows your server's `ox:locale`. Ships with **12 languages**: `en`, `ru`, `de`, `fr`, `es`, `pt`, `zh`, `ko`, `sv`, `no`, `fi`, `ar`. Every string lives in `localization/<lang>.lua` — edit or add your own.

***

### Bridges — how it talks to your stack

All auto-detected. Only change these if detection guesses wrong or you run something custom.

```lua
Config.framework = 'auto'   -- qbox | qbcore | esx | standalone | custom
Config.target    = 'auto'   -- ox_target | qb-target | custom
Config.notify    = 'auto'   -- ox_lib | qb | esx | custom
Config.textUI    = 'auto'   -- ox_lib | qb | custom
```

Set any to `'custom'` and fill the `Custom*` functions in the matching `bridge/*.lua` — that's where you wire a HUD, notify, or job system we don't detect out of the box.
