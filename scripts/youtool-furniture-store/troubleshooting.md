---
description: Read the setup check, fix every message it prints, solve common problems, and know what to send support.
icon: wrench
---

# Troubleshooting

{% hint style="info" %}
YouTool never writes to the chat. Players get on-screen notices, and every diagnostic (the setup check, `/youtool_diag`, `/youtool_testall`, `/youtool_whoami`) prints to the **server console**, so you can copy it straight into a ticket.
{% endhint %}

***

### Read the setup check

The setup check is the first thing to look at. It prints in the server console (and the txAdmin Live Console):

* about 15 seconds after YouTool starts,
* about 8 seconds after a supported housing script starts or restarts,
* whenever you type a `youtool_setup` command in the server console.

| Command (server console only) | What it does |
| --- | --- |
| `youtool_setup` | Runs every check and prints the report |
| `youtool_setup <playerId>` | The same, plus one live delivery test into that player's property |
| `youtool_setup <playerId> force` | Repeats a delivery test that already passed |

The live delivery test puts one free Disposable Coffee Cup into the player's first property and checks that it arrived. It runs once per housing script version (remembered in `data/setup_state.json`), so repeated checks don't fill anyone's property with cups.

#### Status tags

| Tag | Meaning |
| --- | --- |
| `[ OK ]` | Checked and fine. |
| `[INFO]` | Good to know. Read it, but it doesn't stop anything from working. |
| `[WARN]` | Something is wrong or risky. YouTool runs, but fix it. |
| `[FAIL]` | Purchases, or part of YouTool, won't work until you fix this. |

A line with a problem is followed by a `->` line that says how to fix it. When there are no `[WARN]` or `[FAIL]` lines, `Everything looks good.` appears above the support code.

Here is a real `[FAIL]`: the YouTool line in brutal\_housing's manifest is in the wrong place, so brutal's own catalog loads after it.

{% code title="Server console" %}
```
[YouTool] ── setup check ────────────────────────────────────────
  [ OK ] Housing: brutal_housing 2.1.0
  [ OK ] brutal_housing: YouTool install file loaded (v2, 1411 items)
  [FAIL] brutal_housing fxmanifest: in client_scripts, 'configs/youtool_catalog.lua' loads before 'configs/furnitures.lua'
         -> In brutal_housing/fxmanifest.lua add 'configs/youtool_catalog.lua' right after 'configs/furnitures.lua' in BOTH client_scripts and server_scripts, run refresh, then restart it. Every brutal_housing update removes these lines.
  [ OK ] Framework: qbcore, money: auto
  Support code: YT 1.2.0 | qbcore | brutal_housing 2.1.0 | install ok | 1 fail 0 warn | delivery untested
```
{% endcode %}

#### The support code

The last line sums up your setup in one line. Paste it into every ticket.

| Part | Meaning |
| --- | --- |
| `YT 1.2.0` | YouTool version |
| `qbcore` | Framework found: `qbcore`, `qbox`, `esx` or `standalone` |
| `brutal_housing 2.1.0` | Housing script and its version. `custom` for a custom adapter, `no housing` when none was found. |
| `install ok` | The housing install step: `ok`, `missing`, `outdated`, `not_loaded`, `error`, or `-` when there is nothing to check |
| `1 fail 0 warn` | How many `[FAIL]` and `[WARN]` lines the report has |
| `delivery untested` | The live delivery test: `ok`, `fail`, `no_house` or `untested` |

***

### Every setup check message

`<script>` is your housing script's resource name, `<version>` its version, `<tested>` the version we tested YouTool 1.2.0 against.

<details>

<summary>Housing script</summary>

