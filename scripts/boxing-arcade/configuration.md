---
description: config reference — payment & free play, minigame tuning, languages, gym stats, blips and bridges
icon: sliders
---

# Configuration

The master switches live in **`config.lua`**; each area has its own small file in
**`config/`**. Everything an owner should touch is an **open file** — `config.lua`,
`config/*.lua`, all of `bridge/`, `hooks/` and `localization/` ship unencrypted.

***

### Master settings — `config.lua`

{% code title="config.lua" %}
```lua
Config = {
    Modules = {
        creator     = true,   -- /boxarcade in-game placement tool
        leaderboard = true,   -- global high-score board on the cabinet screen
    },

    language = 'en',      -- 'auto' follows the ox:locale convar; or a code (see Languages)

    -- Bridges ('auto' detects; set only to force)
    framework = 'auto',   -- 'auto' | 'qbox' | 'qbcore' | 'esx' | 'standalone'
    target    = 'auto',   -- 'auto' | 'ox_target' | 'qb-target' | 'none'
    notify    = 'auto',   -- 'auto' | 'ox_lib' | 'qb' | 'esx' | 'native' | 'custom'
    textUI    = 'auto',   -- 'auto' | 'qb' | 'native' | 'custom'

    devMode = false,      -- bypasses ONLY the creator ACE (dev servers)
    debug   = false,      -- /boxanim /boxplay /boxpunch /boxstop + console output
}
```
{% endcode %}

