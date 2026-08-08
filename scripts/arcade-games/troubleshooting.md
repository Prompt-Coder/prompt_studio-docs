---
description: Quick fixes for the common setup issues
icon: wrench
---

# Troubleshooting

| Symptom | Cause & fix |
| --- | --- |
| **No "Play" prompt on a cabinet** | No targeting resource running. Start `ox_target` **or** `qb-target` (and `ox_lib`) **before** `prompt_arcade_games` in `server.cfg`. Console shows `target=nil` when neither is found. |
| **Interact works, but the screen is black** | The cabinet isn't a **map-placed** prop. Place the stock cabinet model in your MLO. The **Love Tester** especially requires a map-placed cabinet (render-target screen). |
| **Custom prop doesn't appear / stock cabinet stays** | The resource's `stream/` props didn't register. `refresh` then `ensure prompt_arcade_games`, and make sure the resource started without errors. |
| **Rewards don't pay out** | (1) You haven't added a reward handler — see [For Developers](developers.md). (2) No framework detected — console should print `[arc:framework] detected: qb`/`esx`. (3) The result was rejected by anti-cheat (e.g. finished under `minPlayMs`). |
| **Leaderboard is empty** | Only server-verified runs are recorded. If `Arc.Config.security.validate` is on, results fired without actually starting at a cabinet are dropped. Also check `leaderboard.enabled = true` and that the game has a `score.track` block. |
| **Two players can't pair** | Both must target the **same** cabinet. One player can start solo with `[E]`. |
| **Test commands / `/…dbg` missing** | They only exist with `Arc.Config.debug = true` (off in production, by design). |

***

### Reset a leaderboard

```lua
-- from your server console or a script:
exports['prompt_arcade_games']:ResetLeaderboard('space')
```

Or wipe **all** boards: set `Arc.Config.leaderboard.resetKvp = true`, restart once, then set it back
to `false`.

***

{% hint style="info" %}
Still stuck? Confirm the first-boot lines from the [install checklist](README.md#first-boot-checklist)
appear in your server console — they pinpoint whether targeting and the framework were detected.
{% endhint %}