| Message | Status | What to do |
| --- | --- | --- |
| `Housing: <script> <version>` | OK | Nothing. This is the script YouTool delivers to. If the script has no version in its manifest, the line shows `?` and is `[INFO]`. |
| `Housing: <script> <version> (newer than <tested>, the version we tested: report it if purchases fail)` | INFO | Usually fine. Run the delivery test (`youtool_setup <playerId>`). If purchases fail, send us the report. |
| `Housing: <script> <version> is older than <tested>, the version we tested` | WARN | Update the housing script to the tested version or newer. |
| `Housing: YouTool uses <script>, but <other> is running too` | WARN | Run only one housing script. When several run, YouTool uses the first in this order: qs-housing, ps-housing, nolag\_properties, bcs\_housing, rtx\_housing, RxHousing, vms\_housing, brutal\_housing, rcore\_housing. |
| `Housing: custom adapter registered` | OK | A developer connected another script through a custom adapter. See [For Developers](developers/README.md). |
| `Housing: <script> found, but YouTool has no adapter for it` | FAIL | That script isn't supported, so purchases are blocked. Use one of the [supported scripts](housing/README.md), or have a developer register a custom adapter. |
| `Housing: no supported housing script is running, purchases are blocked` | FAIL | Start your housing script before `prompt_youtool_store_system`, and keep its original folder name (for example `qs-housing`), because YouTool detects it by name. |
| `The <check> check crashed: <error>` | WARN | One of the checks itself failed. Send the whole report to support. |

</details>

<details>

<summary>YouTool install file in your housing script</summary>

Five housing scripts need a YouTool file copied into them. The setup check looks for it here:

| Housing script | File in the housing script | Copied from (inside `prompt_youtool_store_system`) |
| --- | --- | --- |
| nolag\_properties | `custom/furniture/youtool_catalog.lua` | `integrations/nolag-properties/nolag_install/youtool_catalog.lua` |
| bcs\_housing | `furniture/others/youtool_furniture.lua` | `integrations/bcs-housing/bcs_install/youtool_furniture.lua` |
| rtx\_housing | `configs/zz_youtool_props.lua` | `integrations/rtx-housing/zz_youtool_props.lua` |
| RxHousing | `config/furniture/youtool_catalog.lua` | `integrations/rxscripts/rxhousing_install/youtool_catalog.lua` |
| brutal\_housing | `configs/youtool_catalog.lua` | `integrations/brutal-housing/brutal_install/youtool_catalog.lua` |

| Message | Status | What to do |
| --- | --- | --- |
| `<script>: the YouTool install file is missing` | FAIL | Copy the file to the place shown on the `->` line and restart the housing script. |
| `<script>: the YouTool install file is an old copy` | FAIL | Your copy is older than the one this YouTool version ships (common after an update). Copy the new file over the old one and restart the housing script. |
| `<script>: the install file is there but is not loaded` | FAIL | The housing script didn't run the file. Restart it, or the whole server. For brutal\_housing and RxHousing the `->` line gives the manifest change instead (see the next section). |
| `<script>: the install file ran but failed: <reason>` | FAIL | See the reasons below. |
| `<script>: YouTool install file present (v<n>)` | OK | bcs\_housing: the file is in place and current. |
| `<script>: YouTool install file loaded (v<n>, <count> items)` | OK | The file ran and registered `<count>` YouTool items in the housing script. |

Reasons for `the install file ran but failed`. The `->` line says: `Make sure the YouTool folder is named prompt_youtool_store_system and starts before <script>.`

* `catalog.json not found`: the install file reads `data/catalog.json` from a folder named exactly `prompt_youtool_store_system`. Check the name, then restart the housing script.
* `catalog.json failed to decode`: `data/catalog.json` is damaged. Take it again from the download.
* `YouTool not started within 60 s` (nolag\_properties): YouTool didn't start. Check that it is in `server.cfg` and starts without errors.
* `loaded before furniture.lua` (rtx\_housing): the file must sit in `rtx_housing/configs/` under the name `zz_youtool_props.lua`, so it loads after rtx's own `furniture.lua`.

</details>

<details>

<summary>Script-specific checks</summary>

Full steps for each script are on its page under [Housing Integrations](housing/README.md).

**brutal\_housing** ([page](housing/brutal-housing.md))

| Message | Status | What to do |
| --- | --- | --- |
| `brutal_housing fxmanifest: 'configs/youtool_catalog.lua' is missing from <block>` | FAIL | In `brutal_housing/fxmanifest.lua`, add `'configs/youtool_catalog.lua'` right after `'configs/furnitures.lua'` in both `client_scripts` and `server_scripts`. Type `refresh` in the console, then restart brutal\_housing. |
| `brutal_housing fxmanifest: in <block>, 'configs/youtool_catalog.lua' loads before 'configs/furnitures.lua'` | FAIL | Same fix: the YouTool line must come after `'configs/furnitures.lua'` in both blocks. |

