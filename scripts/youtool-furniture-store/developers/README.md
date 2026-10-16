---
description: What is open in YouTool, the bridges you can adapt, and how to connect an unsupported housing or inventory script with a custom adapter.
icon: code
---

# For Developers

YouTool's core is encrypted by Tebex escrow, but the parts you need to fit it to your server are open: settings, texts, hooks, the framework, target and housing bridges, and a small set of exports.

<table data-view="cards"><thead><tr><th></th><th></th><th data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Hooks</strong></td><td>Allow, block or react to purchases, markup, vault, freight, staff and more</td><td><a href="hooks.md">hooks.md</a></td></tr><tr><td><strong>Exports &#x26; Events</strong></td><td>What your other resources can ask YouTool or tell it, including the logistics partner contract</td><td><a href="exports-and-events.md">exports-and-events.md</a></td></tr></tbody></table>

To deliver into a housing or inventory script YouTool doesn't support, see [Custom housing](#custom-housing) below.

***

## What's open

Escrow only encrypts `.lua` files. HTML, JavaScript, CSS, images and `data/*.json` are always readable. These Lua files are listed in `escrow_ignore` in `fxmanifest.lua` and ship open:

| Files | What they are |
| --- | --- |
| `fxmanifest.lua`, `config.lua`, `config/*.lua` | Settings ([Configuration](../configuration.md)) |
| `integrations/<script>/client/config.lua` | Per-integration settings |
| `localization/*.lua` | Texts ([Languages](../languages.md)) |
| `hooks/*.lua` | Your hook files ([Hooks](hooks.md)) |
| `server/framework.lua` | Framework and money bridge |
| `client/target_wrapper.lua` | Target script bridge |
| `integrations/<script>/server/adapter.lua`, `integrations/<script>/client/sync.lua`, `integrations/qs-housing/server/catalog_sync.lua` | The nine housing integrations |
| The install files in `integrations/` | The files you copy into your housing script |
| `server/test_commands.lua` | `/youtool_diag` and `/youtool_testall` |
| `integrations/<script>/README.md` | Install guides |

***

## Bridges

If your server runs a modified or newer version of a framework, target script or housing script, you can adapt these files yourself.

