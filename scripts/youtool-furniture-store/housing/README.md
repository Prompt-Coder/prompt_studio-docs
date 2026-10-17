---
description: How YouTool delivers furniture into your housing script, the 9 supported scripts, the property picker, and what the setup check verifies.
icon: house
---

# Housing Integrations

YouTool doesn't keep furniture itself. Every purchase is delivered into the buyer's property in your housing script, and the player places it with that script's own furniture or decorate tools. YouTool supports nine housing scripts and detects the one you run by itself, so there is no setting to choose it.

Most scripts need a short install step on their side (one file to copy, sometimes a setting or a manifest line). Each script has its own page with the exact steps.

***

### Supported housing scripts

| Script | Resource name | Tested with | Install step on the housing side | Where the purchase goes |
| --- | --- | --- | --- | --- |
| [qs-housing](qs-housing.md) | `qs-housing` | 5.2.16 (5.3.19+ recommended) | None (item pictures optional) | The house's decoration stash, placed with the qs-housing decorator |
| [ps-housing](ps-housing.md) | `ps-housing` | 2.0.7 | Paste a code block into `server/sv_property.lua` | The property's furniture, placed from the ps-housing Furniture Menu |
| [nolag\_properties](nolag-properties.md) | `nolag_properties` | 2.4.12 | Copy one file | The property's furniture storage, placed with the nolag decorator |
| [bcs\_housing](bcs-housing.md) | `bcs_housing` | 4.24.0 | Copy one file, change two settings | The buyer's own furniture inventory (bcs keeps furniture per player), placed with `/furnish` in any house they own |
| [rtx\_housing](rtx-housing.md) | `rtx_housing` | 30.6 | Copy one file | The property's interior furniture inventory, placed from the rtx\_housing furniture menu |
| [RxHousing](rxhousing.md) | `RxHousing` (or `rxscripts_housing`) | 2.5.0 | Copy one file, change one manifest line | The property's furniture inventory, "YouTool Store" category |
| [vms\_housing](vms-housing.md) | `vms_housing` | 1.5.1 (1.4.5 minimum) | None, restart vms\_housing once | The property's stash, placed with the vms\_housing placement tool |
| [brutal\_housing](brutal-housing.md) | `brutal_housing` | 2.1.0 | Copy one file, add one manifest line twice | The property's furniture in brutal\_housing, arranged with its placement tool |
| [rcore\_housing](rcore-housing.md) | `rcore_housing` | 1.1.4 (minimum) | None | The property's furniture stock, placed with rcore's furniture editor (or an rcore delivery box) |

"Tested with" is the version the full YouTool test run passed on. Newer versions usually work; the [setup check](#what-the-setup-check-verifies) tells you when your version differs.

Deliveries only go to properties the buyer **owns** (on vms\_housing and rcore\_housing also properties they rent). Having a key to someone else's property is not enough.

{% hint style="warning" %}
**Updating ps-housing, RxHousing or brutal\_housing removes what you added for YouTool.**

* **ps-housing**: an update overwrites `server/sv_property.lua`, so the pasted YouTool code is gone.
* **RxHousing**: every update replaces `fxmanifest.lua`, so the `config/furniture/*.lua` change is undone.
* **brutal\_housing**: every update replaces `fxmanifest.lua`, so the two `configs/youtool_catalog.lua` lines are gone.

After every update of one of these scripts, redo its install steps. The setup check reports it with a `[FAIL]` line the next time the script starts.
{% endhint %}

***

### How YouTool picks the housing script

One second after YouTool starts, it checks which housing resource is running, in this order, and uses the **first** one it finds:

1. `qs-housing`
2. `ps-housing`
3. `nolag_properties`
4. `bcs_housing`
5. `rtx_housing`
6. `RxHousing` or `rxscripts_housing`
7. `vms_housing`
8. `brutal_housing`
9. `rcore_housing`

The server console shows the result:

```
[YouTool Store] Housing adapter: qs-housing
```

The names it can print are `qs-housing`, `ps-housing`, `nolag_properties`, `bcs_housing`, `rtx_housing`, `rxscripts` (for RxHousing), `vms_housing`, `brutal_housing`, `rcore_housing` and `custom`.

* **Only one housing script is used.** If two supported scripts run at the same time, YouTool uses the one higher in the list and the setup check warns about it.
* **Resource names must match.** A housing script in a renamed folder isn't detected (RxHousing is the exception: both `RxHousing` and `rxscripts_housing` work).
* **Detection runs once, when YouTool starts.** List your housing script before YouTool in `server.cfg`. If you ever start the housing script by hand while YouTool is already running, restart `prompt_youtool_store_system` afterwards.
* **`custom`** means no supported script was found. Purchases are then blocked until you connect a housing or inventory system yourself (see [For Developers](../developers/README.md)).
* **Showcase (demo) mode** skips detection completely: purchases complete but deliver nothing. Turn it off on a live server (`Config.Showcase.enabled = false` in `config/showcase.lua`).

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure qs-housing          # your housing script
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}

