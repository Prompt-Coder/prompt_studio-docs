---
description: Connect YouTool Furniture Store to rcore_housing. Nothing to copy; purchases land in the property's furniture stock, or arrive as an rcore delivery.
icon: house-chimney-window
---

# rcore\_housing

rcore\_housing works without any install step. YouTool hands each purchase to rcore\_housing, which puts it in the property's **furniture stock**. The owner places it with rcore's furniture editor. If you prefer rcore's own delivery (a box and pallet at the property), YouTool can use that instead.

**Tested with:** rcore\_housing 1.1.4. **Minimum:** 1.1.4. Older builds don't list apartments for their owners, so players in a starter apartment couldn't check out. The setup check reports an older version (see [Setup check](#setup-check)).

***

### Install

{% stepper %}
{% step %}
#### Update rcore\_housing

Make sure you run rcore\_housing **1.1.4 or newer**.
{% endstep %}

{% step %}
#### Start rcore\_housing before YouTool

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure rcore_housing_assets
ensure rcore_housing
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}

The console shows:

```
[YouTool Store] Housing adapter: rcore_housing
```
{% endstep %}

{% step %}
#### Move rcore's own furniture shop

rcore\_housing ships with a furniture shop NPC at `vec4(2746.39, 3469.59, 55.66)`, which is inside the YouTool store in Sandy Shores. Move or remove that entry in `Config.Furniture.Shop.Locations` in `rcore_housing/config.lua`, so players don't find two furniture shops in one spot. The setup check warns while they overlap.
{% endstep %}

{% step %}
#### Choose how purchases arrive (optional)

{% code title="config/housing.lua" %}
```lua
Config.RcoreHousing = {
  deliveryDelay = 0,
}
```
{% endcode %}

| `deliveryDelay` | What happens |
| --- | --- |
| `0` (default) | The furniture goes straight into the property's furniture stock. |
| Minutes, for example `5` | rcore's own delivery runs: after that many minutes a box and pallet appear in the property's **DELIVERY** zone, and the owner carries it in. YouTool sends one delivery per product, so an order with 3 different products arrives as 3 boxes. |

With a delay, the property needs a DELIVERY zone (`/housing` › property › zones), or the box has nowhere to appear. rcore's own `Config.Furniture.DeliverySystem` and `DeliveryTime` don't apply to YouTool orders; only `deliveryDelay` does.
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they have several.
2. The items go into that property's **furniture stock** in rcore\_housing (or, with a delay, arrive as an rcore delivery).
3. The owner places them with rcore's furniture editor.

The picker lists the properties rcore\_housing returns for the player: the ones they **own or rent**. YouTool checks this again on the server before it charges anything, so a player can't send furniture into someone else's property.

**Models rcore doesn't have.** The first time a YouTool model is delivered, rcore\_housing adds it to its own furniture list (`rcore_housing_furniture`, marked as an add-on) with the item's name, its YouTool picture, the closest rcore category and the YouTool **corporate base price**. rcore keeps that row from then on. Models rcore already ships keep rcore's own name, picture and price.

rcore\_housing lets owners sell furniture from stock back for its price in that list. That is why YouTool registers the corporate base and not the price the buyer paid: selling back never returns more than the store's cost.

If rcore refuses a product, that product is refunded at the price paid and the rest of the order is kept. If rcore refuses everything, the whole order is refunded and the player sees *"Failed to add furniture to house"*.

***

### Setup check

When everything is right:

```
  [ OK ] Housing: rcore_housing 1.1.4
  [ OK ] rcore_housing: furniture delivery export found
```

While rcore's furniture shop NPC stands inside a YouTool store:

```
  [WARN] rcore_housing: its own furniture shop NPC stands inside the YouTool store YouTool Furniture Store - Sandy Shores
         -> Move or remove that entry in Config.Furniture.Shop.Locations in rcore_housing/config.lua, so players do not get two furniture shops in one spot.
```

On a build that is too old, or that lacks the delivery export:

```
  [FAIL] rcore_housing 1.0.9 is too old: it lists no apartments for their owners
         -> Update rcore_housing to 1.1.4 or newer.
  [FAIL] rcore_housing: the furniture delivery export (RegisterFurnitureDelivery) is missing
         -> Update rcore_housing to 1.1.4 or newer.
```

To test one real delivery, run `youtool_setup <playerId>` in the server console with a property owner online. It puts one Disposable Coffee Cup into their first property:

```
  [ OK ] Properties owned by player 2: 1
  [ OK ] Delivery test: Disposable Coffee Cup arrived in Starter Apartments #2
```

See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>A player in a starter apartment gets "You need to own a house to purchase furniture"</summary>

Update rcore\_housing to 1.1.4 or newer. Older builds don't return apartments inside a building for their owner.

</details>

<details>

<summary>With a delivery delay, the box never shows up</summary>

The property has no DELIVERY zone. Add one in `/housing` › property › zones, or set `deliveryDelay = 0` so purchases go straight into stock.

</details>

<details>

<summary>The furniture isn't in the property</summary>

With `deliveryDelay = 0`, look in the property's furniture **stock** in rcore's furniture editor, not in the room: purchases aren't placed automatically. Then run `youtool_setup <playerId>` and check the delivery test line.

</details>

<details>

<summary>A YouTool item shows the wrong name or price in rcore's menus</summary>

rcore keeps the row from the first delivery of each model, and models rcore already ships keep rcore's own. Change them in rcore\_housing's furniture list (`/housing` › All Furniture) if you want different values there. The YouTool store's prices are not affected.

</details>
