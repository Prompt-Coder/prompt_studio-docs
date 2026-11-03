---
description: >-
  Players can purchase train tickets from interactive kiosk machines placed at
  stations. Tickets are inventory items with embedded metadata showing origin,
  destination, and departure time.
icon: ticket
---

# Tickets

{% hint style="info" %}
**Version 2** (2.1.0) is documented first. Still running 1.0.x? Jump to [Version 1](#version-1).
{% endhint %}

Players buy tickets from kiosk machines placed at stations. A ticket carries origin, destination, and departure metadata and can be displayed on-screen. By default a ticket is needed to open the carriage doors.

### How it works

1. A player interacts with a ticket machine (`ox_target` / `qb-target` / textUI, per `integrations.interaction`).
2. A DUI ticket UI opens showing destinations and prices.
3. The player picks a destination and confirms.
4. The server checks the station, the train and the destination, charges the player (`integrations.payment`, cash or bank) and issues a `train_ticket`. If the ticket can't be added to the inventory, the fare is refunded.
5. The player can use the ticket item to view it again.

All ticket text comes from the locale files: `ticket.use_machine` (the interaction), `ticket.required` (the door message) and `ticketdui.*` (the machine screen). In 2.1.0 the first two were renamed from `use_ticket_machine` and `no_ticket`.

***

### Doors and tickets

With `tickets.requireForDoors = true` (the default), a player needs a `train_ticket` to open a carriage door by walking up to it. Without one the door stays shut, and the player sees *You need a train ticket to board. Purchase one at a ticket machine.*

* **Doors between carriages** (gangway doors) always work, also while the train is moving, so passengers can walk through the train.
* **Side doors** only open while the train is stopped at a station. There, the side doors on the platform side open by themselves, without a ticket check. On a train a player drives, they open when the driver releases the doors.
* `wagons.doorsAlwaysOpen = true` opens the doors for everyone and skips the ticket check. Side doors still only open at stations.

Which doors count as side doors, and what counts as stopped at a station, is set in `wagons.doors.exterior` (see [Configuration § 7](configuration.md#7-wagons)). The Polar Express's sliding doors sit on the carriage's centre line, so they count as doors between carriages: they open for a ticket holder who walks up to them, moving or not.

{% hint style="info" %}
The metro's doors are part of the train model. They open by themselves on the platform side at every station and don't check tickets.
{% endhint %}

***

### Where a machine is defined

Machines are **per-station**, declared on the station itself under `prompt_train_script-assets/stations/`:

```lua
-- a station file, e.g. stations/freight/paletobay_prompt.lua -- id is taken from the filename
Station {
    label = 'Paleto Bay',
    coords = vec3(232.543, 6384.49, 30.641),
    price = 30,
    machines = {
        coords = { vec3(168.706, 6380.335, 30.486), vec3(169.260, 6379.342, 30.486) },
        model  = `i45pt_pts_ticketmachine_prop`,
        txd    = 'i45pt_pts_ticketmachine_prop',
        txn    = 'script_rt_ticketmachine_screen_paleto',
    },
}
```

| Field                            | Description                                                                                                                                                                                |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `price`                          | Price of a ticket **to** this station, matched by its label. Overrides `tickets.defaultPrice`                                                                                             |
| `machines.coords`                | One `vec3` per physical kiosk object in the world. For machines the script spawns, use a `vec4`: the fourth value is the heading                                                          |
| `machines.model` / `txd` / `txn` | The map's own machine prop and the texture the DUI screen replaces. With a `model`, the map's props are re-textured and nothing is spawned. Omit all three to spawn the default machine (`tickets.defaultMachine`) instead |
| `machines.spawn`                 | Set `false` to register interaction on an existing world prop instead of spawning one                                                                                                      |

A station tied to a variant-only resource (its `resource` field) only spawns its machines while that resource is active — same as its platform.

`config/config.lua`'s `tickets.prices` and `tickets.machines` only add to or override what stations declare — see [Configuration § 9](configuration.md#9-tickets). You rarely need to touch them; adding a station is normally enough.

***

### Adding a ticket machine to a new station

1. Find the prop in-game and note its model hash, `txd`/`txn` and exact position (CodeWalker or similar). The script finds the prop by its position, so it must match to within 0.1 m. To have the script spawn its own machine instead, leave out `model`, `txd` and `txn` and give a `vec4` per machine.
2. Add a `machines` block to the station file as shown above. `prompt_train_script-assets/templates/station.lua` has a commented example.
3. Run `train_assets_validate` — no separate registration step needed.

***

### Inventory item

Required unless `integrations.inventory = 'none'`. Register `train_ticket`:

**ox\_inventory** (`items.lua`):

```lua
['train_ticket'] = { label = 'Train Ticket', weight = 10, stack = false, close = true, consume = 0 },
```

**QBCore** (`items.lua`):

```lua
['train_ticket'] = { name = 'train_ticket', label = 'Train Ticket', weight = 100, type = 'item',
    image = 'train_ticket.png', unique = true, useable = true, shouldClose = true, description = 'A train ticket' },
```

The useable-item handler itself is registered automatically for QBx, QBCore, and ESX by `config/server.lua` — you only need the item definition in your inventory resource.

With `ox_inventory`, the server console warns at start if the item is missing: `ox_inventory has no 'train_ticket' item, so ticket machines cannot hand out tickets -- add it to ox_inventory/data/items.lua`.

***

### Standalone mode (`integrations.inventory = 'none'`)

No inventory resource is required. The script keeps tickets itself, keyed per player identifier, persisted to `standalone_tickets.json` in the resource folder with a 24-hour expiry. `requireForDoors` and all pricing behave identically. There is no item to use, so players reopen their latest ticket with `/trainticket`.

***

### Ticket metadata

The item's metadata holds the ticket as `metadata.ticket`:

```lua
{
    number        = '482913',       -- random 6-digit number
    passengerName = 'John Smith',
    from          = 'Paleto Bay',   -- station label
    to            = 'Los Santos',   -- destination label
    date          = 1767225600000,  -- time of purchase, ms since 1970
    departure     = '14:32',
    arrival       = '15:05',
}
```

***

### Payment

`config/server.lua` deducts the fare through whichever framework is detected:

| Framework | Call                                                          |
| --------- | ------------------------------------------------------------- |
| QBx       | `exports.qbx_core:RemoveMoney(source, paymentMethod, amount)` |
| QBCore    | `Player.Functions.RemoveMoney(paymentMethod, amount)`         |
| ESX       | `xPlayer.removeMoney()` / `xPlayer.removeAccountMoney()`      |
| None      | Always succeeds — free tickets, useful for testing            |

If the player can't afford it, the purchase is rejected and nothing is issued.

***

### Exports (external integration)

Run your own ticket flow (an NPC seller, a booth, a phone app, your own economy) and still use the built-in ticket item, ticket viewer and door check. These grant and consume the **same** `train_ticket` the machines do, so the `tickets.requireForDoors` gate keeps working unchanged. All are **server-side** exports.

{% hint style="info" %}
These work with or without an inventory resource. In standalone mode (`integrations.inventory = 'none'`) they read and write the script's own ticket store. See [Standalone mode](#standalone-mode-integrations-inventory-none).
{% endhint %}

#### `giveTicket(source, opts?)`

Grants a ticket. **It does not charge money.** Your system handles payment; this only adds the ticket.

```lua
local ok, ticket = exports.prompt_train_script:giveTicket(src, {
    from      = 'Sandy Shores',  -- optional, default 'Station'
    to        = 'Los Santos',    -- optional, default 'Destination'
    departure = '14:30',         -- optional, default current time (HH:MM)
    arrival   = '15:05',         -- optional, default ''
    -- number        = '123456',      -- optional, default random 6-digit
    -- passengerName = 'John Smith',  -- optional, default the player's character name
})

if ok then
    -- `ticket` is the granted ticket table
else
    -- `ticket` is an error string, e.g. 'Invalid source'
end
```

| Return            | Type                | Description                                                |
| ----------------- | ------------------- | ---------------------------------------------------------- |
| `ok`              | `boolean`           | `true` on success                                          |
| `ticket` \| `err` | `table` \| `string` | The ticket table on success, or an error string on failure |

It fails with `'Invalid source'` if the player isn't online, or `'Could not add ticket to inventory'` if the item or store write fails.

#### `hasTicket(source)`

```lua
if exports.prompt_train_script:hasTicket(src) then
    -- player holds a train ticket
end
```

Returns `boolean`.

#### `takeTicket(source, count?)`

Consumes tickets. Use it for single-use boarding driven by your own system.

```lua
local removed = exports.prompt_train_script:takeTicket(src)      -- removes 1
local removed = exports.prompt_train_script:takeTicket(src, 2)   -- removes 2
```

| Param    | Type      | Description                     |
| -------- | --------- | ------------------------------- |
| `source` | `number`  | Player server id                |
| `count`  | `number?` | How many to remove, default `1` |

Returns `boolean`: `true` if a ticket was removed.

#### Example: sell a ticket from an NPC with your own economy

```lua
RegisterNetEvent('myscript:buyFromNpc', function()
    local src = source
    -- charge with your framework however you like
    if not MyEconomy.charge(src, 50) then return end

    local ok, ticket = exports.prompt_train_script:giveTicket(src, {
        from = 'Sandy Shores', to = 'Los Santos', departure = '14:30',
    })
    if not ok then MyEconomy.refund(src, 50) end
end)
```

***

## Version 1

Everything below applies to **1.0.x** (latest: 1.0.4.1).

### How It Works

1. A player walks up to a ticket machine and an interaction prompt appears (via `ox_target`, `qb-target`, or the built-in `[E]` prompt when neither is installed).
2. The DUI-based ticket UI opens, showing available trains and their ETAs.
3. The player selects a destination and confirms the purchase.
4. The server deducts money, adds a `train_ticket` item to the inventory with ticket metadata, and closes the UI.
5. The player can use the ticket item from their inventory to display it on-screen.

***

### Configuration

#### Prices

In `config/config.lua`:

```lua
tickets = {
    defaultPrice = 50,  -- price used for any station not listed below
    prices = {
        ['paletobay']  = 30,   -- override price for Paleto Bay
        ['lossantos1'] = 80,   -- override price for LS platform 1
    },
}
```

Prices are per journey, deducted in the currency defined by `paymentMethod` (`'cash'` or `'bank'`).

#### Ticket Machines

```lua
tickets = {
    machines = {
        {
            station = 'paletobay',       -- must match a key in config.stations
            label   = 'Paleto Bay',      -- displayed in the UI header
            coords  = {
                vec3(168.706, 6380.335, 30.486),
                vec3(169.260, 6379.342, 30.486),
                -- one vec3 per physical machine object
            },
            model = 1906803940,          -- prop model hash
            txd   = 'i45pt_pts_ticketmachine_prop',
            txn   = 'script_rt_ticketmachine_screen_paleto',
        },
    },
}
```

| Field         | Description                                                               |
| ------------- | ------------------------------------------------------------------------- |
| `station`     | Station ID — determines which route ETAs are shown and the ticket price   |
| `label`       | Title displayed at the top of the ticket machine UI                       |
| `coords`      | Array of `vec3` positions — one per physical kiosk object in the world    |
| `model`       | Model hash of the prop used as the machine (for interaction registration) |
| `txd` / `txn` | Texture dictionary and name to replace with the DUI ticket display        |

***

### Adding a Ticket Machine

#### Step 1 — Find the prop

Go to the location in-game and identify the prop used as the ticket machine. You need its **model hash** and the **txd/txn** of the screen texture. CodeWalker or similar tools can give you these values.

#### Step 2 — Add to config

```lua
{
    station = 'mystation',
    label   = 'My Station',
    coords  = {
        vec3(100.0, 200.0, 30.0),
    },
    model = -1234567890,              -- your prop hash
    txd   = 'my_prop_txd',
    txn   = 'my_screen_texture',
},
```

#### Step 3 — Add the station (if not already present)

```lua
stations = {
    mystation = {
        nodes = { lossantos = 1234 },
    },
},
```

The machine is now functional. No additional scripting is needed.

***

### Standalone Servers (no inventory)

With `inventory = 'none'` (or when no supported inventory is detected), the whole ticket system works without any inventory resource:

* Purchased tickets are stored by the script itself in `standalone_tickets.json`, keyed by the player's license — they survive server restarts and reconnects.
* Tickets stay valid for **24 hours** after purchase.
* Players re-display their latest ticket with the `/trainticket` command (this replaces "using" the inventory item).
* The wagon door check (`requireTicketForDoors`) keeps working unchanged.

{% hint style="info" %}
On standalone servers you do **not** need to register the `train_ticket` item — the snippets below only apply when a real inventory resource is used.
{% endhint %}

***

### Inventory Item

The ticket is stored as a `train_ticket` item. You must add this item to your inventory resource:

**ox\_inventory** (`items.lua` or equivalent):

```lua
['train_ticket'] = {
    label   = 'Train Ticket',
    weight  = 10,
    stack   = false,
    close   = true,
    consume = 0,
},
```

**QBCore** (`items.lua`):

```lua
['train_ticket'] = {
    name        = 'train_ticket',
    label       = 'Train Ticket',
    weight      = 100,
    type        = 'item',
    image       = 'train_ticket.png',
    unique      = true,
    useable     = true,
    shouldClose = true,
    combinable  = nil,
    description = 'A train ticket',
},
```

The item is registered as useable automatically by `config/server.lua` for QBx, QB, and ESX. When used, the ticket UI appears showing the journey details.

***

### Ticket Metadata

Each ticket item contains the following metadata:

```lua
{
    from        = 'paletobay',      -- origin station key
    to          = 'lossantos1',     -- destination station key
    fromLabel   = 'Paleto Bay',
    toLabel     = 'Los Santos',
    departure   = '14:32',          -- estimated departure time (HH:MM)
    arrival     = '15:05',          -- estimated arrival time
    playerName  = 'John Smith',
    price       = 50,
}
```

This metadata is embedded in the inventory item and used to render the ticket display when the player uses the item.

***

### Payment

The deduction is handled by `config/server.lua` via `Bridge.removePayment(source, amount)`. The bridge automatically uses the correct framework call based on what is detected:

| Framework | Method                                                        |
| --------- | ------------------------------------------------------------- |
| QBx       | `exports.qbx_core:RemoveMoney(source, paymentMethod, amount)` |
| QBCore    | `Player.Functions.RemoveMoney(paymentMethod, amount)`         |
| ESX       | `xPlayer.removeMoney()` / `xPlayer.removeAccountMoney()`      |
| None      | Always returns `true` (free tickets — useful for testing)     |

If the player cannot afford the ticket, the purchase is rejected and no item is given.

***

### Exports (External Integration)

Run your own ticket UX — an NPC seller, a booth, a phone app, a custom economy — and still use the built-in board gate, ticket item, and door check. These grant/consume the **same** `train_ticket` the machines do, so the ticket viewer and the `requireTicketForDoors` gate keep working unchanged. All are **server-side** exports.

{% hint style="info" %}
These work with or without an inventory resource. On standalone servers (`inventory = 'none'`) they read/write the script's own ticket store — see [Standalone Servers (no inventory)](#standalone-servers-no-inventory).
{% endhint %}

#### `giveTicket(source, opts?)`

Grants a ticket. **Does not charge money** — your system handles payment; this only adds the ticket.

```lua
local ok, ticket = exports.prompt_train_script:giveTicket(src, {
    from      = 'Sandy Shores',  -- optional, default 'Station'
    to        = 'Los Santos',    -- optional, default 'Destination'
    departure = '14:30',         -- optional, default current time (HH:MM)
    arrival   = '15:05',         -- optional, default ''
    -- number        = '123456',      -- optional, default random 6-digit
    -- passengerName = 'John Smith',  -- optional, default the player's character name
})

if ok then
    -- `ticket` is the granted ticket table (see Ticket Metadata)
else
    -- `ticket` is an error string, e.g. 'Invalid source'
end
```

| Return | Type | |
| ------ | ---- | - |
| `ok` | `boolean` | `true` on success |
| `ticket` \| `err` | `table` \| `string` | the ticket table on success, or an error string on failure |

Fails with `'Invalid source'` if the player isn't online, or `'Could not add ticket to inventory'` if the item/store write fails.

#### `hasTicket(source)`

```lua
if exports.prompt_train_script:hasTicket(src) then
    -- player holds a valid train ticket
end
```

Returns `boolean`.

#### `takeTicket(source, count?)`

Consumes ticket(s) — use for single-use boarding driven by your own system.

```lua
local removed = exports.prompt_train_script:takeTicket(src)      -- removes 1
local removed = exports.prompt_train_script:takeTicket(src, 2)   -- removes 2
```

| Param | Type | |
| ----- | ---- | - |
| `source` | `number` | player server id |
| `count` | `number?` | how many to remove, default `1` |

Returns `boolean` — `true` if a ticket was removed.

#### Example — sell a ticket from an NPC with your own economy

```lua
RegisterNetEvent('myscript:buyFromNpc', function()
    local src = source
    -- charge with your framework however you like
    if not MyEconomy.charge(src, 50) then return end

    local ok, ticket = exports.prompt_train_script:giveTicket(src, {
        from = 'Sandy Shores', to = 'Los Santos', departure = '14:30',
    })
    if not ok then MyEconomy.refund(src, 50) end
end)
```
