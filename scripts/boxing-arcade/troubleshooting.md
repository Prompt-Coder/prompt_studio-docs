---
description: Quick fixes for the common setup issues + the support dump
icon: wrench
---

# Troubleshooting

| Symptom | Cause & fix |
| --- | --- |
| **No cabinets anywhere** | The resource ships with **33 default placements** — if none appear, the resource didn't start cleanly (check the console for the boot report) or `config/machines.lua`'s list was emptied. `machines: 0 config + 0 placed + 0 map` in the boot report = nothing is defined; place one with `/boxarcade` ([Placing Machines](placement.md)). |
| **Too many default cabinets / wrong spots** | The defaults are just config — remove lines from `config/machines.lua` (`list`), or clear it entirely and place your own with `/boxarcade`. |
| **A cabinet disappeared** | It's [bound](placement.md#bind-a-machine-to-a-map-resource) to a map resource that isn't running — check the panel for a dimmed `dormant` row. Maps started after boot are picked up on the next `restart prompt_boxing_machine`. |
| **No interact prompt** | If you run `ox_target`/`qb-target`, start it **before** `prompt_boxing_machine` in `server.cfg`. Without either, the built-in `[E]` prompt appears within 2 m of the cabinet (`Config.Machines.interactDistance`). |
| **`/boxarcade` says access denied** | You don't have the ACE — `add_ace group.admin prompt_boxing.creator allow` (then relog), or `Config.devMode = true` on a dev server. |
| **Players aren't being charged** | (1) `Config.Payment.enabled` is `false` — the default. (2) The server is standalone (no framework, no BigDaddy-Money) — play is free **by design**; the boot report shows `payment: FREE (standalone)`. |
| **Leaderboard shows account names, not RP names** | No framework detected — names fall back to the player name. Check the boot report's `framework:` line; force `Config.framework` if detection picked wrong. |
| **Wrong language / raw text keys** | Set `Config.language` to one of the 12 codes ([Languages](configuration.md#languages)). A custom locale file must be saved as **UTF-8**. |
| **No map blips** | Permanent blips are **off by default** — enable `Config.Machines.blip`. The creator's **Mark** blip is temporary by design (90 s, self-clearing). |
| **Gym stats aren't moving** | `Config.Stats.enable = false` by default; the provider is a **manual pick**, never auto-detected. And don't "fix" the `strenght` spelling — that's really the vendors' stat key. |
| **Debug commands missing** | `/boxplay` `/boxpunch` `/boxstop` `/boxanim` only exist with `Config.debug = true` (off in production, by design). |

***

### The support dump

Before asking for help, run:

```
/boxarcade dump
```

It prints a full diagnostics block to the **server console** — detected framework/target,
payment mode, resource states, version, and every machine with its price and occupancy.
Paste that block with your report.

***

### Reset the leaderboard

Stop the resource, delete `data/leaderboard.json`, start it again. The board rebuilds empty.
The same goes for placements — `data/machines.json` holds every placed machine, and copying
that file to another server carries your placements with it.

***

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
