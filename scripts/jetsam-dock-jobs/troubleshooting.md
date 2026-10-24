---
description: Quick fixes for the common setup and gameplay issues
icon: wrench
---

# Troubleshooting

| Symptom | Cause & fix |
| --- | --- |
| **Falling through the floor at the warehouse** | The JetSam map isn't running. Start `prompt_jetsam` and `prompt_jetsam_warehouse` **before** `prompt_jetsam_script`. |
| **No interaction at the dispatcher** | Run `/dock` and check the detected target. With `bridges.target: "auto"` it uses `ox_target` or `qb-target` if started, otherwise press-E prompts. If you forced a target that isn't installed, set it back to `auto`. |
| **Jobs work but nobody gets paid** | No framework was found, so the server runs standalone and pays nothing. Start QBX, QBCore or ESX, or use a [custom money bridge](developers.md#custom-bridge). Also check that `rewards.enabled` is `true` and `bridges.money` isn't `free`. |
| **"The payment system is unavailable"** | `framework.mode` names a framework that isn't running. Start it, or set `framework.mode` back to `auto`. |
| **Cranes, ramp or props missing after install** | Players who were online during the first install need to reconnect. Restart the resource only when nobody is near the port. |
| **Can't leave the crane cabin** | Move the trolley back to its start position (the bridge) and raise the spreader fully, then exit. |
| **"All gantry cranes are currently occupied"** | Every crane has an operator. Wait for a shift to end, or enable more cranes in `config.advanced.json` (`multiCrane`). |
| **Crane drop zone is full** | The drop slots need clearing by a container handler. Start a handler shift, or wait for one. |
| **Truck can't be loaded** | Bring the pallet to the marked position behind the truck and, for the Mule, set the forks to the height of the cargo floor before pressing **E**. |
| **"This truck was not approved"** | Your own truck was rejected. Sit in the driver seat, stay close to the trailer, unhitch and hitch again. If `truck.ownCab` is `off`, only the job cab is allowed. |
| **"All return bays are occupied"** | Wait in the yard; a bay is assigned as soon as one frees up. |
| **Text is in the wrong language** | Set `locale` in `config.json`, or `auto` to follow `ox:locale`. Custom wording goes in `locales/<language>.json`, saved as UTF-8. |
| **`/dockdev` does nothing** | Developer commands need `debug: true` **and** the `prompt_jetsam_script.admin` ACE. Keep `debug` off on a live server. |

***

### Support dump

Run this in the server console and send the output to us on Discord, together with your F8 console:

```
dock_debugdump
```

It lists the version, framework and target detection, language, bridges, modules, access settings, shift modes, cranes and which related resources are running.
