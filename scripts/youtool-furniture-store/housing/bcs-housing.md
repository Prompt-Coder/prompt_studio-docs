---
description: Connect YouTool Furniture Store to bcs_housing. Copy one file and turn on the furniture shop setting; players place purchases with /furnish.
icon: house-chimney
---

# bcs\_housing

bcs\_housing keeps furniture **per player**, not per house. YouTool puts every purchase into the buyer's own bcs furniture inventory, and the player places it with `/furnish` inside any house they own. You copy one file (the YouTool catalog for bcs) and change two settings in bcs\_housing.

**Tested with:** bcs\_housing 4.24.0 (v4.x).

***

### Install

{% stepper %}
{% step %}
#### Copy the furniture file into bcs\_housing

```
FROM: prompt_youtool_store_system/integrations/bcs-housing/bcs_install/youtool_furniture.lua
TO:   bcs_housing/furniture/others/youtool_furniture.lua
```

bcs\_housing loads every file in its `furniture/` folder by itself, so you don't change its `fxmanifest.lua`. The file lists every YouTool item with a unique name and its price. Without it, YouTool items don't show in `/furnish` and can't be sold back.

The first line of the file, `-- youtoolInstall version = 1 ...`, tells the setup check which copy you have. Keep it, and always copy the file from the YouTool version you are running.
{% endstep %}

{% step %}
#### Turn on furniture shop mode

In `bcs_housing/config/config.lua` set:

{% code title="bcs_housing/config/config.lua" %}
```lua
Config.EnableFurnitureShop = true
Config.FurnitureAsItem = false
```
{% endcode %}

bcs\_housing ships with `EnableFurnitureShop = false`. In that mode `/furnish` sells straight from the catalogue and ignores the furniture a player owns, so YouTool purchases are stored but the player never sees them. `FurnitureAsItem` must stay `false`, because YouTool delivers to the player's furniture storage, not as inventory items.
{% endstep %}

{% step %}
#### Restart

```
restart prompt_youtool_store_system
restart bcs_housing
```

Or restart the whole server.
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app. If they own several houses the property picker still appears, but bcs stores the furniture per player either way.
2. The items go into the player's bcs furniture inventory.
3. Inside any house they own, the player uses `/furnish` and places the items.

Items with the same name are numbered in the bcs list (for example "Bar Cooler", "Bar Cooler #2"), so bcs can tell them apart when a player sells one back.

***

### Setup check

The bcs file is a plain list (nothing in it runs), so the setup check confirms it is there and current, then reads the two settings from `config/config.lua`. When everything is right:

```
  [ OK ] Housing: bcs_housing 4.24.0
  [ OK ] bcs_housing: YouTool install file present (v1)
  [ OK ] bcs_housing: furniture shop mode is on
```

Typical problems:

| Line | Fix |
| --- | --- |
| `[FAIL] bcs_housing: the YouTool install file is missing` | Copy the file (step 1) and restart bcs\_housing. |
| `[FAIL] bcs_housing: the YouTool install file is an old copy` | Copy the file from your current YouTool over the old one and restart bcs\_housing. |
| `[FAIL] bcs_housing: EnableFurnitureShop is off, so players never see the furniture they bought` | Set `Config.EnableFurnitureShop = true` (step 2) and restart bcs\_housing. |
| `[FAIL] bcs_housing: FurnitureAsItem is on, but YouTool delivers to furniture storage` | Set `Config.FurnitureAsItem = false` (step 2) and restart bcs\_housing. |
| `[WARN] bcs_housing: could not read config/config.lua to check the furniture shop setting` | The check looks for a line that starts with `Config.EnableFurnitureShop =`. Make sure that line exists, is not commented out and has no spaces in front of it. |

To test one real delivery, run `youtool_setup <playerId>` with a player who owns a house online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>Purchased items are not in the <code>/furnish</code> menu</summary>

1. `Config.EnableFurnitureShop` must be `true` and `Config.FurnitureAsItem` `false` (step 2).
2. `bcs_housing/furniture/others/youtool_furniture.lua` must be there and current (step 1).
3. Restart bcs\_housing and read the setup check.

</details>

<details>

<summary>The <code>/furnish</code> menu is empty</summary>

No furniture area is set for that house. Use bcs\_housing's `/setarea` inside the house.

</details>

<details>

<summary>The checkout says "You need to own a house to purchase furniture"</summary>

bcs\_housing reports no owned house for that player. The player must buy or be given a house first; keys to someone else's house don't count.

</details>