`'auto'` is right for almost everyone — force a value only when detection picks the wrong
system (e.g. two frameworks installed). The `custom` options route through your own code,
see [For Developers](developers.md#custom-bridges).

{% hint style="danger" %}
Keep **`devMode = false`** and **`debug = false`** on a live server. `devMode` gives *every
player* creator access; `debug` registers test commands.
{% endhint %}

***

### Payment — `config/payment.lua`

```lua
Config.Payment = {
    enabled = false,      -- charge per play
    price   = 20,         -- default price (per-machine prices override this)
    account = 'cash',     -- qb: cash | bank · esx: money | bank
    moneySystem = 'auto', -- 'auto' | 'bigdaddy' | 'custom'
}
```

* **Off by default** — every machine is free until you enable it.
* Per-machine prices set in the [creator panel](placement.md#the-creator-panel) win over the
  global `price`.
* `'auto'` charges via **BigDaddy-Money** when it's running, otherwise your **framework's**
  native money.
* On a **standalone** server (no framework, no BigDaddy) play is always free — players get a
  one-time "free play" notification instead of a charge.
* `'custom'` routes every charge through your own function — see
  [For Developers](developers.md#custom-money).

***

### Languages

Ships with **12 languages**: `en` `es` `fr` `de` `pt` `ru` `zh` `ko` `sv` `no` `fi` `ar` —
covering the prompts, notifications, the creator panel, the cabinet screen and the minigame.

```lua
language = 'auto',   -- follow the ox:locale convar (default en), or set a code
```

A missing key in a translation falls back to English, then to the raw key — never an error.
**Add your own language:** copy `localization/en.lua` to `localization/<code>.lua`, translate
the values (keys stay), save as UTF-8, set `language = '<code>'`.

{% hint style="info" %}
The machine's **voice lines** are recorded audio and stay in English — they're arcade
flavour, like the artwork on the cabinet.
{% endhint %}

***

### Machines — `config/machines.lua`

```lua
Config.Machines = {
    list = {
        -- { coords = vec3(-1042.32, -1411.85, 4.90), heading = 90.0, price = 25 },
    },

    -- Permanent map blips for every machine, visible to ALL players. Off by default.
    blip = { enabled = false, sprite = 740, colour = 5, scale = 0.8 },

    spawnDistance    = 60.0,   -- cabinet streams in within this range
    interactDistance = 2.0,    -- how close to get the prompt

    -- Ped position on the cabinet, tuned together with the animation set.
    playerOffset = vec3(0.0, -0.95, 1.0),
    playerRotZ   = 0.0,
}
```

Most owners never touch `list` — the [creator](placement.md) is easier and writes to
`data/machines.json` instead. If you do use it, remember `cfg_N` ids follow array position
([details](placement.md#the-three-kinds-of-machines)).

{% hint style="warning" %}
Leave **`playerOffset`** alone — it's matched to the animation set. Changing it moves the
ped's fist out of the pad.
{% endhint %}

***

### Gameplay — `config/gameplay.lua`

The minigame ladder — each level sweeps faster with a smaller arc:

```lua
minigame = {
    levels = {
        { speed = 234.0, arc = 42.0 },   -- level 1: sweep speed (deg/s), arc size (deg)
        { speed = 390.0, arc = 32.0 },   -- level 2
        { speed = 460.0, arc = 12.0 },   -- level 3: nearly impossible to hit perfectly
    },
    graceMs = 250,           -- inputs ignored right after opening (E carry-over)
    maxRevolutions = 3,      -- AFK: auto-miss after this many full sweeps

    -- Secret bonus round: >= threshold closeness on ALL three arcs opens a 4th circle
    bonus = { speed = 560.0, arc = 8.0, threshold = 0.98 },
},
```

How far you get picks the **punch tier**, how close you hit picks the **score** inside the band:

| Outcome | Tier | Score band |
| --- | --- | --- |
| Missed the first arc (`l1miss`) | light | 800 – 2 000 |
| Passed 1, missed on 2 (`l2miss`) | light | 2 000 – 4 000 |
| Reached 3, missed the arc (`l3miss`) | medium | 4 000 – 7 000 |
| Hit the level-3 arc (`l3hit`) | high | 7 000 – 10 000 |
| Hit the secret bonus circle (`l4hit`) | high | 10 000 – 12 000 |

All bands are editable in `Config.Gameplay.scoring`. The **server** maps outcome → score —
clients only report how far they got and how close they hit.

Other knobs in the same file:

| Setting | Default | What it does |
| --- | --- | --- |
| `punchCooldownMs` | `1500` | Server-enforced minimum between punches |
| `sessionTimeout` | `90` | Seconds without input before the machine frees itself |
| `scoreCountup` | `5–10 s` | How long the screen rolls the score up (weak → strong hit) |
| `scoreTick` | on | Arcade ticker clicks while the score rolls (vanilla sound, distance-gated) |
| `idleVoice` | `1.2 s / 16 s` | When the machine starts goading you, and how often |
| `idleRollChance` | `0.10` | Chance per idle cycle of the move-around idle |
| `cinematic` | on | Punch camera + screen dolly for the player at the machine — camera offsets, FOV and per-tier impact shake are all editable |

***

### Leaderboard — `config/leaderboard.lua`

```lua
Config.Leaderboard = {
    show    = 5,                        -- rows on the cabinet screen
    maxRows = 100,                      -- high-score rows kept on disk
    file    = 'data/leaderboard.json',
}
```

Global, all-time, one row per player (their best). Names come from the framework character
name when there is one. No database — it's a JSON file, and updates never touch it.

***

### Stats — award gym strength per punch

`config/stats.lua` pushes strength gains to your gym script on every scored punch:

```lua
Config.Stats = {
    enable   = false,
    provider = 'none',   -- 'none' | 'rtx_gym' | 'vms_gym' | 'OT_skills' | 'devhub_skillTree' | 'custom'

    rates = {
        light  = { strength = 0.05 },
        medium = { strength = 0.10 },
        high   = { strength = 0.20 },
        record = { strength = 0.50 },   -- bonus on a new global record
    },
}
```

The provider is a **manual pick** — several gym scripts can coexist on one server, so
nothing is auto-detected here. `'custom'` hands the deltas to your own function
([For Developers](developers.md#custom-stats)).

{% hint style="warning" %}
`rtx_gym` and `vms_gym` really do spell their stat **`strenght`** — that's the vendors'
spelling, pre-wired in `providerMap`. "Fixing" it makes every push silently no-op.
{% endhint %}

***

### Bridges — forcing & overriding

Every third-party touchpoint is one open file in `bridge/` with its own escape hatch:

| Bridge | Auto-detects | Override |
| --- | --- | --- |
| `bridge/framework.lua` | QBox → QBCore → ESX → standalone | `CustomGetName(src)` for leaderboard names |
| `bridge/money.lua` | BigDaddy-Money → framework native → free | `CustomCharge(...)` + `moneySystem = 'custom'` |
| `bridge/notify.lua` | ox_lib → qb → esx → native | `CustomNotify(msg, kind)` + `notify = 'custom'` |
| `bridge/target.lua` | ox_target → qb-target → built-in `[E]` | open file — extend directly |
| `bridge/textui.lua` | qb → native | `CustomShowUI` / `CustomHideUI` + `textUI = 'custom'` |
| `bridge/stats.lua` | — (manual pick) | `CustomStatAward(src, deltas)` + `provider = 'custom'` |

Code examples for each hatch: [For Developers](developers.md#custom-bridges).