Every brutal\_housing update removes these lines, so check again after each update.

**RxHousing** ([page](housing/rxhousing.md))

When the install file is not loaded, the `->` line reads: `In RxHousing/fxmanifest.lua change 'config/furniture/furniture.lua' to 'config/furniture/*.lua' in shared_scripts, run refresh, then restart it.` Every RxHousing update undoes this.

**bcs\_housing** ([page](housing/bcs-housing.md))

| Message | Status | What to do |
| --- | --- | --- |
| `<script>: could not read config/config.lua to check the furniture shop setting` | WARN | YouTool couldn't find the setting in bcs's config. Check it by hand (next rows). |
| `<script>: EnableFurnitureShop is off, so players never see the furniture they bought` | FAIL | In `bcs_housing/config/config.lua`, set `Config.EnableFurnitureShop = true`, then restart bcs\_housing. |
| `<script>: FurnitureAsItem is on, but YouTool delivers to furniture storage` | FAIL | In the same file, set `Config.FurnitureAsItem = false`, then restart bcs\_housing. |
| `<script>: furniture shop mode is on` | OK | Both settings are right. |

**ps-housing** ([page](housing/ps-housing.md))

| Message | Status | What to do |
| --- | --- | --- |
| `<script>: the YouTool furniture API is not added` | FAIL | Paste the code from `integrations/ps-housing/README.md` (Step 1) at the end of `ps-housing/server/sv_property.lua` and restart ps-housing. A ps-housing update overwrites that file, so redo it after each update. |
| `<script>: YouTool furniture API found` | OK | The code is in place. |

**qs-housing** ([page](housing/qs-housing.md))

| Message | Status | What to do |
| --- | --- | --- |
| `qs-housing <version> is too old for YouTool` | FAIL | Update qs-housing to 5.2.16 or newer. |
| `qs-housing <version> works, but prints a warning for every catalog item at boot` | INFO | Purchases work. Update qs-housing to 5.3.19 or newer to get rid of the boot warnings. |

**vms\_housing** ([page](housing/vms-housing.md))

| Message | Status | What to do |
| --- | --- | --- |
| `<script>: this build has no YouTool exports, delivery is off` | FAIL | Update vms\_housing to 1.4.5 or newer. |
| `vms_housing: <n> YouTool models were just registered; vms sees them after its next restart` | WARN | Normal the first time. Restart vms\_housing (or the whole server). |
| `<script>: YouTool catalog registered` | OK | The YouTool items are in vms's furniture list. |

**rcore\_housing** ([page](housing/rcore-housing.md))

| Message | Status | What to do |
| --- | --- | --- |
| `rcore_housing <version> is too old: it lists no apartments for their owners` | FAIL | Update rcore\_housing to 1.1.4 or newer. |
| `<script>: the furniture delivery export (RegisterFurnitureDelivery) is missing` | FAIL | Update rcore\_housing to 1.1.4 or newer. |
| `<script>: furniture delivery export found` | OK | Delivery into rcore\_housing works. |
| `<script>: <n> item(s) cost at least what rcore pays to buy them back, so selling them back cannot make money` | INFO | Normal. Those items' corporate base was raised to rcore's buy-back price. See [rcore\_housing](housing/rcore-housing.md). |
| `<script>: its own furniture shop NPC stands inside the YouTool store <store>` | WARN | Move or remove that entry in `Config.Furniture.Shop.Locations` in `rcore_housing/config.lua`. |

</details>

<details>

<summary>YouTool, framework and server</summary>

