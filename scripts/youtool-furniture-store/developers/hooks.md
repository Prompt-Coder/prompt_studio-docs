---
description: Block or react to purchases, markup, vault, freight, staff, displays, sets, catalog edits and the tablet from YouTool's open hook files.
icon: filter
---

# Hooks

Hooks let you add your own rules and reactions without touching YouTool's protected code: block a purchase, cap a vault withdrawal, post freight orders to Discord, hide the tablet. You write them in three open files in `prompt_youtool_store_system/hooks/`.

| File | Runs on | Use it for |
| --- | --- | --- |
| `hooks_server.lua` | Server | Rules that must hold, and reactions. The only file where secrets (webhook URLs, keys) may go. |
| `hooks_client.lua` | Every player's game | Tablet visibility. |
| `hooks_shared.lua` | Both | A check you want on both sides, written once. The server evaluates every feature from it, the client only `tablet`. |

{% hint style="warning" %}
`hooks_client.lua` and `hooks_shared.lua` are sent to every player's game as plain text. Never put webhooks, keys or other secrets in them.
{% endhint %}

### How the files are created

On start, the server looks for `hooks/hooks_server.lua`, `hooks_client.lua` and `hooks_shared.lua`. A file that is missing or empty is created from its `.example.lua` template, and the console prints `[YouTool] hooks: created hooks/hooks_server.lua from template`. Files that exist are never overwritten, so your hooks survive updates (keep them when you replace the folder, see [Installation](../installation.md)). If the folder isn't writable, YouTool uses the template and prints a warning.

The `.example.lua` files are the full reference with every feature and context field. **Restart the resource** after editing a hook file. Players get the client and shared file from the server when they load in.

***

## How a hook works

Every file returns one table: per **feature** a `global` handler set that runs for every id, and `entries` for one id (usually a store id).

{% code title="hooks/hooks_server.lua" %}
```lua
return {
    vault = {
        global = {
            canWithdraw = function(ctx) return ctx.amount <= 50000 end,   -- every store
        },
        entries = {
            ['youtool_sandy'] = {
                onWithdraw = function(ctx) print(ctx.source, ctx.amount) end, -- Sandy Shores only
            },
        },
    },
}
```
{% endcode %}

Store ids are `youtool_sandy` and `youtool_vespucci` (the `id` in `Config.Stores`).

| Kind | Name | What it does |
| --- | --- | --- |
| **Gate** | `can...` | Return `false` to block. `true` or nothing allows. |
| **Reaction** | `on...` | Runs after the action succeeded. The return value is ignored. |

The rules:

* **Gates can only take access away.** On the server they run after YouTool's own checks (position permissions, corporate ACE) and before anything changes, so a gate never grants what a position doesn't have. To give someone access, change their position in the Staff tab instead.
* **Everything must pass.** `global` and the matching `entries` handler both run; either returning `false` blocks. `hooks_shared.lua` and the side-specific file are combined the same way.
* **No custom message.** A blocked player sees YouTool's own notice, *"You don't have access to this."* (staff changes: *"Not authorized (staff management)"*).
* **Errors fail open.** Every handler runs protected. If one throws an error, the console prints `[YouTool] hook error in <feature>.<id>.<event>: <error>` and the action goes ahead as if the hook allowed it. A syntax error disables that whole file, with a warning in the console.
* **Console commands skip hooks.** `youtool_setowner`, `youtool_hire`, `youtool_fire`, `youtool_setmarkup`, `/youtool_vault_withdraw`, `youtool_freight`, `youtool_restock`, `youtool_setstock` and `youtool_delist` don't call gates or reactions. Everything done in the tablet, the Console, at the dock and with `/youtool_setprice` does.

***

## Features and context

`ctx.source` is always the player's server id. All features run on the server except `tablet`, which runs on the client.

### purchase (id = storeId)

| Event | ctx | When |
| --- | --- | --- |
| `canPurchase` | `source, storeId, items, total` | Checkout, after the cart was checked and priced, before the property, money and stock checks. `items` = `{ { id, quantity }, ... }`, a set appears as `{ setId, quantity = 1 }`. `total` = the cart total at this store's prices. |
| `onPurchase` | `source, storeId, houseId, charged, delivered, ordered, refund` | After a checkout delivered at least one item. `charged` = what the player finally paid, `delivered` / `ordered` = units, `refund` = money returned for units that didn't arrive. |

### markup (id = storeId)

| Event | ctx | When |
| --- | --- | --- |
| `canSet` / `onSet` | `source, storeId, scope, key, percent` | A markup change in the Console. `scope` = `'global'`, `'category'` or `'item'`; `key` = the category name or item id (`nil` for global). |

### vault (id = storeId)

| Event | ctx | When |
| --- | --- | --- |
| `canWithdraw` / `onWithdraw` | `source, storeId, amount` | Withdraw from the vault to the player's bank. |
| `canDeposit` / `onDeposit` | `source, storeId, amount` | Deposit from the player's bank into the vault. |

### freight (id = storeId, Active mode only)

