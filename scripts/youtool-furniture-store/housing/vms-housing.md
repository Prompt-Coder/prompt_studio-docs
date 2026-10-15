---
description: Connect YouTool Furniture Store to vms_housing. Nothing to copy; YouTool registers its catalog itself and purchases land in the property's stash.
icon: house-chimney
---

# vms\_housing

vms\_housing only accepts furniture models that are registered in its furniture list (the `houses_furniture_list` table). YouTool adds its missing models there by itself when it starts, so there is nothing to copy into vms\_housing. Purchases go into the property's **stash**, and the player places them with vms\_housing's own placement tool.

**Tested with:** vms\_housing 1.5.1. **Minimum:** 1.4.5, the first build with the exports YouTool uses. On an older build, YouTool switches delivery off and prints a message (see [Setup check](#setup-check)).

vms\_housing needs a `mysql-async` compatible database layer. `oxmysql` already provides it, so if you run `oxmysql` there is nothing extra to install.

***

### Install

{% stepper %}
{% step %}
#### Update vms\_housing

Make sure you run vms\_housing **1.4.5 or newer**.
{% endstep %}

{% step %}
#### Start both resources

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure vms_housing
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}

YouTool waits up to 60 seconds for vms\_housing to come up, then registers every catalog model vms\_housing doesn't have yet (the numbers depend on your vms\_housing version and catalog):

```
[YouTool VMS] catalog: +1777 registered, 0 repriced (335 already present)
```

YouTool only **adds** rows. Rows vms\_housing ships, and rows you added yourself, are never changed. YouTool's own rows are marked, and only those are re-priced when your prices change.
{% endstep %}

{% step %}
#### Restart once after the first start

vms\_housing reads its furniture list when **it** starts. On the very first start after installing YouTool, YouTool registers its models after vms\_housing has already read the list. Restart the whole server once (or `restart vms_housing` and then `restart prompt_youtool_store_system`). From then on the models are live.
{% endstep %}

{% step %}
#### Set the price in vms's own menus (optional)

The YouTool models also show up in vms\_housing's own furniture menus, at this price:

catalog price × `Config.EconomyScale` × `priceMultiplier`

{% code title="config/housing.lua" %}
```lua
Config.VmsHousing = {
  priceMultiplier = 1.5,
}
```
{% endcode %}

The default `1.5` is above 1.0 on purpose, so vms's own menus never undercut the YouTool store. When you change it (or `Config.EconomyScale`), YouTool re-prices its own rows on the next start.
{% endstep %}

{% step %}
#### Add item pictures to vms's menus (optional)

YouTool's models have no pictures in vms\_housing's own furniture menus; vms looks for them in `vms_housing/html/images/furniture/<model>.webp`. To add them, copy the `.webp` files from `prompt_youtool_store_system/images/` into that folder. The YouTool store itself is not affected either way.
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they have several.
2. The items go into that property's **stash** in vms\_housing.
3. The player places them with vms\_housing's own placement tool.

Both the **owner and the renter** of a property can receive deliveries (vms\_housing's own access rule).

vms\_housing's furniture limits are respected:

* **Per-model limits** (`Config.FurnitureLimitPerProperty` in vms\_housing) are checked before delivery. Items over the limit are refunded.
* **The property's furniture limit** (`Config.FurnitureLimit` plus upgrades): if an order doesn't fully fit, YouTool delivers what fits and refunds the rest.

The player is only charged for the items that actually landed in the property.

What the player sees when vms\_housing refuses a delivery:

| Message | Cause |
| --- | --- |
| This property doesn't allow furniture placement | The property doesn't allow furniture. |
| The property is busy with another delivery — try again in a moment | Another delivery is running; YouTool already retried once. |
| An item isn't registered with the housing system | A model is missing from vms's furniture list. The console also shows `[YouTool VMS] WARNING: model "<model>" missing from houses_furniture_list — registration gap`. Restart as in step 3. |
| The property's furniture limit (N) is reached | The property is full. |
| This property already has the maximum of one of these items | A per-model limit is reached. |
| Some items exceeded this property's furniture limit (refunded) | Part of the order didn't fit and was refunded. |
| Property not found | The property doesn't exist in vms\_housing. |

***

### Setup check

When everything is right:

```
  [ OK ] Housing: vms_housing 1.5.1
  [ OK ] vms_housing: YouTool catalog registered
```

On the first start after installing YouTool:

```
  [WARN] vms_housing: 1777 YouTool models were just registered; vms sees them after its next restart
         -> Restart vms_housing (or the whole server).
```

The count comes from the moment YouTool started. If you restarted only vms\_housing, the line repeats until YouTool restarts too; restarting the whole server clears it.

On a vms\_housing build without the YouTool exports:

```
  [FAIL] vms_housing: this build has no YouTool exports, delivery is off
         -> Update vms_housing to 1.4.5 or newer.
```

The console also prints `[YouTool VMS] vms_housing build lacks the YouTool exports (AddMultipleFurniture) — update vms_housing. Furniture delivery is disabled.`

To test one real delivery, run `youtool_setup <playerId>` with a player who owns or rents a property online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>Players see "An item isn't registered with the housing system"</summary>

vms\_housing hasn't read YouTool's models yet. Restart the whole server once (install step 3). If it keeps happening, check the console at YouTool's start for the `[YouTool VMS] catalog:` line. `houses_furniture_list unreadable` means the vms\_housing SQL wasn't imported.

</details>

<details>

<summary>vms\_housing errors when YouTool delivers into a property</summary>

Create properties with vms\_housing's own creator (`/housing`). Properties inserted into the `houses` table by hand crash inside vms\_housing's code.

</details>

<details>

<summary>The vms furniture menu sells YouTool models cheaper than the store</summary>

Raise `Config.VmsHousing.priceMultiplier` in `config/housing.lua` and restart YouTool.

</details>
