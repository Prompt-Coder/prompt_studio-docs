---
description: Reward hooks, leaderboard exports & the server-side anti-cheat model
icon: code
---

# For Developers

The arcade doesn't decide what a win is worth — **you do**. Every finished game fires a
server-side hook you listen to in your own resource, and every reward is **validated server-side
before it fires**, so you can safely attach money/items.

***

### Reward hooks

Two ways to receive a result — an **event** (multiple listeners) or an **export** (register a
callback). Both carry the same data.

{% tabs %}
{% tab title="Events" %}
```lua
-- score games (space, wizard, badlands, racers, fortune)
AddEventHandler('prompt_arcade_games:onGameResult', function(src, game, score, extra)
    -- e.g. pay out based on score
end)

-- claw machine — a figurine was won
AddEventHandler('prompt_arcade_games:onClawWin', function(src, prizeModel)
    -- exports.ox_inventory:AddItem(src, 'plushie', 1)
end)

-- love tester — a rating was rolled (both players)
AddEventHandler('prompt_arcade_games:onLoveResult', function(src, rating)
    -- rating is a label, e.g. "SIZZLIN'"
end)
```
{% endtab %}
{% tab title="Exports" %}
```lua
exports['prompt_arcade_games']:OnGameResult(function(src, game, score, extra)
    -- ...
end)

exports['prompt_arcade_games']:OnClawWin(function(src, prizeModel)
    -- ...
end)
```
{% endtab %}
{% endtabs %}

**Which hook each game uses:**

| Game(s) | Hook | Payload |
| --- | --- | --- |
| `space`, `wizard`, `badlands`, `rockets`, `truckin`, `street`, `fortune` | `onGameResult` | `(src, game, score, extra)` |
| `claw` | `onClawWin` | `(src, prizeModel)` |
| `love` | `onLoveResult` | `(src, rating)` |

{% hint style="success" %}
`score` is a bounded integer and `src` is the real server id — safe to pay directly. See
[Anti-cheat](#anti-cheat) for why.
{% endhint %}

***

### Leaderboards

Scores persist to FiveM **KVP** (no database needed) and show on each cabinet's attract screen.
Read them from your own resource:

| Export | Returns |
| --- | --- |
| `GetLeaderboard(game)` | top-N array of `{ id = license, name, score, ts }` |
| `GetTopScore(game)` | the best entry, or `nil` |
| `GetPlayerBest(game, license)` | that player's entry, or `nil` |
| `GetAllLeaderboards()` | `{ [game] = array, … }` |
| `ResetLeaderboard(game)` | wipes one board |

```lua
local top = exports['prompt_arcade_games']:GetTopScore('space')
if top then print(('Space high score: %s — %d'):format(top.name, top.score)) end
```

Tracked games: `space`, `wizard`, `badlands`, `rockets`, `truckin`, `street` (high score) and
`claw` (most figurines won). `love` and `fortune` are outcome-based and aren't ranked.

***

### Anti-cheat

Every result is checked **on the server** before it reaches a leaderboard or a reward hook —
controlled by `Arc.Config.security`:

* **Session required** — the server only accepts a result if it saw the player *start* that game at
  a real cabinet within `maxStartDist` metres. A client firing the result event from nowhere is dropped.
* **Not too fast** — runs shorter than `minPlayMs` are rejected.
* **Score envelope** — non-numeric, negative, or above the game's `score.max` are rejected.
* **Per-player cooldown** — `resultCooldown` between accepted results.

The Love Tester is fully server-authoritative (the server rolls the shared rating). You can relax
these checks by lowering `security` values, or disable entirely with `security.validate = false`
(not recommended on a live server).

{% hint style="info" %}
Because validation happens server-side, you never need to re-verify in your reward handler — if a
hook fires, the run was legitimate.
{% endhint %}
