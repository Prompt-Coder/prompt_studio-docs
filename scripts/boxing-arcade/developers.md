---
description: Hooks (gate & react), server exports, and the custom money / stats / minigame / notify hatches
icon: code
---

# For Developers

Two integration surfaces: **hooks** — react to plays and gate who can play, from files that
updates never touch — and **exports** for reading or driving the machine registry from your
own resources. Everything a hook receives has already been **validated server-side**
(session, cooldown, server-computed score), so it's safe to pay out from.

***

### Hooks

Owner hook files live in `hooks/`, auto-created from the `.example.lua` templates on first
boot — updates never overwrite them. Edit, then restart the resource.

| File | Side | Use for |
| --- | --- | --- |
| `hooks/hooks_shared.lua` | both | Write a check once — evaluated on the **client** (hides the prompt) *and* re-run on the **server** (authority) |
| `hooks/hooks_client.lua` | client | UI-side gates / reactions |
| `hooks/hooks_server.lua` | server | Authoritative gates / reactions — pay rewards here |

```lua
-- gates:     return false to BLOCK (nil/true allows)
-- reactions: fire-and-forget
```

{% hint style="success" %}
Every handler runs in `pcall` and **fails open** — a broken or missing hook never blocks
play and never crashes the resource.
{% endhint %}

#### Events

| feature.event | Kind | Fires | ctx |
| --- | --- | --- | --- |
| `machine.canPlay` | gate | before a session starts — both the first press *and* every paid re-press | server: `source, machineId, coords, price` · client adds `ped`, no `source` |
| `machine.onStart` | react | a session begins | `source, machineId` |
| `machine.onScore` | react | a punch lands | `source, machineId, score, tier, outcome, record` |
| `machine.onRecord` | react | the score beats the **global** all-time high | `source, machineId, score, previous` |
| `machine.onEnd` | react | the session ends | `source, machineId, reason` — `left` \| `timeout` \| `dropped` \| `removed` \| `moved` |
| `creator.canPlace` | gate | after the ACE/devMode check, before a placement is saved | `source, coords, price` |

Handlers go under `global` (every machine) or `entries['<id>']` (one machine — ids are
`cfg_1`, a 6-character placed id, or `map_<resource>_<n>`, see
[machine kinds](placement.md#the-three-kinds-of-machines)). For a gate to pass, **both**
`hooks_shared.lua` and the side-specific file must return non-`false`.

#### Examples

{% tabs %}
{% tab title="Block jailed players" %}
```lua
-- hooks/hooks_server.lua
return {
    machine = {
        global = {
            canPlay = function(ctx)
                return not exports.myjail:IsJailed(ctx.source)
            end,
        },
        entries = {},
    },
}
```
{% endtab %}
{% tab title="Reward a new record" %}
```lua
-- hooks/hooks_server.lua
return {
    machine = {
        global = {
            onRecord = function(ctx)
                -- ctx.previous = the old global high
                exports.ox_inventory:AddItem(ctx.source, 'boxing_trophy', 1)
            end,
        },
        entries = {},
    },
}
```
{% endtab %}
{% tab title="Fence off placements" %}
```lua
-- hooks/hooks_server.lua
return {
    creator = {
        global = {
            canPlace = function(ctx)
                return ctx.coords.x < 1000.0   -- no cabinets east of x=1000
            end,
        },
        entries = {},
    },
}
```
{% endtab %}
{% endtabs %}

***

### Exports (server)

```lua
exports.prompt_boxing_machine:GetLeaderboard()                    --> { { name, score, at }, ... }
exports.prompt_boxing_machine:GetMachines()                       --> { { id, coords, heading, price?, occupiedBy? }, ... }
exports.prompt_boxing_machine:IsMachineOccupied(id)               --> serverId | false
exports.prompt_boxing_machine:AddMachine(coords, heading, opts)   --> id | nil, err    -- opts = { price?, persist = true }
exports.prompt_boxing_machine:RemoveMachine(id)                   --> true | false, err
```

`AddMachine` with `opts.persist = false` places a **RAM-only** machine — gone on restart,
never written to `data/machines.json`. Handy for event scripts that stand a cabinet up for
one evening.

There is no separate broadcast-event surface — **hooks are the event surface**; use
`onScore` / `onRecord` / `onEnd` to react to plays.

***

### Custom bridges

<a href="#custom-money" id="custom-money"></a>

#### Money

Route every charge through your own economy — define the function in `bridge/money.lua`
(open file) and set `Config.Payment.moneySystem = 'custom'`:

```lua
function CustomCharge(src, amount, account, reason)
    return exports.my_economy:Remove(src, account, amount)   -- true = paid, false = declined
end
```

<a href="#custom-stats" id="custom-stats"></a>

#### Stats

`Config.Stats.provider = 'custom'` + a function in `bridge/stats.lua`:

```lua
function CustomStatAward(src, deltas)
    -- deltas = { strength = 0.10 } (per Config.Stats.rates)
end
```

#### Notifications & TextUI

Match your HUD — `Config.notify = 'custom'` / `Config.textUI = 'custom'`:

```lua
-- bridge/notify.lua
function CustomNotify(msg, kind)      -- kind: 'success' | 'error' | 'inform'
    exports.my_hud:Notify(msg, kind)
end

-- bridge/textui.lua
function CustomShowUI(text) exports.my_hud:ShowUI(text) end
function CustomHideUI()     exports.my_hud:HideUI()     end
```

#### Leaderboard names

```lua
-- bridge/framework.lua
function CustomGetName(src)
    return exports.my_identity:GetRPName(src)
end
```

***

### Replace the minigame

Swap the circle game for your own skill check — define `CustomMinigame` in
`config/gameplay.lua`. It runs on the client when the player punches:

```lua
function CustomMinigame(machineId)
    -- run your own minigame here, then report how it went:
    return 'l3hit', 0.9   -- outcome key from Config.Gameplay.scoring, closeness 0.0–1.0
    -- return nil to cancel the punch
end
```

The server still owns the outcome → tier/score mapping, the punch cooldown and session
validation — a modified client can't invent a score band it didn't reach.