| File | What it does |
| --- | --- |
| `server/framework.lua` | Detects QBox (`qbx_core`), QBCore (`qb-core`), ESX (`es_extended`) or standalone, in that order. Provides the player identifier (citizenid, ESX identifier, or license on standalone), character names for the Staff tab and Vault list, and money. `Config.MoneySystem = 'custom'` calls your own functions at the bottom of this file ([Custom money](../configuration.md#custom-money)). |
| `client/target_wrapper.lua` | Translates YouTool's ox\_target-style options to ox\_target or qb-target, chosen by `Config.interactionMode`. |
| `integrations/<script>/server/adapter.lua` | One adapter per supported housing script: ownership, the property list for the checkout picker, and the delivery itself. They follow the contract in [Custom housing](#custom-housing). |
| `integrations/<script>/client/sync.lua` | The client half of an integration, where a housing script needs one. |

{% hint style="warning" %}
When you update YouTool, the new version brings new copies of these files. Bring your changes over to the new copies instead of copying your old files over them.
{% endhint %}

***

## Custom housing

When no supported housing script is running, YouTool runs in **custom** mode. The server console shows `[YouTool Store] Housing adapter: custom`, and every checkout is refused before any money is taken until you connect an adapter. Players see *"No housing system configured on this server (custom mode - see server console)"*.

A custom adapter connects any housing or inventory script: you write three functions, YouTool calls them at checkout.

### How YouTool picks the adapter

One second after YouTool starts, it looks for a supported housing script (list and order: [How YouTool picks the housing script](../housing/README.md#how-youtool-picks-the-housing-script)). If it finds one, that integration is used. If it finds none, it uses your custom adapter.

A registration through the export (option 1 below) made **after** that detection always wins, even over a supported script. A custom adapter set as a global inside YouTool (option 2) is only used when no supported script runs.

### The contract

| Function | Required | Returns |
| --- | --- | --- |
| `PlayerOwnsHouse(src)` | yes | `true` if the player has at least one property to deliver to. |
| `GetPlayerHouses(src)` | yes | A list of properties: `{ { id = 'H18', name = 'Beach House', address = 'Del Perro' }, ... }`. `id` is a string or number and is passed back to `AddFurniture`; `name` and the optional `address` are shown in the checkout picker. With one property the picker is skipped. |
| `AddFurniture(src, houseId, furniture)` | yes | `true` if the item was delivered, else `false, 'reason'`. `furniture` is one unit: `{ model, name, price, base, stockClass }`. |
| `AddMultipleFurniture(src, houseId, items)` | no | `allOk, deliveredCount, errorMessage, deliveredIdx`. `items` is a list of units, most expensive first. `deliveredIdx` lists the positions in `items` that arrived. |
| `VerifyFurniturePlaced(src, houseId, model)` | no | How many items of `model` the property holds now (a number). Lets the setup check's delivery test confirm the item was really saved. |

How YouTool uses the answers:

* Without `AddMultipleFurniture`, YouTool calls `AddFurniture` once per unit.
* The player pays only for units that arrived and is refunded for the rest. If you return `deliveredCount` without a matching `deliveredIdx`, YouTool counts the first `deliveredCount` items (the most expensive ones) as delivered.
* If nothing arrived, the player gets a full refund and sees the `errorMessage` from `AddMultipleFurniture`, or *"Failed to add furniture to house"*.

{% hint style="danger" %}
**Check ownership in `AddFurniture`.** The `houseId` comes from the property the player picked on their own client. Every shipped adapter checks that the player owns that property before delivering; yours must too.
{% endhint %}

### Option 1: from your own resource

Export the three functions from a resource of your own and register it by name. YouTool stores the name and calls your exports (functions can't be passed through an export, so it takes the resource name, not a table). The optional functions are not used this way: YouTool delivers one item at a time.

{% code title="my_housing_bridge/server.lua" %}
```lua
-- Replace the bodies with calls into your housing or inventory script.
exports('PlayerOwnsHouse', function(src)
    return #MyHousing.GetOwned(src) > 0
end)

exports('GetPlayerHouses', function(src)
    local list = {}
    for _, h in ipairs(MyHousing.GetOwned(src)) do
        list[#list + 1] = { id = h.id, name = h.label, address = h.street }
    end
    return list
end)

exports('AddFurniture', function(src, houseId, furniture)
    if not MyHousing.IsOwner(src, houseId) then return false, 'Not your property' end
    return MyHousing.GiveFurniture(houseId, furniture.model) == true
end)

local function register()
    exports.prompt_youtool_store_system:RegisterHousingAdapter(GetCurrentResourceName())
end

-- Register after YouTool has started and finished its own detection, and again
-- whenever YouTool restarts (a restart forgets the registration).
CreateThread(function()
    while GetResourceState('prompt_youtool_store_system') ~= 'started' do Wait(500) end
    Wait(2000)
    register()
end)

AddEventHandler('onResourceStart', function(res)
    if res == 'prompt_youtool_store_system' then
        SetTimeout(2000, register)
    end
end)
```
{% endcode %}

On success the console prints `[YouTool Store] custom housing adapter registered -> resource "my_housing_bridge"`. `RegisterHousingAdapter` returns `false` (and prints why) if you pass something other than a resource name or the resource isn't started.

### Option 2: inside YouTool

Set the global `CustomHousingAdapter` in a server file of YouTool itself, for example at the bottom of the open `server/framework.lua`. This way you can also supply `AddMultipleFurniture` and `VerifyFurniturePlaced`.

{% code title="server/framework.lua (bottom of the file)" %}
```lua
CustomHousingAdapter = {
    label = 'my housing',
    PlayerOwnsHouse = function(src) return #MyHousing.GetOwned(src) > 0 end,
    GetPlayerHouses = function(src) --[[ as above ]] end,
    AddFurniture    = function(src, houseId, furniture) --[[ as above ]] end,
}
```
{% endcode %}

Inside YouTool, set the global; don't call `RegisterHousingAdapter`.

### Test it

* `youtool_housing <playerId>` in the server console shows the adapter in force and asks it whether that player owns a property and how many ([Commands](../commands.md#setup-and-diagnostics)).
* `youtool_setup <playerId>` runs the setup check with a live delivery of one free coffee cup into that player's first property.
