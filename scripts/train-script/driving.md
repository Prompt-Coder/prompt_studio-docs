---
description: >-
  Players can drive the trains themselves: take over a line's train or take out
  a service train at a depot, keep to the limits and signals, and get paid for
  every stop they serve.
icon: gauge-high
---

# Driving

{% hint style="info" %}
New in **2.1.0**. All settings are in section 12 of `config/config.lua` (`driving`). Driving needs NPC trains (`npcDriven.enable = true`).
{% endhint %}

Players can drive the trains themselves. They take over a train that is already running on a line, or take out a service train at a depot. The driver works a power/brake controller, keeps to the speed limits and signals, and opens the doors at the stations. Every stop they serve pays them.

***

### Who may drive

By default, players with the `train` job (any grade) may drive while on duty.

* `jobs` maps a job name to its minimum grade, e.g. `{ train = 0, transit = 2 }`. `jobs = {}` lets everyone drive.
* With `requireDuty`, drivers must be on duty. On ESX, a player counts as on duty unless their job reports `onDuty = false`.
* Players with the `prompt_train.drive` ace may always drive, whatever their job. Without a framework there are no jobs, so only they may drive (unless `jobs = {}`).
* `lines` limits the lines drivers may use, for take-overs and depots alike.

{% hint style="warning" %}
Make sure your framework has a job called `train`, or put your own job names in `jobs`.
{% endhint %}

Give the ace in `server.cfg`:

```
# admins may always drive
add_ace group.admin prompt_train.drive allow

# a driver group, and one player in it
add_ace group.traindriver prompt_train.drive allow
add_principal identifier.license:0123456789abcdef group.traindriver
```

The script checks this when a player joins and whenever their job or duty changes. Only players who may drive see the driving options. The job check uses `Bridge.getJob` in `config/server.lua`; a custom job system can refresh a player with `TriggerEvent('prompt_train:onJobChanged', source)` on the server. See [Frameworks](frameworks.md).

***

### Start driving

Both ways use the interaction set in `integrations.interaction` (`ox_target`, `qb-target` or the `[E]` prompt). With `'none'`, players can't start driving.

**Take over a line's train.** Walk up to its locomotive (on the metro, either car) and choose **Drive this train**. You take the driver's seat and the HUD opens. The train no longer stops at stations by itself. If it was moving, it holds its speed (**HOLD**) until you move the controller. Nobody can take a train someone else is driving. If you see *Could not take control of the train.*, try again when the train stands at a station.

**Take out a service train.** Talk to the dispatcher at a depot (**Service train depot**) and choose **Take out a service train**. The train appears at the platform's stop point, you are put in its cab, and the HUD marks it **Service**. A player can have one service train at a time, and the track at the platform must be clear. Players in a routing bucket other than `spawning.bucket` can't take one out.

| Depot        | Line                                    | Dispatcher                      | Train         |
| ------------ | --------------------------------------- | ------------------------------- | ------------- |
| Sandy Shores | `sandy`, Sandy Shores and Paleto Bay    | Sandy Shores station            | Polar Express |
| Los Santos   | `lossantos`, Los Santos to Sandy Shores | Los Santos station, platform 1  | Polar Express |
| Davis        | `metro`                                 | Davis metro station, platform 1 | Metro         |

Add or move depots in `service.depots`:

```lua
{ line = 'sandy', station = 'sandy_prompt', ped = vec4(1878.8, 3554.5, 37.82, 210.0) },
```

| Field     | Meaning                                                                                                                                                       |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `line`    | The line id                                                                                                                                                   |
| `station` | Where the train starts: the station id, plus `_1`, `_2`… for the platform of a station that has several (`lossantos_prompt_1`). It must be a stop of that line |
| `ped`     | Where the dispatcher stands, `vec4(x, y, z, heading)`                                                                                                         |
| `train`   | Optional. The one train this depot offers, a key from `config/trains.lua`. Without it, `service.train` applies                                                |
| `label`   | Optional. The name shown in the menu                                                                                                                          |

A depot whose line isn't running, or whose station isn't a stop of that line, is skipped with a warning in the server console.

***

### Controls

| Key     | Action                                                                   |
| ------- | ------------------------------------------------------------------------ |
| `W`     | Controller up one notch: less brake, then more power. Hold to repeat     |
| `S`     | Controller down one notch: less power, then more brake. Hold to repeat   |
| `Space` | Emergency brake                                                          |
| `G`     | Release or close the doors                                               |
| `R`     | Change direction. Only when stopped, with the controller at N or braking |
| `Q`     | Acknowledge the vigilance device                                         |
| `E`     | Horn                                                                     |
| `F`     | Leave the cab                                                            |

The controller has power notches P1 to P4, N, and brake notches B1 to B4. At N the train coasts. `G`, `R` and `Q` are key bindings: `keys` sets their defaults, and players can change them in **Settings > Key Bindings > FiveM**. The other keys are the game's own vehicle controls.

The HUD, bottom right, shows the line, the direction, the speed and the **Limit** (the speed you may run at now), the controller notch, the signal and the gap to the train ahead, the next stop or stop point, the doors, and any train protection alert.

