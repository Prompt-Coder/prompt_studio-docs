---
description: Connect YouTool Furniture Store to rtx_housing. Copy one file; purchases land in the property's interior furniture inventory.
icon: house-chimney
---

# rtx\_housing

You copy one YouTool file into `rtx_housing/configs/`. On every start it adds the YouTool props that rtx\_housing doesn't have yet to rtx's furniture list; no rtx\_housing file is changed. Purchases then go into the property's interior furniture inventory, and the player places them from the rtx\_housing furniture menu.

**Tested with:** rtx\_housing 30.6 (28.0 was also tested). YouTool needs rtx\_housing 28.0 or newer.

{% hint style="warning" %}
**rtx\_housing 30 loads a property's furniture only when someone enters the property.** Until then, rtx\_housing accepts new furniture but never saves it. YouTool checks this before it delivers: if the property's furniture isn't loaded yet, the purchase is refunded and the player sees *"Enter this property once, then buy again (rtx\_housing has not loaded its furniture yet)"*. After the owner has entered the property once, deliveries work until the next server restart.
{% endhint %}

***

### Install

{% stepper %}
{% step %}
#### Copy the props file into rtx\_housing

```
FROM: prompt_youtool_store_system/integrations/rtx-housing/zz_youtool_props.lua
TO:   rtx_housing/configs/zz_youtool_props.lua
```

rtx\_housing loads every file in `configs/` by itself, so you don't change its `fxmanifest.lua`. **Keep the file name.** rtx\_housing loads these files in alphabetical order, and the `zz_` makes this one load after rtx's own `furniture.lua`. If it loads first, it registers nothing.

Props rtx\_housing already ships are not added twice. Keep the `YOUTOOL_INSTALL` block at the top of the file (the setup check reads it), and always copy the file from the YouTool version you are running.
{% endstep %}

{% step %}
#### Turn off sell-back for unplaced furniture

rtx\_housing lets players sell unplaced furniture back for a percentage of rtx\_housing's own price. For props rtx\_housing already ships, that price can be higher than the YouTool price, so a player could buy in the YouTool store and sell back at a profit. Unless you have checked your prices, turn it off in `rtx_housing/config.lua`:

{% code title="rtx_housing/config.lua" %}
```lua
Config.FurnitureSystem = {
    -- ...the other options stay as they are...
    sellback = { enabled = false, percent = 50 },
}
```
{% endcode %}

rtx\_housing ships with `sellback = { enabled = true, percent = 50 }`.
{% endstep %}

{% step %}
#### Restart

```
restart rtx_housing
restart prompt_youtool_store_system
```

The console shows:

```
[YouTool RTX Patch] Injected <n> props into Config.Furnitures (2112 catalog items checked)
[YouTool Store] Housing adapter: rtx_housing
```

`<n>` is the number of YouTool props rtx\_housing didn't have yet.
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they own several.
2. The items go into that property's **interior** furniture inventory. rtx\_housing stores furniture per property.
3. Inside the property, the player opens the rtx\_housing furniture menu and places the items.

If the property's furniture isn't loaded yet (nobody has entered it since the server started), the purchase is refunded, see the warning at the top.

***

### Setup check

When everything is right:

```
  [ OK ] Housing: rtx_housing 30.6
  [ OK ] rtx_housing: YouTool install file loaded (v1, <n> items)
```

Typical problems:

| Line | Fix |
| --- | --- |
| `[FAIL] rtx_housing: the YouTool install file is missing` | Copy the file (step 1) and restart rtx\_housing. |
| `[FAIL] rtx_housing: the YouTool install file is an old copy` | Copy the file from your current YouTool over the old one and restart rtx\_housing. |
| `[FAIL] rtx_housing: the install file is there but is not loaded` | `restart rtx_housing` (or the whole server). |
| `[FAIL] rtx_housing: the install file ran but failed: loaded before furniture.lua` | The file loads before rtx's `furniture.lua`. Name it `zz_youtool_props.lua` and restart rtx\_housing. |
| `[FAIL] rtx_housing: the install file ran but failed: catalog.json not found` | The YouTool folder was renamed. Rename it back to `prompt_youtool_store_system`. |

The live delivery test (`youtool_setup <playerId>`) uses the player's first property. On rtx\_housing 30, have that player enter the property once before you run it, or the test fails with the "Enter this property once" message. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>"Enter this property once, then buy again (rtx_housing has not loaded its furniture yet)"</summary>

rtx\_housing 30 hasn't loaded that property's furniture since the server started. The player was refunded. Enter the property once, then buy again.

</details>

<details>

<summary>Purchased items are not visible in the furniture menu</summary>

Restart rtx\_housing, then check the setup check for the install file line.

</details>

<details>

<summary>"You don't own this property"</summary>

YouTool only delivers to properties rtx\_housing lists as owned by the player. The player must pick one of their own properties at checkout.

</details>
