---
description: >-
  The script supports QBO, QBCore, ESX, and frameworkless setups through a
  bridge layer defined in config/server.lua and config/client.lua. You normally
  do not need to edit these files — auto-detection
icon: gear-complex
---

# Frameworks

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
