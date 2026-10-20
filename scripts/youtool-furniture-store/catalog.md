---
description: The YouTool catalog file, its fields and 16 categories, item images, corporate price and name changes, adding your own props, and delisting.
icon: book-open
---

# Catalog & Custom Furniture

Everything the store sells comes from one file: `prompt_youtool_store_system/data/catalog.json`. It ships with 2,112 items in 16 categories. The server reads it at start to check every price at checkout; the tablet, the phone app and the Console read the same file.

On top of the catalog, three things change what players see, without editing the file:

* **Corporate changes** to base prices and product names, for all stores (corporate admin).
* **Markup** per store, category or item, set by store staff. See [Markup, Vault & Sales](console/markup-vault-sales.md).
* **Delisting**: a store hides a product from its own customers.

***

## The catalog file

`data/catalog.json` holds an `items` list. One entry:

{% code title="data/catalog.json" %}
```json
{
  "id": "prop_bar_caddy",
  "name": "Cocktail Umbrella Napkin Caddy",
  "model": "prop_bar_caddy",
  "category": "Bar & Entertainment",
  "subcategory": "Bar Accessories",
  "price": 220,
  "image": "images/prop_bar_caddy.webp",
  "stockClass": "clutter",
  "tags": ["caddy", "napkin holder", "bar"]
}
```
{% endcode %}

