---
description: Every YouTool command for owners and staff, where to run it, who may run it, what it prints, and the ACE permissions in server.cfg.
icon: terminal
---

# Commands & Permissions

Most YouTool commands are for the server owner and print their result in the **server console** (also the txAdmin Live Console), so you can copy it into a support ticket. YouTool never writes to the chat. A few in-game commands answer with an on-screen notice instead.

How to read the **Who** column:

* **Console**: the server console or txAdmin Live Console can always run it.
* **Corporate admin**: a player with the corporate ACE, `youtool.admin` by default (`Config.Roles.corporateAce`).
* **Store permission**: a permission of the player's position at that store, set in the Staff tab. See the [permission reference](console/staff-and-permissions.md#permission-reference).
* **Restricted**: FiveM also requires the ACE `command.<name>` to run it in game. Many server.cfg files already give admins every command with `add_ace group.admin command allow`.

Store ids: `youtool_sandy` (Sandy Shores) and `youtool_vespucci` (Davis).

{% hint style="info" %}
Commands typed in the server console are written without the slash (`youtool_setup`); in game you type them in the F8 console or chat box with a slash (`/youtool_whoami`). When an in-game command "prints to the server console", the result appears there, not in your F8 console.
{% endhint %}

***

## Setup and diagnostics

| Command | Run from | Who | Output |
| --- | --- | --- | --- |
| `youtool_setup [playerId] [force]` | Server console only | Console | Server console |
| `youtool_diag [playerId]` | Console or in game | Console, `youtool.tester`, `youtool.admin` | Server console + log file |
| `youtool_testall [playerId]` | Console or in game | Console, `youtool.tester`, `youtool.admin` | Server console + log file |
| `youtool_housing [playerId]` | Console or in game | Console, corporate admin | Server console |

<details>

<summary><code>youtool_setup</code> — the setup check</summary>

Prints the same setup check YouTool runs about 15 seconds after it starts: housing script and version, the install step in your housing script, framework and money, `oxmysql`, the target script, the map, the language file, and risky settings. Every problem has a `->` line with the fix, and the last line is the **Support code** to paste into a ticket.

```
youtool_setup              static checks only
youtool_setup 2            + one live delivery into player 2's first property
youtool_setup 2 force      repeat a delivery test that already passed
```

The live delivery puts one free Disposable Coffee Cup into that player's property. A pass is remembered per housing script version in `data/setup_state.json`, so it isn't repeated unless you add `force`. Typed in game, the command does nothing. Reading the output: [Installation](installation.md) and [Troubleshooting](troubleshooting.md).

</details>

<details>

<summary><code>youtool_diag</code> — what YouTool detected</summary>

Read-only. Prints the framework and housing adapter YouTool detected, the catalog item count with three sample items, a few config values, and which housing adapter functions are present. Only registered while `Config.TestCommands.enabled = true`.

</details>

<details>

<summary><code>youtool_testall</code> — full housing test with a real purchase</summary>

Runs the whole test battery against one player: identifier, owned properties, one item added, three items added in one batch, a $1 bank remove-and-return, **one real purchase** of the cheapest catalog item (the player is charged its price), and a catalog audit. The items go into the player's first property.

* In game it always tests **you**. From the console, pass a player id: `youtool_testall 2`.
* Use a test character and a test property: the items are real.
* Each run is also saved as a log file in `data/test_logs/` (the last 50 are kept). The console shows the file name.
* Only registered while `Config.TestCommands.enabled = true`.

</details>

<details>

<summary><code>youtool_housing</code> — which housing adapter is live</summary>

Prints the active adapter. With a player id it also asks the adapter whether that player owns a property and how many:

```
[YouTool Housing] adapter=qs-housing  active=true  registered=no
[YouTool Housing] PlayerOwnsHouse(2) -> ok=true result=true
[YouTool Housing] GetPlayerHouses(2) -> ok=true count=1
```

