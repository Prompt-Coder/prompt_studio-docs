---
description: >-
  The script supports QBox, QBCore, ESX, and frameworkless setups through a
  bridge layer in config/server.lua. Auto-detection handles it on most servers.
icon: gear-complex
---

# Frameworks

{% hint style="info" %}
**Version 2** (2.0.0-beta) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

The script supports QBox (`qbx`), QBCore (`qb`), ESX, and frameworkless setups through a bridge layer in `config/server.lua`. You normally never touch this file — configure via `config/config.lua § 1` instead:

```lua
integrations = {
    interaction = 'auto',   -- 'auto' | 'ox_target' | 'qb-target' | 'textui' | 'none'
    framework   = 'auto',   -- 'auto' | 'qbx' | 'qb' | 'esx' | 'none'
    inventory   = 'auto',   -- 'auto' | 'ox_inventory' | 'qb-inventory' | 'esx' | 'none'
    payment     = 'cash',   -- 'cash' | 'bank'
}
```

### Supported combinations

| Framework | Resource checked | Inventory options                                                                                                                  |
| --------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| QBox      | `qbx_core`       | `ox_inventory`, `qb-inventory`, `ps-inventory`                                                                                     |
| QBCore    | `qb-core`        | `ox_inventory`, `qb-inventory`, `ps-inventory`                                                                                     |
| ESX       | `es_extended`    | `ox_inventory`, native ESX inventory                                                                                               |
| None      | —                | none (script's own [standalone ticket store](tickets.md#standalone-mode-integrations-inventory-none)) |

***

### Auto-detection

With `'auto'`, `config/server.lua` checks `GetResourceState()` for each candidate resource and takes the first one that's `'started'`. Inventory auto-detection additionally falls back to ESX's native inventory if no dedicated inventory resource is running under an ESX framework. If detection can't find what you asked for explicitly, it logs an error and falls back to `'none'` behaviour rather than crashing.

If auto-detection picks the wrong thing on a server running several of these resources side by side, set the values explicitly.

***

### `interaction = 'textui'`

Needs only `ox_lib`. It's the fallback when neither `ox_target` nor `qb-target` is running, so most servers never set this by hand — ticket machines and doors just work through `ox_lib`'s text-prompt UI instead of a targeting reticle.

***

### Player spawn event

The bridge listens for the framework's own spawn event and re-fires `prompt_train:onPlayerSpawned` internally, which is what kicks off NPC train spawning for that player.

| Framework     | Source event                                                                   |
| ------------- | ------------------------------------------------------------------------------ |
| QBox / QBCore | `QBCore:Server:OnPlayerLoaded`                                                 |
| ESX           | `esx:playerLoaded`                                                             |
| None          | `playerJoining` → `prompt_train:playerSpawned` (client fires this once loaded) |

A custom spawn system that fires none of these can trigger it manually:

```lua
TriggerEvent('prompt_train:onPlayerSpawned', source)
```

***

### Bridge functions

Available globally server-side once `config/server.lua` loads:

| Function                                                                   | Purpose                                                                                                                                              |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Bridge.getPlayerName(source)`                                             | Character name — charinfo first/last for QBox/QBCore, `xPlayer.getName()` for ESX, `GetPlayerName` otherwise                                         |
| `Bridge.addItem` / `hasItem` / `removeItem(source, item, count, metadata)` | Routed to the detected inventory, or the built-in standalone store when `inventory = 'none'`                                                         |
| `Bridge.removePayment(source, amount)`                                     | Deducts `integrations.payment` ('cash' or 'bank'); returns `false` if the player can't afford it. Always returns `true` with no framework configured |

***

### Useable item registration

`train_ticket` is registered as a useable item automatically for QBox, QBCore, and ESX — using it shows the ticket UI via `showTicket` (`server/ticket.lua`). Under `inventory = 'none'`, use the `/trainticket` chat command instead to reopen your latest ticket.

***

### Adding a custom framework

Edit `config/server.lua` — it's a series of `if framework == '...' then ... elseif ...` blocks, one per bridge function. Add your own branch following the existing QBox/QBCore/ESX pattern for `getPlayerName`, `removePayment`, and the spawn-event listener, then set `integrations.framework` to your new key (auto-detection only knows about the three built-in resource names).

***

## Version 1

Everything below applies to **1.0.x** (latest: 1.0.4.1).

### Supported Combinations

| Framework           | Inventory options                              |
| ------------------- | ---------------------------------------------- |
| QBx (`qbx_core`)    | `ox_inventory`, `qb-inventory`, `ps-inventory` |
| QBCore (`qb-core`)  | `ox_inventory`, `qb-inventory`, `ps-inventory` |
| ESX (`es_extended`) | `ox_inventory`, `esx` (native)                 |
| None / custom       | Tickets are free; the script stores them itself (no inventory needed) |

***

### Auto-Detection

```lua
framework = 'auto'
inventory = 'auto'
```

With `'auto'`, the bridge checks `GetResourceState()` for each supported resource in order. The first one that is `'started'` wins. This works for the vast majority of setups.

If auto-detection picks the wrong thing, set the value explicitly:

```lua
framework = 'qbx'
inventory = 'ox_inventory'
```

***

### Interaction System

```lua
-- config/config.lua
interaction = 'auto'   -- 'auto' | 'ox_target' | 'qb-target' | 'textui' | 'none'
```

This controls how players interact with ticket machines and train seats:

* `'auto'` — uses `ox_target` or `qb-target` when one is installed, otherwise falls back to `'textui'`.
* `'ox_target'` — uses `ox_target` zones and entity targeting.
* `'qb-target'` — uses `qb-target`.
* `'textui'` — built-in `[E]` proximity prompts (ox\_lib only — no target resource needed).
* `'none'` — no interaction is registered (you can add your own via exported helpers).

***

### Player Spawn Event

The bridge listens for the framework's player-spawn event and fires `prompt_train:onPlayerSpawned` internally. This triggers the NPC train spawning logic.

| Framework    | Source event                   |
| ------------ | ------------------------------ |
| QBx / QBCore | `QBCore:Server:OnPlayerLoaded` |
| ESX          | `esx:playerLoaded`             |
| None         | `playerJoining`                |

If your server uses a custom spawn system that does not fire any of these events, add a manual trigger in your spawn script:

```lua
TriggerEvent('prompt_train:onPlayerSpawned', source)
```

***

### Bridge Functions

These are server-side functions available globally after `config/server.lua` loads:

#### `Bridge.getPlayerName(source)`

Returns the player's character name.

| Framework    | Implementation                                   |
| ------------ | ------------------------------------------------ |
| QBx / QBCore | `charinfo.firstname .. ' ' .. charinfo.lastname` |
| ESX          | `xPlayer.getName()`                              |
| None         | `GetPlayerName(source)`                          |

#### `Bridge.addItem(source, item, count, metadata)`

Adds an item to the player's inventory. Returns `true` on success.

| Inventory                       | Implementation                      |
| ------------------------------- | ----------------------------------- |
| `ox_inventory`                  | `exports.ox_inventory:AddItem(...)` |
| `qb-inventory` / `ps-inventory` | `Player.Functions.AddItem(...)`     |
| `esx`                           | `xPlayer.addInventoryItem(...)`     |
| None                            | Stored in the script's own ticket store (`standalone_tickets.json`), returns `true` |

#### `Bridge.removePayment(source, amount)`

Deducts money from the player. Returns `true` if successful, `false` if they cannot afford it.

The account used is controlled by `paymentMethod` in `config/config.lua`:

```lua
paymentMethod = 'cash'   -- 'cash' | 'bank'
```

| Framework | `'cash'`                                    | `'bank'`                                     |
| --------- | ------------------------------------------- | -------------------------------------------- |
| QBx       | `RemoveMoney(source, 'cash', amount)`       | `RemoveMoney(source, 'bank', amount)`        |
| QBCore    | `Player.Functions.RemoveMoney('cash', ...)` | `Player.Functions.RemoveMoney('bank', ...)`  |
| ESX       | `xPlayer.removeMoney(amount)`               | `xPlayer.removeAccountMoney('bank', amount)` |
| None      | Always returns `true`                       | Always returns `true`                        |

***

### Useable Item Registration

`config/server.lua` automatically registers `train_ticket` as a useable item for QBx, QBCore, and ESX. When a player uses the item, the ticket UI is shown client-side.

If your inventory system is not one of the three above, register the item manually:

```lua
-- example for a custom inventory
MyInventory.RegisterUseable('train_ticket', function(source, item)
    local ticket = item.metadata and item.metadata.ticket
    if not ticket then return end
    showTicket(source, ticket)
end)
```

`showTicket` is a global server-side function defined in `server/ticket.lua`.

***

### Adding Support for a Custom Framework

Edit `config/server.lua`. The file is structured as a series of `if/elseif` blocks, one per framework. Copy the pattern and add your own:

```lua
-- in the framework detection block:
elseif framework == 'myframework' then
    function Bridge.getPlayerName(source)
        return MyFramework.GetPlayer(source).name
    end

-- in the payment block:
elseif framework == 'myframework' then
    function Bridge.removePayment(source, amount)
        return MyFramework.RemoveMoney(source, amount)
    end

-- in the spawn event block:
elseif framework == 'myframework' then
    AddEventHandler('myframework:playerLoaded', function(src)
        TriggerEvent('prompt_train:onPlayerSpawned', src)
    end)
```
