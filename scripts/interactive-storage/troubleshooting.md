---
description: Quick fixes for the common setup and gameplay issues, and the support dump
icon: wrench
---

# Troubleshooting

| Symptom | Cause & fix |
| --- | --- |
| **No "Open cabinet" option on a GTA cabinet** | Run `/stor` and check the target. With `ox_target` / `qb-target`, aim at the cabinet from within 2 m. Without a target, hold **ALT**, look at the cabinet from close by and press **E**. Only the 46 models in `Config.Storage.replace` open, and the option is hidden while someone else uses that cabinet. |
| **Console: a target "started AFTER detection settled"** | The target resource starts after this one. Move `ensure prompt_interactive_storage` below your target in `server.cfg`, then restart `prompt_interactive_storage`. |
| **"Someone is using this cabinet"** | One player per cabinet. A player who walks off loses the cabinet within a few seconds (more than `claimRadius` + 5 m away, checked every 5 s), and a player who disconnects loses it at once. |
| **"You don't have access to this."** | `Config.Storage.access` is `true` and the player does not match `Config.access`, or your `canOpen` hook returned `false`. On a framework server check the job, grade and duty; the ACE only counts on standalone servers. With `Config.debug = true` the server console prints why (`access: DENY ...`). |
| **The drawer opens but no inventory comes up** | Check the `Inventory` line of the boot report or `stor_debugdump`. `none` means no supported inventory runs, or `Config.inventory` names one that is not started. `qb-inventory` needs version 2.0 or newer. An error line `[STOR INVENTORY SV ERROR] ... refused stash ...` shows the inventory's own error. When no inventory shows within 3 seconds, **X** closes the drawer. |
| **The drawer does not shut when the inventory closes** (custom inventory) | Make `CustomStashIsOpen` on the client return whether your inventory is on screen, or report the close with `StashClosed(src, id)` (see [Custom inventory](configuration.md#custom-inventory)). |
| **A drawer is empty that had items** | A GTA cabinet's stash name contains its position: if a map update moved the cabinet, it has new stashes. A placed cabinet that was removed and placed again has a new id and new stashes; use `/storcreator move` to keep the contents. See [Drawer stash names](developers.md#drawer-stash-names). |
| **"You are not allowed to use the storage creator"** | Grant `add_ace group.admin stor.creator allow` and make sure your account is in `group.admin`. A `canPlace` hook that returns `false` gives the same message. |
| **Enter does nothing in the placer, "Too far away"** | The spot is more than 50 m from you (`maxDistance`). Walk closer. |
| **"No placed cabinet within 3 m"** | `move` and `remove` only work on cabinets placed with `/storcreator`, and you must stand within 3 m of one. |
| **Placed cabinets are gone after an update** | `data/placements.json` was replaced or deleted. Keep that file when you update. An unreadable file is kept as `data/placements.broken.json`. |
| **A GTA cabinet looks different from before** | This resource streams its own mesh for 46 GTA cabinet models. If another resource streams the same model, only one of the two wins. |
| **Players do not see the cabinets after the first install** | Have players who were online during the install reconnect. |
| **The camera is in the way** | Set `Config.Storage.camera.enable = false` to keep the normal game camera. |
| **Text is in the wrong language** | Set `Config.language`, or `auto` to follow `ox:locale`. Custom wording goes in `localization/<language>.lua`, saved as UTF-8. |
| **`/stortest` or the debug commands do nothing** | They need `Config.debug = true`. Keep it off on a live server. |

***

### Support dump

Run this in the server console and send the output to us on Discord, together with your F8 console after `/stor`:

```
stor_debugdump
```

It lists the version, which related resources are started (ox_lib, targets, inventories), the framework, target and inventory in use, the modules and debug flags, the cabinets in use right now and the number of placed cabinets. Players with the ACE `command.stor_debugdump` can run it in game too; the output still goes to the server console.
