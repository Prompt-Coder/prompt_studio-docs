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
