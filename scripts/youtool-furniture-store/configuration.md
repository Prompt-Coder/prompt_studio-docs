---
description: Every owner setting in config.lua and config/*.lua, file by file, with the shipped defaults and what each one does.
icon: sliders
---

# Configuration

All owner settings are open files in `prompt_youtool_store_system`. The main switches are in `config.lua`; feature settings are in the `config/` folder; each housing integration has its own small `client/config.lua`. This page follows the order of the file list at the top of `config.lua`.

Changes take effect when the resource restarts.

{% hint style="info" %}
**Engine constants live in `shared/config_internal.lua`:** data file paths, save timers, texture names, DUI sizes and the price-tag prop pool. That file loads after `config.lua` and `config/*.lua` and only fills keys you did not set, so a value you put in your own config always wins. You normally never need to touch any of these.
{% endhint %}

***

## config.lua

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.language` | `'auto'` | Language of every player-facing text. `'auto'` follows ox\_lib's `setr ox:locale` convar. Or force one of `'en' 'de' 'es' 'fr' 'ru' 'pt' 'sv' 'no' 'fi' 'ar' 'ko' 'zh'`. See [Languages](languages.md). |
| `Config.interactionMode` | `'auto'` | Target script for the store props. `'auto'` uses ox\_target if it is running, else qb-target. `'ox_target'` / `'qb-target'` force one; `'none'` turns targeting off. |
| `Config.MoneySystem` | `'auto'` | `'auto'` uses the framework's money (QBCore, QBox, ESX); with no framework it behaves as `'free'`. `'free'`: nothing costs anything and every charge succeeds. `'custom'`: your own functions, see [Custom money](#custom-money). |
| `Config.EconomyScale` | `1.0` | Multiplies every price (catalog items, sets, freight, wages) before it is shown or charged. `10.0` makes a $1,000 item cost $10,000. |
| `Config.EconomyMode` | `'Passive'` | `'Passive'`: stores never run out. `'Active'`: every store holds limited stock per stock class and managers refill it by ordering freight paid from the store vault. See [Stock & Freight](console/stock-and-freight.md). |
| `Config.Stores` | 2 stores | One entry per store on the map. See [Stores](#stores). |
| `Config.StoreEnterRadius` | `120.0` | When a player enters a store, the server checks they are within this many meters of its `interiorCoords`. Store actions and in-store checkout are refused for a player outside this radius (phone app orders are the exception). Generous on purpose: it stops a manager of one store acting on another; it is not a cheat detector. |
| `Config.Roles.corporateAce` | `'youtool.admin'` | ACE for the corporate tools (base prices, product names). See [Commands & Permissions](commands.md#ace-permissions). |
| `Config.Debug` | `false` | Extra `[YouTool ...]` console output. Real errors always print. |
| `Config.Manager.devBypass` | `false` | Development only. See the warning below. |
| `Config.TestCommands.enabled` | `true` | Registers `/youtool_diag` and `/youtool_testall`. `false` = the commands don't exist. |
| `Config.TestCommands.acePerm` | `'youtool.tester'` | ACE that may run those two commands in game. The server console and players with `youtool.admin` always can. |

{% hint style="danger" %}
**Never turn on `Config.Manager.devBypass` on a live server.** It gives every player every store permission and corporate admin: any player can withdraw any vault, change prices and fire staff. The setup check reports it as a `[FAIL]`. To see what a position can do, use [`/youtool_viewas`](commands.md#store-admin) instead.
{% endhint %}

### Stores

Two stores ship: `youtool_sandy` (Sandy Shores) and `youtool_vespucci` (Davis). Both use the same MLO shell from the `prompt_youtool` map resource.

{% code title="config.lua" %}
```lua
{
  id = 'youtool_sandy',
  name = 'YouTool Furniture Store - Sandy Shores',
  interiorCoords = vector3(2722.26538, 3483.44873, 57.6610527),
  checkoutProp = 'i45pt_youtool_till_checkout',
  targetableProps = true,
},
```
{% endcode %}

| Field | Meaning |
| --- | --- |
| `id` | The store's key. It is saved with all of the store's data (owner, staff, vault, stock, markup, displays) and used by the commands. **Don't rename it once the store has been used.** |
| `name` | Display name of the store. |
| `interiorCoords` | A point inside the store. The client uses it to recognize the interior; the server uses it for the `Config.StoreEnterRadius` check. |
| `checkoutProp` | Model of the till players check out at. |
| `targetableProps` | `true` sets up the targets in this store (display furniture and the till). `false` = no targets in this store. |

### Custom money

Set `Config.MoneySystem = 'custom'` to use an economy script YouTool doesn't know. Then define three global functions **at the bottom of `server/framework.lua`**. That file is open (not encrypted). Functions defined in another resource are invisible to YouTool, so they must go in this file.

| Function | Must return |
| --- | --- |
| `CustomGetMoney(src, account)` | The player's balance (number) |
| `CustomRemoveMoney(src, amount, account)` | `true` only if the money was taken |
| `CustomAddMoney(src, amount, account)` | `true` only if the money was paid |

`account` is `'bank'` or `'cash'`. Checkout, refunds and vault deposits and withdrawals use `'bank'`. Unloading wages use the account from `Config.Delivery.unloadWage.account` (default `'cash'`).

{% code title="server/framework.lua (bottom of the file)" %}
```lua
-- Example only: replace my_economy with your own script's exports.
function CustomGetMoney(src, account)
    return exports.my_economy:GetBalance(src, account) or 0
end

function CustomRemoveMoney(src, amount, account)
    return exports.my_economy:RemoveMoney(src, account, amount) == true
end

function CustomAddMoney(src, amount, account)
    return exports.my_economy:AddMoney(src, account, amount) == true
end
```
{% endcode %}

If one of the three is missing, YouTool fails safe: a missing `CustomGetMoney` counts every balance as 0, a missing `CustomRemoveMoney` refuses every charge, so purchases are blocked instead of given away. A missing `CustomAddMoney` means refunds, withdrawals and wages are not paid. The console prints a `[YouTool Money]` warning once, and the setup check reports `[FAIL]` until all three exist.

***

## config/pricing.lua

How prices and markup work is explained in [Markup, Vault & Sales](console/markup-vault-sales.md).

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.Markup.global` | `0` | Starting markup in % for every category without its own entry. Only used for a store that has no saved markup yet. After that the store's managers set markup in the Console and their values win. |
| `Config.Markup.categories` | `{}` | Starting markup per category, for example `['Bar & Entertainment'] = 25`. The name must match a catalog category exactly ([the 16 categories](catalog.md#categories)). |
| `Config.Markup.maxPercent` | `0` | Highest markup % a manager may set (global, category or single item). The server rejects anything higher. `0` = no cap (the hard ceiling is 10000 %). |
| `Config.PriceAdmin.enabled` | `true` | The corporate catalog tools: base price and product name changes. `false` also switches off delisting and the `youtool_delist`, `youtool_price` and `youtool_whoami` commands, and saved price and name changes are ignored. |

***

## config/stock.lua

Only used when `Config.EconomyMode = 'Active'`. Stock classes, pallets and the stock bars are explained in [Stock & Freight](console/stock-and-freight.md).

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.Stock.initialFill` | `1000` | Points put into each class the first time a store runs in Active mode (capped at the class capacity). |
| `Config.Stock.palletPoints` | `100` | Points in one pallet, the unit managers order. |
| `Config.Stock.maxPoints` | `1000` | Capacity of any class not listed in `classMax`. `0` = no cap. |
| `Config.Stock.lowPercent` | `20` | At or below this % of capacity a class shows as running low (red) in the Console. |
| `Config.Stock.classMax` | see below | Capacity per class in points (the 100 % mark on the stock bar). |
| `Config.Stock.classPoints` | see below | Points one sold unit uses, per class. |

| Class | `classMax` | `classPoints` | About this many units |
| --- | --- | --- | --- |
| `clutter` | 800 | 1 | 800 |
| `lighting` | 800 | 2 | 400 |
| `soft` | 700 | 2 | 350 |
| `electronics` | 800 | 4 | 200 |
| `surfaces` | 960 | 8 | 120 |
| `seating` | 1000 | 10 | 100 |
| `storage` | 960 | 12 | 80 |
| `fixtures` | 980 | 14 | 70 |
| `bulky` | 900 | 18 | 50 |

***

## config/delivery.lua

How restock orders reach the store in Active mode. The delivery modes, unloading and order costs are explained in [Stock & Freight](console/stock-and-freight.md#delivery-modes).

### Config.Delivery

| Option | Default | Meaning |
| --- | --- | --- |
| `mode` | `'instant'` | `'instant'`: stock is credited the moment the order is paid. `'auto'`: pallets appear at the store dock after `arrivalDelayMs`. `'self'`: an employee drives the store truck to the warehouse and back. `'logistics'`: another resource delivers it (see `Config.Logistics`). |
| `requireUnload` | `true` | Every mode except `'instant'` ends with pallets at the dock that employees unload box by box. `false` = arrival credits stock directly (no pallets, no unloading, no wage). |
| `arrivalDelayMs` | `180000` | `'auto'` mode: milliseconds until the pallets arrive. |
| `boxesPerPallet` | `5` | Boxes an employee carries per pallet. |
| `unloadWage.source` | `'vault'` | `'vault'`: the wage is reserved from the store vault when the order is placed. `'mint'`: the wage is created from nothing. |
| `unloadWage.perPallet` | `15` | Wage per pallet before `Config.EconomyScale`, paid per box (`perPallet / boxesPerPallet`) to whoever drops it. |
| `unloadWage.account` | `'cash'` | `'cash'` or `'bank'`. |
| `claimIdleMs` | `300000` | A claimed pallet is released after this long without progress. |
| `dockLeaveRadius` | `60.0` | The claim is also released when the worker leaves the dock area (meters). |
| `renderRadius` | `200.0` | Players see dock pallets within this range (meters). |
| `dropBoxTtlMs` | `25000` | How long a dropped box stays visible in storage. |
| `vehicleKeys.system` | `'auto'` | `'self'` mode truck keys: `'auto'` (wasabi\_carlock, qbx\_vehiclekeys or qb-vehiclekeys), `'qb'`, `'qbx'`, `'wasabi'` or `'none'`. |
| `vehicleKeys.custom` | not set | For any other key script: `function(src, plate, netId) ... end`, runs on the server. |
| `truckTimeoutMs` | `1200000` | 20 minutes: an unfinished `'self'` run is cancelled, the truck removed, and the order can be dispatched again. |

### Config.Freight

The freight cost of an order is points ordered × rate of the class × `Config.EconomyScale`.

| Option | Default | Meaning |
| --- | --- | --- |
| `costPerPoint` | `1` | $ per point for any class not listed in `classCostPerPoint`. |
| `classCostPerPoint` | per class | $ per point per class. The defaults make the cheapest item of each class break even at 20 % markup: `clutter` 2.0, `lighting` 4.5, `soft` 2.5, `electronics` 1.75, `surfaces` 1.25, `seating` 0.6, `storage` 0.83, `fixtures` 0.71, `bulky` 0.56. |

### Config.Logistics

For `mode = 'logistics'`: a delivery resource of your own takes the order. The event and export it uses are on [Exports & Events](developers/exports-and-events.md#logistics-partner).

| Option | Default | Meaning |
| --- | --- | --- |
| `enabled` | `false` | Hand orders to the partner resource. |
| `resource` | `''` | Name of the partner resource. Only this resource may report an arrival. |
| `fallbackDelayMs` | `0` | If the partner isn't running (or `enabled` is `false`), the pallets arrive by themselves after this delay. `0` = immediately. |

***

## config/delivery\_layout.lua

Where restock deliveries happen, per store. It ships matching both YouTool stores at their default positions; edit it only if you moved a store or something on your map blocks a spot. It is used by the `'auto'`, `'self'` and `'logistics'` modes.

| Key | What it holds |
| --- | --- |
| `DeliveryLayout.models` | `pallet` (`prop_pallet_02a`) and `box` (`prop_cs_cardbox_01`) models. |
| `DeliveryLayout.warehouses` | `terminal` and `grapeseed`: `label`, `truckModel` (`mule`), `loadPoint` (vec4) and `loadRadius` (`25.0`) for the `'self'` run. |
| `DeliveryLayout.stores.<storeId>.warehouse` | Which warehouse that store's truck drives to (`youtool_sandy` → `grapeseed`, `youtool_vespucci` → `terminal`). |
| `.dockCenter` | The middle of the dock (vec3). |
| `.truckSpawns` | `'self'` mode truck spawn spots; the first free one is used. |
| `.dockZone` | The box (`center`, `size`, `rotation`) the loaded truck must drive into to deliver. |
| `.dockSpots` | Pallet spots on the dock. The number of spots is the most pallets one order can bring: 15 at Sandy Shores, 19 at Davis. |
| `.storageDrops` | Where carried boxes are dropped, a random one per box (24 per store). |

To record a new point, stand on it in game and run `/youtool_capture_spot <label>` (corporate admin). It appends a ready `vec4(...)` line to `data/captured_spots.txt` and prints it in the server console. Step by step: [The delivery layout](console/stock-and-freight.md#the-delivery-layout).

***

## config/price\_tags.lua

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.PriceTags.enabled` | `true` | Price tags managers place next to display furniture. Displays and tags are one system: `false` also switches off placing display furniture and showroom sets, and in 1.2.0 it stops the tablet key from working. Keep it `true`. |
| `Config.PriceTags.currency` | `{ symbol = '$', position = 'before' }` | Currency on the tags. `position = 'before'` shows `$100`, `'after'` shows `100€`. |
| `Config.PriceAtlas.enabled` | `true` | The price boards built into the store draw their prices live from the catalog, so price and markup changes show up in the store. Keep it `true`. |
| `Config.PriceAtlas.currency` | `{ symbol = '$', position = 'before' }` | Currency on the boards, as above. |

***

## config/sets.lua

Furniture sets are bundles sold together at a discount. Managers build them in the Console; see [Sets in the showroom](console/README.md#sets-in-the-showroom).

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.Sets.enabled` | `true` | `false` switches sets off. |
| `Config.Sets.maxItemsPerSet` | `20` | Items one set may contain. |
| `Config.Sets.maxInstancesPerStore` | `50` | Sets placed in the showroom, per store. |
| `Config.Sets.maxDefinitions` | `100` | Sets a store can have. |

***

## config/tablet.lua

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.Tablet.showKey` | `'E'` | Default key that opens the tablet inside a store. Players can rebind it in GTA Settings › Key Bindings › FiveM; this only sets the starting key. |
| `Config.Tablet.prompt` | `'nui'` | The "\[E] Open Tablet" hint while the tablet is closed: `'nui'` (YouTool's own prompt), `'ox_lib'` (ox\_lib text UI) or `'none'`. |
| `Config.Cart.maxItems` | `50` | Most items one cart may hold (tablet and phone). The server refuses any cart over 200 units regardless. |
| `Config.Target.distance` | `2.5` | How close (meters) a player must be to target a store prop. |
| `Config.Sounds.ui` | `false` | `false` = no tablet sounds; `'native'` = subtle GTA menu sounds. |

***

## config/housing.lua

YouTool detects your housing script by itself. Install steps per script: [Housing Integrations](housing/README.md).

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.VmsHousing.priceMultiplier` | `1.5` | vms\_housing only. YouTool adds its catalog to vms's furniture list at start (only models vms doesn't have). The price written there is catalog price × `Config.EconomyScale` × this value. Above 1.0 so vms's own furniture menu never undercuts the store. |

***

## config/showcase.lua

Demo mode for recording footage or a quick try-out on a bare server (ox\_lib and a target script, no framework, database or housing script). Money is free, every permission is granted and stand-in properties accept the order, so checkout completes. Stock, the vault and Sales History update for real, but the furniture is not delivered anywhere.

Turning it on forces `Config.MoneySystem = 'free'`, `Config.Manager.devBypass = true`, `Config.Delivery.mode = 'instant'` and `Config.Logistics.enabled = false`. `Config.EconomyMode` is left alone; set it to `'Active'` to show the stock bars.

{% hint style="danger" %}
**Never turn on `Config.Showcase.enabled` on a live server.** It hands out free furniture and full admin to every player. The setup check reports it as a `[WARN]`.
{% endhint %}

| Option | Default | Meaning |
| --- | --- | --- |
| `enabled` | `false` | Demo mode on or off. |
| `properties` | `{ 'Mercer Villa', 'Vinewood Hills Apartment', 'Paleto Bay House' }` | Stand-in properties offered at checkout (more than one, so the property picker appears). |
| `note` | `' (showcase demo - the furniture is not delivered)'` | Added to the checkout message. `''` hides it. |
| `displayName` | `'Showcase Account'` | Name on the Console login. |
| `displayRole` | `'Store Owner'` | Position on the Console login. `''` keeps the real one. |
| `names` | `{}` | Display names for identifiers saved in `data/store_roles.json`, so the Staff tab doesn't show every member as `displayName`. Showcase mode only. |

***

## Integration files

Each housing integration has a `client/config.lua` in `integrations/<script>/`. These files are open. YouTool chooses the integration by detecting which housing script is running, not from these files (order and details: [How YouTool picks the housing script](housing/README.md#how-youtool-picks-the-housing-script)).

In 1.2.0 two of these files have settings that change something:

{% tabs %}
{% tab title="qs-housing" %}
{% code title="integrations/qs-housing/client/config.lua" %}
```lua
return {
    enabled = true,
    debug = false,
    syncDelay = 5000,
    defaultCategory = 'decals',
    imagesEnabled = true,
    imagePath = 'nui://qs-housing/web/images/youtool/',
}
```
{% endcode %}

| Option | Default | Meaning |
| --- | --- | --- |
| `enabled` | `true` | `false` stops YouTool from adding its catalog to qs-housing's furniture list and from refreshing qs-housing's decorations after a purchase. Purchases are still delivered while qs-housing runs. |
| `debug` | `false` | `[YouTool QS-Housing]` debug lines in the console. |
| `syncDelay` | `5000` | Milliseconds YouTool waits after starting before it adds the catalog to qs-housing. Raise it if qs-housing loads slowly. |
| `defaultCategory` | `'decals'` | qs-housing category for items that match none of its categories. |
| `imagesEnabled` | `true` | Show the YouTool item images in qs-housing's furniture menu. |
| `imagePath` | `'nui://qs-housing/web/images/youtool/'` | Where those images are. The default needs the images copied into qs-housing; see [qs-housing](housing/qs-housing.md). |
{% endtab %}

{% tab title="ps-housing" %}
| Option | Default | Meaning |
| --- | --- | --- |
| `enabled` | `true` | `false` only hides the "Integration active" line in the client console. Purchases are still delivered while ps-housing runs. |
| `debug` | `false` | `[YouTool PS-Housing]` debug lines in the client console. |
{% endtab %}

{% tab title="Other scripts" %}
The files for bcs\_housing, brutal\_housing, nolag\_properties, rtx\_housing, RxHousing (`integrations/rxscripts/`) and vms\_housing contain `enabled` and `debug` (nolag\_properties also has menu category fields), but nothing reads them in 1.2.0. Leave them as they are.
{% endtab %}
{% endtabs %}
