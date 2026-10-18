---
description: Install YouTool Furniture Store, set the server.cfg order, give admin and store owner rights, read the setup check, and update safely.
icon: download
---

# Installation

{% stepper %}
{% step %}
#### Put both resources in your server

Download both from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+YouTool+Furniture+Store) and copy the two folders into your `resources` directory:

| Folder | What it is |
| --- | --- |
| `prompt_youtool` | The store map: the store interior and the price tag models |
| `prompt_youtool_store_system` | The script |

The map has two optional steps of its own, door locks for `ox_doorlock` and the Truck You Repairs compatibility files: see the [map page](../../civilian-maps/youtool-furniture-store-2-locations.md).

{% hint style="warning" %}
Keep the folder names exactly as they are. The install files you copy into your housing script read the catalog from a folder named `prompt_youtool_store_system`, and so do the item images. The setup check reports a renamed folder as a `[FAIL]`.
{% endhint %}
{% endstep %}

{% step %}
#### Add them to server.cfg

Start everything YouTool uses **before** `prompt_youtool_store_system`:

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure ox_target                     # or qb-target
ensure qb-core                       # or qbx_core / es_extended; leave out on a standalone server
ensure qs-housing                    # your housing script (only one)
ensure lb-phone                      # optional: the YouTool phone app (or sky_phone)
ensure prompt_youtool
ensure prompt_youtool_store_system

add_ace group.admin youtool.admin allow
```
{% endcode %}

Why the order matters:

* `ox_lib` is a hard dependency. FiveM refuses to start YouTool without it.
* The target script (`ox_target` or `qb-target`) is detected the moment YouTool loads. If it starts later, players get no target options on the furniture and the till.
* The framework and the housing script are detected when YouTool starts.
* If you start resources by folder (`ensure [standalone]`), make sure those folders come before YouTool.

The `add_ace` line gives everyone in `group.admin` the **corporate admin** permission, `youtool.admin`. Corporate admins can edit base prices and product names and see the Console button in every store. To give it to one player instead, use their license: `add_ace identifier.license:<license> youtool.admin allow`. If you changed `Config.Roles.corporateAce` in `config.lua`, use that name instead.

{% hint style="info" %}
Corporate admin does **not** make you a store owner. Markup, vault, staff and the other store tools come from being a store's owner or staff (step 5).
{% endhint %}
{% endstep %}

{% step %}
#### Do your housing script's install step

Most housing scripts need a small change on their side: a file copied from `prompt_youtool_store_system/integrations/<script>/` into the housing script, a setting, or a manifest line. Open the page for your script and follow it:

[Housing Integrations](housing/README.md): [qs-housing](housing/qs-housing.md) · [ps-housing](housing/ps-housing.md) · [nolag\_properties](housing/nolag-properties.md) · [bcs\_housing](housing/bcs-housing.md) · [rtx\_housing](housing/rtx-housing.md) · [RxHousing](housing/rxhousing.md) · [vms\_housing](housing/vms-housing.md) · [brutal\_housing](housing/brutal-housing.md) · [rcore\_housing](housing/rcore-housing.md)

You don't need to tell YouTool which script you run. It detects it by itself.
{% endstep %}

{% step %}
#### Restart and read the setup check

Restart the server. About 15 seconds after YouTool starts, it prints a **setup check** in the server console (also the txAdmin Live Console). It checks your housing script and its version, whether the install step is done, your framework and money, `oxmysql`, the target script, the map, the language file, and risky settings. Problems come with a `->` line that says how to fix them.

The check runs again by itself about 8 seconds after your housing script restarts, so you can fix something, restart the housing script, and read the new result. To print it at any time, type this in the **server console**:

```
youtool_setup
```

**Then test one real delivery.** Pick an online player who owns a property and pass their server ID:

```
youtool_setup 2
```

YouTool delivers one free Disposable Coffee Cup (`prop_coffee_cup_trailer`) into that player's first property and checks that it arrived. A passing result looks like this:

{% code title="Server console" %}
```
[YouTool] ── setup check ────────────────────────────────────────
  [ OK ] Housing: bcs_housing 4.24.0
  [ OK ] bcs_housing: YouTool install file present (v1)
  [ OK ] bcs_housing: furniture shop mode is on
  [ OK ] Framework: qbcore, money: auto
  [ OK ] Properties owned by player 2: 1
  [ OK ] Delivery test: Disposable Coffee Cup arrived in <property name>
  Everything looks good.
  Support code: YT 1.0.0 | qbcore | bcs_housing 4.24.0 | install ok | 0 fail 0 warn | delivery ok