| Event | ctx | When |
| --- | --- | --- |
| `canOrder` | `source, storeId, lines, cost, pallets` | A freight order, before the vault is charged. `lines` = `{ { class, pallets, points, cost }, ... }`. |
| `onOrder` | `source, storeId, cost, pallets` | The order was placed. |
| `canDispatch` / `onDispatch` | `source, storeId` | An employee takes the store truck (`'self'` mode). |
| `canCancel` / `onCancel` | `source, storeId` | The order is cancelled. |
| `onArrived` | `storeId, pallets` | The pallets are at the dock. `pallets` = how many. No `source`. |
| `canUnload` | `source, storeId, pallet` | An employee claims a pallet at the dock. `pallet` = its number. |
| `onBoxDropped` | `source, storeId, wage` | A box was stored and the wage paid. |
| `onPalletDone` | `source, storeId, class, points` | A pallet was fully unloaded and its stock credited. |

### staff (id = storeId)

| Event | ctx | When |
| --- | --- | --- |
| `canEdit` / `onEdit` | `source, storeId, action, target, roleId, name` | A Staff tab change. `action` = `'hire'`, `'fire'`, `'assign'`, `'createRole'`, `'updateRole'`, `'deleteRole'`, `'transferOwner'` or `'reorder'`. `target` = the employee's identifier (hire, fire, assign, transferOwner), `roleId` and `name` where they apply. |

Unlike the other gates, `staff.canEdit` runs before YouTool's own staff check, so it also sees attempts YouTool then refuses. `onEdit` only runs for changes that went through.

### displays (id = storeId)

| Event | ctx | When |
| --- | --- | --- |
| `canPlace` | `source, storeId, catalogItemId` | A manager places display furniture. |
| `onPlace` | `source, storeId, catalogItemId, uid` | The display was placed. |
| `canRemove` / `onRemove` | `source, storeId, uid` | A display is removed. |

### sets (id = storeId)

| Event | ctx | When |
| --- | --- | --- |
| `canEdit` | `source, storeId, action, setId` | `action` = `'create'`, `'update'`, `'delete'`, `'place'`, `'removeInstance'` or `'completeInstance'`. There is no `onEdit` for sets. |

### catalog (id = `'corporate'`, or storeId for delist)

| Event | ctx | When |
| --- | --- | --- |
| `canEdit` | `source, action, modelId, value`, plus `storeId` for delist | `action` = `'price'`, `'clearPrice'`, `'name'`, `'clearName'` (id `'corporate'`) or `'delist'` (id = storeId). `value` = the new price, the new name, or `true`/`false` for delisted. |

### tablet (id = storeId, client)

| Event | ctx | When |
| --- | --- | --- |
| `canOpen` | `storeId, ped` | `false` = no tablet and no "\[E] Open Tablet" prompt for this player. Visibility only: the server still checks every action with the server hooks. |

***

## Examples

### Block purchases for some jobs

Players with a blocked job get *"You don't have access to this."* at checkout. In `hooks/hooks_server.lua`, replace the `purchase` block:

{% tabs %}
{% tab title="QBCore / QBox" %}
{% code title="hooks/hooks_server.lua" %}
```lua
purchase = {
    global = {
        canPurchase = function(ctx)
            local blocked = { police = true, ambulance = true }
            local core = GetResourceState('qbx_core') == 'started' and 'qbx_core' or 'qb-core'
            local player = exports[core]:GetCoreObject().Functions.GetPlayer(ctx.source)
            if not player then return false end
            return not blocked[player.PlayerData.job.name]
        end,
    },
    entries = {},
},
```
{% endcode %}
{% endtab %}

{% tab title="ESX" %}
{% code title="hooks/hooks_server.lua" %}
```lua
purchase = {
    global = {
        canPurchase = function(ctx)
            local blocked = { police = true, ambulance = true }
            local xPlayer = exports.es_extended:getSharedObject().GetPlayerFromId(ctx.source)
            if not xPlayer then return false end
            return not blocked[xPlayer.job.name]
        end,
    },
    entries = {},
},
```
{% endcode %}
{% endtab %}
{% endtabs %}

Remember that hooks fail open: if your framework call errors, the purchase is allowed.

### Log vault withdrawals to Discord

Server only, because it holds the webhook URL. In `hooks/hooks_server.lua`, replace the `vault` block:

{% code title="hooks/hooks_server.lua" %}
```lua
vault = {
    global = {
        onWithdraw = function(ctx)
            local webhook = 'https://discord.com/api/webhooks/your/webhook'
            local text = ('%s withdrew $%d from %s'):format(GetPlayerName(ctx.source), ctx.amount, ctx.storeId)
            PerformHttpRequest(webhook, function() end, 'POST',
                json.encode({ content = text }), { ['Content-Type'] = 'application/json' })
        end,
    },
    entries = {},
},
```
{% endcode %}

Withdrawals with the `/youtool_vault_withdraw` command don't run hooks, so they are not posted.

### Tablet only for logged-in players

QBCore and QBox set the `isLoggedIn` state on the player once a character is loaded. In `hooks/hooks_client.lua`:

{% code title="hooks/hooks_client.lua" %}
```lua
return {
    tablet = {
        global = {
            canOpen = function(ctx)
                return LocalPlayer.state.isLoggedIn == true
            end,
        },
        entries = {},
    },
}
```
{% endcode %}

This hides the tablet and its prompt. A client hook is only visibility; if a rule must hold, add a server gate too (for example `purchase.canPurchase`).