| Message | Status | What to do |
| --- | --- | --- |
| `The YouTool folder is named <name>` | FAIL | Rename the folder back to `prompt_youtool_store_system`. The housing install files and item images use that name. |
| `Framework: <framework>, money: <mode>` | OK | The framework found and the `Config.MoneySystem` in use. |
| `Money: MoneySystem is 'custom' but CustomGetMoney, CustomRemoveMoney and CustomAddMoney are not all defined, so purchases are refused` | FAIL | Define all three functions at the bottom of `server/framework.lua`, or set `Config.MoneySystem = 'auto'`. |
| `Money: free mode (<framework>), nothing costs anything` | WARN | `Config.MoneySystem` is `'free'`, or it is `'auto'` and no framework was found. Start QBCore, QBox or ESX before YouTool with `'auto'`, or use `'custom'`. |
| `oxmysql is not running` | WARN | Start `oxmysql` before YouTool. Most housing scripts need it. |
| `Neither ox_target nor qb-target is running: players cannot target store items` | WARN | Start `ox_target` or `qb-target` before YouTool, or set `Config.interactionMode = 'none'` if you don't want targets. The tablet still opens with its key. |
| `The YouTool store map (prompt_youtool) is not running` | INFO | Without the map there is no store to walk into, so players can't open the tablet. Add `ensure prompt_youtool` before the script. |
| `Language '<code>' has no localization file, English is used` | WARN | Set `Config.language` to one of `en de es fr ru pt sv no fi ar ko zh`, or add the file. See [Languages](languages.md). |
| `Config.Manager.devBypass is ON: every player has every store permission` | FAIL | Set `Config.Manager.devBypass = false` in `config.lua` right away. Showcase mode turns it on by itself: if the Showcase line below is there too, switch Showcase off. |
| `Debug output is on (Config.Debug)` | INFO | Extra console output. Set `Config.Debug = false` when you're done. |
| `Showcase (demo) mode is on: purchases deliver nothing` | WARN | Set `Config.Showcase.enabled = false` in `config/showcase.lua` on a live server. Showcase also makes everything free and gives every player every permission. |

</details>

<details>

<summary>Live delivery test</summary>

Most of these lines appear when you run `youtool_setup <playerId>`. The automatic check only says whether a test has passed. While no housing script is active, no delivery lines appear at all.

| Message | Status | What to do |
| --- | --- | --- |
| `Properties owned by player <id>: <n>` | OK | The housing script sees the player's properties. |
| `Player <id> owns no property, so delivery cannot be tested` | WARN | Run it with a player who owns a property. |
| `Player <id> is not online` | WARN | Use the server ID of a player who is online right now (for example from the txAdmin player list). |
| `Delivery test: <item> arrived in <property>` | OK | Delivery works. The result is saved, so the test won't run again for this housing version. |
| `Delivery test passed on <date> (...)` | OK | It passed before. Add `force` to run it again. |
| `Delivery not tested. Run youtool_setup <playerId> with a player who owns a property (...)` | INFO | Shown by the automatic check until a test has passed. Run the test once. |
| `Delivery test failed: <reason>` | FAIL | Fix any other `[FAIL]` lines first. If everything else is OK, send the whole report to support. |
| `Delivery test: <item> was accepted but never showed up in your property` | FAIL | The housing script took the item but it wasn't in the property afterwards. Same as above: fix other `[FAIL]` lines, then send the report. |

</details>

***

### Common problems

<details>

<summary>The tablet doesn't open, or there is no "[E] Open Tablet" prompt</summary>

* **Be inside the store.** The tablet works only inside a YouTool store interior. YouTool finds the store by the interior at `interiorCoords` in `Config.Stores`, so `prompt_youtool` (the map) must be running. If you changed `interiorCoords`, the point must be inside the store.
* **Check the key.** `E` is only the starting key (`Config.Tablet.showKey`). Players can rebind it in GTA **Settings › Key Bindings › FiveM** under "YouTool Tablet", and the prompt shows the key they bound. Changing `showKey` later doesn't change a key a player already has.
* **The prompt can be hidden on purpose.** `Config.Tablet.prompt = 'none'` hides it; the key still works.
* **A hook can block it.** A `tablet.canOpen` hook that returns `false` (in `hooks/hooks_client.lua` or `hooks/hooks_shared.lua`) hides both the tablet and the prompt. See [Hooks](developers/hooks.md).
* **The key is ignored on purpose** while a player previews an item in 3D, carries a freight box, or places a display.

</details>

<details>

<summary>No target options on the furniture or the till</summary>

