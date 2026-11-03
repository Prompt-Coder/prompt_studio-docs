---
description: Connect YouTool Furniture Store to nolag_properties. On 3.x nothing to copy; on 2.4.x copy one file. Purchases land in the property's stored furniture.
icon: house-chimney
---

# nolag\_properties

nolag\_properties only delivers furniture that is in its own furniture catalog. On **nolag 3.x** YouTool adds its products to that catalog by itself; on **2.4.x** you copy one YouTool file into nolag. Purchases then go into the property's stored furniture, and the owner places them with nolag's furniture menu.

**Tested with:** nolag\_properties 3.0.0 and 2.4.12. **Minimum:** 2.4.10. Older builds load custom furniture files on the client only, so nolag's server refuses YouTool items.

***

### Install

{% tabs %}
{% tab title="nolag 3.x" %}
Nothing to copy into nolag\_properties.

{% stepper %}
{% step %}
#### Start nolag\_properties before YouTool

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure bob74_ipl
ensure nolag_properties_assets
ensure nolag_properties
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}
{% endstep %}

{% step %}
#### Let YouTool add its products, then restart nolag once

nolag 3.x keeps its furniture catalog in the database. When YouTool starts, it adds the products nolag doesn't list yet:

```
[YouTool NoLag] furniture catalog: +705 YouTool products added, 0 repriced, 1407 already listed
```

nolag reads its catalog when it starts, so restart it once after that first start:

```
restart nolag_properties
```

From then on the console shows `+0 YouTool products added` and the setup check is green. YouTool adds new products the same way after a YouTool update; the setup check tells you when nolag needs another restart.
{% endstep %}
{% endstepper %}

**What YouTool adds to nolag's catalog:** the products nolag doesn't list, in the collection **YouTool**, with YouTool's names, prices and picture links. They are marked **Disabled** in nolag's Furniture Catalog: hidden from nolag's own furniture shop, so nolag doesn't sell YouTool's products, but delivered and placed like any other furniture. Models nolag already lists keep nolag's own entry.

{% hint style="info" %}
**Updating nolag from 2.x to 3.x:** follow nolag's own guide and back up the database first (the first 3.0 start imports the 2.x data and drops the old tables). The old `custom/furniture/youtool_catalog.lua` isn't used by 3.x and goes away with the old folder. YouTool pieces that were still in storage are imported by nolag and can be placed again once YouTool has added its products and nolag was restarted.
{% endhint %}
{% endtab %}

{% tab title="nolag 2.4.x" %}
{% stepper %}
{% step %}
#### Copy the catalog file into nolag\_properties

```
FROM: prompt_youtool_store_system/integrations/nolag-properties/nolag_install/youtool_catalog.lua
TO:   nolag_properties/custom/furniture/youtool_catalog.lua
```

nolag\_properties loads every `.lua` file in `custom/furniture/` by itself, so you don't change its `fxmanifest.lua`. Keep the `YOUTOOL_INSTALL` block at the top of the file; the setup check reads it.

Always copy the file from the YouTool version you are running. When you update YouTool, copy it again if the setup check says it is an old copy.
{% endstep %}

{% step %}
#### Start nolag\_properties before YouTool

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure nolag_properties
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}

The catalog file waits up to 60 seconds for `prompt_youtool_store_system` to start, then registers the items.
{% endstep %}

{% step %}
#### Restart nolag\_properties

```
restart nolag_properties
```

The console shows how many items were registered (the numbers depend on your catalog):

```
[YouTool x NoLag] Registered 2112 items in YouTool category, <n> in existing categories
```
{% endstep %}

{% step %}
#### Add item pictures (optional)

nolag's furniture menu shows a picture for each item from `nolag_properties/web/build/images/props/<model>.webp`. Items without a picture there show a blank picture. To add them, copy the `.webp` files from `prompt_youtool_store_system/images/` into `nolag_properties/web/build/images/props/`.
{% endstep %}
{% endstepper %}

