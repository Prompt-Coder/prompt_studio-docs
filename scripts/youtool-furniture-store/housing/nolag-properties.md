---
description: Connect YouTool Furniture Store to nolag_properties. Copy one file; purchases land in the property's furniture storage.
icon: house-chimney
---

# nolag\_properties

nolag\_properties only accepts furniture that is listed in its own furniture configuration. You copy one YouTool file into nolag\_properties; it adds the whole YouTool catalog to nolag's furniture list every time nolag starts. Purchases then go into the property's furniture storage, and the player places them with the nolag decorator.

**Tested with:** nolag\_properties 2.4.12. **Minimum:** 2.4.10. Older builds load custom furniture files on the client only, so nolag's server refuses YouTool items.

***

### Install

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

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app.
2. Checkout asks **Inside** or **Outside**, then which property, if they own several. With one property, the inside/outside choice is the only question.
3. The items are stored in that property's furniture storage: **Inside** for the house, **Outside** for the yard (nolag's outside furniture), for example a hot tub or garden furniture.
4. The player opens the nolag decorator, inside the house or in the yard, and places the items from storage.

To always deliver inside and skip the question, set `outsideDelivery = false` in `integrations/nolag-properties/client/config.lua` and restart YouTool.

In nolag's furniture menu, YouTool items are listed in a **YouTool Store** category, and also in nolag's matching categories (sofas, chairs, tables, beds, storage, kitchen, bathroom, lighting and so on).

Only properties the player owns receive deliveries; rented properties don't.

***

### Setup check

When everything is right:

```
  [ OK ] Housing: nolag_properties 2.4.12
  [ OK ] nolag_properties: YouTool install file loaded (v1, <n> items)
```

Typical problems:

| Line | Fix |
| --- | --- |
| `[FAIL] nolag_properties: the YouTool install file is missing` | Copy the file (step 1) and restart nolag\_properties. |
| `[FAIL] nolag_properties: the YouTool install file is an old copy` | Copy the file from your current YouTool over the old one and restart nolag\_properties. |
| `[FAIL] nolag_properties: the install file is there but is not loaded` | `restart nolag_properties` (or the whole server). |
| `[FAIL] nolag_properties: the install file ran but failed: YouTool not started within 60 s` | `prompt_youtool_store_system` didn't start within 60 seconds of nolag. Make sure it is in `server.cfg` and starts without errors, then restart nolag\_properties. |
| `[FAIL] nolag_properties: the install file ran but failed: catalog.json not found` | The YouTool folder was renamed. Rename it back to `prompt_youtool_store_system`. |
| `[WARN] Housing: nolag_properties 2.4.9 is older than 2.4.12, the version we tested` | Update nolag\_properties. Below 2.4.10, purchases are refused. |

To test one real delivery, run `youtool_setup <playerId>` with a player who owns a property online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>The purchase fails with "nolag rejected all models"</summary>

nolag\_properties refused every item, and the player was refunded. Usually the catalog file isn't loaded or nolag is older than 2.4.10. Run `youtool_setup` and fix the `[FAIL]` lines, then restart nolag\_properties.

If only some items are refused, the player sees *"nolag rejected N/M models (likely not whitelisted for indoor placement)"* and is refunded for those items.

</details>

<details>

<summary>There is no "YouTool Store" category in nolag's furniture menu</summary>

The catalog file is in the wrong folder, is an old copy, or nolag wasn't restarted after you copied it. The path must be exactly `nolag_properties/custom/furniture/youtool_catalog.lua`.

</details>

<details>

<summary>Items show a blank picture</summary>

nolag has no picture for those models. Copy the pictures as described in install step 4.

</details>
