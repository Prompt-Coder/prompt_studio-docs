---
description: Connect YouTool Furniture Store to Prodigy Studios prp-property. Nothing to copy; purchases arrive as Placeable Furniture in the property's furniture storage or mailbox.
icon: house-user
---

# prp-property

prp-property (Prodigy Studios) works without copying anything into it. YouTool hands each purchase to prp-property, which puts it in the property as an unplaced **Placeable Furniture** item. The owner places it with prp-property's furnish mode, like furniture bought in prp-property itself.

**Tested with:** prp-property 1.1.0 and prp-bridge 1.1.7. **Minimum:** 1.1.0. Older builds only accept furniture from prp-property's own list, so most YouTool products would be refused (and refunded). The setup check reports an older version (see [Setup check](#setup-check)).

***

### Install

{% stepper %}
{% step %}
#### Install prp-property as Prodigy's guide says

Run prp-property **1.1.0 or newer** with **prp-bridge** and its other dependencies, set up as Prodigy's installation guide describes.
{% endstep %}

{% step %}
#### Make sure the furniture item exists

Deliveries are `placeable_furniture_item` items. The item is part of prp-property's own install (Items). On ox\_inventory it looks like this in `ox_inventory/data/items.lua`:

```lua
["placeable_furniture_item"] = {
    label = "Placeable Furniture",
    weight = 1000,
    stack = false,
    close = true,
    consume = 0,
},
```

Without it nothing can be delivered and every buyer is refunded. The setup check reports a missing item on ox\_inventory.
{% endstep %}

{% step %}
#### Start prp-property before YouTool

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure ox_doorlock
ensure prp-bridge
ensure prp-property
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}

The console shows:

```
[YouTool Store] Housing adapter: prp-property
```
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they have several.
2. Each piece arrives as a **Placeable Furniture** item with the YouTool name and picture. prp-property puts it in a placed **Furniture Storage** in the property, or, when there is none, in the property's **mailbox**.
3. The owner takes it out and places it with prp-property's furnish mode.

The picker lists the properties the player **owns**, plus properties where they hold a key or rent with the **FURNISH** privilege. YouTool checks this again on the server before it charges anything.

**How much fits.** The mailbox holds **5 pieces**. A placed Furniture Storage (prp-property furniture, Shelves) holds **12** in prp-property 1.1.0. If the storage or mailbox fills up halfway through an order, the pieces that didn't fit are refunded at the price the player paid and the rest is kept. Place what's waiting, then buy the rest.

**What the pieces do in prp-property.** Models prp-property already lists keep its own category, so a fridge works as a fridge. Other YouTool products get the closest prp-property category: storage furniture becomes a cabinet with storage, refrigerators become fridges, beds become beds, chairs and benches become seating, and everything else is decoration.

Removing a placed piece in prp-property gives the item back, not money, so there is no sell-back price to watch.

***

### Setup check

When everything is right:

```
  [ OK ] Housing: prp-property 1.1.0
  [ OK ] prp-property: furniture delivery export found
```

Problems it reports:

```
  [FAIL] prp-property 1.0.10 only takes furniture from its own list, so most YouTool products would be refused
         -> Update prp-property to 1.1.0 or newer.
  [FAIL] prp-property: the furniture delivery export (AddFurnitureToProperty) is missing
         -> Update prp-property to 1.1.0 or newer.
  [FAIL] prp-property: the item placeable_furniture_item is not in ox_inventory, so nothing can be delivered
         -> Add placeable_furniture_item to ox_inventory/data/items.lua as the prp-property installation guide shows (Items), then restart the server.
```

To test one real delivery, run `youtool_setup <playerId>` in the server console with a property owner online. It puts one Disposable Coffee Cup into their first property. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>Part of the order was refunded</summary>

The property's mailbox or Furniture Storage was full. The console shows `[YouTool prp-property] property <id>: its furniture storage / mailbox is full, <n> of <m> item(s) refunded`. Place the waiting pieces, or place a Furniture Storage, then buy the rest.

</details>

<details>

<summary>Every purchase is refunded</summary>

Run `youtool_setup <playerId>` and fix the `[FAIL]` lines. The usual causes are a prp-property older than 1.1.0 or a missing `placeable_furniture_item` item.

</details>

<details>

<summary>The furniture isn't in the property</summary>

Purchases aren't placed automatically. Look in the property's Furniture Storage and mailbox for **Placeable Furniture** items, then place them with furnish mode.

</details>