```
{% endcode %}

A passed delivery test is remembered per housing script version in `data/setup_state.json`, so later checks don't drop another cup into someone's property. To run it again anyway, add `force`: `youtool_setup 2 force`. The cup is a real item in that property.

If you see `[WARN]` or `[FAIL]` lines, fix them first. [Troubleshooting](troubleshooting.md) explains every message.

{% hint style="info" %}
`youtool_setup` works only from the server console. Typed in game, it does nothing.
{% endhint %}
{% endstep %}

{% step %}
#### Make someone the store owner

Each store has one owner. The owner holds every store permission, hires staff and decides what each position may do in the Console's Staff tab. A new store has no owner, so set one for each store you use.

Run this in the **server console**:

```
youtool_setowner <playerId|citizenid> <storeId>
```

| Store | `storeId` |
| --- | --- |
| Sandy Shores | `youtool_sandy` |
| Davis | `youtool_vespucci` |

For example, `youtool_setowner 2 youtool_sandy` makes the player with server ID 2 the owner of the Sandy Shores store. A server ID only works while that player is online. For an offline player, pass their character identifier instead: the citizenid on QBCore and QBox, the identifier on ESX. The console confirms it:

```
[YouTool Roles] ABC12345 is now OWNER of youtool_sandy
```

* On QBCore, QBox and ESX the owner is a **character**, not a player account. Another character of the same player is not the owner.
* Running the command again for the same store replaces the owner.
* If the new owner is inside the store when you run it, they leave and come back in to see the Console.
* In game, `/youtool_setowner` works for corporate admins who may also run restricted commands (the `command.youtool_setowner` ACE; many server.cfg files grant all commands to admins with `add_ace group.admin command allow`). The result is still printed in the server console.

Next: [Staff & Permissions](console/staff-and-permissions.md).
{% endstep %}

{% step %}
#### Adjust the settings (optional)

Open `config.lua` to set the language, `Config.EconomyScale` (multiplies every price), and the stock mode. Feature settings live in the `config/` folder. Changes take effect when the resource restarts. See [Configuration](configuration.md) and [Languages](languages.md).
{% endstep %}
{% endstepper %}

***

### The `data/` folder

YouTool saves each store's state as JSON files in `prompt_youtool_store_system/data/`. These files are your server's data: back them up, and never replace them with the copies from a new download.

| File | What it holds |
| --- | --- |
| `store_roles.json` | Store owners, staff and positions |
| `store_vaults.json` | Vault balances and the vault activity list |
| `store_sales.json` | Sales history |
| `markup.json` | Markup of every store |
| `store_stock.json` | Stock levels (Active mode) |
| `freight_shipments.json` | Freight orders on their way |
| `store_placements.json` | Display furniture and price tags placed in the stores |
| `store_sets.json` | Furniture sets and their displays |
| `catalog_overrides.json` | Corporate changes: base prices, product names and delisted products |
| `entity_set_state.json` | Floor Map zones switched on or off |
| `player_carts.json` | Carts players left without checking out |
| `setup_state.json` | Delivery tests that passed |

`store_placements.json` and `store_sets.json` also come with the download, empty: staff place the display furniture, price tags and sets themselves. Your copies hold everything your staff placed, so keep yours. `catalog.json` is not in the table: it is the catalog itself, so always take the new one when you update.

YouTool writes these files a few seconds after a change and when the resource stops, so stop the resource or the server before you copy them.

***

### Updating from an older version

{% stepper %}
{% step %}
#### Stop the server and back up

Stop the server, then copy the whole `prompt_youtool_store_system` folder somewhere safe.
{% endstep %}

{% step %}
#### Replace the folder, then restore your files

Put the new `prompt_youtool_store_system` in place, then copy back from your backup:

* The `data/` files from the table above (not `catalog.json`).
* `hooks/hooks_server.lua`, `hooks/hooks_client.lua` and `hooks/hooks_shared.lua`. YouTool only creates these from the `.example.lua` files when they are missing, so your copies are used as they are.
* Any language file you added yourself, for example `localization/it.lua`.

Then bring your changes over to the new copies of the files you edited, instead of copying the old files over the new ones, since a new version can add settings and texts:

* `config.lua` and the files in `config/`
* `integrations/<script>/client/config.lua` (per-integration settings)
* `localization/<lang>.lua`, if you edited a language. Texts added in the new version show in English until you translate them. See [Languages](languages.md).
* `server/framework.lua`, if you added your own money functions at the bottom of it (`Config.MoneySystem = 'custom'`)
{% endstep %}

{% step %}
#### Start and read the setup check

If a YouTool install file in your housing script is out of date, the setup check says `the YouTool install file is an old copy` and tells you which file to copy where.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
**Updating your housing script** can undo its YouTool install step. Every brutal\_housing update removes the YouTool lines from its `fxmanifest.lua`, every RxHousing update undoes the manifest change, and a ps-housing update overwrites `server/sv_property.lua`. Redo the step from your script's [housing page](housing/README.md); the setup check reports it as a `[FAIL]` until you do.
{% endhint %}
