---
description: Connect YouTool Furniture Store to brutal_housing (Brutal Scripts). Copy one file and add one manifest line in two places.
icon: house-chimney
---

# brutal\_housing

brutal\_housing only keeps furniture whose model is in its own furniture list (`Config.Furnitures`) and silently drops anything else. You copy one YouTool file into brutal\_housing and add it to brutal's `fxmanifest.lua`; the file then adds the YouTool models brutal doesn't ship as a **YouTool Store** category every time brutal\_housing starts. Purchases are added to the property's furniture, and the player arranges them with brutal\_housing's placement tool.

**Tested with:** brutal\_housing 2.1.0 (2.0.8 was also tested).

{% hint style="warning" %}
**Every brutal\_housing update replaces `fxmanifest.lua`.** After each update, add the two lines from step 2 again. The setup check shows a `[FAIL]` line for brutal\_housing until you do.
{% endhint %}

***

### Install

{% stepper %}
{% step %}
#### Copy the catalog file into brutal\_housing

```
FROM: prompt_youtool_store_system/integrations/brutal-housing/brutal_install/youtool_catalog.lua
TO:   brutal_housing/configs/youtool_catalog.lua
```

The file only adds models brutal\_housing doesn't already ship, each one once. brutal stores one furniture entry for every category that lists a model, so a model listed twice would be delivered twice.

**If you installed an older copy of this file, replace it.** The old copy listed all 2,112 models and doubled about 600 of them on delivery. Keep the `YOUTOOL_INSTALL` block at the top of the file (the setup check reads it), and always copy the file from the YouTool version you are running.
{% endstep %}

{% step %}
#### Add it to brutal\_housing's fxmanifest.lua

In **both** the `client_scripts { ... }` and the `server_scripts { ... }` block, add this line **right after** `'configs/furnitures.lua',`:

```lua
'configs/youtool_catalog.lua',
```

On brutal\_housing 2.1.0 the start of the two blocks then looks like this (the rest of each block stays as it is):

{% code title="brutal_housing/fxmanifest.lua" %}
```lua
client_scripts {
	'config.lua',
	'configs/furnitures.lua',
	'configs/youtool_catalog.lua',
	'configs/interiors.lua',
	'configs/apartments.lua',
```
{% endcode %}

{% code title="brutal_housing/fxmanifest.lua" %}
```lua
server_scripts {
	'@mysql-async/lib/MySQL.lua',
	'config.lua',
	'configs/furnitures.lua',
	'configs/youtool_catalog.lua',
	'configs/interiors.lua',
	'configs/apartments.lua',
```
{% endcode %}

It must come **after** `'configs/furnitures.lua'` in both blocks: loaded earlier, brutal's own file replaces the list and the YouTool category is lost.
{% endstep %}

{% step %}
#### Check server.cfg

{% code title="server.cfg" %}
```
ensure ox_lib
ensure brutal_housing
ensure prompt_youtool_store_system
```
{% endcode %}

`oxmysql` must also be running.
{% endstep %}

{% step %}
#### Refresh and restart

A changed `fxmanifest.lua` is only read after `refresh`:

```
refresh
restart brutal_housing
restart prompt_youtool_store_system
```

The console shows (numbers on brutal\_housing 2.1.0):

```
[YouTool brutal_housing] registered 1484 items into Config.Furnitures["YouTool Store"] (628 already in brutal or duplicated, skipped)
[YouTool Store] Housing adapter: brutal_housing
```
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they own several. brutal\_housing properties are listed by their brutal ID (for example `H245`).
2. brutal\_housing only adds furniture through the player's own game, so YouTool sends each item to the buyer's game, which hands it to brutal\_housing. The items go out about a quarter of a second apart, so a large order takes a few seconds.
3. brutal\_housing adds each item to the property. The player moves the items into place with brutal\_housing's own placement tool.

**Storage limit.** brutal\_housing saves all of a property's furniture as one block of data and sends it in a single network message, which FiveM caps at 64 KB. Once a property gets close to that, further placements would disconnect the owner. YouTool keeps an eye on the size and stops before that point. The items that don't fit are refunded, and the player sees *"This property is full — some items could not be placed (you were refunded for them)"*. If nothing fits, the whole order is refunded.

***

### Setup check

When everything is right:

```
  [ OK ] Housing: brutal_housing 2.1.0
  [ OK ] brutal_housing: YouTool install file loaded (v1, 1484 items)
```

Typical problems:

| Line | Fix |
| --- | --- |
| `[FAIL] brutal_housing: the YouTool install file is missing` | Copy the file (step 1), do step 2 if you haven't, then `refresh` and restart brutal\_housing. |
| `[FAIL] brutal_housing: the YouTool install file is an old copy` | Copy the file from your current YouTool over the old one and restart brutal\_housing. |
| `[FAIL] brutal_housing: the install file is there but is not loaded` | The manifest lines (step 2) are missing, often after a brutal\_housing update. |
| `[FAIL] brutal_housing fxmanifest: 'configs/youtool_catalog.lua' is missing from client_scripts` | The line is only in one block. Add it to the block named in the message. |
| `[FAIL] brutal_housing fxmanifest: in client_scripts, 'configs/youtool_catalog.lua' loads before 'configs/furnitures.lua'` | Move the line below `'configs/furnitures.lua'` in that block. |

The manifest lines all come with the same fix line:

```
         -> In brutal_housing/fxmanifest.lua add 'configs/youtool_catalog.lua' right after 'configs/furnitures.lua' in BOTH client_scripts and server_scripts, run refresh, then restart it. Every brutal_housing update removes these lines.
```

To test one real delivery, run `youtool_setup <playerId>` with a player who owns a property online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>Some items are delivered twice</summary>

You are running an old copy of `brutal_housing/configs/youtool_catalog.lua`. Copy the current file from YouTool over it (step 1), then `refresh` and `restart brutal_housing`. The console line should show items as skipped, for example `(628 already in brutal or duplicated, skipped)`.

</details>

<details>

<summary>Purchases vanish: paid, but nothing in the property</summary>

brutal\_housing drops models that aren't in its furniture list. The YouTool file isn't loaded: check step 2, run `refresh` and `restart brutal_housing`, then read the setup check.

</details>

<details>

<summary>"You don't own this property"</summary>

YouTool only delivers to properties where the player is the owner in brutal\_housing. Having a key isn't enough.

</details>

<details>

<summary>"This property is full — some items could not be placed"</summary>

The property has reached brutal\_housing's storage limit (see [Storage limit](#how-players-get-the-furniture)). Remove furniture from that property, or deliver to another one.

</details>