* Start `ox_target` or `qb-target` **before** `prompt_youtool_store_system`. YouTool detects the target script once, when it loads. If none was found, the F8 console shows `[YouTool] no target system (ox_target / qb-target) running, targeting disabled`.
* Check `Config.interactionMode` in `config.lua` isn't `'none'`, and that `targetableProps = true` for the store in `Config.Stores`.
* Targets only show inside the store: on furniture that is in the catalog within `Config.Target.distance` (2.5 m by default), and on the till within 2 m.

</details>

<details>

<summary>"No housing system detected" at checkout</summary>

Players see `No housing system detected on this server` or `No housing system configured on this server (custom mode - see server console)`. YouTool found no supported housing script, so it refuses the checkout before any money is taken.

Read the setup check: it shows which script it found, or that none is running. Start your housing script before YouTool, keep its original resource name, and restart.

</details>

<details>

<summary>"You need to own a house to purchase furniture"</summary>

The housing script reports that this character owns no property. Check with `youtool_setup <playerId>` in the server console: it prints `Properties owned by player <id>: <n>` or `owns no property`. Which kinds of property each housing script counts is on its [housing page](housing/README.md).

</details>

<details>

<summary>"Not enough money. Need: $..."</summary>

Checkout charges the player's **bank** account, not cash. The amount is the full cart total. If the bank balance changes between the check and the payment, the player sees `Payment failed — insufficient funds at checkout` and nothing is charged.

</details>

<details>

<summary>"This store cannot cover its discount right now"</summary>

The store sells below the base price (a negative markup), and its vault can't pay corporate the difference for this order. YouTool refuses the order before the customer pays. The difference is counted over the whole order, so items sold above base pay for items sold below it.

To fix it, a staff member with the `vault.deposit` permission deposits money into the vault (Console › Vault), or someone with `markup.edit` raises the markup to 0% or more. See [Markup, Vault & Sales](console/markup-vault-sales.md).

</details>

<details>

<summary>"These items aren't in stock at this store"</summary>

The store runs in Active mode (`Config.EconomyMode = 'Active'`) and is out of stock for these items. Staff refill it by ordering freight. See [Stock & Freight](console/stock-and-freight.md). If only some items were out of stock, the purchase goes through for the rest and the player isn't charged for the missing ones.

</details>

<details>

<summary>The purchase went through, but the furniture isn't in the house</summary>

* **Look in the right place.** YouTool delivers into the housing script, and where the furniture shows up depends on that script (a furniture storage, a stash, a furniture menu). Your [housing page](housing/README.md) says where.
* **Check the property.** Players with more than one property choose one at checkout. Make sure you're looking in that one.
* **Run the delivery test**: `youtool_setup <playerId>` (add `force` if it passed before). A `[FAIL]` line says what's wrong.
* **Read the server console** at the time of the purchase. `[YouTool Server] Delivery failed for <id> (refunded $...)` means nothing arrived and the player got the money back. `Partial delivery for <id>: n/m items, refunded $...` means some items didn't fit; the player was charged only for the items that arrived. `REFUND FAILED for <id>: $N not returned` means the player left the game before the refund could be paid; pay it back by hand.
* **Showcase mode** delivers nothing on purpose, and the checkout message says so.
* **vms\_housing**: items registered for the first time appear after vms\_housing restarts.
* **After a housing script update**, its YouTool install step may be gone. The setup check shows it.

<figure><img src="../../.gitbook/assets/youtool-checkout.png" alt="The Deliver to... property picker at checkout, for a player who owns two homes"><figcaption><p>"Deliver to…": players with more than one property choose where the order goes</p></figcaption></figure>

</details>

<details>

<summary>Prices look wrong</summary>

The price a customer pays is:

**base price × `Config.EconomyScale` × (1 + store markup %)**, rounded down.

* `Config.EconomyScale` (`config.lua`) multiplies every price, for every store. It also scales freight and wages.
* The base price comes from the catalog, unless a corporate admin changed it in the Console. A base price change applies to all stores.
* Markup is per store. An item's own markup wins over its category's markup, which wins over the store's global markup.
* `Config.Markup` in `config/pricing.lua` is only the **starting** markup for a store that has none saved yet. Once a store has markup in `data/markup.json`, change it in the Console's Markup tab; editing the config does nothing for that store.
* A set's discount never takes its price below the corporate base price.
* The phone app shows the prices of the store the player picked.
* vms\_housing: YouTool writes its items into vms's own furniture list at a higher price (`Config.VmsHousing.priceMultiplier`, 1.5 by default), so vms's furniture menu never undercuts the store. That difference is intended.