Run it first when furniture "won't buy", and to test a custom adapter ([Custom housing](developers/README.md#custom-housing)).

</details>

***

## Store admin

| Command | Run from | Who | Output |
| --- | --- | --- | --- |
| `youtool_setowner <playerId\|citizenid> <storeId>` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_hire <storeId> <citizenid> <roleId>` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_fire <storeId> <citizenid>` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_roles [storeId]` | Console or in game | Console, corporate admin (restricted) | Server console |
| `/youtool_viewas <roleId\|owner\|off\|list>` | In game, inside a store | Corporate admin | On-screen notice |
| `/youtool_whoami` | In game | Anyone | Server console |

`citizenid` means the character identifier: the citizenid on QBCore and QBox, the identifier on ESX, the license on a standalone server. `roleId` is `owner`, `manager`, `worker`, or the id of a position the store created (like `r36992`); `youtool_roles` lists them.

<details>

<summary><code>youtool_setowner</code> — make someone a store's owner</summary>

`youtool_setowner 2 youtool_sandy` makes the character of online player 2 the owner of Sandy Shores. For an offline player pass their citizenid. Running it again replaces the owner. Prints `[YouTool Roles] ABC12345 is now OWNER of youtool_sandy`. Details: [Staff & Permissions](console/staff-and-permissions.md#set-the-store-owner).

</details>

<details>

<summary><code>youtool_hire</code>, <code>youtool_fire</code>, <code>youtool_roles</code> — staff from the console</summary>

The console versions of the Staff tab. `youtool_hire` puts a character on a position, `youtool_fire` removes them, `youtool_roles` prints the owner, every position (with its permission count) and every staff member, for one store or all of them. The identifier isn't checked against your database, so copy it exactly.

```
[YouTool Roles] ABC12345 hired as manager at youtool_sandy
[YouTool Roles] ABC12345 removed from youtool_sandy
```

</details>

<details>

<summary><code>/youtool_viewas</code> — preview what a position sees</summary>

Stand in a store and run `/youtool_viewas manager`. The tablet and the server now treat you exactly like that position, so you see which tabs and buttons it gets. `/youtool_viewas list` shows your current preview and the store's role ids; `/youtool_viewas off` (or `owner`) ends it. While you preview a position you are not corporate admin, but you can always run `/youtool_viewas off`. Needs the corporate ACE (or `Config.Manager.devBypass`).

</details>

<details>

<summary><code>/youtool_whoami</code> — your identity and corporate status</summary>

Prints your server id, whether you count as corporate admin, the framework, whether you have the corporate ACE, and your license:

```
[YouTool] src=2  corporateAdmin=false  framework=qbcore
[YouTool] ace[youtool.admin]=false
[YouTool] license=license:1a2b3c...
```

To grant corporate admin to that player, use the license with `identifier.` in front: `add_ace identifier.license:1a2b3c... youtool.admin allow`. Store positions are per store; see `youtool_roles`.

</details>

***

## Economy

| Command | Run from | Who | Output |
| --- | --- | --- | --- |
| `youtool_vault [storeId]` | Console or in game | Console, corporate admin (restricted) | Server console |
| `/youtool_vault_withdraw <storeId> <amount>` | In game only | `vault.withdraw` at that store (restricted) | Server console |
| `youtool_stock [storeId]` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_restock <storeId> <class> <pallets>` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_setstock <storeId> <class\|all> <points>` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_freight <storeId> <class> <pallets> [auto\|self\|logistics]` | Console or in game | Console, `stock.order` at that store (restricted) | Server console |
| `youtool_shipments` | Console or in game | Console, corporate admin | Server console |
| `youtool_markup [storeId]` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_setmarkup <storeId> <global\|Category Name> <percent>` | Console or in game | Console, `markup.edit` at that store (restricted) | Server console |
| `youtool_sales [storeId]` | Console or in game | Console, corporate admin (restricted) | Server console |
| `youtool_price <model> [storeId]` | Console or in game | Console, corporate admin (restricted) | Server console |
| `/youtool_setprice` | In game | Corporate admin | Dialog, on-screen notice |
| `/youtool_clearprice` | In game | Corporate admin | Dialog |
| `youtool_delist <storeId> <model> [on\|off]` | Console or in game | Console, corporate admin (restricted) | Server console |

Classes for the stock commands: `clutter`, `lighting`, `soft`, `electronics`, `surfaces`, `seating`, `storage`, `fixtures`, `bulky`. The stock and freight commands work in Active mode only (`Config.EconomyMode = 'Active'`).

<details>

<summary><code>youtool_vault</code> and <code>/youtool_vault_withdraw</code></summary>

`youtool_vault` lists every store's vault balance. With a store id it prints that balance and the last 10 vault entries. `/youtool_vault_withdraw youtool_sandy 5000` moves $5,000 from that vault to **your** bank; it needs `vault.withdraw` at that store. The Vault tab in the Console does the same with a button: see [Markup, Vault & Sales](console/markup-vault-sales.md#vault-tab).

</details>

<details>

<summary><code>youtool_stock</code>, <code>youtool_restock</code>, <code>youtool_setstock</code></summary>

`youtool_stock` prints the stock mode and the points in every class, for one store or all of them. `youtool_restock youtool_sandy seating 2` adds two pallets (`Config.Stock.palletPoints` each) to a class, up to its capacity, **free of charge**. `youtool_setstock youtool_sandy all 0` sets one class (or `all`) to an exact number of points and can also lower stock. Both are admin tools; managers refill stock by ordering freight. See [Stock & Freight](console/stock-and-freight.md).

</details>

<details>

<summary><code>youtool_freight</code> and <code>youtool_shipments</code></summary>

`youtool_freight youtool_sandy seating 2` orders freight like the Stock tab does: it prints the quote and the vault balance, then pays the order from the store vault. If the vault can't cover the quote, nothing is ordered and it prints `failed: Insufficient vault balance ($N)`. The optional last word (`auto`, `self` or `logistics`) delivers this one order in that mode without changing `Config.Delivery.mode`, which is handy for testing a mode. `youtool_shipments` lists the active shipment of every store with its pallets, unload progress and who claimed each pallet.

</details>

<details>

<summary><code>youtool_markup</code> and <code>youtool_setmarkup</code></summary>

`youtool_markup` prints every store's global, category and single-item markup and `Config.Markup.maxPercent`. `youtool_setmarkup youtool_sandy global 20` sets the global markup; a category name can have spaces: `youtool_setmarkup youtool_sandy Bar & Entertainment 25`. A negative percent needs `markup.negative` in game (the console may always). The cap from `Config.Markup.maxPercent` applies. Single-item markup is only in the Console.

</details>

<details>

<summary><code>youtool_sales</code> and <code>youtool_price</code></summary>

`youtool_sales` prints the sales count of every store (or one) and its last 10 sales: date, buyer, delivered / ordered units, gross and the vault's share. `youtool_price prop_bar_caddy youtool_sandy` shows how an item's price is built: base, corporate override, `Config.EconomyScale`, the store's markup and the final price. Without a store id it stops at the corporate price.

</details>

<details>

<summary><code>/youtool_setprice</code> and <code>/youtool_clearprice</code> — corporate base prices</summary>

`/youtool_setprice` opens a dialog: pick the item (searchable), enter the new base price. The price is before `Config.EconomyScale` and markup, and it applies to every store. `/youtool_clearprice` returns an item to its catalog price. Changes are saved in `data/catalog_overrides.json` and show at once. See [Catalog & Custom Furniture](catalog.md#corporate-changes). Only registered while `Config.PriceAdmin.enabled = true`.

</details>

<details>

<summary><code>youtool_delist</code> — hide a product at one store</summary>

`youtool_delist youtool_sandy prop_bar_caddy on` hides the product from that store's tablet and phone; `off` lists it again; without `on`/`off` it toggles. The Console's Catalog tab does the same for staff with `delist.edit`. See [Delisting](catalog.md#delisting).

</details>

***

## Player

| Command | Run from | Who | Output |
| --- | --- | --- | --- |
| `youtool_toggle_tablet` | Key binding (default `E`) | Anyone, inside a store | Opens or closes the tablet |

`youtool_toggle_tablet` is the key binding behind "\[E] Open Tablet". Players can change the key in GTA Settings › Key Bindings › FiveM; `Config.Tablet.showKey` only sets the starting key; `showKey = false` turns the key off for everyone. It does nothing outside a store, during a 3D preview, while carrying a freight box, or while placing a display.

### Testing helpers

| Command | Run from | Who | What it does |
| --- | --- | --- | --- |
| `/youtool_open` | In game | Anyone | Opens the tablet anywhere on the map, for testing without walking to a store. |
| `/youtool_close` | In game | Anyone | Closes it again. |

{% hint style="warning" %}
These two have no permission check: any player can open the tablet away from a store and browse. Checkout still works only inside a store (or through the phone app), because the server checks where the player is.
{% endhint %}

***

## ACE permissions

YouTool uses two ACEs of its own. Store work (markup, vault, stock, staff) is **not** an ACE: it comes from being a store's owner or staff. See [Corporate admin vs store roles](console/staff-and-permissions.md#corporate-admin-vs-store-roles).

| ACE | Set in | Grants |
| --- | --- | --- |
| `youtool.admin` | `Config.Roles.corporateAce` | **Corporate admin**: base prices and product names for all stores, the console-style commands above in game, `/youtool_viewas`, the Console button in every store. Also allowed to run `/youtool_diag` and `/youtool_testall`. |
| `youtool.tester` | `Config.TestCommands.acePerm` | `/youtool_diag` and `/youtool_testall` in game, nothing else. |

{% code title="server.cfg" %}
```
# Corporate admin for everyone in group.admin
add_ace group.admin youtool.admin allow

# Put a player in group.admin (their license from /youtool_whoami)
add_principal identifier.license:1a2b3c4d5e6f group.admin

# Or give one player only the corporate ACE
add_ace identifier.license:1a2b3c4d5e6f youtool.admin allow

# A tester who may run /youtool_diag and /youtool_testall
add_ace identifier.license:7a8b9c0d1e2f youtool.tester allow

# Restricted commands in game (already in many server.cfg files)
add_ace group.admin command allow
```
{% endcode %}

If you change `Config.Roles.corporateAce` or `Config.TestCommands.acePerm`, use your names in these lines. Lines in server.cfg apply on the next server start; to apply one now, type it in the server console.

{% hint style="danger" %}
`Config.Manager.devBypass = true` makes **every** player corporate admin and gives them every store permission. Keep it `false` on a live server.
{% endhint %}
