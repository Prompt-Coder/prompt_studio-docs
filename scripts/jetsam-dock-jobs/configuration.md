---
description: config.json reference — payments, access, languages, pay, shift length, truck contracts and crane controls
icon: sliders
---

# Configuration

| File | What it controls |
| --- | --- |
| `config.json` | Everything a server owner normally changes (this page) |
| `config.advanced.json` | Entity geometry, networking, collision, multi-crane layout, garage door bindings (see [Advanced](#advanced-settings)) |
| `locales/*.json` | Every text players see |
| `hooks/*.js` | Your own rules and reactions (see [For Developers](developers.md)) |

All of these stay open under escrow.

{% hint style="warning" %}
`config.json` is JSON: keep the quotes and commas intact. Restart `prompt_jetsam_script` after editing, when nobody is near the port.
{% endhint %}

***

### Main settings

{% code title="config.json" %}
```json
"modules": { "crane": true, "handler": true, "forklift": true },
"bridges": {
  "target": "auto",
  "notify": "nui",
  "textUI": "auto",
  "progress": "auto",
  "menu": "nui",
  "money": "auto",
  "customResource": ""
},
"locale": "en",
"fallbackLocale": "en",
"debug": false,
"framework": { "mode": "auto", "paymentAccount": "bank" }
```
{% endcode %}

| Setting | Values |
| --- | --- |
| `modules` | Turn the crane, handler and forklift jobs on or off. The truck job has its own `truck.enabled` |
| `bridges.target` | `auto` \| `ox_target` \| `qb-target` \| `none` \| `custom`. `none` uses press-E prompts |
| `bridges.notify` | `nui` \| `auto` \| `ox_lib` \| `qb` \| `esx` \| `native` \| `custom` |
| `bridges.textUI` | `auto` \| `ox_lib` \| `qb` \| `native` \| `custom` |
| `bridges.progress` | `auto` \| `ox_lib` \| `native` \| `custom` |
| `bridges.menu` | `nui` \| `auto` \| `ox_lib` \| `custom` |
| `bridges.money` | `auto` \| `free` \| `custom` (see [Payments](#payments)) |
| `bridges.customResource` | Your own bridge resource, for any `custom` value |
| `framework.mode` | `auto` \| `qbx` \| `qbcore` \| `esx` \| `standalone` \| `custom` |
| `framework.paymentAccount` | `bank` \| `cash` |
| `debug` | Console logging and developer commands. Keep `false` on a live server |

***

### Payments

* **With a framework** (QBX, QBCore or ESX), pay goes to the player's `framework.paymentAccount`.
* **Without a framework**, the jobs work but no money is paid. To pay through your own system, set `bridges.money` to `custom` and point `bridges.customResource` at your bridge resource ([For Developers](developers.md#custom-bridge)).
* `bridges.money: "free"` turns payment off on any server.

{% hint style="info" %}
`auto` finds the framework by itself. If you set `framework.mode` to a framework that isn't running, the dispatcher refuses paid shifts with "The payment system is unavailable" until that framework starts.
{% endhint %}

***

### Access (job locks)

Every job is open to everyone by default. To lock a job, set it to `true`:

{% code title="config.json" %}
```json
"access": {
  "crane": false,
  "handler": false,
  "forklift": false,
  "jobs": [],
  "minGrade": 0,
  "requireOnDuty": false,
  "ace": "prompt_jetsam_script.access"
}
```
{% endcode %}

A locked job is available to players whose framework job is in `jobs` (with at least `minGrade`, and on duty if `requireOnDuty` is `true`), **or** who have the ACE:

```
add_ace group.dockworker prompt_jetsam_script.access allow
```

The ACE works on every server, including standalone. The truck job follows the `forklift` lock.

***

### Languages

`locale` picks the language: `en` `de` `es` `fr` `ru` `pt` `sv` `no` `fi` `ar` `ko` `zh` `pl`, or `auto` to follow the server's `ox:locale` convar. A text missing in that language falls back to `fallbackLocale`, then English.

To change a wording, edit `locales/<language>.json` (save as UTF-8).

***

### Pay

| Job | Setting | Default |
| --- | --- | --- |
| Gantry crane | `rewards.base` / `rewards.perContainer` / `rewards.completionBonus` | $500 / $350 / $750 |
| Container handler | `handler.reward.amount` (per container) | $750 |
| Forklift | `forklift.reward.amount` (per pallet) | $650 |
| Truck delivery | `truck.orders.destinations[].reward` (per contract) | $650 – $4,500 |

`rewards.currencySymbol` sets the symbol shown in messages. `rewards.enabled: false` turns all pay off.

***

### Shift length

The handler and forklift shifts use `job.mode`:

{% code title="config.json" %}
```json
"job": {
  "mode": "infinity",
  "requiredLoads": { "min": 5, "max": 10 }
}
```
{% endcode %}

* `infinity`: the shift runs until the player ends it at the dispatcher.
* `random`: the shift ends after a random number of loads between `min` and `max`.

The crane uses the same idea in `crane.containerSpawner.job` with `requiredContainers`.

***

### Truck contracts

| Setting | What it does |
| --- | --- |
| `truck.enabled` | `false` hides the truck job; the forklift job stays |
| `truck.vehicleProfiles` | The vehicles offered on the contract board: `mule` (box truck, 3 pallets) and `hauler` (Hauler + `trailers3`, 7 pallets) |
| `truck.ownCab` | `off`: job cab only. `optional`: job cab or the player's own truck. `required`: own truck only |
| `truck.orders.offerCount` | Contracts shown on the board (default 4) |
| `truck.orders.palletCount` | Random pallet count per contract (default 4–7), capped at what the vehicle holds |
| `truck.orders.pickupModes` | Where pallets come from: `warehouse` (shelves), `outside` (forklift yard stack) |
| `truck.orders.unloadMs` | How long the truck must stand in the delivery area (default 3000 ms) |
| `truck.orders.distanceUnit` | `km` \| `mi`: the unit shown on the board |
| `truck.orders.destinations` | Destination list (20 by default) |

{% code title="config.json — one destination" %}
```json
{
  "id": "paleto",
  "label": "Paleto Bay",
  "coords": { "x": 41.259, "y": 6450.312, "z": 31.484 },
  "reward": 4500
}
```
{% endcode %}

`truck.spawns` and `truck.cabSpawns` are the loading bays and cab parking at the JetSam warehouse. They match the map; leave them unless you move the bays.

***

### Crane controls

Keyboard and gamepad bindings use GTA control ids:

{% code title="config.json — crane.operatorController" %}
```json
"controls": {
  "exit": 75,
  "trolleyNegative": 34,
  "trolleyPositive": 35,
  "hoistUp": 21,
  "hoistDown": 36,
  "baseNegative": 33,
  "basePositive": 32,
  "attach": 38,
  "cameraCycle": 0
}
```
{% endcode %}

The defaults are F (exit), A/D (trolley), Left Shift / Left Ctrl (hoist), S/W (crane travel), E (attach) and V (camera). `gamepadControls` holds the gamepad bindings, and `ui` sets the on-screen panel and key hints (`gamepadDevice`: `auto` \| `xbox` \| `playstation`).

***

### Advanced settings

`config.advanced.json` holds technical values: crane geometry and cables, entity networking, collision, multi-crane layout and the garage door bindings. Its `overrides` replace matching `config.json` values, and only apply while `enabled` and `iKnowWhatIAmDoing` are both `true`.

{% hint style="danger" %}
Change `config.advanced.json` only if you know what each value does. The defaults are calibrated to the JetSam map.
{% endhint %}
