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