| Field | Meaning |
| --- | --- |
| `id` | Unique key of the item. Markup, delisting, corporate changes, displays and sets refer to it. In the shipped catalog it is always the same as `model`; keep it that way for your own items. |
| `name` | Product name shown to players. |
| `model` | The GTA model that is delivered to the property and spawned as a display. |
| `category` | One of the [categories](#categories). It drives the tablet's category list and category markup. |
| `subcategory` | Free text, used by the tablet's subcategory filter. |
| `price` | Base price in whole dollars, before `Config.EconomyScale` and markup. |
| `image` | Product image, relative to the resource folder (see [Images](#images)). |
| `stockClass` | Stock class for Active mode: `clutter`, `lighting`, `soft`, `electronics`, `surfaces`, `seating`, `storage`, `fixtures` or `bulky`. See [Stock & Freight](console/stock-and-freight.md#stock-classes). |
| `tags` | Descriptive keywords. The tablet and phone search don't use them yet; search matches the name, model, category and subcategory. |

112 items are YouTool's own models (their names start with `i45pt_youtool_`). They are streamed by the `prompt_youtool` map resource, so keep it running.

### Categories

| Category | Items |
| --- | --- |
| Decor & Accessories | 376 |
| Outdoor & Patio | 252 |
| Living Room | 213 |
| Lighting | 196 |
| Bar & Entertainment | 170 |
| Electronics | 149 |
| Kitchen | 142 |
| Garage & Workshop | 107 |
| Office | 101 |
| Commercial & Specialty | 88 |
| Storage | 65 |
| Bathroom & Laundry | 63 |
| Dining Room | 60 |
| Miscellaneous | 51 |
| Bedroom | 44 |
| Building & Doors | 35 |

Use these names exactly (with the `&`) in `Config.Markup.categories` and in `youtool_setmarkup`.

### Images

Product images are `.webp` files in `prompt_youtool_store_system/images/`. The `image` field is the path inside the resource, usually `images/<model>.webp` (YouTool's own models drop the `i45pt_youtool_` prefix, for example `images/ba_vip_table3.webp`). The tablet, the Console and the phone app load them straight from the resource; `fxmanifest.lua` already serves every `images/*.webp`, so a new image only has to be in that folder.

If an image is missing, the product still sells: the tablet shows an empty picture and the Console a placeholder icon.

Some housing scripts show their own pictures in their furniture menus and need YouTool's images copied into them (for example qs-housing). That's part of the install step on your script's [housing page](housing/README.md).

***

## Corporate changes

Corporate admins (`youtool.admin`, see [Commands & Permissions](commands.md#ace-permissions)) can change an item's base price and name for **every** store. Changes show at once in all tablets, price tags and price boards, and are saved in `data/catalog_overrides.json`, next to `catalog.json`, so they survive an update as long as you keep that file (see [The data folder](installation.md#the-data-folder)).

| Change | How |
| --- | --- |
| Base price | `/youtool_setprice` in game: pick the item, enter the new price. The price is before `Config.EconomyScale` and markup. |
| Back to the catalog price | `/youtool_clearprice` in game: pick the item. |
| Product name | Console › **Catalog**, select the item, edit **Name** (up to 64 characters). |
| Back to the catalog name | Type the catalog name back into **Name**. |

**Reset** in the Catalog tab appears on items you changed from your own Console. It clears both the item's base price change and its name change, and shows a hidden product again (with `delist.edit`).

To see how a price is built for one store, run `youtool_price <model> <storeId>` in the server console.

These tools only exist while `Config.PriceAdmin.enabled = true` (`config/pricing.lua`).

{% hint style="warning" %}
**Only some of the Catalog tab is saved on the server.** Name, **Reset**, the per-item markup, the visibility switch and **Place Display** are real changes. **Add Product**, the category, subcategory and image fields, **Export** and **Reset all** only keep a draft inside your own game client: customers never see it, and it can't be bought or placed. To add a product for real, add it to `data/catalog.json` as described below.
{% endhint %}

***

## Adding your own furniture

{% stepper %}
{% step %}
#### Make sure the model loads for everyone

The model must exist for every player: a base-game prop, or a custom prop streamed by a resource every player loads (the way `prompt_youtool` streams YouTool's own models). Check the name in game first, for example by spawning it with your admin menu.
{% endstep %}

{% step %}
#### Add an entry to data/catalog.json

Add an object to the `items` list with every field from [the catalog file](#the-catalog-file). Use the model name as `id`, an existing category, and one of the nine stock classes. Keep the file valid JSON (a comma between entries, none after the last one).
{% endstep %}

{% step %}
#### Add the image

Put `<model>.webp` in `prompt_youtool_store_system/images/` and point `image` at it: `images/<model>.webp`.
{% endstep %}

{% step %}
#### Tell your housing script about it

Most housing scripts only accept furniture they know. YouTool's install files add the catalog to them, but they read it when they start:

| Housing script | After you add an item |
| --- | --- |
| qs-housing | Nothing extra. YouTool adds every catalog item to qs-housing's furniture list each time YouTool starts. |
| ps-housing | Nothing extra. |
| nolag\_properties | Restart `nolag_properties` while YouTool is running. |
| bcs\_housing | Its install file is a fixed list. Add a line like `{ label = 'My Table', model = 'my_table', price = 500 },` to the list in `bcs_housing/furniture/others/youtool_furniture.lua`, and the same line to `integrations/bcs-housing/bcs_install/youtool_furniture.lua` (YouTool reads the label from there). Restart `bcs_housing`. |
| rtx\_housing | Restart `rtx_housing`. |
| RxHousing | Restart `RxHousing`. |
| vms\_housing | Restart YouTool (it adds missing models to vms's furniture list at start), then restart `vms_housing` once so it reloads that list. |
| brutal\_housing | Restart `brutal_housing`. |

Details per script: [Housing Integrations](housing/README.md).
{% endstep %}

{% step %}
#### Restart and test

Restart `prompt_youtool_store_system`, buy the item once and check it arrives and can be placed in the property. Staff can also put it in the showroom with **Place Display** in the Console.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
When you update YouTool you take the new `data/catalog.json`, which replaces your additions. Keep your own entries in a separate file and add them again after each update. Your images in `images/` and your corporate changes in `catalog_overrides.json` are kept if you copy them back.
{% endhint %}

***

## Delisting

A store can hide a product from its own customers. Delisting is **per store**: Sandy Shores can stop selling an item that Davis still sells.

* **Console:** Catalog tab, click the item's **Visible** / **Delisted** switch. Needs the `delist.edit` permission at that store.
* **Server console:** `youtool_delist <storeId> <model> [on|off]` (corporate admin). Without `on` or `off` it toggles.

A delisted product disappears from that store's tablet and phone app, is refused at checkout, and stays in the Console's Catalog marked **Delisted**, so you can list it again. Delisting is saved in `data/catalog_overrides.json`.

To stop selling an item everywhere, delist it at every store rather than deleting it from `catalog.json`: displays, sets and markup refer to the item by its id.
