# 🏙️ Sandy Shores Downtown

## Sandy Shores Downtown

The downtown block of Sandy Shores, fully reworked — a row of shopfronts with **16 enterable interiors** behind them, from the bakery and coffee shop to the club, the pawn shop and the fire station museum. Built to slot into the wider Sandy Shores rework as the town's commercial centre.

{% embed url="https://www.youtube.com/watch?v=SkQnps2NYU4" %}

***

{% hint style="info" %}
Pure map resource — no framework, no dependencies. It only needs the correct **Sandy MapData** installed.
{% endhint %}

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Add the resource

Place the `prompt_sandy_downtown` folder inside your `resources` directory.

<pre><code><strong>resources/prompt_sandy_downtown
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Add to your server.cfg

Insert the following line to ensure the map loads automatically:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_downtown
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 3 — Set up MapData

Make sure you have the correct [**Sandy MapData**](sandy-mapdata.md) installed.
{% endstep %}

{% step %}
#### Step 4 — Test the map

Restart your server and visit **Sandy Shores Downtown**.\
If the map and interiors load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

{% hint style="info" %}
💡 **Tip:** Always restart your server after adding new resources — especially when adding multiple Sandy area maps.
{% endhint %}

***

:round\_pushpin:Location: **1680.4, 3735.15, 35.58**

***

### Interiors

Sixteen interiors sit behind the downtown shopfronts.

{% tabs %}
{% tab title="Custom-built" %}
Purpose-built interiors with their own streamed models, props and textures:

| Business | Type | Folder |
| --- | --- | --- |
| **Aztec Threadz** | Clothing store | `Aztec` |
| **Wholesum Bakery** | Bakery | `Bakery` |
| **Las Cuadras Bar** | Bar | `Bar` |
| **Revolution Nightclub** | Nightclub | `Club` |
| **RimShot Coffee** | Coffee shop | `Coffee Shop` |
| **Dream Cream** | Ice cream parlour | `Dream Cream` |
| **Fire Station Museum** | Museum | `Fire Station` |
| **Kirklands Lawfirm** | Law office | `Lawyers Office` |
| **Pawn World** | Pawn shop | `Pawn Shop` |
| **Post Op** | — | `Post Op` |
| **Pipe Down** | — | `Pipedown` |
| **Apartment Tunnel** | Connecting tunnel | `Apartment_Tunnel` |

{% hint style="info" %}
The **Folder** column is the directory under `stream/Interiors/` — useful when editing assets or picking which interiors to strip with the Exterior-Only add-on, since the folder names don't always match the shop sign.
{% endhint %}
{% endtab %}

{% tab title="Placement-only" %}
Existing GTA interiors re-instanced into the downtown block, so the shopfronts open into a usable space out of the box:

* **Ammunation**
* **Fleeca**
* **Barber Shop**
* **Tattoo Shop**

