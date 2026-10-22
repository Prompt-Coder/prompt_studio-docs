---
description: The public API surface — small, stable, and safe
icon: right-left
---

# Exports & Commands

MRPD exposes a **small, stable** surface on purpose. Call exports as `exports.prompt_mrpd_scripts:Name(...)`.

***

### Client exports

| Export | Returns | Use |
| --- | --- | --- |
| `IsPlayerAnimated()` | `animating, spotId, phase` | is the local player in an MRPD prop anim, and which one |
| `StopPlayerAnim(instant)` | `stopped` (bool) | cancel it — graceful, or `true` for instant (death / being dragged) |
| `IsCarrying()` | bool | is the local player carrying a prop (coffee cup) |
| `StopCarry()` | — | drop the carried prop |
| `IsConvoying()` | bool | is the local player in a prisoner escort |
| `StartConvoy` / `StopConvoy` | — | drive the escort |
| `IsInteriorLoaded(key)` | bool | is the MLO streamed in |

### Server exports

| Export | Returns | Use |
| --- | --- | --- |
| `IsOfficer(src)` | bool | does MRPD count this player as police — same jobs/grade/duty/ACE rule as every gated feature |
| `StartConvoy(cop, zek, handoff)` / `StopConvoy(src)` | — | escort control |
| `GetRangeStats(src)` | table / `nil` | a player's saved shooting-range stats — what the personal leaderboard shows (1.4.0+) |

***

### Typical usage

```lua
-- death / arrest cleanup — no more frozen peds or floating coffee cups
if exports.prompt_mrpd_scripts:IsPlayerAnimated() then
    exports.prompt_mrpd_scripts:StopPlayerAnim(true)   -- instant
end
exports.prompt_mrpd_scripts:StopCarry()

-- dispatch / evidence / MDT gating off MRPD's own officer definition (server)
if exports.prompt_mrpd_scripts:IsOfficer(src) then
    -- ...
end

-- skill trees / progression: saved range stats (server)
local stats = exports.prompt_mrpd_scripts:GetRangeStats(src)
if stats and stats.games >= 10 and (stats.accuracy or 0) >= 0.75 then
    -- ...
end
```

`GetRangeStats(src)` returns `nil` when the player isn't online, otherwise:

```lua
{
    name        = 'John Doe',
    games       = 12,          -- completed range runs
    accuracy    = 0.83,        -- 0–1 over all runs, nil before the first one
    totalHits   = 240,
    totalMisses = 49,
    bestTimes   = { pistols = 18.4, rifles = 15.9 },  -- seconds, per preset
    ranks       = { pistols = 3 },                     -- top-10 board position, per preset
}
```

Stats are saved per **license**, so every character on one account shares them. For live results as they happen, use the `onDrillEnd` [hook](hooks.md#training-events).

***

### Commands

| Command | Access | Purpose |
| --- | --- | --- |
| `/mrpd` | anyone | quick info about the resource |
| `/mrpd_debugdump` | ACE `command.mrpd_debugdump` (console always) | full support snapshot — see [Troubleshooting](../troubleshooting.md) |

***

### Extending — use hooks & providers, not internal events

{% hint style="warning" %}
The resource's internal net events and `lib.callback` handlers are **not** a public contract. They're access-gated and change between versions — calling them directly will break and can bypass security. To integrate, use the **exports** above, plus [Hooks](hooks.md) (who may) and [Providers](providers.md) (how). That's the stable, supported surface.
{% endhint %}