In nolag's furniture menu, YouTool items are listed in a **YouTool Store** category, and also in nolag's matching categories (sofas, chairs, tables, beds, storage, kitchen, bathroom, lighting and so on).
{% endtab %}
{% endtabs %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app.
2. Checkout asks **Inside** or **Outside**, then which property, if they own several. With one property, the inside/outside choice is the only question.
3. The items are stored in that property's furniture storage: **Inside** for the house, **Outside** for the yard (nolag's outside furniture), for example a hot tub or garden furniture.
4. The player opens nolag's furniture menu, inside the house or in the yard, and places the items from **Stored Furniture**.

To always deliver inside and skip the question, set `outsideDelivery = false` in `integrations/nolag-properties/client/config.lua` and restart YouTool.

Only properties the player owns receive deliveries; rented properties don't.

***

### Setup check

When everything is right on nolag 3.x:

```
  [ OK ] Housing: nolag_properties 3.0.0
  [ OK ] nolag_properties: YouTool products are in its furniture catalog
```

On nolag 2.4.x:

```
  [ OK ] Housing: nolag_properties 2.4.12
  [ OK ] nolag_properties: YouTool install file loaded (v1, <n> items)
```

Typical problems:

| Line | Fix |
| --- | --- |
| `[WARN] nolag_properties: <n> YouTool products were just added to its furniture catalog; it can deliver them after its next restart` | 3.x: `restart nolag_properties` once. |
| `[FAIL] nolag_properties: YouTool could not add its products to the furniture catalog (nolag_furniture_items), so they cannot be delivered` | 3.x: look for the `[YouTool NoLag]` line in the server console (usually a database error), then restart nolag\_properties. |
| `[FAIL] nolag_properties: the YouTool install file is missing` | 2.4.x: copy the file (step 1) and restart nolag\_properties. |
| `[FAIL] nolag_properties: the YouTool install file is an old copy` | 2.4.x: copy the file from your current YouTool over the old one and restart nolag\_properties. |
| `[FAIL] nolag_properties: the install file is there but is not loaded` | 2.4.x: `restart nolag_properties` (or the whole server). |
| `[FAIL] nolag_properties: the install file ran but failed: YouTool not started within 60 s` | 2.4.x: `prompt_youtool_store_system` didn't start within 60 seconds of nolag. Make sure it is in `server.cfg` and starts without errors, then restart nolag\_properties. |
| `[FAIL] nolag_properties: the install file ran but failed: catalog.json not found` | The YouTool folder was renamed. Rename it back to `prompt_youtool_store_system`. |
| `[WARN] Housing: nolag_properties 2.4.9 is older than 3.0.0, the version we tested` | Update nolag\_properties. Below 2.4.10, purchases are refused. |

To test one real delivery, run `youtool_setup <playerId>` with a player who owns a property online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>After updating nolag to 3.x, purchases are refunded ("nolag rejected ...")</summary>

nolag 3.x only delivers what is in its database catalog, and it reads that catalog when it starts. Restart nolag\_properties once after YouTool has added its products (the setup check says so), then try again.

</details>

<details>

<summary>The purchase fails with "nolag rejected all models"</summary>

nolag\_properties refused every item, and the player was refunded. On 3.x, restart nolag\_properties once (see above). On 2.4.x, the catalog file usually isn't loaded or nolag is older than 2.4.10. Run `youtool_setup` and fix the `[FAIL]` lines, then restart nolag\_properties.

If only some items are refused, the player sees *"nolag rejected N/M models (likely not whitelisted for indoor placement)"* and is refunded for those items.

</details>

<details>

<summary>YouTool products don't appear in nolag's furniture shop (3.x)</summary>

That's intended: YouTool's products are sold by the YouTool store. In nolag's Furniture Catalog they are in the **YouTool** collection and marked Disabled, which hides them from nolag's shop. Delivered pieces are in **Stored Furniture**.

</details>

<details>

<summary>There is no "YouTool Store" category in nolag's furniture menu (2.4.x)</summary>

The catalog file is in the wrong folder, is an old copy, or nolag wasn't restarted after you copied it. The path must be exactly `nolag_properties/custom/furniture/youtool_catalog.lua`.

</details>

<details>

<summary>Items show a blank picture (2.4.x)</summary>

nolag has no picture for those models. Copy the pictures as described in install step 4.

</details>