The barber and tattoo slots are automatically upgraded when you own our custom versions — see [Custom interior swap](#custom-interior-swap) below.
{% endtab %}
{% endtabs %}

***

### Custom interior swap

The **Barber Shop** and **Tattoo Shop** slots ship with the standard GTA interior in place, and swap themselves out for our custom interiors the moment you install them:

<table data-view="cards"><thead><tr><th>Slot</th><th>Custom interior</th><th data-hidden data-card-target data-type="content-ref">Link</th></tr></thead><tbody><tr><td><strong>Barber Shop</strong></td><td><a href="https://store.prompt-mods.com/store/package/6897176">Sandy Barber Shop</a></td><td></td></tr><tr><td><strong>Tattoo Shop</strong></td><td><a href="https://store.prompt-mods.com/store/package/7226101">Sandy Tattoo Shop</a></td><td></td></tr></tbody></table>

**No configuration required.** When `prompt_barber` or `prompt_tattoo` is running, the map despawns the default GTA interior — visual *and* collision — and activates the custom placement in its place. Stop the resource and the default interior comes back.

{% hint style="success" %}
Start order doesn't matter. The custom interior resource can start before or after `prompt_sandy_downtown`, and the swap survives stopping and restarting it mid-session.
{% endhint %}

<details>

<summary>Forcing a slot manually</summary>

Auto-detection covers virtually every setup, but you can override a slot in `config.lua`:

{% code title="config.lua" %}
```lua
Config.Enabled = true   -- master switch for the whole auto-swap system
Config.Debug   = false  -- prints swap steps to F8; keep false for release

Config.Slots = {
    barber = {
        customResource = 'prompt_barber',
        forceUseCustom = nil,   -- nil = autodetect · true = always custom · false = always GTA
        -- ...
    },
}
```
{% endcode %}

Set `forceUseCustom = true` to pin the custom interior, or `false` to keep the GTA one even when the custom resource is running.

</details>

***

### Exterior-Only Mode

Don't need the interiors? Downtown is supported by the free [**Exterior-Only Add-On**](exterior-only-add-on.md), which strips 10 of its interiors while leaving the exterior fully intact — useful for servers that never send players inside.

***

### 🚪 Doorlock System

Every business in the block is compatible with [`ox_doorlock`](https://github.com/overextended/ox_doorlock). Import the SQL below into your database and restart `ox_doorlock`.

{% hint style="info" %}
The SQL uses `DEFAULT` for the `id` column, so your database assigns free IDs automatically on import — it won't conflict with doorlocks you already have.
{% endhint %}

<details>

<summary><strong>Sandy Shores Downtown Doorlock SQL (43 doors)</strong></summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(DEFAULT, 'Downtown - Post Op E-1', '{"doors":[{"heading":32,"coords":{"x":1717.7593994140626,"y":3767.69677734375,"z":34.6270523071289},"model":1016384536},{"heading":32,"coords":{"x":1719.25830078125,"y":3768.64990234375,"z":34.6270523071289},"model":234188502}],"coords":{"x":1718.5087890625,"y":3768.17333984375,"z":34.6270523071289},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Post Op E-2', '{"heading":305,"auto":true,"model":37538980,"doors":false,"coords":{"x":1706.1990966796876,"y":3764.38525390625,"z":35.37136459350586},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Post Op 1-1', '{"heading":302,"model":-920748642,"doors":false,"coords":{"x":1715.58203125,"y":3763.85546875,"z":34.65030288696289},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Post Op 1-2', '{"doors":[{"heading":215,"coords":{"x":1713.1656494140626,"y":3763.302978515625,"z":34.58510971069336},"model":570452871},{"heading":35,"coords":{"x":1711.03125,"y":3761.80859375,"z":34.58510971069336},"model":570452871}],"coords":{"x":1712.098388671875,"y":3762.5556640625,"z":34.58510971069336},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fire Station Museum E-1', '{"heading":215,"model":766714334,"doors":false,"coords":{"x":1704.80322265625,"y":3781.224853515625,"z":35.90521621704101},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fire Station Museum E-2', '{"heading":35,"model":766714334,"doors":false,"coords":{"x":1696.121826171875,"y":3786.700439453125,"z":35.90521621704101},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fire Station Museum E-3', '{"doors":[{"heading":35,"coords":{"x":1691.7496337890626,"y":3783.638916015625,"z":35.90521621704101},"model":-1343755796},{"heading":35,"coords":{"x":1694.921875,"y":3785.860107421875,"z":35.90521621704101},"model":1613908582}],"coords":{"x":1693.335693359375,"y":3784.74951171875,"z":35.90521621704101},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fire Station Museum E-4', '{"doors":[{"heading":35,"coords":{"x":1686.9989013671876,"y":3780.3125,"z":35.90521621704101},"model":-1343755796},{"heading":35,"coords":{"x":1690.171142578125,"y":3782.53369140625,"z":35.90521621704101},"model":1613908582}],"coords":{"x":1688.5849609375,"y":3781.423095703125,"z":35.90521621704101},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fire Station Museum 1-1', '{"heading":305,"model":315469615,"doors":false,"coords":{"x":1698.8798828125,"y":3793.843994140625,"z":35.79061508178711},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fire Station Museum 2-1', '{"heading":125,"model":-168004211,"doors":false,"coords":{"x":1700.2408447265626,"y":3783.67041015625,"z":42.22216796875},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Aztec Threadz E-1', '{"heading":30,"model":1769547318,"doors":false,"coords":{"x":1691.7607421875,"y":3755.64453125,"z":34.87936401367187},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Aztec Threadz 1-1', '{"doors":[{"heading":30,"coords":{"x":1695.7860107421876,"y":3748.296630859375,"z":34.50715637207031},"model":1663781267},{"heading":30,"coords":{"x":1697.1544189453126,"y":3749.0849609375,"z":34.50701904296875},"model":-1174964494}],"coords":{"x":1696.47021484375,"y":3748.69091796875,"z":34.50708770751953},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Aztec Threadz 1-2', '{"doors":[{"heading":30,"coords":{"x":1693.447021484375,"y":3746.9462890625,"z":34.50715637207031},"model":1663781267},{"heading":30,"coords":{"x":1694.8154296875,"y":3747.734375,"z":34.50701904296875},"model":-1174964494}],"coords":{"x":1694.1312255859376,"y":3747.34033203125,"z":34.50708770751953},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Ammunation E-1', '{"doors":[{"heading":32,"coords":{"x":1686.771240234375,"y":3763.7333984375,"z":35.68030548095703},"model":497763766},{"heading":212,"coords":{"x":1684.5654296875,"y":3762.36572265625,"z":35.68030548095703},"model":769975849}],"coords":{"x":1685.6683349609376,"y":3763.049560546875,"z":35.68030548095703},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Kirklands Lawfirm E-1', '{"heading":300,"model":-657338479,"doors":false,"coords":{"x":1690.3583984375,"y":3744.852294921875,"z":35.1551628112793},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Kirklands Lawfirm 1-1', '{"heading":210,"model":-797976951,"doors":false,"coords":{"x":1696.85888671875,"y":3750.578857421875,"z":40.38014984130859},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Kirklands Lawfirm 1-2', '{"heading":120,"model":1499821880,"doors":false,"coords":{"x":1692.5509033203126,"y":3754.761474609375,"z":40.38014984130859},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Kirklands Lawfirm 1-3', '{"heading":210,"model":1499821880,"doors":false,"coords":{"x":1691.7098388671876,"y":3748.40478515625,"z":40.38014984130859},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Kirklands Lawfirm E-2', '{"heading":30,"model":2115712982,"doors":false,"coords":{"x":1691.4508056640626,"y":3753.34423828125,"z":49.15582656860351},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub E-1', '{"doors":[{"heading":344,"coords":{"x":1674.8883056640626,"y":3757.180419921875,"z":35.21772003173828},"model":-808077456},{"heading":344,"coords":{"x":1673.5428466796876,"y":3757.5751953125,"z":35.21767807006836},"model":1895365180}],"coords":{"x":1674.215576171875,"y":3757.3779296875,"z":35.21769714355469},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-1', '{"heading":31,"model":-371594628,"doors":false,"coords":{"x":1679.6328125,"y":3780.285888671875,"z":29.73286056518554},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-2', '{"heading":31,"model":1320539233,"doors":false,"coords":{"x":1681.886962890625,"y":3762.947509765625,"z":29.74816131591797},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-3', '{"heading":31,"model":1320539233,"doors":false,"coords":{"x":1685.3421630859376,"y":3765.0234375,"z":29.74816131591797},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-4', '{"heading":31,"model":1320539233,"doors":false,"coords":{"x":1688.797119140625,"y":3767.099365234375,"z":29.74816131591797},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-5', '{"heading":301,"auto":true,"model":-86787942,"doors":false,"coords":{"x":1680.5911865234376,"y":3783.451904296875,"z":29.86302185058593},"state":1,"maxDistance":2,"hideUi":true}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-6', '{"heading":121,"model":1119224844,"doors":false,"coords":{"x":1679.550537109375,"y":3792.27685546875,"z":29.73316955566406},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-7', '{"heading":35,"model":1243635233,"doors":false,"coords":{"x":1695.07177734375,"y":3786.44140625,"z":31.85436630249023},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Revolution Nightclub 1-8', '{"heading":35,"model":-481505234,"doors":false,"coords":{"x":1701.3238525390626,"y":3785.4814453125,"z":31.8347110748291},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fleeca Bank E-1', '{"doors":[{"heading":121,"coords":{"x":1648.72216796875,"y":3724.705322265625,"z":34.5079116821289},"model":-1152174184},{"heading":121,"coords":{"x":1650.053466796875,"y":3722.481201171875,"z":34.50785064697265},"model":73386408}],"coords":{"x":1649.3878173828126,"y":3723.59326171875,"z":34.50788116455078},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Fleeca Bank 1-1', '{"heading":211,"model":-131754413,"doors":false,"coords":{"x":1642.5670166015626,"y":3723.789306640625,"z":34.43131256103515},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - RimShot Coffee E-1', '{"doors":[{"heading":305,"coords":{"x":1633.929443359375,"y":3740.447265625,"z":35.23486328125},"model":1483806759},{"heading":305,"coords":{"x":1635.2401123046876,"y":3738.575439453125,"z":35.23486328125},"model":-1377615086}],"coords":{"x":1634.584716796875,"y":3739.51123046875,"z":35.23486328125},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - RimShot Coffee E-2', '{"heading":303,"model":-2012649108,"doors":false,"coords":{"x":1625.266357421875,"y":3738.086669921875,"z":34.95374298095703},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - RimShot Coffee E-3', '{"heading":35,"model":-27801622,"doors":false,"coords":{"x":1620.510986328125,"y":3729.586669921875,"z":43.51833724975586},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Pawn World E-1', '{"doors":[{"heading":33,"coords":{"x":1631.35986328125,"y":3719.2109375,"z":34.84858703613281},"model":1880434591},{"heading":33,"coords":{"x":1633.0791015625,"y":3720.327392578125,"z":34.84858703613281},"model":1528200594}],"coords":{"x":1632.219482421875,"y":3719.76904296875,"z":34.84858703613281},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Pipe Down E-1', '{"doors":[{"heading":213,"coords":{"x":1623.6591796875,"y":3724.278564453125,"z":35.15398025512695},"model":-1487016665},{"heading":213,"coords":{"x":1622.1756591796876,"y":3723.3251953125,"z":35.15398025512695},"model":-490773479}],"coords":{"x":1622.91748046875,"y":3723.8017578125,"z":35.15398025512695},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Wholesum Bakery E-1', '{"heading":213,"model":1196418584,"doors":false,"coords":{"x":1622.7188720703126,"y":3712.94091796875,"z":34.68304061889648},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Wholesum Bakery E-2', '{"heading":29,"model":-904975529,"doors":false,"coords":{"x":1629.1640625,"y":3704.13134765625,"z":34.70452499389648},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Wholesum Bakery 1-1', '{"heading":303,"model":-720135998,"doors":false,"coords":{"x":1625.8714599609376,"y":3702.72900390625,"z":34.70452499389648},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Barber E-1', '{"heading":215,"model":-1844444717,"doors":false,"coords":{"x":1607.0667724609376,"y":3714.312255859375,"z":34.76668548583984},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Dream Cream E-1', '{"heading":30,"model":-1803541520,"doors":false,"coords":{"x":1620.0350341796876,"y":3698.97021484375,"z":34.73792266845703},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Dream Cream 1-1', '{"heading":33,"model":710765272,"doors":false,"coords":{"x":1615.76806640625,"y":3705.2646484375,"z":34.70764541625976},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Tattoo E-1', '{"heading":210,"model":1996122903,"doors":false,"coords":{"x":1601.6453857421876,"y":3710.825927734375,"z":35.13147735595703},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Downtown - Las Cuadras Bar E-1', '{"doors":[{"heading":212,"coords":{"x":1605.4034423828126,"y":3704.1201171875,"z":34.92715454101562},"model":-530185747},{"heading":32,"coords":{"x":1603.351806640625,"y":3702.861083984375,"z":34.92715454101562},"model":54922041}],"coords":{"x":1604.377685546875,"y":3703.49072265625,"z":34.92715454101562},"state":1,"maxDistance":2}');
```

</details>

***

### Notes

* Part of the **Sandy Shores rework** — designed to sit alongside the other Sandy maps.
* Exterior ships with **LODs, distant lights and LOD lights**, so the block reads correctly at range and at night.
* Textures, props and placements are left **open for editing** — the `unlocked` folders and the map's `.ymap` / `.ytyp` / `.ytd` files are not escrow-locked.
* A separate free [**Downtown Construction**](free-construction-zones.md) lot is available if you want a construction-in-progress variant of the area.

***

Need help? Join the [Prompt Studio Discord](https://discord.gg/rKbHHdfZFU) for support, bug reports, and feedback. Enjoy Sandy Shores Downtown on your FiveM server! 🚀
