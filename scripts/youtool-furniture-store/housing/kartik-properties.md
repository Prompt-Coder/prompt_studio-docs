---
description: Connect YouTool Furniture Store to kartik-properties. Nothing to copy; purchases arrive unplaced in the modeler's Delivered tab.
icon: house-laptop
---

# kartik-properties

kartik-properties works without copying anything into it. YouTool hands each purchase to kartik-properties, which puts it **unplaced** in the property. The owner places it from the **Delivered** tab in the kartik-properties furniture modeler.

**Tested with:** kartik-properties 1.1.3.

**Needs:** a kartik-properties version with the `AddPropertyFurniture` export (added for YouTool; update to the latest version). The setup check reports a build without it (see [Setup check](#setup-check)).

***

### Install

{% stepper %}
{% step %}
#### Update kartik-properties

Run the **latest** kartik-properties.
{% endstep %}

{% step %}
#### Start kartik-properties before YouTool

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure kartik-properties
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}

The console shows:

```
[YouTool Store] Housing adapter: kartik-properties
```
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they have several.
2. The pieces land **unplaced** in that property.
3. The owner opens the furniture modeler and places them from the **Delivered** tab.

The picker lists the properties the player **owns or leases**. A key to someone else's property is not enough. YouTool checks this again on the server before it charges anything.

**Products kartik-properties doesn't list.** The first time one is delivered, YouTool adds it to kartik-properties' furniture catalogue with its YouTool name, marked **not for sale**, so kartik-properties' own shop doesn't sell it. kartik-properties forgets these entries when it restarts, so YouTool adds them again whenever kartik-properties or YouTool starts, and pieces already delivered stay placeable.

**Furniture limits.** kartik-properties caps the pieces per property (`Config.MaxFurniture`, 60 by default, and a per-model maximum). If a property fills up halfway through an order, the pieces that didn't fit are refunded at the price the player paid and the rest is kept. A product kartik-properties won't add to its catalogue is refunded the same way. A property without a usable interior (its shell pack isn't running) takes nothing, so the whole order is refunded.

Delivered pieces never pay anything back in kartik-properties: removing one puts it back in the house.

***

### Setup check

When everything is right:

```
  [ OK ] Housing: kartik-properties 1.1.3
  [ OK ] kartik-properties: furniture delivery export found
```

On a newer kartik-properties the housing line is `[INFO]` and names the version YouTool was tested with.

On a build without the delivery export:

```
  [FAIL] kartik-properties: the furniture delivery export (AddPropertyFurniture) is missing, so nothing can be delivered
         -> Update kartik-properties to its latest version (AddPropertyFurniture was added for YouTool).
```

To test one real delivery, run `youtool_setup <playerId>` in the server console with a property owner online. It puts one Disposable Coffee Cup into their first property. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>Part of the order was refunded</summary>

The property reached its furniture limit (`limit_reached`), the property has no usable interior (`no_interior`, its shell pack isn't running), or kartik-properties refused a product. The console shows `[YouTool kartik-properties] <model> refused for property <id>: <reason>` for each one.

</details>

<details>

<summary>The furniture isn't in the property</summary>

Purchases aren't placed automatically. Open the furniture modeler in the property and look in the **Delivered** tab. Then run `youtool_setup <playerId>` and check the delivery test line.

</details>
