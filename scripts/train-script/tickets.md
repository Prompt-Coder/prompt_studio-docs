---
description: >-
  Players can purchase train tickets from interactive kiosk machines placed at
  stations. Tickets are inventory items with embedded metadata showing origin,
  destination, and departure time.
icon: ticket
---

# Tickets

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
