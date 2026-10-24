---
description: Hooks, server exports, commands and the custom money / job bridge
icon: code
---

# For Developers

Everything here works without touching the protected files: rules and reactions go into the open hook files, other resources read state through exports, and your own money or job system plugs in through a bridge resource.

***

### Hooks

Hook files live in `hooks/`. They are created from the `.example.js` templates on the first start and are never overwritten by updates. Each file returns a JavaScript object. Restart the resource after editing.

| File | Role |
| --- | --- |
| `hooks_server.js` | Decides. Return `false` from a `can*` hook to block the action |
| `hooks_client.js` | Only controls what players see (for example hiding a target option) |
| `hooks_shared.js` | Runs on both sides. Do not put secrets in it |

The `global` handler and the matching `entries[id]` handler must both allow an action. A hook that throws never stops the job. On the server, `ctx.source` is always the player.

| Feature | `entries` id | Gates | Reactions | ctx |
| --- | --- | --- | --- | --- |
| `jobs` | `gantry-crane`, `container-handler`, `warehouse-forklift`, `truck-delivery` | `canStart`, `canFinish` | `onStart`, `onEnd` | `source`, `jobId`; `onEnd` adds `reason` and `payment` |
| `crane` | crane id (`jetsam-dock-1` …) | `canOperate`, `canPickup`, `canDeliver` | `onPickup`, `onDeliver` | `source`, `craneId`; pickup and delivery add `containerId`, `sessionId` |
| `handler` | container id | `canPickup`, `canDeliver` | `onPickup`, `onDeliver` | `source`, `cargo` |
| `forklift` | pallet id | `canPickup`, `canDeliver` | `onPickup`, `onDeliver` | `source`, `pallet` |
| `truck` | destination id (`truck.orders.destinations[].id`) | `canPickup`, `canLoad`, `canDeliver`, `canHitch` | `onPickup`, `onLoad`, `onLoaded`, `onDeliveryStart`, `onDeliver`, `onReturnBayAssigned`, `onHitch` | `source`, `sessionId`, `session`, `truck`; plus `pallet`, `slotIndex`, `cabNetId`, `ownCab` where they apply |

Client side: `jobs.global.canInteract(ctx)` with `ctx = { source, entity }`; its `entries` use the target option name.

{% code title="hooks/hooks_server.js" %}
```js
return {
  jobs: {
    entries: {
      "truck-delivery": {
        canStart(ctx) {
          return exports["my-jobs"].CanStartTruck(ctx.source);
        },
        onEnd(ctx) {
          if (ctx.reason === "completed") {
            exports["my-jobs"].RecordTruckDelivery(
              ctx.source,
              ctx.session.truck.destination.id,
            );
          }
        },
      },
    },
  },
  truck: {
    global: {
      onLoad(ctx) {
        exports["my-jobs"].RecordTruckLoad(ctx.source, ctx.pallet.palletId, ctx.slotIndex);
      },
    },
    entries: {},
  },
};
```
{% endcode %}

* `onEnd` receives `reason`: check `reason === "completed"` to tell a finished shift from a cancel or expiry.
* `canFinish` runs after the vehicle return, before payment, and is retried while it returns `false`.
* `canDeliver` on the truck is checked every second while the truck stands in the delivery area.
* `canHitch` gets the towing vehicle the client reported. The server still checks the driver seat, routing bucket and distance after the gate passes; `onHitch` fires only once the hitch is accepted.

***

### Exports

Server, `exports['prompt_jetsam_script']`. Every export returns a copy.

| Export | Returns / does |
| --- | --- |
| `GetPlayerSession(source)` | The player's current shift, or `nil` |
| `GetJobAvailability()` | Which jobs can be started right now |
| `HasJobAccess(source, jobId)` | Access check for `gantry-crane`, `container-handler`, `warehouse-forklift`, `truck-delivery` |
| `FinishShift(source, sessionId)` | Finishes a shift (the truck job finishes itself after the truck is returned) |
| `CancelShift(source, sessionId)` | Cancels a shift |
| `GetPallets()` | Forklift pallets |
| `GetTruckJob(source)` | The player's truck job, or `nil`: destination, pickup mode, vehicles, loading bay, return bay, loaded pallets |
| `GetTruckPallets(source)` | Pallets still to load for the truck job |
| `GetTruckDestinations()` | Configured truck destinations |
| `GetWarehouseContainers()` | Containers delivered to the warehouse |
| `ClaimWarehouseContainer(cargoId)` | Claims a delivered container for processing by the calling resource |
| `CompleteWarehouseContainer(cargoId)` | Marks a claimed container as processed |
| `GetSupportReport()` | The support snapshot printed by `/dock_debugdump` |

Client: `wakeProximity()` wakes the crane proximity checks.

```lua
local dock = exports['prompt_jetsam_script']
local session = dock:GetTruckJob(source)
if session then
    print(session.sessionId, session.truck.stage, session.truck.destination.id)
end
```

***

### Commands

| Command | Who | What |
| --- | --- | --- |
| `/dock` | Everyone | Shows what was detected: framework, target, language, modules |
| `/dock_debugdump` | Server console, or ACE `command.dock_debugdump` / `prompt_jetsam_script.admin` | Full support snapshot |
| `/dockdev` | `debug = true` **and** ACE `prompt_jetsam_script.admin` | Developer tools: layout editors, truck spawn tests |

***

### Custom bridge

For your own money or job system, create a small resource, set `bridges.customResource` to its name and switch the matching setting to `custom` (`bridges.money`, or `framework.mode`). The script then calls these server exports on that resource:

| Export | Used for | Return |
| --- | --- | --- |
| `GiveMoney(source, amount, account, reason)` | Paying a finished shift | `true` when paid |
| `GetJob(source)` | Job locks (see [Access](configuration.md#access-job-locks)) | `{ name, grade, onDuty }` or `nil` |
| `GetPaymentIdentity(source)` | A stable player id for the payment ledger (`framework.mode: "custom"`) | string |

`bridges.notify`, `textUI`, `progress`, `menu` and `target` can point to the same resource with `custom`.

{% hint style="info" %}
Payouts are recorded server-side in a ledger before the money is sent, so the same shift is not paid twice.
{% endhint %}
