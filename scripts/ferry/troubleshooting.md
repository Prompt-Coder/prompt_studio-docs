---
description: Quick fixes for the common setup and sailing issues, and the support dump
icon: wrench
---

# Troubleshooting

| Symptom | Cause & fix |
| --- | --- |
| **No "Take the helm" prompt, or "You need the keys to steer this ferry."** | The helm rule is `keys` by default: the player needs keys to that ferry (with a keys script), or must be the player who spawned it (without one), or staff. Check the `Keys` and `Access` lines of the boot report or `ferry_debugdump`. To let anyone steer, set `Config.Helm.access = 'everyone'`. A `canOperate` hook that returns `false` hides the prompt too. |
| **A ferry from a garage cannot be steered by its owner** | The keys script has to give the owner keys to the ferry's plate, as for any garage vehicle. Check that the plate the garage uses is the one the keys script knows. |
| **"Someone is already at the helm."** | One player at the helm. They leave it with **F**. |
| **`/ferry` does nothing** | The player needs the ACE `command.ferry` (`add_ace group.admin command.ferry allow`). The server console always may. |
| **"No deep water here: spawn the ferry on open water."** | The spot needs at least `Config.Spawn.minDepth` (4 m) of water under it. Swim out farther, or give coordinates: `/ferry <x> <y> <z> [heading]`. |
| **Every player can spawn ferries and take any helm** | `Config.access.showcase = true`. The console warns `SHOWCASE MODE` at every start. Set it to `false` in `config.lua`. |
| **The ferry will not go faster than 2 m/s** | A ramp is open. Raise both ramps for full speed (`Ramps closed: full speed.`). |
| **"Slow down below 2 m/s (7 km/h) to lower the bow ramp."** | Ramps only lower when the ferry is almost still. |
| **The ramp stops before it is down** | It touched the ground: the quay, a slipway, an object or a vehicle (`On the ground`). Bring the ferry to a lower quay or closer to it. |
| **The ramp will not rise** | A vehicle is on it (`A vehicle is on the bow ramp: it stays down.`). Drive it off or onto the deck. |
| **"Slow the ferry almost to a stop before docking."** | Docking needs the ferry at 1 m/s or less (`Config.Helm.parkMaxSpeed`). |
| **A car slid or fell off during the crossing** | Only empty cars on the car deck are held, after standing still for 2 seconds. A car with someone in it, a car on a ramp, or a vehicle type set to `false` in `Config.Carry.types` rides loose. |
| **A car jumps or flies when someone gets in on a moving ferry** | Update to 1.1.0 or newer: getting into a held car was fixed there. |
| **The ferry's lights go dark when you look away and back** | Update to 1.1.0 or newer, and keep `Config.Interior.lights.intervalMs` at `100`. |
| **No interior, or the ferry looks plain from far away** | The interior and the detailed model show within `Config.Interior.distance` (150 m) of the ferry. |
| **Players fall over on deck** | Check that `Config.Modules.aboard = true`. |
| **A ferry from a spawn menu vanishes at once** | `Config.Spawn.adoptClientSpawns = false`, or your server's OneSync entity lockdown removes vehicles created by players. Spawn the ferry on the server: `/ferry`, the `SpawnFerry` export or a server-side garage. |
| **All ferries are gone after a restart** | By design: restarting `prompt_ferry` removes every ferry, because a ferry left in the world without its resource crashes the players near it. Spawn them again after the restart. |
| **A ramp key shows a blank box in the help text** | GTA has no icon for that key. Use letters, digits, `[` `]` `.`, the arrows, Home or End (see [Keys](configuration.md#keys)). |
| **Players keep their old key after you changed a default** | A key default only applies to players who never had the binding. Players change it in **Settings > Key Bindings > FiveM**. |
| **Text is in the wrong language** | Set `Config.language`, or `auto` to follow `ox:locale`. Custom wording goes in `localization/<language>.lua`, saved as UTF-8. |
| **`/ferry_test` does nothing** | It needs `Config.debug = true`. Keep it off on a live server. |

***

### Support dump

Run this in the server console and send the output to us on Discord, together with your F8 console after `/ferry_info`:

```
ferry_debugdump
```

It lists the version, which related resources are started (ox_lib, targets, fuel and keys scripts), the framework, target, notify, fuel and keys in use, who counts as staff, the modules and debug flags, and every ferry in the world: its id, plate, routing bucket, owner, position, docked state, seated players and ramps, plus the number of held cars. Players with the ACE `command.ferry_debugdump` can run it in game too; the output still goes to the server console.
