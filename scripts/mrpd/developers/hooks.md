---
description: Allow, deny, or react to any interaction
icon: filter
---

# Hooks

A single gate service lets you control **who can use what** and **react** to events — without touching protected logic. Edit the open files in `hooks/` (auto-created from the `.example.lua` templates on first start; **restart** to apply). `hooks_shared.lua` runs on **both** sides (client = hide the option, server = enforce) and is AND-ed with the side-specific files.

```lua
Hooks.gate(feature, id, event, ctx) -> boolean   -- return false ONLY to block; nil/true allows
Hooks.fire(feature, id, event, ctx)              -- fire-and-forget reactions
```

{% hint style="success" %}
Every handler runs in `pcall` and **fails open** — a broken or missing hook never blocks and never crashes.
{% endhint %}

Each feature already enforces a **built-in** access check (`Config.access` / instructor tier); your hook is AND-ed on top, so it can only **tighten**. To *loosen*, edit config instead.

***

### Gates by feature

| feature | id | event · ctx | built-in default |
| --- | --- | --- | --- |
| `anims` | `spotId` / `'convoy'` | `canUse` · `{ spotId, spot, ped, coords }` (client) / `{ source, spotId, … }` (server); `canPartner` · `{ lead, partner }` | convoy: cop job + cuffed target |
| `training` | `'instructor'` | `canUse` · `{ source }` — the instructor panel **and** all instructor commands | instructor ACE / job |
| `training` | `'team'` / `'stall'` / `'preset'` | `canUse` · `{ source, … }` — join team / claim stall / switch preset | police (`Config.access`) |
| `custody` | `'briefing'` | `canToggle` · `{ source }` — flip briefing / classroom layout | instructor tier |
| `banners` | `'toggle'` | `canToggle` · `{ source }` — raise / lower banners | police OR admin/instructor ACE |

***

### Example

Only **on-duty** officers may use the training instructor panel (`hooks/hooks_shared.lua`):

```lua
return {
    training = { entries = { ['instructor'] = {
        canUse = function(ctx)
            local st = IsDuplicityVersion() and Player(ctx.source).state or LocalPlayer.state
            return st.onDuty == true
        end,
    } } },
}
```

See `hooks/hooks_shared.example.lua` for the full reference with every feature, id, and ctx.

***

### Training events

React to training results in `hooks/hooks_server.lua` — e.g. XP for a skill tree or rewards for a match win. Each handler gets one `ctx` table; return values are ignored.

| id | event | ctx |
| --- | --- | --- |
| `'stall'` | `onStart` / `onEnd` | `{ source, stallIdx }` · `onEnd` adds `reason` = `'left'` \| `'dropped'` |
| `'stall'` | `onDrillEnd` | `{ source, stallIdx, preset, weapon, hits, shots, accuracy, time, completed, reason }` |
| `'killhouse'` | `onStart` / `onEnd` | `{ source }` · `onEnd` adds `reason` = `'left'` \| `'dropped'` |
| `'killhouse'` | `onLap` | `{ source, time, weapon }` — `weapon` is the preset name |
| `'match'` | `onStart` | `{ mode, red, blue }` — `red` / `blue` are team sizes |
| `'match'` | `onEnd` | `{ winner, red, blue, reason, redPlayers, bluePlayers }` |

* **`onDrillEnd`** (1.4.0+) fires once per range drill. `weapon` is the weapon **hash**, `preset` the leaderboard category (`pistols`, `rifles`, `shotguns`, `snipers`), `accuracy` is 0–1 and `time` is in seconds. `reason` is `'completed'`, `'timeout'` or `'left'` (walked out mid-run). Only completed runs reach the leaderboard; a run where no target was hit isn't reported.
* **match `onEnd`** — `reason` is `'ended'` (played out) or `'stopped'` (instructor force-stop). `red` / `blue` are the final score (rounds won; kills in TDM) and `winner` is `nil` on a draw — none of the three are sent on `'stopped'`. `redPlayers` / `bluePlayers` (1.4.0+) list the server ids on each team at the end: bots excluded, players who left mid-match not listed.

{% hint style="warning" %}
Range and killhouse results are measured on the player's client. The server checks them — the player must be in a stall / the killhouse, hits must match the target count, the weapon must belong to the preset, and a run can't claim more time than the player really spent there — but still **cap valuable rewards** (e.g. per hour).
{% endhint %}

```lua
-- hooks/hooks_server.lua
return {
    training = { entries = {
        ['stall'] = {
            onDrillEnd = function(ctx)
                if ctx.completed and ctx.accuracy >= 0.8 then
                    -- exports.my_skills:AddXP(ctx.source, 'marksmanship', 10)
                end
            end,
        },
        ['match'] = {
            onEnd = function(ctx)
                if ctx.reason ~= 'ended' or not ctx.winner then return end
                for _, src in ipairs(ctx.winner == 'red' and ctx.redPlayers or ctx.bluePlayers) do
                    -- exports.my_skills:AddXP(src, 'tactics', 25)
                end
            end,
        },
    } },
}
```

To read a player's **saved** range stats (what the personal leaderboard shows), use the [`GetRangeStats`](exports-and-commands.md) export.
