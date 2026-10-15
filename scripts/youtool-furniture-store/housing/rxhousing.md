---
description: Connect YouTool Furniture Store to RxHousing (rxscripts). Copy one file and change one manifest line; purchases land in the property's furniture inventory.
icon: house-chimney
---

# RxHousing (rxscripts)

RxHousing only accepts furniture that is listed in its own `Config.Furniture`. You copy one YouTool file into RxHousing and change one line in its `fxmanifest.lua`; the file then adds the whole YouTool catalog as a **YouTool Store** category every time RxHousing starts. Purchases go into the property's furniture inventory, and the player places them with RxHousing's placer.

**Tested with:** RxHousing 2.5.0 (v2.4.x is also supported). **Resource name:** `RxHousing` (the default) or `rxscripts_housing`. Any other folder name isn't detected.

{% hint style="warning" %}
**Every RxHousing update replaces `fxmanifest.lua`.** After each update, redo step 2, or YouTool purchases are rejected because the YouTool Store category no longer loads. The setup check shows `[FAIL] RxHousing: the install file is there but is not loaded` until you do.
{% endhint %}

***

### Install

{% stepper %}
{% step %}
#### Copy the catalog file into RxHousing

```
FROM: prompt_youtool_store_system/integrations/rxscripts/rxhousing_install/youtool_catalog.lua
TO:   RxHousing/config/furniture/youtool_catalog.lua
```

It reads YouTool's catalog when RxHousing starts and adds one new category, **YouTool Store**. RxHousing's own furniture is not changed. Keep the `YOUTOOL_INSTALL` block at the top of the file (the setup check reads it), and always copy the file from the YouTool version you are running.
{% endstep %}

{% step %}
#### Load the file from RxHousing's fxmanifest.lua

Open `RxHousing/fxmanifest.lua`. In the `shared_script { ... }` block near the top, find:

```lua
'config/furniture/furniture.lua',
```

and replace it with:

```lua
'config/furniture/*.lua',
```

RxHousing then loads every `.lua` file in `config/furniture/`: its own `furniture.lua` and the YouTool file. The files load in alphabetical order, so RxHousing's catalog comes first and the YouTool category is added after it.
{% endstep %}

{% step %}
#### Refresh and restart

A changed `fxmanifest.lua` is only read after `refresh`:

```
refresh
restart RxHousing
restart prompt_youtool_store_system
```

The console shows:

```
[YouTool RxHousing] registered 2112 items into Config.Furniture["YouTool Store"]
[YouTool Store] Housing adapter: rxscripts
```

(The number depends on your catalog.)
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they own several.
2. The items appear right away in that property's inventory in RxHousing's furniture menu, under **YouTool Store**.
3. The player places them with RxHousing's placer.

The item pictures in that category load from YouTool, so there is nothing to copy for them. Sell-back through RxHousing is switched off for this category, so YouTool purchases can't be refunded through RxHousing.

***

### Setup check

When everything is right:

```
  [ OK ] Housing: RxHousing 2.5.0
  [ OK ] RxHousing: YouTool install file loaded (v1, <n> items)
```

Typical problems:

| Line | Fix |
| --- | --- |
| `[FAIL] RxHousing: the YouTool install file is missing` | Copy the file (step 1) and restart RxHousing. |
| `[FAIL] RxHousing: the YouTool install file is an old copy` | Copy the file from your current YouTool over the old one and restart RxHousing. |
| `[FAIL] RxHousing: the install file is there but is not loaded` | The manifest change (step 2) is missing, often after an RxHousing update. The fix line reads: `In RxHousing/fxmanifest.lua change 'config/furniture/furniture.lua' to 'config/furniture/*.lua' in shared_scripts, run refresh, then restart it. Every RxHousing update undoes this.` |
| `[FAIL] RxHousing: the install file ran but failed: catalog.json not found` | The YouTool folder was renamed. Rename it back to `prompt_youtool_store_system`. |

To test one real delivery, run `youtool_setup <playerId>` with a player who owns a property online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>"RxHousing rejected the item"</summary>

The YouTool Store category didn't load. Check step 2 (saved, then `refresh`), restart RxHousing, and look for the `registered ... items into Config.Furniture["YouTool Store"]` line in the console.

</details>

<details>

<summary>"YouTool catalog not loaded yet — try again in a moment"</summary>

YouTool was started a moment ago and is still reading its catalog. Wait a few seconds and check out again.

</details>

<details>

<summary>The console shows <code>[YouTool Store] Housing adapter: custom</code></summary>

RxHousing wasn't detected. The resource must be named `RxHousing` or `rxscripts_housing` and must be running when YouTool starts. Rename the folder if needed, then restart `prompt_youtool_store_system`.

</details>

<details>

<summary>Duplicate label warning in the RxHousing logs</summary>

An item name exists both in the YouTool catalog and in RxHousing's own `furniture.lua`. Remove the duplicate from RxHousing's `furniture.lua`.

</details>