***

### Speed limits and signals

The **Limit** is the lowest of these:

* **Line limit**: the line's cruise speed (`spawning.predictive.cruiseSpeed`, or the line's own `predictive.cruiseSpeed`) times `controls.speedLimitFactor`. By default, 86 km/h (54 mph) on the Los Santos and Sandy Shores lines and 43 km/h (27 mph) on the metro.
* **Curve limits** (`speedProfile`): worked out from how tight each curve is.
* **Speed zones**: a line's own `speedZones`, in its `line.lua`.
* **Signals**: see below.

A curve or zone limit holds until the last carriage has passed it. A lower limit up to `speedProfile.lookahead` ahead shows on the HUD in yellow with its distance, and the permitted speed falls along a braking curve so you can slow down in time.

```lua
-- lines/<line>/line.lua
speedZones = {
    { from = 1200, to = 1260, limit = 40 }, -- rail nodes 1200 to 1260 (0-based), 40 km/h
},
```

A zone replaces the curve limit on its stretch, but never goes above the line limit. `toggletrainnodes` shows the node numbers around you (see [Commands](commands.md)).

The signals look at the next train ahead on your rails, using the distances NPC trains keep: `collision.stopDistance` and `resumeDistance` ([Configuration § 5](configuration.md#5-anti-collision)), which a line can set for itself.

| Signal             | When                                                  | Limit                                             |
| ------------------ | ----------------------------------------------------- | ------------------------------------------------- |
| Line clear (green) | No train within `resumeDistance`                      | Line limit                                        |
| Caution (yellow)   | A train within `resumeDistance` (1040 m; metro 260 m) | Line limit times `signals.cautionFactor` (0.5)    |
| Stop (red)         | A train within `stopDistance` (720 m; metro 180 m)    | At most `signals.redSpeed` (8 m/s, about 29 km/h) |

***

### Train protection

* **Overspeed**: about 3 km/h over the limit, the HUD shows **Overspeed - brake** and the cab beeps. Stay over for `signals.overspeedMs` (5 s), or go more than `signals.interventionMargin` (10 km/h) over, and the service brake comes on until you are back at the limit.
* **Train ahead**: a train closer than `signals.atpGap` (80 m) while you are moving puts on the emergency brake.
* **Vigilance**: while moving, after `vigilance.intervalMs` (60 s) without any action from you, the device beeps and the HUD shows **VIGILANCE - press \[Q]**. Press `Q` within `vigilance.warnMs` (5 s), or the emergency brake comes on. Moving the controller, the doors key and the horn also reset the timer.

The emergency brake stays on until the train has stopped. Then press `W` to release it.

***

### Stops and pay

When the next stop is within 600 m, the HUD shows its **Stop point** and distance, and a marker as long as your train appears on the track. It turns green when the front of the train is within `stopTolerance` (8 m) of the stop point. This is a guide, not a rule.

Stop at the platform and press `G` to release the doors: the doors on the platform side open. The train takes no power while the doors are released, so close them with `G` before you leave.

A stop pays once the doors have been released for `pay.minDwellMs` (8 s): `pay.perStop` ($150) goes to `pay.account` (bank), with the message *You earned $150 for serving Sandy Shores.*

* No pay at the station where you started driving, or for the same station again within `pay.sameStationCooldownMs` (5 minutes). All platforms of a station count as one.
* Pay goes through the detected framework (QBX, QBCore or ESX), via `Bridge.addMoney` in `config/server.lua`. Without a framework, drivers are not paid.
* `pay.account` is separate from `integrations.payment`, which is for tickets.

***

### Leaving the cab

Press `F` to leave. The shift also ends when the driver walks more than 40 m from the locomotive, dies, or the train is removed.

* A **line's train** goes back to autopilot and carries on. It also does this by itself if you stand still away from a station for `takeover.idleReleaseMs` (3 minutes).
* A **service train** stops where you left it, and only you can get back in, with **Drive this train**. With no driver for `service.abandonMs` (60 s), it is removed. It is also removed at once if you disconnect.

***

### Which trains can be driven

Any train the script runs can be taken over. Without a `cab` setting, the driver uses the locomotive's own driver seat, as on the Polar Express and the metro. Two optional fields per train in `config/trains.lua`, or in a [train pack](train-packs.md):

| Field     | Meaning                                                                                                                                                                                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `driving` | Replaces values of `driving.physics` for this train, and can set `maxSpeed` (m/s; default 15% above the line limit). Shipped: Polar Express `{ accel = 0.7, brake = 1.2 }`, metro `{ accel = 1.3, brake = 1.6 }` |
| `cab`     | A driver's seat: `offset` (`vec3` from the locomotive), `heading`, `anim` (`{ dict, clip }`) and `exit` (where the driver steps out). With a cab, `V` switches between three camera views                       |

To place a cab, set `debug = true` and, while driving, run `train_cab x y z [heading]` in the F8 console. It moves your seat and prints the `cab = { ... }` line to paste.

***

### Options

Section 12 of `config/config.lua`. Speeds are in m/s unless marked km/h, whatever `units` says.

| Option                                   | Default                                                  | What it does                                                                     |
| ---------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `enable`                                 | `true`                                                   | Turns driving on or off                                                          |
| `jobs`                                   | `{ train = 0 }`                                          | Job name = minimum grade. `{}` lets everyone drive                               |
| `requireDuty`                            | `true`                                                   | Drivers must be on duty                                                          |
| `ace`                                    | `'prompt_train.drive'`                                   | Players with this ace may always drive. `false` turns it off                     |
| `lines`                                  | `{}`                                                     | Line ids drivers may use. `{}` = every line                                      |
| `units`                                  | `'mph'`                                                  | HUD speed unit, `'kmh'` or `'mph'`                                               |
| `sounds`                                 | `true`                                                   | Cab beeps and warnings. The horn always works                                    |
| `stopTolerance`                          | `8.0`                                                    | How close (m) to the stop point counts as in the stop zone                       |
| `takeover.enable`                        | `true`                                                   | Allow taking over a line's train                                                 |
| `takeover.maxSpeed`                      | `nil`                                                    | Fastest a train may go and still be taken over. `nil` = any speed                |
| `takeover.range`                         | `25.0`                                                   | How close (m) the player must be to the train                                    |
| `takeover.idleReleaseMs`                 | `180000`                                                 | Standing still away from a station this long hands the train back to autopilot   |
| `service.enable`                         | `true`                                                   | Depots and service trains                                                        |
| `service.perLine`                        | `1`                                                      | Service trains allowed on one line at once                                       |
| `service.abandonMs`                      | `60000`                                                  | A service train with no driver for this long is removed                          |
| `service.train`                          | `nil`                                                    | The one train every depot offers. `nil` = each train the line runs               |
| `service.dispatcher`                     | `s_m_m_lsmetro_01`, `WORLD_HUMAN_CLIPBOARD`, `100.0`     | The dispatcher's `model` and `scenario`, and the `range` (m) at which they appear |
| `service.depots`                         | Sandy Shores, Los Santos, Davis                          | See [Start driving](#start-driving)                                              |
| `controls.powerNotches` / `brakeNotches` | `4` / `4`                                                | Notches on the controller                                                        |
| `controls.notchRepeatMs`                 | `250`                                                    | Holding `W` or `S` moves a notch this often (ms)                                 |
| `controls.reverseMaxSpeed`               | `4.0`                                                    | Top speed in reverse                                                             |
| `controls.speedLimitFactor`              | `1.2`                                                    | Line limit = the line's cruise speed times this                                  |
| `physics`                                | `accel = 1.0`, `brake = 1.4`, `emergency = 3.0`, `coast = 0.04` | Full power, full service brake, emergency brake and slowing at N, in m/s². A train's own `driving` wins |
| `speedProfile.enable`                    | `true`                                                   | Curve speed limits                                                               |
| `speedProfile.lateralAccel`              | `0.8`                                                    | Sideways acceleration allowed in a curve (m/s²). Higher = faster curves          |
| `speedProfile.minSpeed` / `step`         | `30` / `5`                                               | Lowest curve limit, and the step curve limits are rounded down to (km/h)         |
| `speedProfile.smoothing`                 | `25.0`                                                   | A lower limit is stretched this far (m) both ways, so it doesn't flicker         |
| `speedProfile.lookahead`                 | `1500.0`                                                 | How far ahead (m) the HUD shows a lower limit                                    |
| `vigilance.enable`                       | `true`                                                   | The vigilance device                                                             |
| `vigilance.intervalMs`                   | `60000`                                                  | Time without a driver action before it asks                                      |
| `vigilance.warnMs`                       | `5000`                                                   | Time to answer before the emergency brake                                        |
| `vigilance.minSpeed`                     | `1.0`                                                    | Only active above this speed                                                     |
| `signals.cautionFactor`                  | `0.5`                                                    | Yellow: the limit times this                                                     |
| `signals.redSpeed`                       | `8.0`                                                    | Red: the most you may run at                                                     |
| `signals.atpGap`                         | `80.0`                                                   | A train closer than this (m) ahead puts on the emergency brake                   |
| `signals.overspeedMs`                    | `5000`                                                   | Over the limit this long puts on the service brake                               |
| `signals.interventionMargin`             | `10`                                                     | This many km/h over the limit puts on the service brake at once                  |
| `pay.enable`                             | `true`                                                   | Driver pay                                                                       |
| `pay.perStop`                            | `150`                                                    | Paid per stop served                                                             |
| `pay.account`                            | `'bank'`                                                 | `'cash'` or `'bank'`                                                             |
| `pay.minDwellMs`                         | `8000`                                                   | How long the doors must be released at a stop                                    |
| `pay.sameStationCooldownMs`              | `300000`                                                 | No pay for the same station again within this time                               |
| `keys`                                   | `{ doors = 'G', reverser = 'R', vigilance = 'Q' }`       | Default keys. The horn is `E`                                                    |
| `horn`                                   | `name = 'Horn'`, `set = 'DLC_Apt_Yacht_Ambient_Soundset'` | Horn sound and sound set. `bank` loads a custom audio bank first                |