See [Markup, Vault & Sales](console/markup-vault-sales.md) and [Configuration](configuration.md).

</details>

<details>

<summary>The Console button is missing, or tabs are missing</summary>

The **Console** button sits top right in the tablet, next to the cart. It shows only to corporate admins and to players with at least one Console permission at the store they're in. Customers never see it.

* **Make sure you are the owner** of this store: `youtool_setowner <playerId|citizenid> <storeId>` (see [Installation](installation.md)). On QBCore, QBox and ESX, ownership belongs to one character.
* **Corporate admin is not store access.** `youtool.admin` shows the Console and the corporate catalog tools, but markup, vault, staff and the other store tabs need the owner or a staff position.
* **Staff need a position with permissions.** Each tab and button follows the position's permissions. A position whose only permissions are `freight.unload`, `vault.deposit` or `markup.negative` doesn't show the Console button. See [Staff & Permissions](console/staff-and-permissions.md).
* **Permissions load when you enter the store.** After changing an ACE or running `youtool_setowner`, leave the store and come back in. Changes made in the Staff tab reach players in the store right away; if a button or tab still doesn't show, close and reopen the tablet.
* **Check your ACE**: run `/youtool_whoami` in game. The server console shows `corporateAdmin=true/false` and your license. To grant it to that license, the ACE principal is `identifier.license:<license>`.

</details>

<details>

<summary>/youtool_setowner does nothing in game</summary>

`youtool_setowner` is a restricted command. In game you need both `youtool.admin` and permission to run the command (`command.youtool_setowner`, or all commands through `add_ace group.admin command allow`). Without `youtool.admin` you get an on-screen notice. The result is printed in the **server console**, not in game. The simplest way is to run it from the server console.

</details>

<details>

<summary>"Select a store before checking out" or "You are not in a store"</summary>

The server didn't accept that you're inside the store. It checks that you are within `Config.StoreEnterRadius` (120 m) of the store's `interiorCoords`. When it rejects an entry, the server console shows `[YouTool Trust] rejected playerEnteredStore(...) (invalid or too far)`.

Leave the store and walk back in. If it keeps happening, check `interiorCoords` for that store in `config.lua`: it must be a point inside the store.

</details>

<details>

<summary>The language doesn't change, or texts show as key names</summary>

* Restart `prompt_youtool_store_system` after changing the language.
* With `Config.language = 'auto'`, the convar must be set with `setr ox:locale "de"`, not `set`.
* Regional codes like `zh-cn` or `pt-br` have no YouTool file and fall back to English.
* A syntax error in a language file makes YouTool ignore the whole file.
* A text that shows as its key name (for example `checkout_done`) is missing from `en.lua` too.

Product names, category names and console output are not translated. See [Languages](languages.md).

</details>

<details>

<summary>"Checkout failed, please try again"</summary>

Something went wrong on the server during the purchase. The server console has a line starting `[YouTool Server] checkout error for` with the reason. Send that line and the setup check report to support.

</details>

***

### Getting support

Before you open a ticket, collect:

1. **The whole setup check report**, including the `Support code:` line. Type `youtool_setup` in the server console to print it again.
2. **The `youtool_diag` output.** Type `youtool_diag` in the server console, or `/youtool_diag` in game. It prints what YouTool detected (framework, housing script, catalog, settings) in the server console and also saves it to `data/test_logs/`. In game it needs the `youtool.tester` or `youtool.admin` ACE. If the command doesn't exist, `Config.TestCommands.enabled` is `false` in `config.lua`.
3. **Red error lines** from the server console and the F8 console from the moment the problem happened.
4. **What you did, what you expected, and what happened.** For permission problems, add the `/youtool_whoami` output.

Only run `/youtool_testall` if support asks for it: it puts a few test items into the player's property and makes one real purchase with their money.

Then open a ticket on our Discord:

<a href="https://discord.gg/rKbHHdfZFU" class="button primary" data-icon="discord">Prompt Studio Discord</a>
