---
description: config.lua reference — games, controls, leaderboards, anti-cheat & placement
icon: sliders
---

# Configuration

Everything is driven by **`config.lua`** — one file, left open under escrow so you can edit it. It
has a global settings block (`Arc.Config`) and one entry per cabinet (`Arc.Cabinets`).

***

### Global settings — `Arc.Config`

{% code title="config.lua" %}
```lua
Arc.Config = {
  framework    = 'auto',   -- 'auto' | 'qb' | 'esx' | 'standalone'
  targetSystem = 'auto',   -- 'auto' | 'ox_target' | 'qb-target'

  defaults = {
    targetDistance = 1.8,  -- how close to interact with a cabinet
    findRange      = 12.0, -- how far to look for the placed cabinet
    cooldown       = 1500, -- ms before the same cabinet re-triggers
    duiTimeout     = 10000,
  },

  debug = false,           -- MUST be false in production (enables test commands + verbose logs)

  leaderboard = {
    enabled  = true,
    keep     = 25,         -- entries retained per game
    resetKvp = false,      -- set true + restart ONCE to wipe every board, then set back to false
  },

  security = {             -- server-side anti-cheat (see For Developers)
    validate       = true,
    requireSession = true, -- a result only counts if the player actually started at a cabinet
    maxStartDist   = 6.0,  -- metres
    minPlayMs      = 2000,
    resultCooldown = 2500,
    maxScore       = 10000000,
  },
}
```
{% endcode %}

{% hint style="danger" %}
Leave **`debug = false`** for a live server. `true` registers fullscreen test commands and prints
verbose logs.
{% endhint %}

***

### Languages

_Since v0.5.0._ Ships with **English, German, Spanish, French, Portuguese and Russian**. Pick one
in `config.lua`:

{% code title="config.lua" %}
```lua
language = 'en',   -- 'en' | 'de' | 'es' | 'fr' | 'pt' | 'ru'
```
{% endcode %}

**Add your own language:** copy `locales/en.lua` to `locales/<code>.lua`, translate the **values**
only (never the keys), and set `language = '<code>'`. Save the file as **UTF-8** so accented
characters render correctly.

{% hint style="info" %}
Anything a translation is missing falls back to English automatically, so a partial translation
never shows a blank line or a raw key name.
{% endhint %}

To change just one or two strings without editing a locale file, override them inline — this wins
over the selected language:

{% code title="config.lua" %}
```lua
Locale = {
  menu_play   = '[E] START',
  target_claw = 'Try the claw machine',
},
```
{% endcode %}

{% hint style="warning" %}
Cabinet **titles** and **interaction labels** come from the locale only when `language` is *not*
`'en'`. On English the values written in `Arc.Cabinets` are used as-is, so a server that renamed a
cabinet by hand keeps its wording after updating.
{% endhint %}

<details>

