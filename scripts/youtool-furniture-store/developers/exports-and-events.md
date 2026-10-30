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
| `SetSectionEnabled(storeId, section, enabled)` | `true, changed`, or `false, reason` | Turn a store section (Floor Map zones) on or off. See [Store sections](#store-sections). |
| `IsSectionEnabled(storeId, section)` | `true` / `false` / `nil` | Whether every zone of a section is on. |

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

### Store sections

Turns display furniture in a store on and off from another resource, the same way the Console's [Floor Map](../console/README.md#floor-map) does. The change shows for every player at once, is saved in `data/entity_set_state.json` and survives restarts. It is a server-to-server call: there is no permission check and no hook.

{% code title="your_resource/server.lua" %}
```lua
-- close the garden for an event, open it again later
exports.prompt_youtool_store_system:SetSectionEnabled('youtool_sandy', 'garden', false)
exports.prompt_youtool_store_system:SetSectionEnabled('youtool_sandy', 'garden', true)

-- one zone only
exports.prompt_youtool_store_system:SetSectionEnabled('youtool_vespucci', 'beds_2', false)

if exports.prompt_youtool_store_system:IsSectionEnabled('youtool_sandy', 'garage') then
    -- every garage zone is on
end
```
{% endcode %}

* `storeId` is a store `id` from `Config.Stores` (`youtool_sandy`, `youtool_vespucci`).
* `section` is a whole room or one zone of it. Rooms: `main` (zones 1 to 19), `home` (1 to 10), `beds` (1 to 6), `furniture` (1 to 6), `garden` (1 to 6), `garage` (1 to 5), `staff_storage` (1 and 2). One zone is the room plus its number, as the Floor Map shows it on hover: `garden_3`, `staff_storage_1`. The full entity set name (`youtool_zone_garden_3`, shown in the zone panel) works too. Not case-sensitive.
* `SetSectionEnabled` returns `true` and how many zones changed (`0` when they already were that way), or `false, 'unknown_store'` / `false, 'unknown_section'`.
* `IsSectionEnabled` returns `true` when every zone of the section is on, `false` when at least one is off, and `nil` for an unknown store or section.

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