***

### At checkout

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/youtool-checkout.png" alt="Deliver to property picker"><figcaption><p>The "Deliver to..." picker: the player owns two properties and chooses where the order goes</p></figcaption></figure>
{% endcolumn %}

{% column %}
Before any money is taken, YouTool asks the housing script which properties the buyer owns:

* **No property**: the checkout stops with *"You need to own a house to purchase furniture"*. Nothing is charged.
* **One property**: the order goes straight there, no question asked.
* **Several properties**: a **Deliver to...** picker lists them with the order total. The player clicks one, or cancels. The same picker appears in the phone app.

The order waits 5 minutes for the pick. After that the player sees *"No pending checkout"* and checks out again.
{% endcolumn %}
{% endcolumns %}

On bcs\_housing the picker still appears for players with several houses, but bcs stores furniture per player, so the items can be placed in any of their houses.

**Partial deliveries.** If the housing script refuses some items (for example a furniture limit is reached or the property is full), YouTool keeps the items that arrived and refunds each refused item at the price the player paid. The message then ends with *"(N failed, refunded)"*. If nothing arrives, the whole order is refunded and the player sees the reason the housing script gave.

***

### What the setup check verifies

The setup check prints to the **server console** about 15 seconds after YouTool starts, and again about 8 seconds after any supported housing script starts or restarts. So after you fix an install step, restart the housing script and read the console. Each line is `[ OK ]`, `[WARN]`, `[FAIL]` or `[INFO]`, and every problem has a `->` line that says how to fix it. The full check (framework, money, target script, map, language) is described in [Troubleshooting](../troubleshooting.md).

For housing it checks:

* **Which housing script runs, and its version** compared with the version we tested.
* **The YouTool install step** for that script: the install file is copied, is the current copy, and is actually loaded by the housing script (which also catches a missing manifest change on RxHousing and brutal\_housing); the position of the manifest lines (brutal\_housing); the settings (bcs\_housing); the pasted code (ps-housing); the YouTool exports and catalog registration (vms\_housing); the minimum version (qs-housing).
* **That the YouTool folder is still named** `prompt_youtool_store_system`. The install files read YouTool's catalog by that name.
* **That `oxmysql` is running.** Most housing scripts and several YouTool adapters need it.

Lines you can see for any housing script:

| Line | Meaning |
| --- | --- |
| `[ OK ] Housing: <script> <version>` | Detected, same version we tested |
| `[INFO] Housing: <script> <version> (newer than <tested>, the version we tested: report it if purchases fail)` | Newer version, usually fine |
| `[WARN] Housing: <script> <version> is older than <tested>, the version we tested` | Update the housing script |
| `[WARN] Housing: YouTool uses <script>, but <other> is running too` | Two housing scripts run; only the first is used |
| `[FAIL] Housing: <script> found, but YouTool has no adapter for it` | An [unsupported script](#unsupported-housing-scripts) runs |
| `[FAIL] Housing: no supported housing script is running, purchases are blocked` | Nothing detected |
| `[FAIL] The YouTool folder is named <name>` | Rename it back to `prompt_youtool_store_system` |
| `[WARN] oxmysql is not running` | Start `oxmysql` before YouTool |
| `[WARN] Showcase (demo) mode is on: purchases deliver nothing` | Turn off Showcase mode on a live server |

#### Always copy the install file from your current YouTool version

The files you copy into nolag\_properties, bcs\_housing, rtx\_housing, RxHousing and brutal\_housing carry a version number (a `YOUTOOL_INSTALL = { version = 1, ... }` block at the top; in the bcs\_housing file a first-line comment `-- youtoolInstall version = 1`). Leave that part in the file. When a YouTool update changes an install file, the setup check reports the copy in your housing script as outdated:

```
  [FAIL] brutal_housing: the YouTool install file is an old copy
         -> Copy integrations/brutal-housing/brutal_install/youtool_catalog.lua over the old brutal_housing/configs/youtool_catalog.lua and restart that script.
```

After every YouTool update, read the setup check once and copy the file again if it asks.

#### Live delivery test

The automatic check never puts anything into a property. To test a real delivery, have a player who owns a property online and run this in the **server console** (or the txAdmin console):

```
youtool_setup <playerId>
```

It delivers one free **Disposable Coffee Cup** (`prop_coffee_cup_trailer`) into that player's first property and confirms it was saved:

```
  [ OK ] Properties owned by player 2: 1
  [ OK ] Delivery test: Disposable Coffee Cup arrived in Starter Apartments #2
```

A passed test is remembered per housing script and version, so later checks show `Delivery test passed on <date>` instead of adding more cups. To run it again anyway, add `force`: `youtool_setup <playerId> force`. Without a player id, `youtool_setup` repeats the static checks.

The report ends with a **Support code** line, for example:

```
  Support code: YT 1.2.0 | qbcore | bcs_housing 4.24.0 | install ok | 0 fail 0 warn | delivery ok
```

When you open a ticket, copy the whole setup-check block from the console, including that line.

***

### Unsupported housing scripts

YouTool has no adapter for these scripts. The setup check recognizes them and reports them, but nothing is delivered:

* `qb-houses`
* `esx_property`
* `loaf_housing`
* `origen_housing`
* `jg-housing`

On a server that runs only one of these, the console shows:

```
  [FAIL] Housing: qb-houses found, but YouTool has no adapter for it
         -> Supported: qs-housing, ps-housing, nolag_properties, bcs_housing, rtx_housing, RxHousing, vms_housing, brutal_housing, rcore_housing. For any other script, register a custom adapter (YouTool documentation, Custom housing).
```

Players who try to check out see *"No housing system configured on this server (custom mode - see server console)"* and are not charged. To use another housing or inventory script, connect it with a custom adapter, see [For Developers](../developers/README.md).

***

### Troubleshooting

<details>

<summary>Players see "No housing system configured on this server (custom mode - see server console)"</summary>

YouTool found no supported housing script when it started. Check the console for `[YouTool Store] Housing adapter: custom`.

1. Make sure the housing script is running and its folder has the exact resource name from the table above.
2. If it was started after YouTool, run `restart prompt_youtool_store_system`.
3. Read the setup check for the `Housing:` line.

</details>

<details>

<summary>Players see "You need to own a house to purchase furniture" but they own one</summary>

YouTool asks the housing script for properties the player **owns**. Keyholders and (except on vms\_housing) renters don't count. To see what the housing script answers for a player, run this in the server console:

```
youtool_housing <playerId>
```

It prints the active adapter and how many properties the housing script returns for that player. Then run `youtool_setup <playerId>` for the full check plus a test delivery.

</details>

<details>

<summary>The purchase went through but the furniture isn't in the house</summary>

1. Run `youtool_setup <playerId>` with that player online and fix every `[FAIL]` line.
2. Open the page of your housing script: each one says exactly where purchases appear and has its own troubleshooting list.
3. If everything is `[ OK ]` and the delivery test passes, send the whole setup-check block to Prompt Studio.

</details>