<summary>What is translated (and what isn't)</summary>

**Translated:** cabinet names, interaction labels, the Text UI prompt, the pre-game menu
(play / volume / leave / co-op hint), Love Tester messages and its 10 ratings, Nazar's
notifications, Strength Tester result and its 4 tiers.

**Not translated:** the artwork *inside* the arcade games themselves (`SCORE`, `WAVE`,
`INSERT COIN`, `GAME OVER` …) — that's drawn on the cabinet screens and is intentionally left in
arcade English. Nazar's fortune texts are edited directly in `config.lua` (see above).

</details>

***

### Text UI (no ox\_lib, no target script)

_Since v0.5.0._ The script no longer requires **ox\_lib** at all, and works with **no targeting
resource**: if neither `ox_target` nor `qb-target` is running, a built-in `[E]` prompt appears when
you walk up to a cabinet.

{% code title="config.lua" %}
```lua
textUI = {
  enabled = 'auto',   -- 'auto' (only without a target script) | true (always) | false (never)
  key     = 38,       -- interaction control (38 = [E])
  style   = 'help',   -- 'help' = native GTA help box | 'text' = centred bottom text
  range   = 2.0,      -- metres
  custom  = nil,      -- route it to YOUR TextUI instead (see below)
},
```
{% endcode %}

Already have a TextUI you like? Point it there — called with `(true, label)` to show and
`(false)` to hide:

```lua
custom = function(show, label)
    if show then exports.ox_lib:showTextUI(label) else exports.ox_lib:hideTextUI() end
end,
```

{% hint style="info" %}
With `ox_target` or `qb-target` installed nothing changes — the cabinets keep using it, and the
Text UI costs nothing.
{% endhint %}

***

### Custom notifications (match your HUD)

_Since v0.4.1._ By default the script uses the native GTA feed ticker. Every player-facing message
routes through **one hook** in `config.lua` — set `notification.custom` to a function that shows
the message with **your** HUD/notify system:

{% code title="config.lua" %}
```lua
notification = {
  -- pick ONE (or write your own) — colour codes are stripped before your function is called:

  -- ox_lib:
  custom = function(msg) exports.ox_lib:notify({ description = msg, type = 'inform' }) end,

  -- QBCore:
  -- custom = function(msg) exports['qb-core']:GetCoreObject().Functions.Notify(msg, 'primary') end,

  -- ESX:
  -- custom = function(msg) exports.esx:ShowNotification(msg) end,

  -- your custom HUD (use your resource's notify export):
  -- custom = function(msg) exports['my_hud']:AddNotification(msg) end,
},
```
{% endcode %}

{% hint style="info" %}
Leave `custom = nil` to keep the native ticker. If your function errors, the script logs it and
falls back to the native ticker — notifications never silently vanish.
{% endhint %}

***

### Per-cabinet entries — `Arc.Cabinets`

Each game is one entry. The fields you'll actually touch:

| Field | What it does |
| --- | --- |
| `title` | Display name (menus, leaderboard header) |
| `enabled` | `true`/`false` — turn a whole cabinet on or off |
| `players` | `1` or `2` |
| `controls` | Logical key → FiveM control IDs (rebind here) |
| `target` | `{ label = 'Play …', icon = 'fa-solid fa-…' }` — the interact prompt |
| `score` | `{ track = true, kind = 'high' \| 'wins', max = … }` — leaderboard behaviour |

You normally **don't** edit `models`, `glass`, `dui`, `ped`, `cam`, `sync` or `occupancy` — those
bind the game to its cabinet, screen and animations.

<details>
<summary>Example — the Space Monkey entry</summary>

```lua
space = {
  title='Space Monkey', kind='screen', players=1, enabled=true, fw=true,
  models = { `ch_prop_arcade_space_01a` },
  controls = { left={174,34}, right={175,35}, fire={38,22}, bomb={21} },
  target = { label='Play Space Monkey', icon='fa-solid fa-meteor' },
  score  = { track=true, kind='high', max=1000000 },
}
```
</details>

***

### Common edits

{% tabs %}
{% tab title="Enable / disable a game" %}
```lua
-- turn a cabinet off (no interact prompt, not loaded):
strength = { ..., enabled = false }
```
{% endtab %}
{% tab title="Rebind a control" %}
```lua
-- controls map a logical action to one or more FiveM control IDs.
-- e.g. make Space Monkey fire on [E] (38) or Left Mouse (24):
controls = { left={174,34}, right={175,35}, fire={38,24}, bomb={21} },
```
{% endtab %}
{% tab title="Change the interact label" %}
```lua
target = { label='Play the Space Shooter', icon='fa-solid fa-rocket' },
```
{% endtab %}
{% tab title="Turn a leaderboard off" %}
```lua
-- drop the score block (or set track=false) — the game still plays, just isn't ranked:
score = { track=false },
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Volume** isn't a config value — players set it in each cabinet's pre-game menu with **Up/Down**,
starting at **50%** and remembered for the session.
{% endhint %}

***

### Props & Placement

The games bind to the **stock arcade cabinet props** — place these in your arcade MLO/map and the
script does the rest:

| Game | Cabinet model to place |
| --- | --- |
| Space Monkey | `ch_prop_arcade_space_01a` |
| The Wizard's Ruin | `ch_prop_arcade_wizard_01a` |
| Badlands Revenge | `ch_prop_arcade_gun_01a` |
| Crotch Rockets / Get Truckin' / Street Legal | `ch_prop_arcade_race_02a` / `race_01b` / `race_01a` |
| Love Tester | `ch_prop_arcade_love_01a` |
| Claw Machine | `ch_prop_arcade_claw_01a` |
| Nazar the Fortune Teller | `ch_prop_arcade_fortune_01a` |

The custom clean-screen props the screen games draw onto ship **inside this resource** (`stream/`)
and load automatically — you don't install anything extra. On play, the script hides the stock
cabinet and swaps in the matching custom prop to render the game on its glass.

{% hint style="warning" %}
The **Love Tester** must be a **map-placed** cabinet. Its screen is an engine render target that
only binds to a streamed map prop — a script-spawned one shows a black screen.
{% endhint %}

{% hint style="info" %}
`config.lua` is the only file left editable under escrow; all game logic, HTML and props stay
encrypted.
{% endhint %}

***

### Nazar's fortunes (edit / translate)

_Since v0.4.3_ the Fortune Teller's messages live in **`config.lua`**, inside the `fortune`
cabinet entry — edit, translate, or add as many as you like:

{% code title="config.lua — Arc.Cabinets.fortune" %}
```lua
fortunes = {
  { text = "Fortune leans your way — keep an empty pocket ready to fill.", mood = 'amused', rarity = 86, rare = false },
  { text = "A golden hand reaches from the glass. Seize this day!",        mood = 'surprised', rarity = 96, rare = true },
  -- add your own...
},
```
{% endcode %}

| Field | Meaning |
| --- | --- |
| `text` | What Nazar says (shown to the player) |
| `mood` | His reaction animation — one of `amused`, `pondering`, `surprised`, `confused`, `disgusted`, `insulted`, `angry` (a typo safely falls back to `pondering`) |
| `rarity` | 0–100 flavour value |
| `rare` | `true` = golden omen — drawn very rarely, with a longer build-up flourish |
