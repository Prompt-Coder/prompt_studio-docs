# 🚓 San Andreas Highway Patrol (2 Locations)

{% embed url="https://store.prompt-mods.com/store/package/7030238" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**
{% endembed %}

{% embed url="https://youtu.be/ilTj6G166b4" fullWidth="false" %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt+Studio+-+San+Andreas+Highway+Patrol+%28SAHP%29).

After downloading, **you will get a folder named:**

<pre><code><strong>prompt_sahp
</strong></code></pre>

Drag and drop the downloaded folder inside your resources directory.\
When done, the full path should look like this:

<pre><code><strong>resources/prompt_sahp
</strong></code></pre>
{% endstep %}

{% step %}
#### Open your `server.cfg` and add this line:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sahp
</strong></code></pre>

Save the file once done.
{% endstep %}

{% step %}
#### If you’re using [**ox\_lib**](https://github.com/overextended/ox_lib), you can use the command `/sahp`.

> This command allows you to toggle entity sets (like the **Briefing Room**) inside the map.
>
> Currently, the entity set does **not** auto-spawn based on config — use the command manually for now.
{% endstep %}

{% step %}
#### Restart your server and test both map locations:

**1. La Mesa Location:** `839.7197, -1291.275, 27.0595`\
**2. Freeway Location:** `1538.29822, 803.9021, 77.9835052`

If both interiors appear, installation is complete ✅\
[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

{% hint style="info" %}
💡 **Tip:** You can remove one of the two locations by deleting its placement folder inside `/stream`:

* `city_placement` — removes La Mesa
* `freeway_placement` — removes the Freeway location
{% endhint %}

***

### Additional Information

{% tabs %}
{% tab title="Features & Customization" %}
**🏢 Main Features**

* **Two Unique Locations:**
  * City (La Mesa)
  * Freeway (Countryside)
* **Briefing Room** — Includes two entity sets:
  * `onlychairs`
  * `chairsandtables`
* **Mechanic Interior** _(only La Mesa)_
* **Jail Cells**
* **Armory**
* **Evidence Room**
* **Dispatch Nest with 360° View**
* **Dynamic Props** (chairs, tables, etc.)
* **Editable 3D Logos** — Fully customizable

***

**🎨 Custom Logo & Texture Editing**

If you want to replace 3D logos with a flat texture for custom branding:

1.  Copy everything from:

    ```
    prompt_sahp/replacethese
    ```

    into:

    ```
    prompt_sahp/stream/3d_logos_replace
    ```

    _(Replace existing files when prompted)_
2. Open `chuz_is_exterior_props.YTD` using **OpenIV**.
3. Change the following texture names to your custom ones:
   * `customtexture1`
   * `customtexture2`
4. Save the file and enjoy your custom signage!
{% endtab %}

{% tab title="Compatibility & Locations" %}
**✅ Compatible Scripts**

* **ox\_lib** — Entity set toggle via `/sahp`
* **ox\_doorlock** — Supports door configuration
* **Custom dispatch or PD scripts** — Fully compatible with multiple interiors

***

**🗺️ Map Locations**

| Location            | Coordinates                     | Notes                                       |
| ------------------- | ------------------------------- | ------------------------------------------- |
| **La Mesa HQ**      | `839.7197, -1291.275, 27.0595`  | Includes mechanic garages + bigger car park |
| **Freeway Outpost** | `1538.29822, 803.9021, 77.9835` | Highway Station                             |
{% endtab %}

{% tab title="Doorlock SQL" %}
**🚪 ox\_doorlock — Preconfigured Doors (SQL)**

> IDs shifted to start at **1157** as requested.\
> Table: `ox_doorlock` (columns: `id`, `name`, `data`)

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(1157, 'San Andreas Highway Patrol 1-E-1', '{"state":1,"maxDistance":2,"doors":[{"model":1500778245,"heading":269,"coords":{"x":826.8927612304688,"y":-1292.00732421875,"z":26.94489860534668}},{"model":-1648968777,"heading":90,"coords":{"x":826.8682250976563,"y":-1289.55859375,"z":27.13917350769043}}],"coords":{"x":826.8804931640625,"y":-1290.782958984375,"z":27.04203605651855}}'),
	(1158, 'San Andreas Highway Patrol 1-G-1', '{"heading":269,"state":1,"maxDistance":2,"doors":false,"model":-296465450,"coords":{"x":832.0521240234375,"y":-1308.6317138671876,"z":21.99654197692871}}'),
	(1159, 'San Andreas Highway Patrol 1-G-2', '{"heading":90,"state":1,"maxDistance":2,"doors":false,"model":-296465450,"coords":{"x":855.1661376953125,"y":-1309.1171875,"z":21.99654197692871}}'),
	(1160, 'San Andreas Highway Patrol 1-0-1', '{"state":1,"maxDistance":2,"doors":[{"model":-401689590,"heading":360,"coords":{"x":838.494384765625,"y":-1286.6285400390626,"z":21.38411521911621}},{"model":-401689590,"heading":180,"coords":{"x":841.5875244140625,"y":-1286.6397705078126,"z":21.38411521911621}}],"coords":{"x":840.0409545898438,"y":-1286.6341552734376,"z":21.38411521911621}}'),
	(1161, 'San Andreas Highway Patrol 1-0-2', '{"heading":359,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":842.0283813476563,"y":-1282.2674560546876,"z":21.26981163024902}}'),
	(1162, 'San Andreas Highway Patrol 1-0-3', '{"heading":360,"state":1,"maxDistance":2,"doors":false,"model":-512052251,"coords":{"x":836.7098388671875,"y":-1279.031494140625,"z":21.3351936340332}}'),
	(1163, 'San Andreas Highway Patrol 1-0-4', '{"heading":359,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":845.5384521484375,"y":-1279.945068359375,"z":21.26668357849121}}'),
	(1164, 'San Andreas Highway Patrol 1-0-5', '{"heading":360,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":842.05322265625,"y":-1275.26318359375,"z":21.37964630126953}}'),
	(1165, 'San Andreas Highway Patrol 1-0-6', '{"heading":90,"state":1,"maxDistance":2,"doors":false,"model":-2023754432,"coords":{"x":831.04638671875,"y":-1276.3692626953126,"z":20.92032432556152}}'),
	(1166, 'San Andreas Highway Patrol 1-0-7', '{"heading":90,"state":1,"maxDistance":2,"doors":false,"model":-2023754432,"coords":{"x":831.0704956054688,"y":-1272.58447265625,"z":20.91679954528808}}'),
	(1167, 'San Andreas Highway Patrol 1-0-8', '{"heading":359,"state":1,"maxDistance":2,"doors":false,"model":-534808108,"coords":{"x":824.4942016601563,"y":-1282.20849609375,"z":21.37639617919922}}'),
	(1168, 'San Andreas Highway Patrol 1-0-9', '{"heading":270,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":822.12255859375,"y":-1283.512451171875,"z":21.22291374206543}}'),
	(1169, 'San Andreas Highway Patrol 1-0-10', '{"heading":360,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":819.4856567382813,"y":-1286.0904541015626,"z":21.22292327880859}}'),
	(1170, 'San Andreas Highway Patrol 1-0-11', '{"heading":360,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":815.2892456054688,"y":-1286.0638427734376,"z":21.22292327880859}}'),
	(1171, 'San Andreas Highway Patrol 1-0-12', '{"heading":270,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":811.853271484375,"y":-1283.5311279296876,"z":21.22291183471679}}'),
	(1172, 'San Andreas Highway Patrol 1-E-2', '{"heading":360,"state":1,"maxDistance":2,"doors":false,"model":-1496111416,"coords":{"x":853.1488647460938,"y":-1303.2391357421876,"z":26.87011528015136}}'),
	(1173, 'San Andreas Highway Patrol 1-1-1', '{"heading":179,"state":1,"maxDistance":2,"doors":false,"model":-2096870465,"coords":{"x":855.608642578125,"y":-1287.7509765625,"z":26.86820793151855}}'),
	(1174, 'San Andreas Highway Patrol 1-1-2', '{"heading":359,"state":1,"maxDistance":2,"doors":false,"model":-2096870465,"coords":{"x":848.4393310546875,"y":-1291.828857421875,"z":26.86978721618652}}'),
	(1175, 'San Andreas Highway Patrol 1-1-3', '{"heading":359,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":840.3541259765625,"y":-1294.625,"z":26.73783683776855}}'),
	(1176, 'San Andreas Highway Patrol 1-1-4', '{"heading":359,"state":1,"maxDistance":2,"doors":false,"model":-534808108,"coords":{"x":838.0148315429688,"y":-1282.7620849609376,"z":26.85284233093261}}'),
	(1177, 'San Andreas Highway Patrol 1-1-5', '{"heading":269,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":843.0404663085938,"y":-1282.5860595703126,"z":26.74373435974121}}'),
	(1178, 'San Andreas Highway Patrol 1-E-3', '{"heading":90,"state":1,"maxDistance":2,"doors":false,"model":-1496111416,"coords":{"x":850.45166015625,"y":-1279.9642333984376,"z":31.92238044738769}}'),
	(1179, 'San Andreas Highway Patrol 1-2-1', '{"state":1,"maxDistance":2,"doors":[{"model":1058603288,"heading":269,"coords":{"x":850.8414306640625,"y":-1298.3837890625,"z":32.03200531005859}},{"model":1058603288,"heading":89,"coords":{"x":850.7913818359375,"y":-1296.424072265625,"z":32.03200531005859}}],"coords":{"x":850.81640625,"y":-1297.4039306640626,"z":32.03200531005859}}'),
	(1180, 'San Andreas Highway Patrol 1-2-2', '{"heading":360,"state":1,"maxDistance":2,"doors":false,"model":-337791066,"coords":{"x":848.3809204101563,"y":-1298.91845703125,"z":31.91198539733886}}'),
	(1181, 'San Andreas Highway Patrol 1-2-3', '{"heading":359,"state":1,"maxDistance":2,"doors":false,"model":-534808108,"coords":{"x":828.7325439453125,"y":-1294.5235595703126,"z":31.89305877685547}}'),
	(1182, 'San Andreas Highway Patrol 1-E-4', '{"state":1,"maxDistance":2,"doors":[{"model":-769163936,"heading":360,"coords":{"x":839.744873046875,"y":-1281.71337890625,"z":36.55096435546875}},{"model":588988478,"heading":179,"coords":{"x":837.1387939453125,"y":-1281.7440185546876,"z":36.35515594482422}}],"coords":{"x":838.4418334960938,"y":-1281.728759765625,"z":36.45306015014648}}'),
	(1183, 'San Andreas Highway Patrol 1-E-5', '{"state":1,"maxDistance":2,"doors":[{"model":-769163936,"heading":180,"coords":{"x":837.0455322265625,"y":-1300.1422119140626,"z":36.55103302001953}},{"model":588988478,"heading":359,"coords":{"x":839.6484985351563,"y":-1300.1131591796876,"z":36.35523223876953}}],"coords":{"x":838.3470458984375,"y":-1300.127685546875,"z":36.45313262939453}}'),
	(1184, 'San Andreas Highway Patrol 1-E-6', '{"heading":0,"state":1,"maxDistance":2,"doors":false,"model":1890297615,"coords":{"x":817.7721557617188,"y":-1395.22998046875,"z":26.44643974304199}}'),
	(1185, 'San Andreas Highway Patrol 1-E-7', '{"heading":0,"state":1,"maxDistance":2,"doors":false,"model":-1920147247,"coords":{"x":838.7015991210938,"y":-1395.229736328125,"z":26.44643974304199}}'),
	(1186, 'San Andreas Highway Patrol 1-E-8', '{"heading":0,"state":1,"maxDistance":2,"doors":false,"model":1890297615,"coords":{"x":837.3860473632813,"y":-1376.09521484375,"z":26.49585723876953}}'),
	(1187, 'San Andreas Highway Patrol 1-G-3', '{"heading":180,"state":1,"maxDistance":2,"doors":false,"model":1009208002,"coords":{"x":832.53857421875,"y":-1376.1351318359376,"z":27.54445457458496}}'),
	(1188, 'San Andreas Highway Patrol 1-G-4', '{"heading":180,"state":1,"maxDistance":2,"doors":false,"model":1009208002,"coords":{"x":823.892822265625,"y":-1376.1351318359376,"z":27.54445457458496}}'),
	(1189, 'San Andreas Highway Patrol 1-E-9', '{"heading":0,"state":1,"maxDistance":2,"doors":false,"model":-1920147247,"coords":{"x":818.9462280273438,"y":-1376.1114501953126,"z":26.49904441833496}}'),
	(1190, 'San Andreas Highway Patrol 1-E-10', '{"heading":180,"state":1,"maxDistance":2,"doors":false,"model":1890297615,"coords":{"x":876.484130859375,"y":-1362.327392578125,"z":27.78296089172363}}'),
	(1191, 'San Andreas Highway Patrol 1-E-11', '{"heading":270,"state":1,"maxDistance":2,"doors":false,"model":-1498975473,"coords":{"x":865.5462036132813,"y":-1336.844970703125,"z":26.47219085693359}}'),
	(1192, 'San Andreas Highway Patrol 1-1-6', '{"heading":0,"state":1,"maxDistance":2,"doors":false,"model":-1498975473,"coords":{"x":869.1976928710938,"y":-1336.5875244140626,"z":26.48830413818359}}'),
	(1193, 'San Andreas Highway Patrol 1-1-7', '{"heading":180,"state":1,"maxDistance":2,"doors":false,"model":263193286,"coords":{"x":876.7420654296875,"y":-1335.4268798828126,"z":26.48928070068359}}'),
	(1194, 'San Andreas Highway Patrol 1-G-5', '{"heading":270,"state":1,"maxDistance":2,"doors":false,"model":312268926,"coords":{"x":865.620361328125,"y":-1357.7913818359376,"z":27.77894592285156}}'),
	(1195, 'San Andreas Highway Patrol 1-G-6', '{"heading":270,"state":1,"maxDistance":2,"doors":false,"model":312268926,"coords":{"x":865.620361328125,"y":-1350.2237548828126,"z":27.77894592285156}}'),
	(1196, 'San Andreas Highway Patrol 1-G-7', '{"heading":270,"state":1,"maxDistance":2,"doors":false,"model":312268926,"coords":{"x":865.620361328125,"y":-1342.6832275390626,"z":27.77894592285156}}'),
	(1197, 'San Andreas Highway Patrol 2-E-1', '{"state":1,"maxDistance":2,"doors":[{"model":1500778245,"heading":331,"coords":{"x":1532.7564697265626,"y":792.3108520507813,"z":77.86890411376953}},{"model":-1648968777,"heading":151,"coords":{"x":1530.5992431640626,"y":793.4698486328125,"z":78.06317901611328}}],"coords":{"x":1531.6778564453126,"y":792.890380859375,"z":77.9660415649414}}'),
	(1198, 'San Andreas Highway Patrol 2-G-1', '{"heading":331,"state":1,"maxDistance":2,"doors":false,"model":-296465450,"coords":{"x":1549.808837890625,"y":788.8172607421875,"z":72.92054748535156}}'),
	(1199, 'San Andreas Highway Patrol 2-G-2', '{"heading":151,"state":1,"maxDistance":2,"doors":false,"model":-296465450,"coords":{"x":1561.37646484375,"y":808.8342895507813,"z":72.92054748535156}}'),
	(1200, 'San Andreas Highway Patrol 2-0-1', '{"state":1,"maxDistance":2,"doors":[{"model":-401689590,"heading":61,"coords":{"x":1533.6365966796876,"y":805.0684204101563,"z":72.30812072753906}},{"model":-401689590,"heading":241,"coords":{"x":1535.137451171875,"y":807.7730102539063,"z":72.30812072753906}}],"coords":{"x":1534.386962890625,"y":806.4207153320313,"z":72.30812072753906}}'),
	(1201, 'San Andreas Highway Patrol 2-0-3', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-512052251,"coords":{"x":1526.1202392578126,"y":807.1671142578125,"z":72.25920104980469}}'),
	(1202, 'San Andreas Highway Patrol 2-0-2', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":1531.519287109375,"y":810.2669677734375,"z":72.19381713867188}}'),
	(1203, 'San Andreas Highway Patrol 2-0-5', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":1525.3946533203126,"y":813.6651611328125,"z":72.30364990234375}}'),
	(1204, 'San Andreas Highway Patrol 2-0-4', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":1531.1766357421876,"y":814.4617919921875,"z":72.19068908691406}}'),
	(1205, 'San Andreas Highway Patrol 2-0-6', '{"heading":151,"state":1,"maxDistance":2,"doors":false,"model":-2023754432,"coords":{"x":1521.0577392578126,"y":803.4884643554688,"z":71.84432983398438}}'),
	(1206, 'San Andreas Highway Patrol 2-0-7', '{"heading":151,"state":1,"maxDistance":2,"doors":false,"model":-2023754432,"coords":{"x":1517.7532958984376,"y":805.3341064453125,"z":71.84080505371094}}'),
	(1207, 'San Andreas Highway Patrol 2-0-8', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-534808108,"coords":{"x":1523.01513671875,"y":794.9329833984375,"z":72.30039978027344}}'),
	(1208, 'San Andreas Highway Patrol 2-0-9', '{"heading":331,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":1523.0142822265626,"y":792.2265014648438,"z":72.14691925048828}}'),
	(1209, 'San Andreas Highway Patrol 2-0-10', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":1524.0018310546876,"y":788.6735229492188,"z":72.14692687988281}}'),
	(1210, 'San Andreas Highway Patrol 2-0-11', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":1521.95556640625,"y":785.0096435546875,"z":72.14692687988281}}'),
	(1211, 'San Andreas Highway Patrol 2-0-12', '{"heading":331,"state":1,"maxDistance":2,"doors":false,"model":581799596,"coords":{"x":1518.0802001953126,"y":783.2202758789063,"z":72.14691925048828}}'),
	(1212, 'San Andreas Highway Patrol 2-1-1', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":1541.5390625,"y":802.8430786132813,"z":77.6618423461914}}'),
	(1213, 'San Andreas Highway Patrol 2-1-2', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-534808108,"coords":{"x":1530.017822265625,"y":806.5121459960938,"z":77.77684783935547}}'),
	(1214, 'San Andreas Highway Patrol 2-1-3', '{"heading":331,"state":1,"maxDistance":2,"doors":false,"model":-548154470,"coords":{"x":1532.2862548828126,"y":811.0001220703125,"z":77.66773986816406}}'),
	(1215, 'San Andreas Highway Patrol 2-1-4', '{"heading":241,"state":1,"maxDistance":2,"doors":false,"model":-2096870465,"coords":{"x":1542.8701171875,"y":819.5217895507813,"z":77.7922134399414}}'),
	(1216, 'San Andreas Highway Patrol 2-1-5', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-2096870465,"coords":{"x":1542.98681640625,"y":811.2747192382813,"z":77.79379272460938}}'),
	(1217, 'San Andreas Highway Patrol 2-E-2', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-1496111416,"coords":{"x":1555.254150390625,"y":809.9004516601563,"z":77.79412078857422}}'),
	(1218, 'San Andreas Highway Patrol 2-2-1', '{"state":1,"maxDistance":2,"doors":[{"model":1058603288,"heading":330,"coords":{"x":1549.8878173828126,"y":810.2194213867188,"z":82.95600891113281}},{"model":1058603288,"heading":150,"coords":{"x":1548.146728515625,"y":811.1202392578125,"z":82.95600891113281}}],"coords":{"x":1549.017333984375,"y":810.6697998046875,"z":82.95600891113281}}'),
	(1219, 'San Andreas Highway Patrol 2-2-2', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-337791066,"coords":{"x":1549.170166015625,"y":807.805908203125,"z":82.83599090576172}}'),
	(1220, 'San Andreas Highway Patrol 2-2-3', '{"heading":61,"state":1,"maxDistance":2,"doors":false,"model":-534808108,"coords":{"x":1535.847900390625,"y":792.7098388671875,"z":82.81706237792969}}'),
	(1221, 'San Andreas Highway Patrol 2-E-3', '{"heading":151,"state":1,"maxDistance":2,"doors":false,"model":-1496111416,"coords":{"x":1533.561767578125,"y":818.7572021484375,"z":82.84638977050781}}'),
	(1222, 'San Andreas Highway Patrol 2-E-4', '{"state":1,"maxDistance":2,"doors":[{"model":-769163936,"heading":61,"coords":{"x":1529.9329833984376,"y":808.533447265625,"z":87.47496795654297}},{"model":588988478,"heading":241,"coords":{"x":1528.7034912109376,"y":806.2354125976563,"z":87.27915954589844}}],"coords":{"x":1529.3182373046876,"y":807.3843994140625,"z":87.37705993652344}}'),
	(1223, 'San Andreas Highway Patrol 2-E-5', '{"state":1,"maxDistance":2,"doors":[{"model":-769163936,"heading":241,"coords":{"x":1544.7779541015626,"y":797.2846069335938,"z":87.47503662109375}},{"model":588988478,"heading":61,"coords":{"x":1546.00732421875,"y":799.5791625976563,"z":87.27923583984375}}],"coords":{"x":1545.392578125,"y":798.431884765625,"z":87.37713623046875}}'),
	(1224, 'San Andreas Highway Patrol 2-G-3', '{"heading":62,"state":1,"maxDistance":2,"doors":false,"model":-1883393727,"coords":{"x":1548.6038818359376,"y":832.1038208007813,"z":78.27686309814453}}'),
	(1225, 'San Andreas Highway Patrol 2-G-4', '{"heading":62,"state":1,"maxDistance":2,"doors":false,"model":-1883393727,"coords":{"x":1551.8739013671876,"y":838.1289672851563,"z":78.27686309814453}}'),
	(1226, 'San Andreas Highway Patrol 2-G-5', '{"heading":331,"state":1,"maxDistance":2,"doors":false,"model":-810254778,"coords":{"x":1564.72607421875,"y":855.074462890625,"z":76.65892028808594}}');

```

{% hint style="warning" %}
Don’t edit IDs or JSON structure unless you know your door manager’s exact schema.\
The above is ready for **ox\_doorlock** as-is with IDs from **1157 → 1226**.
{% endhint %}
{% endtab %}

{% tab title="Chairs" %}


Chairs:

* prop\_off\_chair\_04b
* prop\_off\_chair\_03
* v\_corp\_offchair
* prop\_off\_chair\_01
* prop\_bench\_02
* prop\_sol\_chair
* apa\_mp\_h\_stn\_chairarm\_03
* prop\_chair\_04a
* v\_ret\_gc\_chair01
* v\_corp\_sidechair
* v\_serv\_ct\_chair02
* v\_ilev\_leath\_chr
* prop\_couch\_lg\_08
* v\_ret\_gc\_chair02
* bkr\_prop\_clubhouse\_offchair\_01a
* chuz\_is\_chair\_brief\_hwpdd
* chuz\_is\_custom\_bench\_bl\_hw\_pd
{% endtab %}

{% tab title="Troubleshooting & Support" %}
**Common Issues**

* **Interior not spawning?**
  * Ensure `prompt_sahp` is started in `server.cfg`.
  * Verify `ox_lib` is installed (if using `/sahp` command).
  * Check that `stream` folders aren’t missing or renamed.
* **Want only one location?**
  * Delete either `city_placement` or `freeway_placement` from `/stream`.
* **Textures not changing?**
  * Confirm you replaced files correctly and re-imported `.ytd` using OpenIV.

**Need help?**

Open a ticket on our support Discord with:

* Resource name (`prompt_sahp`)
* Console errors (if any)
* Screenshot or coordinates of issue

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endtab %}
{% endtabs %}
