# 🛋️ YouTool Furniture Store (2 locations)

{% embed url="https://portal.cfx.re/assets/granted-assets?page=1&sort=asset.updated_at&direction=asc&search=Prompt%27s+-+YouTool+Furniture+Store" %}
**Official asset for FiveM — available on CFX Portal and** [**Prompt’s Mods Store**](https://store.prompt-mods.com/store/package/7744463)
{% endembed %}

{% embed url="https://youtu.be/zkvGT3JkK-U" %}

The YouTool furniture store map: the vanilla **YouTool in Sandy Shores**, now fully enterable, and a brand-new **YouTool building in Davis**. Both have the same full showroom interior with 54 display zones across the furniture, bedroom, home, garden and garage departments.

{% hint style="info" %}
The map works on its own. To turn it into a working store with tablet shopping, checkout into your housing script, staff, markup and stock, add the **YouTool Furniture Store script**: [installation and documentation](../scripts/youtool-furniture-store/README.md).
{% endhint %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Install the map

Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+YouTool+Furniture+Store).

After downloading, **you will get a zip with a folder named**:

```
prompt_youtool
```

Drag and drop the folder inside your `resources` directory. Keep the folder name exactly as it is. When done, the full path should look like this:

```
resources/prompt_youtool
```
{% endstep %}

{% step %}
#### Step 2 — Add it to your server.cfg

```
ensure prompt_youtool
```

If you also use the YouTool Furniture Store script, start the map **before** the script:

```
ensure ox_lib
ensure prompt_youtool
ensure prompt_youtool_store_system
```

The rest of the script's start order is on the script's [installation page](../scripts/youtool-furniture-store/installation.md).
{% endstep %}

{% step %}
#### Step 3 — Optional: door locks

If you use [ox\_doorlock](https://github.com/overextended/ox_doorlock), run the SQL from the **Doorlock SQL** tab below on your database. It adds every door of both stores to the `ox_doorlock` table. Restart `ox_doorlock` (or the server) afterwards.
{% endstep %}

{% step %}
#### Step 4 — Optional: Truck You Repairs compatibility

If you also own [Truck You Repairs](truck-you-repairs.md), follow the **Compatibility** tab below. Both maps change the same ground and collision files next to the Sandy Shores YouTool, so without this step one of them loses its changes.
{% endstep %}

{% step %}
#### Step 5 — Restart your server

Restart your server and join it. Both stores should be enterable at the coordinates in the **Locations** tab.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

{% hint style="info" %}
💡 **Tip:** Always restart your server after adding new resources.
{% endhint %}

***

### Additional Information

{% tabs %}
{% tab title="Locations" %}
| Store | Coordinates | Folder |
| --- | --- | --- |
| Sandy Shores | 2722.27, 3483.45, 57.66 | `stream/sandy` |
| Davis | 69.41, -1768.76, 31.41 | `stream/grove` |

{% hint style="info" %}
To remove one of the stores, delete its folder from `prompt_youtool/stream` (`sandy` or `grove`). Keep everything in `stream/base (do not delete)`: both stores use it.
{% endhint %}
{% endtab %}

{% tab title="Compatibility" %}
#### Truck You Repairs

Truck You Repairs and YouTool both edit three vanilla files next to the Sandy Shores store. The merged versions of those files ship in:

```
prompt_youtool/compatibility_folder/truck_you_repairs/
```

```
hi@lr_cs4_02_13.ybn
lr_cs4_02_30.ybn
lr_cs4_02_strm_7.ymap
```

Copy these three files into **both** of the places below, replacing the files that are already there:

1. `prompt_youtool/stream/sandy/`
2. The `stream/Sandy_Shores_Placement/` folder of your Truck You Repairs resource. This is the same for both versions of the map: `cfx_prompt_Truck_you_Repairs` or `cfx_prompt_custom_Truck_Repairs`.

Then restart the server. With the same files in both resources, the start order of the two maps does not matter.
{% endtab %}

{% tab title="Doorlock SQL" %}
24 doors, 12 per store, with the same numbers at both stores. `E-` doors lead outside; `1-` doors are inside the store.

* **E-1, E-2** — main entrance double doors. They start **unlocked**, so customers can walk in.
* **E-3** — staff exit.
* **E-4, E-5** — staff-yard gates. They open automatically for authorised players in a vehicle (`auto`).
* **1-1 to 1-4** — gates behind the checkout counters.
* **1-5 to 1-7** — staff area doors.

To change which doors start locked, set `"state"` to `1` (locked) or `0` (unlocked) in a door's line before you run the SQL.

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES

	-- YouTool Davis (69, -1768)
	(DEFAULT, 'YouTool - Davis E-1', '{"doors":[{"model":-465829676,"heading":50,"coords":{"x":46.0933837890625,"y":-1755.1065673828125,"z":28.421070098876953}},{"model":-465829676,"heading":230,"coords":{"x":48.00187683105469,"y":-1752.8248291015625,"z":28.421070098876953}}],"coords":{"x":47.047630310058594,"y":-1753.9656982421875,"z":28.421070098876953},"state":0,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis E-2', '{"doors":[{"model":-465829676,"heading":230,"coords":{"x":51.851375579833984,"y":-1748.2225341796875,"z":28.421070098876953}},{"model":-465829676,"heading":50,"coords":{"x":49.94288635253906,"y":-1750.5042724609375,"z":28.421070098876953}}],"coords":{"x":50.897132873535156,"y":-1749.3634033203125,"z":28.421070098876953},"state":0,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis E-3', '{"model":-1551512196,"heading":320,"doors":false,"coords":{"x":88.48631286621094,"y":-1745.420166015625,"z":29.07091522216797},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis E-4', '{"model":-932256561,"heading":140,"doors":false,"coords":{"x":94.16400146484375,"y":-1749.9381103515625,"z":29.81410026550293},"state":1,"maxDistance":2,"auto":true}'),
	(DEFAULT, 'YouTool - Davis E-5', '{"model":-1696298565,"heading":140,"doors":false,"coords":{"x":101.24884033203125,"y":-1755.864013671875,"z":30.44591522216797},"state":1,"maxDistance":2,"auto":true}'),
	(DEFAULT, 'YouTool - Davis 1-1', '{"doors":[{"model":784332635,"heading":230,"coords":{"x":53.93782043457031,"y":-1757.480712890625,"z":29.12737274169922}},{"model":-893604018,"heading":50,"coords":{"x":55.56706619262695,"y":-1755.5328369140625,"z":29.12737274169922}}],"coords":{"x":54.75244140625,"y":-1756.5067138671875,"z":29.12737274169922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis 1-2', '{"doors":[{"model":784332635,"heading":230,"coords":{"x":64.11980438232422,"y":-1765.9986572265625,"z":29.12737274169922}},{"model":-893604018,"heading":50,"coords":{"x":65.7490463256836,"y":-1764.05078125,"z":29.12737274169922}}],"coords":{"x":64.9344253540039,"y":-1765.0247802734375,"z":29.12737274169922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis 1-3', '{"doors":[{"model":808995933,"heading":230,"coords":{"x":53.47763442993164,"y":-1760.4266357421875,"z":29.12737274169922}},{"model":-1838149389,"heading":50,"coords":{"x":55.086341857910156,"y":-1758.5032958984375,"z":29.12737274169922}}],"coords":{"x":54.281986236572266,"y":-1759.4649658203125,"z":29.12737274169922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis 1-4', '{"doors":[{"model":808995933,"heading":230,"coords":{"x":56.7808723449707,"y":-1756.4774169921875,"z":29.12737274169922}},{"model":-1838149389,"heading":50,"coords":{"x":58.3883056640625,"y":-1754.5555419921875,"z":29.12737274169922}}],"coords":{"x":57.584590911865234,"y":-1755.5164794921875,"z":29.12737274169922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis 1-5', '{"doors":[{"model":-1349811094,"heading":320,"coords":{"x":83.30101013183594,"y":-1757.037841796875,"z":28.61928939819336}},{"model":-1349811094,"heading":140,"coords":{"x":84.92583465576172,"y":-1758.3968505859375,"z":28.61928939819336}}],"coords":{"x":84.11341857910156,"y":-1757.7174072265625,"z":28.61928939819336},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis 1-6', '{"doors":[{"model":-1349811094,"heading":230,"coords":{"x":80.77375030517578,"y":-1755.595947265625,"z":28.61931610107422}},{"model":-1349811094,"heading":50,"coords":{"x":79.41470336914062,"y":-1757.220703125,"z":28.61931610107422}}],"coords":{"x":80.09422302246094,"y":-1756.4083251953125,"z":28.61931610107422},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Davis 1-7', '{"model":-1551512196,"heading":320,"doors":false,"coords":{"x":84.55655670166016,"y":-1750.292724609375,"z":28.61928939819336},"state":1,"maxDistance":2}'),

	-- YouTool Sandy Shores (2722, 3483)
	(DEFAULT, 'YouTool - Sandy Shores E-1', '{"doors":[{"model":-465829676,"heading":247,"coords":{"x":2748.5849609375,"y":3477.326171875,"z":54.672306060791016}},{"model":-465829676,"heading":67,"coords":{"x":2747.439453125,"y":3474.5810546875,"z":54.672306060791016}}],"coords":{"x":2748.01220703125,"y":3475.95361328125,"z":54.672306060791016},"state":0,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores E-2', '{"doors":[{"model":-465829676,"heading":67,"coords":{"x":2745.12890625,"y":3469.043701171875,"z":54.672306060791016}},{"model":-465829676,"heading":247,"coords":{"x":2746.2744140625,"y":3471.788818359375,"z":54.672306060791016}}],"coords":{"x":2745.70166015625,"y":3470.416259765625,"z":54.672306060791016},"state":0,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores E-3', '{"model":-1551512196,"heading":157,"doors":false,"coords":{"x":2710.97509765625,"y":3455.497802734375,"z":55.32215118408203},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores E-4', '{"model":-932256561,"heading":337,"doors":false,"coords":{"x":2704.212646484375,"y":3458.12744140625,"z":56.06533432006836},"state":1,"maxDistance":2,"auto":true}'),
	(DEFAULT, 'YouTool - Sandy Shores E-5', '{"model":-1696298565,"heading":337,"doors":false,"coords":{"x":2695.6884765625,"y":3461.6845703125,"z":56.69715118408203},"state":1,"maxDistance":2,"auto":true}'),
	(DEFAULT, 'YouTool - Sandy Shores 1-1', '{"doors":[{"model":784332635,"heading":67,"coords":{"x":2740.389404296875,"y":3477.265869140625,"z":55.37860870361328}},{"model":-893604018,"heading":247,"coords":{"x":2739.411376953125,"y":3474.92236328125,"z":55.37860870361328}}],"coords":{"x":2739.900390625,"y":3476.09423828125,"z":55.37860870361328},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores 1-2', '{"doors":[{"model":784332635,"heading":67,"coords":{"x":2728.138427734375,"y":3482.379150390625,"z":55.37860870361328}},{"model":-893604018,"heading":247,"coords":{"x":2727.16064453125,"y":3480.03564453125,"z":55.37860870361328}}],"coords":{"x":2727.649658203125,"y":3481.20751953125,"z":55.37860870361328},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores 1-3', '{"doors":[{"model":808995933,"heading":67,"coords":{"x":2739.954833984375,"y":3480.215576171875,"z":55.37860870361328}},{"model":-1838149389,"heading":247,"coords":{"x":2738.9892578125,"y":3477.901611328125,"z":55.37860870361328}}],"coords":{"x":2739.471923828125,"y":3479.05859375,"z":55.37860870361328},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores 1-4', '{"doors":[{"model":808995933,"heading":67,"coords":{"x":2737.971923828125,"y":3475.464111328125,"z":55.37860870361328}},{"model":-1838149389,"heading":247,"coords":{"x":2737.007080078125,"y":3473.152099609375,"z":55.37860870361328}}],"coords":{"x":2737.489501953125,"y":3474.30810546875,"z":55.37860870361328},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores 1-5', '{"doors":[{"model":-1349811094,"heading":157,"coords":{"x":2712.479736328125,"y":3468.130615234375,"z":54.87052536010742}},{"model":-1349811094,"heading":337,"coords":{"x":2710.52490234375,"y":3468.946533203125,"z":54.87052536010742}}],"coords":{"x":2711.50244140625,"y":3468.53857421875,"z":54.87052536010742},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores 1-6', '{"doors":[{"model":-1349811094,"heading":67,"coords":{"x":2715.321044921875,"y":3467.503662109375,"z":54.87055206298828}},{"model":-1349811094,"heading":247,"coords":{"x":2716.136962890625,"y":3469.45849609375,"z":54.87055206298828}}],"coords":{"x":2715.72900390625,"y":3468.48095703125,"z":54.87055206298828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'YouTool - Sandy Shores 1-7', '{"model":-1551512196,"heading":157,"doors":false,"coords":{"x":2713.2822265625,"y":3461.31689453125,"z":54.87052536010742},"state":1,"maxDistance":2}');
```
{% endtab %}

{% tab title="Open Files" %}
These files are not encrypted, so you can edit them:

* every `.ymap`, `.ytyp`, `.ybn` and `.ytd` in `stream`, including the store textures
* `stream/sandy`, `stream/grove` and `stream/occlusion`
* `stream/base (do not delete)/pricetags` (the price tag models)
* `stream/base (do not delete)/unlocked`
* `compatibility_folder`
{% endtab %}

{% tab title="Troubleshooting & Support" %}
**Common Issues**

* **Store not loading?** Check that the folder is named `prompt_youtool` and that `ensure prompt_youtool` is in your `server.cfg`.
* **Parts of the building or some props missing?** Set `sv_enforceGameBuild 3258` (or newer) in your `server.cfg`.
* **No price tags or price boards in the store?** Those are spawned by the [YouTool Furniture Store script](../scripts/youtool-furniture-store/README.md); the map only provides the models.
* **Ground or bushes look wrong next to Truck You Repairs in Sandy Shores?** Follow the **Compatibility** tab.

**Need Help?**

Open a ticket with:

* Resource name: **prompt\_youtool**
* Server artifact version and game build
* Console error logs (if any)

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endtab %}
{% endtabs %}
