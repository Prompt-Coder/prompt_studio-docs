---
description: YouTool's server and client exports and the logistics partner contract, the shipmentCreated event and the FreightArrived export.
icon: right-left
---

# Exports & Events

Call exports as `exports.prompt_youtool_store_system:Name(...)`. Keep the resource name as it is: the exports, the housing install files and the item images all use it.

***

## Server exports

| Export | Returns | Use |
| --- | --- | --- |
| `RegisterHousingAdapter(resourceName)` | `true` / `false` | Connect your own housing or inventory resource. See [Custom housing](README.md#custom-housing). |
| `FreightArrived(shipmentId)` | `true`, or `false, reason` | A logistics partner reports that a shipment reached the store. See [Logistics partner](#logistics-partner). |
| `RequestFreight(storeId, order, who)` | `ok, result` | Order freight for a store from another resource. |

### RequestFreight

Orders freight the same way the Console's Stock tab does, paid from the store's vault and delivered with `Config.Delivery.mode`. It is a server-to-server call: there is no permission check and no hook.

{% code title="your_resource/server.lua" %}
```lua
local ok, result = exports.prompt_youtool_store_system:RequestFreight('youtool_sandy', { seating = 2, clutter = 1 }, 'my_resource')
if not ok then print('freight refused: ' .. tostring(result)) end
```
{% endcode %}

* `order` is `{ [class] = pallets }` with the nine stock classes (`clutter`, `lighting`, `soft`, `electronics`, `surfaces`, `seating`, `storage`, `fixtures`, `bulky`). A class is only filled up to its capacity.
* `who` is written into the vault ledger (default `'logistics'`).
* It refuses with `false, 'Active mode only'`, `false, 'Nothing to order'` or `false, 'Insufficient vault balance'`, or with the reason from the delivery (for example when the store already has an order on its way).
* On success, `result` is `{ points, cost }` in `'instant'` mode, or `{ shipment = true, id, arriving }` when a shipment was created (`arriving` = milliseconds until arrival where YouTool knows it).

***

## Client exports

| Export | Returns | Use |
| --- | --- | --- |
| `isInsideStore()` | boolean | Is the local player inside a YouTool store. |
| `getCurrentStore()` | table or `nil` | The `Config.Stores` entry of the store the player is in (`id`, `name`, ...). |
| `getCurrentInteriorId()` | number or `nil` | Interior id of that store. |
| `isTabletVisible()` | boolean | Is the tablet open. |
| `showTablet()` / `hideTablet()` / `toggleTablet()` | — | Open or close the tablet. `showTablet` respects the `tablet.canOpen` [hook](hooks.md) but not the store check, so it opens anywhere; checkout still only works inside a store. |
| `isPhoneAppOpen()` | boolean | Is the YouTool phone app open. |
| `isPreviewActive()` | boolean | Is the player in the 3D item preview. |
| `isCarryingFreightBox()` | boolean | Is the player carrying a freight box. |
| `isPlacing()` | boolean | Is a manager placing a display or price tag. Only exists while `Config.PriceTags.enabled = true`. |

{% code title="your_resource/client.lua" %}
```lua
-- e.g. keep your own E-key interaction quiet while the YouTool tablet is in use
if exports.prompt_youtool_store_system:isTabletVisible() then return end
```
{% endcode %}

The other client exports in YouTool's files exist for YouTool's own scripts (placement, price-tag textures, sets) and are not meant to be called from outside.

***

## Logistics partner

With `Config.Delivery.mode = 'logistics'`, freight orders are delivered by a resource of your own, for example a trucking job. YouTool handles the order, the money and the unloading at the dock; your resource handles the trip.

{% code title="config/delivery.lua" %}
```lua
-- in Config.Delivery:
  mode           = 'logistics',

-- and below it:
Config.Logistics = {
  enabled         = true,
  resource        = 'my_logistics',   -- your resource's name
  fallbackDelayMs = 0,
}
```
{% endcode %}

{% stepper %}
{% step %}
#### A manager orders freight

The store vault pays the freight (and, with `unloadWage.source = 'vault'`, the unloading wages) up front. YouTool creates the shipment; a store has one at a time.
{% endstep %}

{% step %}
#### YouTool fires `youtool:freight:shipmentCreated`

If `Config.Logistics.enabled` is `true` and your resource is started, YouTool triggers this **server** event with the shipment:

| Field | Value |
| --- | --- |
| `shipmentId` | String id, pass it back to `FreightArrived` |
| `storeId` | `'youtool_sandy'` or `'youtool_vespucci'` |
| `warehouse` | Key of the store's warehouse in `config/delivery_layout.lua` (`'grapeseed'` or `'terminal'`) |
| `dockCenter` | `vector3` of the store's dock |
| `pallets` | `{ { class, points }, ... }`, one entry per pallet |

If your resource isn't running (or `enabled` is `false`), there is no event: the pallets arrive by themselves after `fallbackDelayMs`.
{% endstep %}

{% step %}
#### Your resource delivers and calls `FreightArrived`

When the run reaches the store, call the export from your **server** code. Only the resource named in `Config.Logistics.resource` may call it.

```lua
local ok, reason = exports.prompt_youtool_store_system:FreightArrived(shipmentId)
```

It returns `true`, or `false` with `'not the logistics partner'`, `'not in transit'` or `'unknown shipment id'`.
{% endstep %}

{% step %}
#### Employees unload

The pallets appear on the store's dock and employees unload them as in every other mode. With `requireUnload = false` the stock is credited at once instead. See [Unloading pallets](../console/stock-and-freight.md#unloading-pallets).
{% endstep %}
{% endstepper %}

{% code title="my_logistics/server.lua" %}
```lua
AddEventHandler('youtool:freight:shipmentCreated', function(shipment)
    -- shipment.shipmentId, shipment.storeId, shipment.warehouse, shipment.dockCenter, shipment.pallets
    StartMyDeliveryRun(shipment, function()
        exports.prompt_youtool_store_system:FreightArrived(shipment.shipmentId)
    end)
end)
```
{% endcode %}

Good to know:

* A shipment handed to your resource has no timeout. It waits until you call `FreightArrived` or a manager cancels the order in the Console.
* YouTool doesn't tell your resource about a cancellation; a later `FreightArrived` returns `false, 'unknown shipment id'`.
* Shipments survive a YouTool restart (`data/freight_shipments.json`) and keep their id, but the event is not sent again. Keep the ids on your side if your runs can outlive a restart.

***

## Internal events

{% hint style="warning" %}
YouTool's net events and `lib.callback` handlers are not a public contract. They check permissions and the player's position, and they change between versions. To integrate, use the exports and the event on this page and [Hooks](hooks.md).
{% endhint %}
