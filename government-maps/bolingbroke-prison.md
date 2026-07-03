# ⛓️ BolingBroke Prison

{% embed url="https://fivem.prompt-mods.com/package/5771366" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**&#x20;
{% endembed %}

{% embed url="https://youtu.be/MxoVT-qNN14" fullWidth="false" %}
Part 1
{% endembed %}

{% embed url="https://youtu.be/DcwNL_X5vo8?si=2bXPnlWGAOjLvEEh" %}

***

## Installation Instructions

{% stepper %}
{% step %}
### Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc). <a href="#step-1" id="step-1"></a>

After downloading, **you will get a zip with a folder named**:

```
[Prompt_Prison_Completed]
```

Drag and drop the downloaded folder inside your `resources` directory.\
When done, the full path should look like this:

<pre><code><strong>resources/[Prompt_Prison_Completed]
</strong></code></pre>
{% endstep %}

{% step %}
### Open your `server.cfg` file and add this line at the bottom:

<pre class="language-cfg"><code class="lang-cfg"><strong>start [Prompt_Prison_Completed]
</strong></code></pre>

Save the file once done.
{% endstep %}

{% step %}
### If you’re using [**ox\_doorlock**](https://github.com/overextended/ox_doorlock), go to the [**Doorlock SQL**](bolingbroke-prison.md#doorlock-sql) tab in this documentation.

> Copy the SQL script and import it into your database.\
> This will automatically configure all prison doors to be locked.
{% endstep %}

{% step %}
### Restart your server and join it.

Once in-game, go to these coordinates to check the map:

```
1850.58, 2586.18, 45.67
```

If the map loads correctly, installation was successful ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

{% hint style="info" %}
💡 **Tip:** Always restart your server after adding a new resource, especially if it includes doorlocks or scripts.
{% endhint %}

***

## Additional Information

{% tabs %}
{% tab title="Compatibility & Location" %}
#### ✅ Compatible Scripts

* Prison Escape - [https://prompt-studio.gitbook.io/prompt-studio/\~/revisions/ltKPABJygiYCzkGaDUlF/scripts/prison-escape](https://prompt-studio.gitbook.io/prompt-studio/~/revisions/ltKPABJygiYCzkGaDUlF/scripts/prison-escape)
* Anim Core - [https://store.prompt-mods.com/store/package/7110180](https://store.prompt-mods.com/store/package/7110180)
* RCore Prison — [https://store.rcore.cz/package/5341769](https://store.rcore.cz/package/5341769) (ALSO SUPPORTS ESCAPE CABALITIES NATIVELY)
*   PrisonSim — [https://store.dragonheartstudios.net/product/6633631](https://store.dragonheartstudios.net/product/6633631) (use code&#x20;

    `Prompt2025` for 15% off



* pioteq Police Job — [https://youtu.be/inQUbIoPwfg](https://youtu.be/inQUbIoPwfg)
* Prison Script — [https://www.dynyxscripts.com/product/6882920](https://www.dynyxscripts.com/product/6882920)



***

#### 🗺️ Map Location

* **Position**: `1850.58, 2586.18, 45.67`
{% endtab %}

{% tab title="Doorlock SQL" %}


#### 🚪 ox\_doorlock — Preconfigured Doors (SQL)

> Copy & import this into your database.\
> Table: `ox_doorlock` (columns: `id`, `name`, `data`)

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
-- Bolingbroke Entrance
(1986, 'Bolingbroke Entrance E-1', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1845.273193359375,"y":2586.538818359375,"z":46.05537033081055},"model":-129553421}'),
(1987, 'Bolingbroke Entrance E-2', '{"auto":true,"heading":90,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1844.998046875,"y":2604.81201171875,"z":44.63977813720703},"model":741314661}'),
(1988, 'Bolingbroke Entrance E-3', '{"auto":true,"heading":90,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1818.54296875,"y":2604.81201171875,"z":44.61100006103515},"model":741314661}'),
(1989, 'Bolingbroke Entrance E-4', '{"auto":true,"heading":180,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1799.6080322265626,"y":2616.97509765625,"z":44.6032485961914},"model":741314661}'),
(1990, 'Bolingbroke Entrance E-7', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1819.1627197265626,"y":2594.97900390625,"z":46.1569595336914},"model":-519068795}'),
(1991, 'Bolingbroke Entrance E-8', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1798.0899658203126,"y":2591.68701171875,"z":46.41783905029297},"model":-1156020871}'),
(1992, 'Bolingbroke Entrance E-9', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1797.760986328125,"y":2596.56494140625,"z":46.38731002807617},"model":-1156020871}'),
(1993, 'Bolingbroke Entrance E-10', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1790.9835205078126,"y":2593.050537109375,"z":46.18799591064453},"model":-519068795}'),
(1994, 'Bolingbroke Entrance E-11', '{"auto":true,"heading":110,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1835.2847900390626,"y":2689.10400390625,"z":44.44670104980469},"model":741314661}'),
(1995, 'Bolingbroke Entrance E-12', '{"auto":true,"heading":289,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1830.13427734375,"y":2703.49853515625,"z":44.44670104980469},"model":741314661}'),
(1996, 'Bolingbroke Entrance E-13', '{"auto":true,"heading":160,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1776.7012939453126,"y":2747.14794921875,"z":44.44668960571289},"model":741314661}'),
(1997, 'Bolingbroke Entrance E-14', '{"auto":true,"heading":340,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1762.195556640625,"y":2752.48876953125,"z":44.44668960571289},"model":741314661}'),
(1998, 'Bolingbroke Entrance E-15', '{"auto":true,"heading":207,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1662.010986328125,"y":2748.702880859375,"z":44.44668960571289},"model":741314661}'),
(1999, 'Bolingbroke Entrance E-16', '{"auto":true,"heading":27,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1648.411376953125,"y":2741.66845703125,"z":44.44668960571289},"model":741314661}'),
(2000, 'Bolingbroke Entrance E-17', '{"auto":true,"heading":234,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1584.65283203125,"y":2679.74951171875,"z":44.50946807861328},"model":741314661}'),
(2001, 'Bolingbroke Entrance E-18', '{"auto":true,"heading":55,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1575.719482421875,"y":2667.15185546875,"z":44.50946807861328},"model":741314661}'),
(2002, 'Bolingbroke Entrance E-19', '{"auto":true,"heading":267,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1547.7061767578126,"y":2591.2822265625,"z":44.50946807861328},"model":741314661}'),
(2003, 'Bolingbroke Entrance E-20', '{"auto":true,"heading":87,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1546.9833984375,"y":2576.129638671875,"z":44.39032745361328},"model":741314661}'),
(2004, 'Bolingbroke Entrance E-21', '{"auto":true,"heading":298,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1550.930419921875,"y":2482.743408203125,"z":44.39528656005859},"model":741314661}'),
(2005, 'Bolingbroke Entrance E-22', '{"auto":true,"heading":118,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1558.22119140625,"y":2469.34912109375,"z":44.39528656005859},"model":741314661}'),
(2006, 'Bolingbroke Entrance E-23', '{"auto":true,"heading":353,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1652.9840087890626,"y":2409.571044921875,"z":44.44308090209961},"model":741314661}'),
(2007, 'Bolingbroke Entrance E-24', '{"auto":true,"heading":173,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1667.6689453125,"y":2407.64794921875,"z":44.42879104614258},"model":741314661}'),
(2008, 'Bolingbroke Entrance E-25', '{"auto":true,"heading":27,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1749.1419677734376,"y":2419.81201171875,"z":44.4251708984375},"model":741314661}'),
(2009, 'Bolingbroke Entrance E-26', '{"auto":true,"heading":206,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1762.5419921875,"y":2426.507080078125,"z":44.43787002563476},"model":741314661}'),
(2010, 'Bolingbroke Entrance E-27', '{"auto":true,"heading":71,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1808.991943359375,"y":2474.544921875,"z":44.48077011108398},"model":741314661}'),
(2011, 'Bolingbroke Entrance E-28', '{"auto":true,"heading":252,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1813.7490234375,"y":2488.906982421875,"z":44.46368026733398},"model":741314661}'),

-- Bolingbroke Entrance 1
(2012, 'Bolingbroke Entrance 1-1', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1838.1968994140626,"y":2585.98974609375,"z":46.04365539550781},"model":320433149}'),
(2013, 'Bolingbroke Entrance 1-2', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1833.7188720703126,"y":2583.408203125,"z":46.03871154785156},"model":1242124150}'),
(2014, 'Bolingbroke Entrance 1-3', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1833.400634765625,"y":2579.8515625,"z":46.0405044555664},"model":-129553421}'),
(2015, 'Bolingbroke Entrance 1-4', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1836.760986328125,"y":2579.8515625,"z":46.0405044555664},"model":-129553421}'),
(2016, 'Bolingbroke Entrance 1-5', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1833.81103515625,"y":2586.61962890625,"z":44.87434768676758},"model":430324891}'),
(2017, 'Bolingbroke Entrance 1-6', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1833.81103515625,"y":2591.548828125,"z":44.87434768676758},"model":430324891}'),

-- Bolingbroke CellBlock1
(2018, 'Bolingbroke CellBlock1 E-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1773.1287841796876,"y":2678.835693359375,"z":45.82787704467773},"heading":325,"model":-1033001619},{"coords":{"x":1775.260498046875,"y":2677.34326171875,"z":45.82787704467773},"heading":145,"model":-1033001619}],"coords":{"x":1774.194580078125,"y":2678.08935546875,"z":45.82787704467773}}'),
(2019, 'Bolingbroke CellBlock1 E-2', '{"heading":10,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1760.3297119140626,"y":2678.4443359375,"z":46.11336898803711},"model":-519068795}'),
(2020, 'Bolingbroke CellBlock1 1-1', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1777.046142578125,"y":2681.793701171875,"z":44.64850616455078},"model":430324891}'),
(2021, 'Bolingbroke CellBlock1 1-2', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1762.1468505859376,"y":2681.101806640625,"z":45.0000114440918},"model":430324891}'),
(2022, 'Bolingbroke CellBlock1 1-3', '{"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1758.7388916015626,"y":2683.40185546875,"z":46.17937469482422},"model":458025182}'),
(2023, 'Bolingbroke CellBlock1 1-4', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1766.158447265625,"y":2686.98095703125,"z":45.0000114440918},"model":430324891}'),
(2024, 'Bolingbroke CellBlock1 1-5', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1763.9632568359376,"y":2690.733154296875,"z":46.18107223510742},"heading":325,"model":458025182},{"coords":{"x":1766.096923828125,"y":2689.239013671875,"z":46.18107223510742},"heading":145,"model":458025182}],"coords":{"x":1765.030029296875,"y":2689.986083984375,"z":46.18107223510742}}'),
(2025, 'Bolingbroke CellBlock1 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1767.1883544921876,"y":2695.328857421875,"z":45.81584167480469},"heading":325,"model":458025182},{"coords":{"x":1769.3177490234376,"y":2693.837890625,"z":45.81584167480469},"heading":145,"model":458025182}],"coords":{"x":1768.2530517578126,"y":2694.58349609375,"z":45.81584167480469}}'),
(2026, 'Bolingbroke CellBlock1 1-7', '{"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1763.770751953125,"y":2707.224365234375,"z":45.79965209960937},"model":458025182}'),
(2027, 'Bolingbroke CellBlock1 1-8', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1764.76806640625,"y":2710.88818359375,"z":45.79965209960937},"heading":325,"model":458025182},{"coords":{"x":1766.901123046875,"y":2709.394775390625,"z":45.79965209960937},"heading":145,"model":458025182}],"coords":{"x":1765.8345947265626,"y":2710.1416015625,"z":45.79965209960937}}'),
(2028, 'Bolingbroke CellBlock1 1-9', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1773.0447998046876,"y":2704.534423828125,"z":45.81743240356445},"heading":235,"model":458025182},{"coords":{"x":1771.5543212890626,"y":2702.40576171875,"z":45.81743240356445},"heading":55,"model":458025182}],"coords":{"x":1772.299560546875,"y":2703.47021484375,"z":45.81743240356445}}'),
(2029, 'Bolingbroke CellBlock1 1-10', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1791.1011962890626,"y":2677.056884765625,"z":44.64661026000976},"model":430324891}'),
(2030, 'Bolingbroke CellBlock1 1-11', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1789.3106689453126,"y":2672.483642578125,"z":45.80596542358398},"heading":145,"model":-1033001619},{"coords":{"x":1787.1827392578126,"y":2673.973388671875,"z":45.80596542358398},"heading":325,"model":-1033001619}],"coords":{"x":1788.2467041015626,"y":2673.228515625,"z":45.80596542358398}}'),
(2031, 'Bolingbroke CellBlock1 1-12', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1777.093017578125,"y":2688.26025390625,"z":44.62490844726562},"model":430324891}'),
(2032, 'Bolingbroke CellBlock1 1-13', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1774.0518798828126,"y":2690.3896484375,"z":44.62490844726562},"model":430324891}'),
(2033, 'Bolingbroke CellBlock1 1-14', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1771.1590576171876,"y":2692.4150390625,"z":44.62490844726562},"model":430324891}'),
(2034, 'Bolingbroke CellBlock1 1-15', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1768.25439453125,"y":2697.62353515625,"z":44.63115310668945},"model":430324891}'),
(2035, 'Bolingbroke CellBlock1 1-16', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.2705078125,"y":2700.5029296875,"z":44.63115310668945},"model":430324891}'),
(2036, 'Bolingbroke CellBlock1 1-17', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1774.1448974609376,"y":2706.0361328125,"z":44.63115310668945},"model":430324891}'),
(2037, 'Bolingbroke CellBlock1 1-18', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1777.524169921875,"y":2707.619140625,"z":44.62801742553711},"model":430324891}'),
(2038, 'Bolingbroke CellBlock1 1-19', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1780.2642822265626,"y":2705.700439453125,"z":44.62801742553711},"model":430324891}'),
(2039, 'Bolingbroke CellBlock1 1-20', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1783.272705078125,"y":2703.593994140625,"z":44.62801742553711},"model":430324891}'),
(2040, 'Bolingbroke CellBlock1 1-21', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1786.1363525390626,"y":2701.5888671875,"z":44.62801742553711},"model":430324891}'),
(2041, 'Bolingbroke CellBlock1 1-22', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1791.779541015625,"y":2697.63720703125,"z":44.62801742553711},"model":430324891}'),
(2042, 'Bolingbroke CellBlock1 1-23', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1794.7613525390626,"y":2695.549560546875,"z":44.62801742553711},"model":430324891}'),
(2043, 'Bolingbroke CellBlock1 1-24', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1797.63720703125,"y":2693.53564453125,"z":44.62801742553711},"model":430324891}'),
(2044, 'Bolingbroke CellBlock1 1-25', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1800.41552734375,"y":2691.59033203125,"z":44.62801742553711},"model":430324891}'),
(2045, 'Bolingbroke CellBlock1 1-26', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1800.793701171875,"y":2688.19580078125,"z":44.62445068359375},"model":430324891}'),
(2046, 'Bolingbroke CellBlock1 1-27', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1798.7735595703126,"y":2685.310791015625,"z":44.62445068359375},"model":430324891}'),
(2047, 'Bolingbroke CellBlock1 1-28', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1796.80419921875,"y":2682.49853515625,"z":44.62445068359375},"model":430324891}'),
(2048, 'Bolingbroke CellBlock1 1-29', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1794.8955078125,"y":2679.772705078125,"z":44.62445068359375},"model":430324891}'),
(2049, 'Bolingbroke CellBlock1 1-30', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1788.80224609375,"y":2680.062744140625,"z":44.62796783447265},"model":430324891}'),
(2050, 'Bolingbroke CellBlock1 1-31', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1785.90380859375,"y":2682.092041015625,"z":44.62796783447265},"model":430324891}'),
(2051, 'Bolingbroke CellBlock1 1-32', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1783.101318359375,"y":2684.054443359375,"z":44.62796783447265},"model":430324891}'),
(2052, 'Bolingbroke CellBlock1 2-1', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1777.093017578125,"y":2688.26025390625,"z":47.7756118774414},"model":430324891}'),
(2053, 'Bolingbroke CellBlock1 2-2', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1774.0518798828126,"y":2690.3896484375,"z":47.7756118774414},"model":430324891}'),
(2054, 'Bolingbroke CellBlock1 2-3', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1771.1590576171876,"y":2692.4150390625,"z":47.7756118774414},"model":430324891}'),
(2055, 'Bolingbroke CellBlock1 2-4', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1768.3978271484376,"y":2694.3486328125,"z":47.7756118774414},"model":430324891}'),
(2056, 'Bolingbroke CellBlock1 2-5', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1768.25439453125,"y":2697.62353515625,"z":47.7756118774414},"model":430324891}'),
(2057, 'Bolingbroke CellBlock1 2-6', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.2705078125,"y":2700.5029296875,"z":47.7756118774414},"model":430324891}'),
(2058, 'Bolingbroke CellBlock1 2-7', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1772.234375,"y":2703.3076171875,"z":47.7756118774414},"model":430324891}'),
(2059, 'Bolingbroke CellBlock1 2-8', '{"auto":true,"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1774.1448974609376,"y":2706.0361328125,"z":47.7756118774414},"model":430324891}'),
(2060, 'Bolingbroke CellBlock1 2-9', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1777.524169921875,"y":2707.619140625,"z":47.7756118774414},"model":430324891}'),
(2061, 'Bolingbroke CellBlock1 2-10', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1780.2642822265626,"y":2705.700439453125,"z":47.7756118774414},"model":430324891}'),
(2062, 'Bolingbroke CellBlock1 2-11', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1783.272705078125,"y":2703.593994140625,"z":47.7756118774414},"model":430324891}'),
(2063, 'Bolingbroke CellBlock1 2-12', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1786.1363525390626,"y":2701.5888671875,"z":47.7756118774414},"model":430324891}'),
(2064, 'Bolingbroke CellBlock1 2-13', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1791.779541015625,"y":2697.63720703125,"z":47.7756118774414},"model":430324891}'),
(2065, 'Bolingbroke CellBlock1 2-14', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1794.7613525390626,"y":2695.549560546875,"z":47.7756118774414},"model":430324891}'),
(2066, 'Bolingbroke CellBlock1 2-15', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1797.63720703125,"y":2693.53564453125,"z":47.7756118774414},"model":430324891}'),
(2067, 'Bolingbroke CellBlock1 2-16', '{"auto":true,"heading":145,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1800.41552734375,"y":2691.59033203125,"z":47.7756118774414},"model":430324891}'),
(2068, 'Bolingbroke CellBlock1 2-17', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1800.793701171875,"y":2688.19580078125,"z":47.7756118774414},"model":430324891}'),
(2069, 'Bolingbroke CellBlock1 2-18', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1798.7735595703126,"y":2685.310791015625,"z":47.7756118774414},"model":430324891}'),
(2070, 'Bolingbroke CellBlock1 2-19', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1796.80419921875,"y":2682.49853515625,"z":47.7756118774414},"model":430324891}'),
(2071, 'Bolingbroke CellBlock1 2-20', '{"auto":true,"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1794.8974609375,"y":2679.775146484375,"z":47.7756118774414},"model":430324891}'),
(2072, 'Bolingbroke CellBlock1 2-21', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1791.77197265625,"y":2677.9833984375,"z":47.7756118774414},"model":430324891}'),
(2073, 'Bolingbroke CellBlock1 2-22', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1788.80224609375,"y":2680.062744140625,"z":47.7756118774414},"model":430324891}'),
(2074, 'Bolingbroke CellBlock1 2-23', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1785.90380859375,"y":2682.092041015625,"z":47.7756118774414},"model":430324891}'),
(2075, 'Bolingbroke CellBlock1 2-24', '{"auto":true,"heading":325,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1783.101318359375,"y":2684.054443359375,"z":47.7756118774414},"model":430324891}'),

-- Bolingbroke Visitation
(2076, 'Bolingbroke Visitation 1-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1786.6636962890626,"y":2588.302490234375,"z":46.16910552978515},"heading":0,"model":458025182},{"coords":{"x":1789.2606201171876,"y":2588.302490234375,"z":46.16910552978515},"heading":180,"model":458025182}],"coords":{"x":1787.962158203125,"y":2588.302490234375,"z":46.16910552978515}}'),
(2077, 'Bolingbroke Visitation 1-2', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1787.639892578125,"y":2572.741455078125,"z":46.15494155883789},"model":-519068795}'),
(2078, 'Bolingbroke Visitation 1-3', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1783.682373046875,"y":2570.60693359375,"z":46.14706802368164},"model":-519068795}'),
(2079, 'Bolingbroke Visitation 1-4', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1780.4674072265626,"y":2572.834228515625,"z":46.150146484375},"model":-519068795}'),
(2080, 'Bolingbroke Visitation 1-5', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.8663330078126,"y":2572.825439453125,"z":46.15084457397461},"model":-519068795}'),
(2081, 'Bolingbroke Visitation 1-6', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1785.1614990234376,"y":2561.552734375,"z":45.92799758911133},"model":-519068795}'),
(2082, 'Bolingbroke Visitation 1-7', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1787.4793701171876,"y":2559.309326171875,"z":45.9248161315918},"model":1242124150}'),
(2083, 'Bolingbroke Visitation 1-8', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1784.28271484375,"y":2557.01318359375,"z":45.92927551269531},"model":-519068795}'),
(2084, 'Bolingbroke Visitation 1-9', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1787.4652099609376,"y":2555.90869140625,"z":45.92572784423828},"model":1242124150}'),
(2085, 'Bolingbroke Visitation 1-10', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1791.521728515625,"y":2551.3525390625,"z":45.79612731933594},"model":-519068795}'),
(2086, 'Bolingbroke Visitation 1-11', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1782.1964111328126,"y":2550.969970703125,"z":45.93147659301758},"model":-519068795}'),
(2087, 'Bolingbroke Visitation 1-12', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1782.2481689453126,"y":2548.346923828125,"z":45.92691421508789},"model":1242124150}'),
(2088, 'Bolingbroke Visitation 1-13', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1785.20703125,"y":2548.34912109375,"z":45.92604827880859},"model":-1207991715}'),
(2089, 'Bolingbroke Visitation 1-14', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1776.2974853515626,"y":2552.66943359375,"z":45.79232788085937},"model":-519068795}'),
(2090, 'Bolingbroke Visitation 1-15', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.006103515625,"y":2570.6044921875,"z":46.15395736694336},"model":-519068795}'),
(2091, 'Bolingbroke Visitation 1-16', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1769.859130859375,"y":2579.389892578125,"z":46.16268157958984},"model":458025182}'),
(2092, 'Bolingbroke Visitation 1-17', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1769.837158203125,"y":2580.716064453125,"z":46.16410064697265},"model":458025182}'),
(2093, 'Bolingbroke Visitation 1-18', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.865234375,"y":2584.030517578125,"z":46.15682983398437},"model":-519068795}'),
(2094, 'Bolingbroke Visitation 1-19', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1765.0096435546876,"y":2566.765380859375,"z":45.79558563232422},"model":-519068795}'),

-- Bolingbroke Medical1
(2095, 'Bolingbroke Medical1 1-1', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1783.5570068359376,"y":2589.258056640625,"z":46.13809585571289},"model":-519068795}'),
(2096, 'Bolingbroke Medical1 1-2', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1782.77880859375,"y":2588.259521484375,"z":50.15034103393555},"model":-519068795}'),
(2097, 'Bolingbroke Medical1 1-3', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1783.138916015625,"y":2599.4873046875,"z":50.2009162902832},"heading":0,"model":-131296141},{"coords":{"x":1780.5389404296876,"y":2599.4873046875,"z":50.2010498046875},"heading":180,"model":-131296141}],"coords":{"x":1781.8388671875,"y":2599.4873046875,"z":50.20098114013672}}'),
(2098, 'Bolingbroke Medical1 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1783.79638671875,"y":2602.33251953125,"z":50.07903671264648},"heading":270,"model":-770740285},{"coords":{"x":1783.79638671875,"y":2604.633544921875,"z":50.07903671264648},"heading":90,"model":-770740285}],"coords":{"x":1783.79638671875,"y":2603.48291015625,"z":50.07903671264648}}'),
(2099, 'Bolingbroke Medical1 1-5', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1783.7755126953126,"y":2610.721923828125,"z":50.08312225341797},"heading":270,"model":-770740285},{"coords":{"x":1783.7755126953126,"y":2613.024169921875,"z":50.08312225341797},"heading":90,"model":-770740285}],"coords":{"x":1783.7755126953126,"y":2611.873046875,"z":50.08312225341797}}'),

-- Bolingbroke Medical2
(2100, 'Bolingbroke Medical2 1-1', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1769.308349609375,"y":2584.425537109375,"z":50.15702819824219},"model":-519068795}'),
(2101, 'Bolingbroke Medical2 1-2', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1760.619873046875,"y":2584.569091796875,"z":50.14244079589844},"model":-519068795}'),
(2102, 'Bolingbroke Medical2 1-3', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1763.380615234375,"y":2576.183349609375,"z":50.02164840698242},"heading":0,"model":-770740285},{"coords":{"x":1761.0830078125,"y":2576.183349609375,"z":50.02164840698242},"heading":180,"model":-770740285}],"coords":{"x":1762.2318115234376,"y":2576.183349609375,"z":50.02164840698242}}'),
(2103, 'Bolingbroke Medical2 1-4', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1754.7530517578126,"y":2584.562744140625,"z":49.53458023071289},"model":-519068795}'),
(2104, 'Bolingbroke Medical2 1-5', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1763.0880126953126,"y":2570.31640625,"z":46.14545059204101},"heading":90,"model":-1033001619},{"coords":{"x":1763.0880126953126,"y":2572.920654296875,"z":46.14545059204101},"heading":270,"model":-1033001619}],"coords":{"x":1763.0880126953126,"y":2571.61865234375,"z":46.14545059204101}}'),
(2105, 'Bolingbroke Medical2 1-6', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1760.072509765625,"y":2576.989013671875,"z":46.01856231689453},"model":-770740285}'),
(2106, 'Bolingbroke Medical2 1-7', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1760.496826171875,"y":2577.91357421875,"z":46.01856231689453},"heading":180,"model":-770740285},{"coords":{"x":1762.7969970703126,"y":2577.91357421875,"z":46.01856231689453},"heading":0,"model":-770740285}],"coords":{"x":1761.64697265625,"y":2577.91357421875,"z":46.01856231689453}}'),

-- Bolingbroke Offices
(2107, 'Bolingbroke Offices 1-1', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1783.895751953125,"y":2585.819580078125,"z":50.14841842651367},"model":1242124150}'),
(2108, 'Bolingbroke Offices 1-2', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1787.4930419921876,"y":2588.110595703125,"z":50.15394592285156},"model":1242124150}'),
(2109, 'Bolingbroke Offices 1-3', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1780.826171875,"y":2584.49462890625,"z":50.15519714355469},"model":1438783233}'),
(2110, 'Bolingbroke Offices 1-4', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1782.8583984375,"y":2582.820068359375,"z":50.14811325073242},"model":1242124150}'),
(2111, 'Bolingbroke Offices 1-5', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1782.8626708984376,"y":2577.962890625,"z":50.15485763549805},"model":1242124150}'),
(2112, 'Bolingbroke Offices 1-6', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1778.4461669921876,"y":2571.94775390625,"z":50.16043853759765},"model":-519068795}'),
(2113, 'Bolingbroke Offices 1-7', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1774.8953857421876,"y":2570.021240234375,"z":50.15822219848633},"model":-129553421}'),
(2114, 'Bolingbroke Offices 1-8', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1769.9774169921876,"y":2573.94580078125,"z":50.14423751831055},"model":-129553421}'),
(2115, 'Bolingbroke Offices 1-9', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1772.171142578125,"y":2583.785888671875,"z":50.14719772338867},"model":-519068795}'),

-- Bolingbroke Mess
(2116, 'Bolingbroke Mess 1-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1751.5302734375,"y":2566.300048828125,"z":45.71941757202148},"heading":45,"model":-1033001619},{"coords":{"x":1753.3682861328126,"y":2568.136962890625,"z":45.71941757202148},"heading":225,"model":-1033001619}],"coords":{"x":1752.44921875,"y":2567.218505859375,"z":45.71941757202148}}'),
(2117, 'Bolingbroke Mess 1-2', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1752.8359375,"y":2572.02294921875,"z":44.41974639892578},"model":430324891}'),
(2118, 'Bolingbroke Mess 1-3', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1749.382080078125,"y":2568.904541015625,"z":45.57469177246094},"model":-1033001619}'),
(2119, 'Bolingbroke Mess 1-4', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1749.369384765625,"y":2583.269775390625,"z":45.57509994506836},"model":-1033001619}'),
(2120, 'Bolingbroke Mess 1-5', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1753.3673095703126,"y":2589.904541015625,"z":45.72142791748047},"heading":135,"model":-1033001619},{"coords":{"x":1751.5286865234376,"y":2591.744140625,"z":45.72142791748047},"heading":315,"model":-1033001619}],"coords":{"x":1752.447998046875,"y":2590.82421875,"z":45.72142791748047}}'),
(2121, 'Bolingbroke Mess 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1746.9344482421876,"y":2593.157470703125,"z":45.57748031616211},"heading":180,"model":-1033001619},{"coords":{"x":1744.3343505859376,"y":2593.158935546875,"z":45.57748031616211},"heading":0,"model":-1033001619}],"coords":{"x":1745.6343994140626,"y":2593.158203125,"z":45.57748031616211}}'),
(2122, 'Bolingbroke Mess 1-7', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1742.4228515625,"y":2589.940673828125,"z":45.57609176635742},"model":-519068795}'),
(2123, 'Bolingbroke Mess 1-8', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1730.808837890625,"y":2589.941650390625,"z":45.57574462890625},"model":-1033001619}'),
(2124, 'Bolingbroke Mess 1-9', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1728.9881591796876,"y":2593.15966796875,"z":45.57730865478515},"heading":180,"model":-1033001619},{"coords":{"x":1726.3880615234376,"y":2593.159423828125,"z":45.57730865478515},"heading":0,"model":-1033001619}],"coords":{"x":1727.6881103515626,"y":2593.15966796875,"z":45.57730865478515}}'),
(2125, 'Bolingbroke Mess 1-10', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1721.7596435546876,"y":2591.743896484375,"z":45.71649551391601},"heading":225,"model":-1033001619},{"coords":{"x":1719.9207763671876,"y":2589.906982421875,"z":45.71649551391601},"heading":45,"model":-1033001619}],"coords":{"x":1720.8402099609376,"y":2590.825439453125,"z":45.71649551391601}}'),
(2126, 'Bolingbroke Mess 1-11', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1723.847900390625,"y":2583.2705078125,"z":45.57617568969726},"model":-519068795}'),
(2127, 'Bolingbroke Mess 1-12', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1723.917236328125,"y":2568.90478515625,"z":45.57489395141601},"model":-1033001619}'),
(2128, 'Bolingbroke Mess 1-13', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1719.9346923828126,"y":2568.130859375,"z":45.71869659423828},"heading":315,"model":-1033001619},{"coords":{"x":1721.772216796875,"y":2566.291748046875,"z":45.71869659423828},"heading":135,"model":-1033001619}],"coords":{"x":1720.853515625,"y":2567.21142578125,"z":45.71869659423828}}'),
(2129, 'Bolingbroke Mess 1-14', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1721.6876220703126,"y":2572.017578125,"z":44.42159652709961},"model":430324891}'),
(2130, 'Bolingbroke Mess 2-1', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1754.7530517578126,"y":2584.562744140625,"z":49.53458023071289},"model":-519068795}'),

-- Bolingbroke CellBlock2
(2131, 'Bolingbroke CellBlock2 E-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1709.787353515625,"y":2696.775390625,"z":45.80870056152344},"heading":0,"model":-1033001619},{"coords":{"x":1712.3896484375,"y":2696.775634765625,"z":45.80870056152344},"heading":180,"model":-1033001619}],"coords":{"x":1711.0885009765626,"y":2696.775390625,"z":45.80870056152344}}'),
(2132, 'Bolingbroke CellBlock2 E-2', '{"heading":45,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1699.5274658203126,"y":2689.113525390625,"z":46.09419250488281},"model":-519068795}'),
(2133, 'Bolingbroke CellBlock2 1-1', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1711.2996826171876,"y":2701.4453125,"z":44.62932968139648},"model":430324891}'),
(2134, 'Bolingbroke CellBlock2 1-2', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1699.49169921875,"y":2692.332763671875,"z":44.9808349609375},"model":430324891}'),
(2135, 'Bolingbroke CellBlock2 1-3', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.3807373046876,"y":2692.261962890625,"z":46.16019821166992},"model":458025182}'),
(2136, 'Bolingbroke CellBlock2 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1695.4554443359376,"y":2701.263916015625,"z":46.16189575195312},"heading":0,"model":458025182},{"coords":{"x":1698.0601806640626,"y":2701.263916015625,"z":46.16189575195312},"heading":180,"model":458025182}],"coords":{"x":1696.7578125,"y":2701.263916015625,"z":46.16189575195312}}'),
(2137, 'Bolingbroke CellBlock2 1-5', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1699.40576171875,"y":2699.449462890625,"z":44.9808349609375},"model":430324891}'),
(2138, 'Bolingbroke CellBlock2 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1695.461181640625,"y":2706.87841796875,"z":45.79666519165039},"heading":0,"model":458025182},{"coords":{"x":1698.0606689453126,"y":2706.87841796875,"z":45.79666519165039},"heading":180,"model":458025182}],"coords":{"x":1696.760986328125,"y":2706.87841796875,"z":45.79666519165039}}'),
(2139, 'Bolingbroke CellBlock2 1-7', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1694.9783935546876,"y":2717.7783203125,"z":45.79825592041015},"heading":270,"model":458025182},{"coords":{"x":1694.9783935546876,"y":2715.1796875,"z":45.79825592041015},"heading":90,"model":458025182}],"coords":{"x":1694.9783935546876,"y":2716.47900390625,"z":45.79825592041015}}'),
(2140, 'Bolingbroke CellBlock2 1-8', '{"heading":360,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1685.838623046875,"y":2714.66259765625,"z":45.78047561645508},"model":458025182}'),
(2141, 'Bolingbroke CellBlock2 1-9', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1684.5540771484376,"y":2718.23583984375,"z":45.78047561645508},"heading":360,"model":458025182},{"coords":{"x":1687.1580810546876,"y":2718.23583984375,"z":45.78047561645508},"heading":180,"model":458025182}],"coords":{"x":1685.8560791015626,"y":2718.23583984375,"z":45.78047561645508}}'),
(2142, 'Bolingbroke CellBlock2 1-10', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1725.52978515625,"y":2705.626953125,"z":44.62743377685547},"model":430324891}'),
(2143, 'Bolingbroke CellBlock2 1-11', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1726.6861572265626,"y":2700.853515625,"z":45.78678894042969},"heading":180,"model":-1033001619},{"coords":{"x":1724.0885009765626,"y":2700.853515625,"z":45.78678894042969},"heading":0,"model":-1033001619}],"coords":{"x":1725.3873291015626,"y":2700.853515625,"z":45.78678894042969}}'),
(2144, 'Bolingbroke CellBlock2 1-12', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1707.6290283203126,"y":2706.76904296875,"z":44.60573196411133},"model":430324891}'),
(2145, 'Bolingbroke CellBlock2 1-13', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.91650390625,"y":2706.76904296875,"z":44.60573196411133},"model":430324891}'),
(2146, 'Bolingbroke CellBlock2 1-14', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1700.3851318359376,"y":2706.76904296875,"z":44.60573196411133},"model":430324891}'),
(2147, 'Bolingbroke CellBlock2 1-15', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.018310546875,"y":2709.36962890625,"z":44.61197662353515},"model":430324891}'),
(2148, 'Bolingbroke CellBlock2 1-16', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.018310546875,"y":2712.884521484375,"z":44.61197662353515},"model":430324891}'),
(2149, 'Bolingbroke CellBlock2 1-17', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.018310546875,"y":2719.639404296875,"z":44.61197662353515},"model":430324891}'),
(2150, 'Bolingbroke CellBlock2 1-18', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1696.8785400390626,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2151, 'Bolingbroke CellBlock2 1-19', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1700.2235107421876,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2152, 'Bolingbroke CellBlock2 1-20', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.8961181640626,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2153, 'Bolingbroke CellBlock2 1-21', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1707.3919677734376,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2154, 'Bolingbroke CellBlock2 1-22', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1714.2811279296876,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2155, 'Bolingbroke CellBlock2 1-23', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1717.921142578125,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2156, 'Bolingbroke CellBlock2 1-24', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1721.4320068359376,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2157, 'Bolingbroke CellBlock2 1-25', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1724.8236083984376,"y":2722.874267578125,"z":44.60884094238281},"model":430324891}'),
(2158, 'Bolingbroke CellBlock2 1-26', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2720.310791015625,"z":44.60527420043945},"model":430324891}'),
(2159, 'Bolingbroke CellBlock2 1-27', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2716.788818359375,"z":44.60527420043945},"model":430324891}'),
(2160, 'Bolingbroke CellBlock2 1-28', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2713.35546875,"z":44.60527420043945},"model":430324891}'),
(2161, 'Bolingbroke CellBlock2 1-29', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2710.027587890625,"z":44.60527420043945},"model":430324891}'),
(2162, 'Bolingbroke CellBlock2 1-30', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1721.9227294921876,"y":2706.770263671875,"z":44.60879135131836},"model":430324891}'),
(2163, 'Bolingbroke CellBlock2 1-31', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1718.3843994140626,"y":2706.770263671875,"z":44.60879135131836},"model":430324891}'),
(2164, 'Bolingbroke CellBlock2 1-32', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1714.963134765625,"y":2706.770263671875,"z":44.60879135131836},"model":430324891}'),
(2165, 'Bolingbroke CellBlock2 2-1', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1707.6290283203126,"y":2706.76904296875,"z":47.75643539428711},"model":430324891}'),
(2166, 'Bolingbroke CellBlock2 2-2', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.91650390625,"y":2706.76904296875,"z":47.75643539428711},"model":430324891}'),
(2167, 'Bolingbroke CellBlock2 2-3', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1700.3851318359376,"y":2706.76904296875,"z":47.75643539428711},"model":430324891}'),
(2168, 'Bolingbroke CellBlock2 2-4', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1697.01416015625,"y":2706.76904296875,"z":47.75643539428711},"model":430324891}'),
(2169, 'Bolingbroke CellBlock2 2-5', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.018310546875,"y":2709.36962890625,"z":47.75643539428711},"model":430324891}'),
(2170, 'Bolingbroke CellBlock2 2-6', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.018310546875,"y":2712.884521484375,"z":47.75643539428711},"model":430324891}'),
(2171, 'Bolingbroke CellBlock2 2-7', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.018310546875,"y":2716.30859375,"z":47.75643539428711},"model":430324891}'),
(2172, 'Bolingbroke CellBlock2 2-8', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1695.018310546875,"y":2719.639404296875,"z":47.75643539428711},"model":430324891}'),
(2173, 'Bolingbroke CellBlock2 2-9', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1696.8785400390626,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2174, 'Bolingbroke CellBlock2 2-10', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1700.2235107421876,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2175, 'Bolingbroke CellBlock2 2-11', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.8961181640626,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2176, 'Bolingbroke CellBlock2 2-12', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1707.3919677734376,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2177, 'Bolingbroke CellBlock2 2-13', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1714.2811279296876,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2178, 'Bolingbroke CellBlock2 2-14', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1717.921142578125,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2179, 'Bolingbroke CellBlock2 2-15', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1721.4320068359376,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2180, 'Bolingbroke CellBlock2 2-16', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1724.8236083984376,"y":2722.874267578125,"z":47.75643539428711},"model":430324891}'),
(2181, 'Bolingbroke CellBlock2 2-17', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2720.310791015625,"z":47.75643539428711},"model":430324891}'),
(2182, 'Bolingbroke CellBlock2 2-18', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2716.788818359375,"z":47.75643539428711},"model":430324891}'),
(2183, 'Bolingbroke CellBlock2 2-19', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2713.35546875,"z":47.75643539428711},"model":430324891}'),
(2184, 'Bolingbroke CellBlock2 2-20', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1727.080322265625,"y":2710.031005859375,"z":47.75643539428711},"model":430324891}'),
(2185, 'Bolingbroke CellBlock2 2-21', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1725.5479736328126,"y":2706.770263671875,"z":47.75643539428711},"model":430324891}'),
(2186, 'Bolingbroke CellBlock2 2-22', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1721.9227294921876,"y":2706.770263671875,"z":47.75643539428711},"model":430324891}'),
(2187, 'Bolingbroke CellBlock2 2-23', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1718.3843994140626,"y":2706.770263671875,"z":47.75643539428711},"model":430324891}'),
(2188, 'Bolingbroke CellBlock2 2-24', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1714.963134765625,"y":2706.770263671875,"z":47.75643539428711},"model":430324891}'),

-- Bolingbroke Deathrow
(2189, 'Bolingbroke Deathrow 1-1', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1668.7120361328126,"y":2566.652587890625,"z":45.81643295288086},"model":-1322318348}'),
(2190, 'Bolingbroke Deathrow 1-2', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1667.4915771484376,"y":2575.304443359375,"z":45.83337783813476},"model":-892190840}'),
(2191, 'Bolingbroke Deathrow 1-3', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1672.924560546875,"y":2574.115478515625,"z":45.83338165283203},"model":-892190840}'),
(2192, 'Bolingbroke Deathrow 1-4', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1667.4942626953126,"y":2580.1162109375,"z":45.83337783813476},"model":-892190840}'),
(2193, 'Bolingbroke Deathrow 1-5', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1672.9244384765626,"y":2578.9130859375,"z":45.83337783813476},"model":-892190840}'),
(2194, 'Bolingbroke Deathrow 1-6', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1667.4942626953126,"y":2584.8994140625,"z":45.83337783813476},"model":-892190840}'),
(2195, 'Bolingbroke Deathrow 1-7', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1672.9244384765626,"y":2583.712890625,"z":45.83337783813476},"model":-892190840}'),
(2196, 'Bolingbroke Deathrow 1-8', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1667.4893798828126,"y":2589.677978515625,"z":45.83337783813476},"model":-892190840}'),
(2197, 'Bolingbroke Deathrow 1-9', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1672.924560546875,"y":2588.410888671875,"z":45.83337783813476},"model":-892190840}'),
(2198, 'Bolingbroke Deathrow 1-10', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1677.461669921875,"y":2593.102783203125,"z":45.81643295288086},"model":-1322318348}'),
(2199, 'Bolingbroke Deathrow 1-11', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1680.1173095703126,"y":2569.601806640625,"z":45.75301742553711},"model":-1259801187}'),

-- Bolingbroke Solitary
(2200, 'Bolingbroke Solitary 1-1', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1635.7808837890626,"y":2566.08837890625,"z":45.73348999023437},"model":-519068795}'),
(2201, 'Bolingbroke Solitary 1-2', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1636.1239013671876,"y":2568.654052734375,"z":44.60936737060547},"model":430324891}'),
(2202, 'Bolingbroke Solitary 1-3', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1638.6895751953126,"y":2570.80029296875,"z":45.78060531616211},"model":179442879}'),
(2203, 'Bolingbroke Solitary 1-4', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1633.25341796875,"y":2571.946533203125,"z":45.77914047241211},"model":179442879}'),
(2204, 'Bolingbroke Solitary 1-5', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1639.561767578125,"y":2577.35546875,"z":45.78677368164062},"model":179442879}'),
(2205, 'Bolingbroke Solitary 1-6', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1642.1397705078126,"y":2577.357666015625,"z":45.78713226318359},"model":179442879}'),
(2206, 'Bolingbroke Solitary 1-7', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1646.3643798828126,"y":2577.357666015625,"z":45.78713226318359},"model":179442879}'),
(2207, 'Bolingbroke Solitary 1-8', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1648.9407958984376,"y":2577.357666015625,"z":45.78713226318359},"model":179442879}'),
(2208, 'Bolingbroke Solitary 1-9', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1651.5421142578126,"y":2577.357666015625,"z":45.78713226318359},"model":179442879}'),
(2209, 'Bolingbroke Solitary 1-10', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1650.3922119140626,"y":2574.290771484375,"z":45.83855819702148},"model":179442879}'),
(2210, 'Bolingbroke Solitary 1-11', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1654.13720703125,"y":2577.357666015625,"z":45.78713226318359},"model":179442879}'),
(2211, 'Bolingbroke Solitary 1-12', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1656.72900390625,"y":2577.357666015625,"z":45.78713226318359},"model":179442879}'),
(2212, 'Bolingbroke Solitary 1-13', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1644.3311767578126,"y":2584.651611328125,"z":45.74608993530273},"model":-519068795}'),
(2213, 'Bolingbroke Solitary 1-14', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1642.99365234375,"y":2582.107666015625,"z":44.61269378662109},"model":430324891}'),

-- Bolingbroke Booking
(2214, 'Bolingbroke Booking 1-1', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1691.384521484375,"y":2590.595947265625,"z":46.05594253540039},"model":-519068795}'),
(2215, 'Bolingbroke Booking 1-2', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1691.15771484375,"y":2585.480712890625,"z":44.93408584594726},"model":430324891}'),
(2216, 'Bolingbroke Booking 1-3', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1691.6751708984376,"y":2582.415771484375,"z":46.0701904296875},"model":-519068795}'),
(2217, 'Bolingbroke Booking 1-4', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1694.67431640625,"y":2581.146484375,"z":46.06319046020508},"model":-519068795}'),
(2218, 'Bolingbroke Booking 1-5', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1692.202392578125,"y":2569.6591796875,"z":45.703369140625},"model":-519068795}'),
(2219, 'Bolingbroke Booking 1-6', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1690.88671875,"y":2566.7109375,"z":45.6850471496582},"model":-519068795}'),
(2220, 'Bolingbroke Booking 1-7', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1684.4090576171876,"y":2591.292724609375,"z":46.05979919433594},"model":-519068795}'),

-- Bolingbroke Gym
(2221, 'Bolingbroke Gym 1-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1719.671875,"y":2625.49072265625,"z":45.84365081787109},"heading":135,"model":1393184367},{"coords":{"x":1721.8460693359376,"y":2623.316162109375,"z":45.84365081787109},"heading":135,"model":-2111460187}],"coords":{"x":1720.759033203125,"y":2624.4033203125,"z":45.84365081787109}}'),
(2222, 'Bolingbroke Gym 1-2', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1724.355712890625,"y":2627.75439453125,"z":45.71500778198242},"heading":180,"model":1756602537},{"coords":{"x":1726.9530029296876,"y":2627.754150390625,"z":45.71500778198242},"heading":180,"model":-519068795}],"coords":{"x":1725.654296875,"y":2627.75439453125,"z":45.71500778198242}}'),
(2223, 'Bolingbroke Gym 1-3', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1719.7120361328126,"y":2647.0185546875,"z":45.84365081787109},"heading":45,"model":-2111460187},{"coords":{"x":1721.88671875,"y":2649.19287109375,"z":45.84365081787109},"heading":45,"model":1393184367}],"coords":{"x":1720.79931640625,"y":2648.105712890625,"z":45.84365081787109}}'),

-- Bolingbroke Classroom
(2224, 'Bolingbroke Classroom 1-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1753.5601806640626,"y":2625.445068359375,"z":45.84365463256836},"heading":225,"model":-2111460187},{"coords":{"x":1751.385498046875,"y":2623.270751953125,"z":45.84365463256836},"heading":225,"model":1393184367}],"coords":{"x":1752.472900390625,"y":2624.35791015625,"z":45.84365463256836}}'),
(2225, 'Bolingbroke Classroom 1-2', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1749.0224609375,"y":2627.751708984375,"z":45.71500778198242},"heading":180,"model":1756602537},{"coords":{"x":1751.6197509765626,"y":2627.75146484375,"z":45.71500778198242},"heading":180,"model":-519068795}],"coords":{"x":1750.321044921875,"y":2627.75146484375,"z":45.71500778198242}}'),
(2226, 'Bolingbroke Classroom 1-3', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1747.407470703125,"y":2629.77490234375,"z":45.71479415893555},"model":-519068795}'),
(2227, 'Bolingbroke Classroom 1-4', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1747.4083251953126,"y":2636.884033203125,"z":45.71479415893555},"model":-519068795}'),
(2228, 'Bolingbroke Classroom 1-5', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1753.254150390625,"y":2638.231201171875,"z":45.71479415893555},"model":-519068795}'),
(2229, 'Bolingbroke Classroom 1-6', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1753.2535400390626,"y":2631.121826171875,"z":45.71479415893555},"model":-519068795}'),
(2230, 'Bolingbroke Classroom 1-7', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1753.6131591796876,"y":2646.987548828125,"z":45.84365081787109},"heading":315,"model":1393184367},{"coords":{"x":1751.43896484375,"y":2649.162109375,"z":45.84365081787109},"heading":315,"model":-2111460187}],"coords":{"x":1752.526123046875,"y":2648.07470703125,"z":45.84365081787109}}'),

-- Bolingbroke CellBlock3
(2231, 'Bolingbroke CellBlock3 E-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1649.3779296875,"y":2668.5439453125,"z":45.81834030151367},"heading":50,"model":-1033001619},{"coords":{"x":1651.050537109375,"y":2670.53759765625,"z":45.81834030151367},"heading":230,"model":-1033001619}],"coords":{"x":1650.2142333984376,"y":2669.540771484375,"z":45.81834030151367}}'),
(2232, 'Bolingbroke CellBlock3 E-2', '{"heading":95,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1648.65234375,"y":2655.759521484375,"z":46.10383224487305},"model":-519068795}'),
(2233, 'Bolingbroke CellBlock3 1-1', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1646.772705078125,"y":2672.704345703125,"z":44.63896942138672},"model":430324891}'),
(2234, 'Bolingbroke CellBlock3 1-2', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1646.1632080078126,"y":2657.801513671875,"z":44.99047470092773},"model":430324891}'),
(2235, 'Bolingbroke CellBlock3 1-3', '{"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1643.5750732421876,"y":2654.60693359375,"z":46.16983795166015},"model":458025182}'),
(2236, 'Bolingbroke CellBlock3 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1636.7271728515626,"y":2660.450439453125,"z":46.17153549194336},"heading":50,"model":458025182},{"coords":{"x":1638.4014892578126,"y":2662.44580078125,"z":46.17153549194336},"heading":230,"model":458025182}],"coords":{"x":1637.5643310546876,"y":2661.4482421875,"z":46.17153549194336}}'),
(2237, 'Bolingbroke CellBlock3 1-5', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1640.6563720703126,"y":2662.31005859375,"z":44.99047470092773},"model":430324891}'),
(2238, 'Bolingbroke CellBlock3 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1632.4298095703126,"y":2664.063720703125,"z":45.80630493164062},"heading":50,"model":458025182},{"coords":{"x":1634.100830078125,"y":2666.054931640625,"z":45.80630493164062},"heading":230,"model":458025182}],"coords":{"x":1633.265380859375,"y":2665.059326171875,"z":45.80630493164062}}'),
(2239, 'Bolingbroke CellBlock3 1-7', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1625.7603759765626,"y":2669.02978515625,"z":45.80789566040039},"heading":140,"model":458025182},{"coords":{"x":1623.7696533203126,"y":2670.7001953125,"z":45.80789566040039},"heading":320,"model":458025182}],"coords":{"x":1624.7650146484376,"y":2669.864990234375,"z":45.80789566040039}}'),
(2240, 'Bolingbroke CellBlock3 1-8', '{"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1620.2816162109376,"y":2661.69580078125,"z":45.79011535644531},"model":458025182}'),
(2241, 'Bolingbroke CellBlock3 1-9', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1616.7186279296876,"y":2663.0087890625,"z":45.79011535644531},"heading":50,"model":458025182},{"coords":{"x":1618.3924560546876,"y":2665.00341796875,"z":45.79011535644531},"heading":230,"model":458025182}],"coords":{"x":1617.5555419921876,"y":2664.006103515625,"z":45.79011535644531}}'),
(2242, 'Bolingbroke CellBlock3 1-10', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1652.71630859375,"y":2686.293212890625,"z":44.6370735168457},"model":430324891}'),
(2243, 'Bolingbroke CellBlock3 1-11', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1657.1162109375,"y":2684.110595703125,"z":45.79642868041992},"heading":230,"model":-1033001619},{"coords":{"x":1655.446533203125,"y":2682.120849609375,"z":45.79642868041992},"heading":50,"model":-1033001619}],"coords":{"x":1656.2813720703126,"y":2683.11572265625,"z":45.79642868041992}}'),
(2244, 'Bolingbroke CellBlock3 1-12', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1640.3349609375,"y":2673.314453125,"z":44.61537170410156},"model":430324891}'),
(2245, 'Bolingbroke CellBlock3 1-13', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1637.9486083984376,"y":2670.470458984375,"z":44.61537170410156},"model":430324891}'),
(2246, 'Bolingbroke CellBlock3 1-14', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1635.6787109375,"y":2667.765380859375,"z":44.61537170410156},"model":430324891}'),
(2247, 'Bolingbroke CellBlock3 1-15', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1630.23681640625,"y":2665.32568359375,"z":44.62161636352539},"model":430324891}'),
(2248, 'Bolingbroke CellBlock3 1-16', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1627.544189453125,"y":2667.5849609375,"z":44.62161636352539},"model":430324891}'),
(2249, 'Bolingbroke CellBlock3 1-17', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1622.36962890625,"y":2671.927001953125,"z":44.62161636352539},"model":430324891}'),
(2250, 'Bolingbroke CellBlock3 1-18', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1621.08740234375,"y":2675.431396484375,"z":44.61848068237305},"model":430324891}'),
(2251, 'Bolingbroke CellBlock3 1-19', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1623.237548828125,"y":2677.993896484375,"z":44.61848068237305},"model":430324891}'),
(2252, 'Bolingbroke CellBlock3 1-20', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1625.59814453125,"y":2680.80712890625,"z":44.61848068237305},"model":430324891}'),
(2253, 'Bolingbroke CellBlock3 1-21', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1627.8453369140626,"y":2683.485107421875,"z":44.61848068237305},"model":430324891}'),
(2254, 'Bolingbroke CellBlock3 1-22', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1632.2735595703126,"y":2688.7626953125,"z":44.61848068237305},"model":430324891}'),
(2255, 'Bolingbroke CellBlock3 1-23', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1634.61328125,"y":2691.551025390625,"z":44.61848068237305},"model":430324891}'),
(2256, 'Bolingbroke CellBlock3 1-24', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1636.8699951171876,"y":2694.240478515625,"z":44.61848068237305},"model":430324891}'),
(2257, 'Bolingbroke CellBlock3 1-25', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1639.0501708984376,"y":2696.838623046875,"z":44.61848068237305},"model":430324891}'),
(2258, 'Bolingbroke CellBlock3 1-26', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1642.4644775390626,"y":2696.91943359375,"z":44.61491394042969},"model":430324891}'),
(2259, 'Bolingbroke CellBlock3 1-27', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1645.1624755859376,"y":2694.655517578125,"z":44.61491394042969},"model":430324891}'),
(2260, 'Bolingbroke CellBlock3 1-28', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1647.7926025390626,"y":2692.44873046875,"z":44.61491394042969},"model":430324891}'),
(2261, 'Bolingbroke CellBlock3 1-29', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1650.341796875,"y":2690.3095703125,"z":44.61491394042969},"model":430324891}'),
(2262, 'Bolingbroke CellBlock3 1-30', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1649.5218505859376,"y":2684.264892578125,"z":44.61843109130859},"model":430324891}'),
(2263, 'Bolingbroke CellBlock3 1-31', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1647.24755859375,"y":2681.554443359375,"z":44.61843109130859},"model":430324891}'),
(2264, 'Bolingbroke CellBlock3 1-32', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1645.04833984375,"y":2678.93359375,"z":44.61843109130859},"model":430324891}'),
(2265, 'Bolingbroke CellBlock3 2-1', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1640.3349609375,"y":2673.314453125,"z":47.76607513427734},"model":430324891}'),
(2266, 'Bolingbroke CellBlock3 2-2', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1637.9486083984376,"y":2670.470458984375,"z":47.76607513427734},"model":430324891}'),
(2267, 'Bolingbroke CellBlock3 2-3', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1635.6787109375,"y":2667.765380859375,"z":47.76607513427734},"model":430324891}'),
(2268, 'Bolingbroke CellBlock3 2-4', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1633.5118408203126,"y":2665.18310546875,"z":47.76607513427734},"model":430324891}'),
(2269, 'Bolingbroke CellBlock3 2-5', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1630.23681640625,"y":2665.32568359375,"z":47.76607513427734},"model":430324891}'),
(2270, 'Bolingbroke CellBlock3 2-6', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1627.544189453125,"y":2667.5849609375,"z":47.76607513427734},"model":430324891}'),
(2271, 'Bolingbroke CellBlock3 2-7', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1624.9212646484376,"y":2669.785888671875,"z":47.76607513427734},"model":430324891}'),
(2272, 'Bolingbroke CellBlock3 2-8', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1622.36962890625,"y":2671.927001953125,"z":47.76607513427734},"model":430324891}'),
(2273, 'Bolingbroke CellBlock3 2-9', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1621.08740234375,"y":2675.431396484375,"z":47.76607513427734},"model":430324891}'),
(2274, 'Bolingbroke CellBlock3 2-10', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1623.237548828125,"y":2677.993896484375,"z":47.76607513427734},"model":430324891}'),
(2275, 'Bolingbroke CellBlock3 2-11', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1625.59814453125,"y":2680.80712890625,"z":47.76607513427734},"model":430324891}'),
(2276, 'Bolingbroke CellBlock3 2-12', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1627.8453369140626,"y":2683.485107421875,"z":47.76607513427734},"model":430324891}'),
(2277, 'Bolingbroke CellBlock3 2-13', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1632.2735595703126,"y":2688.7626953125,"z":47.76607513427734},"model":430324891}'),
(2278, 'Bolingbroke CellBlock3 2-14', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1634.61328125,"y":2691.551025390625,"z":47.76607513427734},"model":430324891}'),
(2279, 'Bolingbroke CellBlock3 2-15', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1636.8699951171876,"y":2694.240478515625,"z":47.76607513427734},"model":430324891}'),
(2280, 'Bolingbroke CellBlock3 2-16', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1639.0501708984376,"y":2696.838623046875,"z":47.76607513427734},"model":430324891}'),
(2281, 'Bolingbroke CellBlock3 2-17', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1642.4644775390626,"y":2696.91943359375,"z":47.76607513427734},"model":430324891}'),
(2282, 'Bolingbroke CellBlock3 2-18', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1645.1624755859376,"y":2694.655517578125,"z":47.76607513427734},"model":430324891}'),
(2283, 'Bolingbroke CellBlock3 2-19', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1647.7926025390626,"y":2692.44873046875,"z":47.76607513427734},"model":430324891}'),
(2284, 'Bolingbroke CellBlock3 2-20', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1650.3392333984376,"y":2690.311767578125,"z":47.76607513427734},"model":430324891}'),
(2285, 'Bolingbroke CellBlock3 2-21', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1651.8521728515626,"y":2687.0419921875,"z":47.76607513427734},"model":430324891}'),
(2286, 'Bolingbroke CellBlock3 2-22', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1649.5218505859376,"y":2684.264892578125,"z":47.76607513427734},"model":430324891}'),
(2287, 'Bolingbroke CellBlock3 2-23', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1647.24755859375,"y":2681.554443359375,"z":47.76607513427734},"model":430324891}'),
(2288, 'Bolingbroke CellBlock3 2-24', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1645.04833984375,"y":2678.93359375,"z":47.76607513427734},"model":430324891}'),

-- Bolingbroke Garage
(2289, 'Bolingbroke Garage 1-1', '{"auto":true,"heading":90,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1663.2327880859376,"y":2602.430908203125,"z":44.56966018676758},"model":741314661}'),
(2290, 'Bolingbroke Garage 1-2', '{"auto":true,"heading":90,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1631.7606201171876,"y":2592.39208984375,"z":46.54840850830078},"model":-1812441654}'),
(2291, 'Bolingbroke Garage 1-3', '{"auto":true,"heading":90,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1631.7607421875,"y":2598.681640625,"z":46.54840850830078},"model":-1812441654}'),
(2292, 'Bolingbroke Garage 1-4', '{"auto":true,"heading":90,"maxDistance":6,"state":1,"doors":false,"coords":{"x":1631.7606201171876,"y":2604.9736328125,"z":46.54840850830078},"model":-1812441654}'),
(2293, 'Bolingbroke Garage 1-5', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1630.885498046875,"y":2611.57373046875,"z":45.71753311157226},"model":458025182}'),
(2294, 'Bolingbroke Garage 1-6', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1624.5211181640626,"y":2608.58203125,"z":45.71753311157226},"model":458025182}'),
(2295, 'Bolingbroke Garage 1-7', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1637.6026611328126,"y":2619.829345703125,"z":45.84349060058594},"model":1817008884}'),

-- Bolingbroke Garden
(2296, 'Bolingbroke Garden 1-1', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1618.340576171875,"y":2618.52734375,"z":45.80540466308594},"model":-1993722359}'),

-- Bolingbroke Church
(2297, 'Bolingbroke Church 1-1', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.6983642578126,"y":2645.6591796875,"z":45.7855110168457},"model":-1492625345}'),

-- Bolingbroke Tower
(2298, 'Bolingbroke Tower 1-1', '{"heading":85,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1820.7698974609376,"y":2620.77001953125,"z":45.95126342773437},"model":-1033001619}'),
(2299, 'Bolingbroke Tower 1-2', '{"heading":265,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1820.9156494140626,"y":2622.06201171875,"z":63.26435470581055},"model":-1033001619}'),
(2300, 'Bolingbroke Tower 1-3', '{"heading":95,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1845.7899169921876,"y":2698.62060546875,"z":45.95530700683594},"model":-1033001619}'),
(2301, 'Bolingbroke Tower 1-4', '{"heading":275,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1845.7091064453126,"y":2699.91845703125,"z":63.26839828491211},"model":-1033001619}'),
(2302, 'Bolingbroke Tower 1-5', '{"heading":165,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1773.1080322265626,"y":2759.699951171875,"z":45.88673400878906},"model":-1033001619}'),
(2303, 'Bolingbroke Tower 1-6', '{"heading":345,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1771.860595703125,"y":2760.06787109375,"z":63.19982528686523},"model":-1033001619}'),
(2304, 'Bolingbroke Tower 1-7', '{"heading":200,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1651.16064453125,"y":2755.43603515625,"z":45.87868499755859},"model":-1033001619}'),
(2305, 'Bolingbroke Tower 1-8', '{"heading":20,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1649.928955078125,"y":2755.018798828125,"z":63.19177627563476},"model":-1033001619}'),
(2306, 'Bolingbroke Tower 1-9', '{"heading":235,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1572.6617431640626,"y":2679.19140625,"z":45.72975921630859},"model":-1033001619}'),
(2307, 'Bolingbroke Tower 1-10', '{"heading":55,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1571.8895263671876,"y":2678.145263671875,"z":63.04285049438476},"model":-1033001619}'),
(2308, 'Bolingbroke Tower 1-11', '{"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1537.8109130859376,"y":2585.9951171875,"z":45.68914794921875},"model":-1033001619}'),
(2309, 'Bolingbroke Tower 1-12', '{"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1537.7783203125,"y":2584.69482421875,"z":63.00223922729492},"model":-1033001619}'),
(2310, 'Bolingbroke Tower 1-13', '{"heading":290,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1543.24072265625,"y":2471.294189453125,"z":45.7120132446289},"model":-1033001619}'),
(2311, 'Bolingbroke Tower 1-14', '{"heading":110,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1543.6546630859376,"y":2470.061279296875,"z":63.02510452270508},"model":-1033001619}'),
(2312, 'Bolingbroke Tower 1-15', '{"heading":355,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1658.58447265625,"y":2397.721923828125,"z":45.71525573730469},"model":-1033001619}'),
(2313, 'Bolingbroke Tower 1-16', '{"heading":175,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1659.876708984375,"y":2397.576171875,"z":63.02834701538086},"model":-1033001619}'),
(2314, 'Bolingbroke Tower 1-17', '{"heading":25,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1759.6202392578126,"y":2412.837158203125,"z":45.71166229248047},"model":-1033001619}'),
(2315, 'Bolingbroke Tower 1-18', '{"heading":205,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1760.8121337890626,"y":2413.35693359375,"z":63.02475357055664},"model":-1033001619}'),
(2316, 'Bolingbroke Tower 1-19', '{"heading":65,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1821.1702880859376,"y":2476.2646484375,"z":45.68914794921875},"model":-1033001619}'),
(2317, 'Bolingbroke Tower 1-20', '{"heading":245,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1821.7491455078126,"y":2477.42919921875,"z":63.00223922729492},"model":-1033001619}'),
(2318, 'Bolingbroke Tower 1-21', '{"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1690.3150634765626,"y":2647.255615234375,"z":54.93532562255859},"model":-120705257}'),
(2319, 'Bolingbroke Tower 1-22', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1691.3846435546876,"y":2540.318359375,"z":54.93532562255859},"model":-120705257}'),
(2320, 'Bolingbroke Tower 1-23', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1740.4302978515626,"y":2650.273681640625,"z":55.57597351074219},"model":-519068795}'),

-- Bolingbroke CellBlock4
(2321, 'Bolingbroke CellBlock4 E-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1597.466796875,"y":2552.609130859375,"z":45.75990676879883},"heading":90,"model":-1033001619},{"coords":{"x":1597.466796875,"y":2555.209228515625,"z":45.75990676879883},"heading":270,"model":-1033001619}],"coords":{"x":1597.466796875,"y":2553.9091796875,"z":45.75990676879883}}'),
(2322, 'Bolingbroke CellBlock4 1-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1592.8038330078126,"y":2552.694580078125,"z":45.75810241699219},"heading":90,"model":-1033001619},{"coords":{"x":1592.8038330078126,"y":2555.297119140625,"z":45.75810241699219},"heading":270,"model":-1033001619}],"coords":{"x":1592.8038330078126,"y":2553.995849609375,"z":45.75810241699219}}'),
(2323, 'Bolingbroke CellBlock4 1-2', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1587.4444580078126,"y":2551.18359375,"z":45.75644302368164},"heading":180,"model":-1033001619},{"coords":{"x":1584.8453369140626,"y":2551.18359375,"z":45.75644302368164},"heading":360,"model":-1033001619}],"coords":{"x":1586.1448974609376,"y":2551.18359375,"z":45.75644302368164}}'),
(2324, 'Bolingbroke CellBlock4 1-3', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1583.4468994140626,"y":2553.38916015625,"z":45.75942230224609},"heading":90,"model":-2023754432},{"coords":{"x":1583.4468994140626,"y":2555.99072265625,"z":45.75942230224609},"heading":270,"model":-2023754432}],"coords":{"x":1583.4468994140626,"y":2554.68994140625,"z":45.75942230224609}}'),
(2325, 'Bolingbroke CellBlock4 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1584.84716796875,"y":2556.6005859375,"z":45.76445007324219},"heading":360,"model":-1033001619},{"coords":{"x":1587.4459228515626,"y":2556.6005859375,"z":45.76445007324219},"heading":180,"model":-1033001619}],"coords":{"x":1586.146484375,"y":2556.6005859375,"z":45.76445007324219}}'),
(2326, 'Bolingbroke CellBlock4 1-5', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1588.162841796875,"y":2549.414306640625,"z":45.77554321289062},"heading":270,"model":-1033001619},{"coords":{"x":1588.162841796875,"y":2546.81591796875,"z":45.77554321289062},"heading":90,"model":-1033001619}],"coords":{"x":1588.162841796875,"y":2548.115234375,"z":45.77554321289062}}'),
(2327, 'Bolingbroke CellBlock4 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1584.0794677734376,"y":2546.818603515625,"z":45.75551986694336},"heading":90,"model":-1033001619},{"coords":{"x":1584.0794677734376,"y":2549.419189453125,"z":45.75551986694336},"heading":270,"model":-1033001619}],"coords":{"x":1584.0794677734376,"y":2548.118896484375,"z":45.75551986694336}}'),

-- Bolingbroke CellBlock5
(2328, 'Bolingbroke CellBlock5 E-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1623.970947265625,"y":2491.425537109375,"z":45.82904434204101},"heading":320,"model":-1033001619},{"coords":{"x":1625.9644775390626,"y":2489.752685546875,"z":45.82904434204101},"heading":140,"model":-1033001619}],"coords":{"x":1624.9677734375,"y":2490.589111328125,"z":45.82904434204101}}'),
(2329, 'Bolingbroke CellBlock5 E-2', '{"heading":185,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1638.7490234375,"y":2489.02734375,"z":46.11453628540039},"model":-519068795}'),
(2330, 'Bolingbroke CellBlock5 1-1', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1621.80419921875,"y":2487.147705078125,"z":44.64967346191406},"model":430324891}'),
(2331, 'Bolingbroke CellBlock5 1-2', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1636.7071533203126,"y":2486.538330078125,"z":45.00117874145508},"model":430324891}'),
(2332, 'Bolingbroke CellBlock5 1-3', '{"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1639.90185546875,"y":2483.949951171875,"z":46.1805419921875},"model":458025182}'),
(2333, 'Bolingbroke CellBlock5 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1634.0582275390626,"y":2477.102294921875,"z":46.1822395324707},"heading":140,"model":458025182},{"coords":{"x":1632.0628662109376,"y":2478.776611328125,"z":46.1822395324707},"heading":320,"model":458025182}],"coords":{"x":1633.060546875,"y":2477.939453125,"z":46.1822395324707}}'),
(2334, 'Bolingbroke CellBlock5 1-5', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1632.1983642578126,"y":2481.03125,"z":45.00117874145508},"model":430324891}'),
(2335, 'Bolingbroke CellBlock5 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1630.4449462890626,"y":2472.804931640625,"z":45.81700897216797},"heading":140,"model":458025182},{"coords":{"x":1628.45361328125,"y":2474.475830078125,"z":45.81700897216797},"heading":320,"model":458025182}],"coords":{"x":1629.44921875,"y":2473.640380859375,"z":45.81700897216797}}'),
(2336, 'Bolingbroke CellBlock5 1-7', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1625.8084716796876,"y":2464.144775390625,"z":45.81859970092773},"heading":50,"model":458025182},{"coords":{"x":1625.478759765625,"y":2466.135498046875,"z":45.81859970092773},"heading":230,"model":458025182}],"coords":{"x":1624.6435546875,"y":2465.14013671875,"z":45.81859970092773}}'),
(2337, 'Bolingbroke CellBlock5 1-8', '{"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1632.8126220703126,"y":2460.656494140625,"z":45.80081939697265},"model":458025182}'),
(2338, 'Bolingbroke CellBlock5 1-9', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1631.4998779296876,"y":2457.09375,"z":45.80081939697265},"heading":140,"model":458025182},{"coords":{"x":1629.505126953125,"y":2458.767578125,"z":45.80081939697265},"heading":320,"model":458025182}],"coords":{"x":1630.50244140625,"y":2457.9306640625,"z":45.80081939697265}}'),
(2339, 'Bolingbroke CellBlock5 1-10', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1608.2154541015626,"y":2493.09130859375,"z":44.64777755737305},"model":430324891}'),
(2340, 'Bolingbroke CellBlock5 1-11', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1610.3978271484376,"y":2497.4912109375,"z":45.80713272094726},"heading":320,"model":-1033001619},{"coords":{"x":1612.3878173828126,"y":2495.821533203125,"z":45.80713272094726},"heading":140,"model":-1033001619}],"coords":{"x":1611.392822265625,"y":2496.65625,"z":45.80713272094726}}'),
(2341, 'Bolingbroke CellBlock5 1-12', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1621.194091796875,"y":2480.7099609375,"z":44.6260757446289},"model":430324891}'),
(2342, 'Bolingbroke CellBlock5 1-13', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1624.0380859375,"y":2478.323486328125,"z":44.6260757446289},"model":430324891}'),
(2343, 'Bolingbroke CellBlock5 1-14', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1626.7432861328126,"y":2476.0537109375,"z":44.6260757446289},"model":430324891}'),
(2344, 'Bolingbroke CellBlock5 1-15', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1629.182861328125,"y":2470.61181640625,"z":44.63232040405273},"model":430324891}'),
(2345, 'Bolingbroke CellBlock5 1-16', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1626.9234619140626,"y":2467.91943359375,"z":44.63232040405273},"model":430324891}'),
(2346, 'Bolingbroke CellBlock5 1-17', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1622.58154296875,"y":2462.744873046875,"z":44.63232040405273},"model":430324891}'),
(2347, 'Bolingbroke CellBlock5 1-18', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1619.0771484375,"y":2461.46240234375,"z":44.62918472290039},"model":430324891}'),
(2348, 'Bolingbroke CellBlock5 1-19', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1616.5147705078126,"y":2463.612548828125,"z":44.62918472290039},"model":430324891}'),
(2349, 'Bolingbroke CellBlock5 1-20', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1613.701416015625,"y":2465.973388671875,"z":44.62918472290039},"model":430324891}'),
(2350, 'Bolingbroke CellBlock5 1-21', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1611.0234375,"y":2468.220458984375,"z":44.62918472290039},"model":430324891}'),
(2351, 'Bolingbroke CellBlock5 1-22', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1605.74609375,"y":2472.648681640625,"z":44.62918472290039},"model":430324891}'),
(2352, 'Bolingbroke CellBlock5 1-23', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1602.9576416015626,"y":2474.988525390625,"z":44.62918472290039},"model":430324891}'),
(2353, 'Bolingbroke CellBlock5 1-24', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1600.2681884765626,"y":2477.2451171875,"z":44.62918472290039},"model":430324891}'),
(2354, 'Bolingbroke CellBlock5 1-25', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1597.6700439453126,"y":2479.42529296875,"z":44.62918472290039},"model":430324891}'),
(2355, 'Bolingbroke CellBlock5 1-26', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1597.589111328125,"y":2482.83935546875,"z":44.62561798095703},"model":430324891}'),
(2356, 'Bolingbroke CellBlock5 1-27', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1599.8529052734376,"y":2485.537353515625,"z":44.62561798095703},"model":430324891}'),
(2357, 'Bolingbroke CellBlock5 1-28', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1602.059814453125,"y":2488.16748046875,"z":44.62561798095703},"model":430324891}'),
(2358, 'Bolingbroke CellBlock5 1-29', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1604.198974609375,"y":2490.716796875,"z":44.62561798095703},"model":430324891}'),
(2359, 'Bolingbroke CellBlock5 1-30', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1610.24365234375,"y":2489.896728515625,"z":44.62913513183594},"model":430324891}'),
(2360, 'Bolingbroke CellBlock5 1-31', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1612.9542236328126,"y":2487.622314453125,"z":44.62913513183594},"model":430324891}'),
(2361, 'Bolingbroke CellBlock5 1-32', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1615.5750732421876,"y":2485.42333984375,"z":44.62913513183594},"model":430324891}'),
(2362, 'Bolingbroke CellBlock5 2-1', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1621.194091796875,"y":2480.7099609375,"z":47.77677917480469},"model":430324891}'),
(2363, 'Bolingbroke CellBlock5 2-2', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1624.0380859375,"y":2478.323486328125,"z":47.77677917480469},"model":430324891}'),
(2364, 'Bolingbroke CellBlock5 2-3', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1626.7432861328126,"y":2476.0537109375,"z":47.77677917480469},"model":430324891}'),
(2365, 'Bolingbroke CellBlock5 2-4', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1629.3255615234376,"y":2473.886962890625,"z":47.77677917480469},"model":430324891}'),
(2366, 'Bolingbroke CellBlock5 2-5', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1629.182861328125,"y":2470.61181640625,"z":47.77677917480469},"model":430324891}'),
(2367, 'Bolingbroke CellBlock5 2-6', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1626.9234619140626,"y":2467.91943359375,"z":47.77677917480469},"model":430324891}'),
(2368, 'Bolingbroke CellBlock5 2-7', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1624.7225341796876,"y":2465.29638671875,"z":47.77677917480469},"model":430324891}'),
(2369, 'Bolingbroke CellBlock5 2-8', '{"auto":true,"heading":50,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1622.58154296875,"y":2462.744873046875,"z":47.77677917480469},"model":430324891}'),
(2370, 'Bolingbroke CellBlock5 2-9', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1619.0771484375,"y":2461.46240234375,"z":47.77677917480469},"model":430324891}'),
(2371, 'Bolingbroke CellBlock5 2-10', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1616.5147705078126,"y":2463.612548828125,"z":47.77677917480469},"model":430324891}'),
(2372, 'Bolingbroke CellBlock5 2-11', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1613.701416015625,"y":2465.973388671875,"z":47.77677917480469},"model":430324891}'),
(2373, 'Bolingbroke CellBlock5 2-12', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1611.0234375,"y":2468.220458984375,"z":47.77677917480469},"model":430324891}'),
(2374, 'Bolingbroke CellBlock5 2-13', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1605.74609375,"y":2472.648681640625,"z":47.77677917480469},"model":430324891}'),
(2375, 'Bolingbroke CellBlock5 2-14', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1602.9576416015626,"y":2474.988525390625,"z":47.77677917480469},"model":430324891}'),
(2376, 'Bolingbroke CellBlock5 2-15', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1600.2681884765626,"y":2477.2451171875,"z":47.77677917480469},"model":430324891}'),
(2377, 'Bolingbroke CellBlock5 2-16', '{"auto":true,"heading":320,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1597.6700439453126,"y":2479.42529296875,"z":47.77677917480469},"model":430324891}'),
(2378, 'Bolingbroke CellBlock5 2-17', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1597.589111328125,"y":2482.83935546875,"z":47.77677917480469},"model":430324891}'),
(2379, 'Bolingbroke CellBlock5 2-18', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1599.8529052734376,"y":2485.537353515625,"z":47.77677917480469},"model":430324891}'),
(2380, 'Bolingbroke CellBlock5 2-19', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1602.059814453125,"y":2488.16748046875,"z":47.77677917480469},"model":430324891}'),
(2381, 'Bolingbroke CellBlock5 2-20', '{"auto":true,"heading":230,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1604.19677734375,"y":2490.714111328125,"z":47.77677917480469},"model":430324891}'),
(2382, 'Bolingbroke CellBlock5 2-21', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1607.466552734375,"y":2492.22705078125,"z":47.77677917480469},"model":430324891}'),
(2383, 'Bolingbroke CellBlock5 2-22', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1610.24365234375,"y":2489.896728515625,"z":47.77677917480469},"model":430324891}'),
(2384, 'Bolingbroke CellBlock5 2-23', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1612.9542236328126,"y":2487.622314453125,"z":47.77677917480469},"model":430324891}'),
(2523, 'Bolingbroke CellBlock5 2-24', '{"auto":true,"heading":140,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1615.5750732421876,"y":2485.42333984375,"z":47.77677917480469},"model":430324891}'),

-- Bolingbroke CellBlock6
(2385, 'Bolingbroke CellBlock6 E-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1693.9384765625,"y":2468.79296875,"z":45.82977294921875},"heading":180,"model":-1033001619},{"coords":{"x":1691.336181640625,"y":2468.792724609375,"z":45.82977294921875},"heading":0,"model":-1033001619}],"coords":{"x":1692.6373291015626,"y":2468.79296875,"z":45.82977294921875}}'),
(2386, 'Bolingbroke CellBlock6 E-2', '{"heading":225,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1704.1983642578126,"y":2476.454833984375,"z":46.11526489257812},"model":-519068795}'),
(2387, 'Bolingbroke CellBlock6 1-1', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1692.4261474609376,"y":2464.123046875,"z":44.6504020690918},"model":430324891}'),
(2388, 'Bolingbroke CellBlock6 1-2', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1704.234130859375,"y":2473.235595703125,"z":45.00190734863281},"model":430324891}'),
(2389, 'Bolingbroke CellBlock6 1-3', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.3450927734376,"y":2473.306396484375,"z":46.18127059936523},"model":458025182}'),
(2390, 'Bolingbroke CellBlock6 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1705.6656494140626,"y":2464.304443359375,"z":46.18296813964844},"heading":360,"model":458025182},{"coords":{"x":1708.2703857421876,"y":2464.304443359375,"z":46.18296813964844},"heading":180,"model":458025182}],"coords":{"x":1706.968017578125,"y":2464.304443359375,"z":46.18296813964844}}'),
(2391, 'Bolingbroke CellBlock6 1-5', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1704.320068359375,"y":2466.118896484375,"z":45.00190734863281},"model":430324891}'),
(2392, 'Bolingbroke CellBlock6 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1708.2646484375,"y":2458.68994140625,"z":45.8177375793457},"heading":180,"model":458025182},{"coords":{"x":1705.6651611328126,"y":2458.68994140625,"z":45.8177375793457},"heading":0,"model":458025182}],"coords":{"x":1706.96484375,"y":2458.68994140625,"z":45.8177375793457}}'),
(2393, 'Bolingbroke CellBlock6 1-7', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1708.7474365234376,"y":2450.388671875,"z":45.81932830810547},"heading":270,"model":458025182},{"coords":{"x":1708.7474365234376,"y":2447.7900390625,"z":45.81932830810547},"heading":90,"model":458025182}],"coords":{"x":1708.7474365234376,"y":2449.08935546875,"z":45.81932830810547}}'),
(2394, 'Bolingbroke CellBlock6 1-8', '{"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1717.88720703125,"y":2450.90576171875,"z":45.80154800415039},"model":458025182}'),
(2395, 'Bolingbroke CellBlock6 1-9', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1719.1717529296876,"y":2447.33251953125,"z":45.80154800415039},"heading":180,"model":458025182},{"coords":{"x":1716.5677490234376,"y":2447.33251953125,"z":45.80154800415039},"heading":0,"model":458025182}],"coords":{"x":1717.8697509765626,"y":2447.33251953125,"z":45.80154800415039}}'),
(2396, 'Bolingbroke CellBlock6 1-10', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1678.196044921875,"y":2459.94140625,"z":44.64850616455078},"model":430324891}'),
(2397, 'Bolingbroke CellBlock6 1-11', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1677.0396728515626,"y":2464.71484375,"z":45.807861328125},"heading":0,"model":-1033001619},{"coords":{"x":1679.6373291015626,"y":2464.71484375,"z":45.807861328125},"heading":180,"model":-1033001619}],"coords":{"x":1678.3385009765626,"y":2464.71484375,"z":45.807861328125}}'),
(2398, 'Bolingbroke CellBlock6 1-12', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1696.0968017578126,"y":2458.79931640625,"z":44.62680435180664},"model":430324891}'),
(2399, 'Bolingbroke CellBlock6 1-13', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1699.809326171875,"y":2458.79931640625,"z":44.62680435180664},"model":430324891}'),
(2400, 'Bolingbroke CellBlock6 1-14', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.3406982421876,"y":2458.79931640625,"z":44.62680435180664},"model":430324891}'),
(2401, 'Bolingbroke CellBlock6 1-15', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.70751953125,"y":2456.19873046875,"z":44.63304901123047},"model":430324891}'),
(2402, 'Bolingbroke CellBlock6 1-16', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.70751953125,"y":2452.683837890625,"z":44.63304901123047},"model":430324891}'),
(2403, 'Bolingbroke CellBlock6 1-17', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.70751953125,"y":2445.928955078125,"z":44.63304901123047},"model":430324891}'),
(2404, 'Bolingbroke CellBlock6 1-18', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1706.8472900390626,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2405, 'Bolingbroke CellBlock6 1-19', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.5023193359376,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2406, 'Bolingbroke CellBlock6 1-20', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1699.8297119140626,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2407, 'Bolingbroke CellBlock6 1-21', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1696.3338623046876,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2408, 'Bolingbroke CellBlock6 1-22', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1689.4447021484376,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2409, 'Bolingbroke CellBlock6 1-23', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1685.8046875,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2410, 'Bolingbroke CellBlock6 1-24', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1682.2938232421876,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2411, 'Bolingbroke CellBlock6 1-25', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1678.9022216796876,"y":2442.694091796875,"z":44.62991333007812},"model":430324891}'),
(2412, 'Bolingbroke CellBlock6 1-26', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2445.257568359375,"z":44.62634658813476},"model":430324891}'),
(2413, 'Bolingbroke CellBlock6 1-27', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2448.779541015625,"z":44.62634658813476},"model":430324891}'),
(2414, 'Bolingbroke CellBlock6 1-28', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2452.212890625,"z":44.62634658813476},"model":430324891}'),
(2415, 'Bolingbroke CellBlock6 1-29', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2455.540771484375,"z":44.62634658813476},"model":430324891}'),
(2416, 'Bolingbroke CellBlock6 1-30', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1681.8031005859376,"y":2458.798095703125,"z":44.62986373901367},"model":430324891}'),
(2417, 'Bolingbroke CellBlock6 1-31', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1685.3414306640626,"y":2458.798095703125,"z":44.62986373901367},"model":430324891}'),
(2418, 'Bolingbroke CellBlock6 1-32', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1688.7626953125,"y":2458.798095703125,"z":44.62986373901367},"model":430324891}'),
(2419, 'Bolingbroke CellBlock6 2-1', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1696.0968017578126,"y":2458.79931640625,"z":47.77750778198242},"model":430324891}'),
(2420, 'Bolingbroke CellBlock6 2-2', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1699.809326171875,"y":2458.79931640625,"z":47.77750778198242},"model":430324891}'),
(2421, 'Bolingbroke CellBlock6 2-3', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.3406982421876,"y":2458.79931640625,"z":47.77750778198242},"model":430324891}'),
(2422, 'Bolingbroke CellBlock6 2-4', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1706.711669921875,"y":2458.79931640625,"z":47.77750778198242},"model":430324891}'),
(2423, 'Bolingbroke CellBlock6 2-5', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.70751953125,"y":2456.19873046875,"z":47.77750778198242},"model":430324891}'),
(2424, 'Bolingbroke CellBlock6 2-6', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.70751953125,"y":2452.683837890625,"z":47.77750778198242},"model":430324891}'),
(2425, 'Bolingbroke CellBlock6 2-7', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.70751953125,"y":2449.259765625,"z":47.77750778198242},"model":430324891}'),
(2426, 'Bolingbroke CellBlock6 2-8', '{"auto":true,"heading":90,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1708.70751953125,"y":2445.928955078125,"z":47.77750778198242},"model":430324891}'),
(2427, 'Bolingbroke CellBlock6 2-9', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1706.8472900390626,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2428, 'Bolingbroke CellBlock6 2-10', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1703.5023193359376,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2429, 'Bolingbroke CellBlock6 2-11', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1699.8297119140626,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2430, 'Bolingbroke CellBlock6 2-12', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1696.3338623046876,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2431, 'Bolingbroke CellBlock6 2-13', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1689.4447021484376,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2432, 'Bolingbroke CellBlock6 2-14', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1685.8046875,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2433, 'Bolingbroke CellBlock6 2-15', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1682.2938232421876,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2434, 'Bolingbroke CellBlock6 2-16', '{"auto":true,"heading":0,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1678.9022216796876,"y":2442.694091796875,"z":47.77750778198242},"model":430324891}'),
(2435, 'Bolingbroke CellBlock6 2-17', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2445.257568359375,"z":47.77750778198242},"model":430324891}'),
(2436, 'Bolingbroke CellBlock6 2-18', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2448.779541015625,"z":47.77750778198242},"model":430324891}'),
(2437, 'Bolingbroke CellBlock6 2-19', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2452.212890625,"z":47.77750778198242},"model":430324891}'),
(2438, 'Bolingbroke CellBlock6 2-20', '{"auto":true,"heading":270,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1676.6455078125,"y":2455.537353515625,"z":47.77750778198242},"model":430324891}'),
(2439, 'Bolingbroke CellBlock6 2-21', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1678.1778564453126,"y":2458.798095703125,"z":47.77750778198242},"model":430324891}'),
(2440, 'Bolingbroke CellBlock6 2-22', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1681.8031005859376,"y":2458.798095703125,"z":47.77750778198242},"model":430324891}'),
(2441, 'Bolingbroke CellBlock6 2-23', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1685.3414306640626,"y":2458.798095703125,"z":47.77750778198242},"model":430324891}'),
(2442, 'Bolingbroke CellBlock6 2-24', '{"auto":true,"heading":180,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1688.7626953125,"y":2458.798095703125,"z":47.77750778198242},"model":430324891}'),

-- Bolingbroke CellBlock7
(2443, 'Bolingbroke CellBlock7 E-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1755.5020751953126,"y":2501.862060546875,"z":45.82977294921875},"heading":210,"model":-1033001619},{"coords":{"x":1753.24853515625,"y":2500.560791015625,"z":45.82977294921875},"heading":30,"model":-1033001619}],"coords":{"x":1754.375244140625,"y":2501.21142578125,"z":45.82977294921875}}'),
(2444, 'Bolingbroke CellBlock7 E-2', '{"heading":255,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1760.556396484375,"y":2513.62744140625,"z":46.11526489257812},"model":-519068795}'),
(2445, 'Bolingbroke CellBlock7 1-1', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1756.52734375,"y":2497.061767578125,"z":44.6504020690918},"model":430324891}'),
(2446, 'Bolingbroke CellBlock7 1-2', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1762.197021484375,"y":2510.857177734375,"z":45.00190734863281},"model":430324891}'),
(2447, 'Bolingbroke CellBlock7 1-3', '{"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1765.7218017578126,"y":2512.97412109375,"z":46.18127059936523},"model":458025182}'),
(2448, 'Bolingbroke CellBlock7 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1770.1580810546876,"y":2505.140869140625,"z":46.18296813964844},"heading":210,"model":458025182},{"coords":{"x":1767.90234375,"y":2503.83837890625,"z":46.18296813964844},"heading":30,"model":458025182}],"coords":{"x":1769.0302734375,"y":2504.48974609375,"z":46.18296813964844}}'),
(2449, 'Bolingbroke CellBlock7 1-5', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1765.829833984375,"y":2504.73681640625,"z":45.00190734863281},"model":430324891}'),
(2450, 'Bolingbroke CellBlock7 1-6', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1772.9603271484376,"y":2500.275634765625,"z":45.8177375793457},"heading":210,"model":458025182},{"coords":{"x":1770.7091064453126,"y":2498.975830078125,"z":45.8177375793457},"heading":30,"model":458025182}],"coords":{"x":1771.834716796875,"y":2499.625732421875,"z":45.8177375793457}}'),
(2451, 'Bolingbroke CellBlock7 1-7', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1777.5291748046876,"y":2493.328125,"z":45.81932830810547},"heading":300,"model":458025182},{"coords":{"x":1778.8284912109376,"y":2491.07763671875,"z":45.81932830810547},"heading":120,"model":458025182}],"coords":{"x":1778.1788330078126,"y":2492.202880859375,"z":45.81932830810547}}'),
(2452, 'Bolingbroke CellBlock7 1-8', '{"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1785.1859130859376,"y":2498.345703125,"z":45.80154800415039},"model":458025182}'),
(2453, 'Bolingbroke CellBlock7 1-9', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1788.0849609375,"y":2495.8935546875,"z":45.80154800415039},"heading":210,"model":458025182},{"coords":{"x":1785.829833984375,"y":2494.591552484375,"z":45.80154800415039},"heading":30,"model":458025182}],"coords":{"x":1786.9573974609376,"y":2495.24267578125,"z":45.80154800415039}}'),
(2454, 'Bolingbroke CellBlock7 1-10', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1746.29443359375,"y":2486.325439453125,"z":44.64850616455078},"model":430324891}'),
(2455, 'Bolingbroke CellBlock7 1-11', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":1742.90625,"y":2489.880859375,"z":45.807861328125},"heading":30,"model":-1033001619},{"coords":{"x":1745.1558837890626,"y":2491.1796875,"z":45.807861328125},"heading":210,"model":-1033001619}],"coords":{"x":1744.031005859375,"y":2490.5302734375,"z":45.807861328125}}'),
(2456, 'Bolingbroke CellBlock7 1-12', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1762.3680419921876,"y":2494.286376953125,"z":44.62680435180664},"model":430324891}'),
(2457, 'Bolingbroke CellBlock7 1-13', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1765.5831298828126,"y":2496.142822265625,"z":44.62680435180664},"model":430324891}'),
(2458, 'Bolingbroke CellBlock7 1-14', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1768.6414794921876,"y":2497.908447265625,"z":44.62680435180664},"model":430324891}'),
(2459, 'Bolingbroke CellBlock7 1-15', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1774.5894775390626,"y":2498.339599609375,"z":44.63304901123047},"model":430324891}'),
(2460, 'Bolingbroke CellBlock7 1-16', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1776.346923828125,"y":2495.295654296875,"z":44.63304901123047},"model":430324891}'),
(2461, 'Bolingbroke CellBlock7 1-17', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1779.724365234375,"y":2489.44580078125,"z":44.63304901123047},"model":430324891}'),
(2462, 'Bolingbroke CellBlock7 1-18', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1779.7308349609376,"y":2485.714111328125,"z":44.62991333007812},"model":430324891}'),
(2463, 'Bolingbroke CellBlock7 1-19', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1776.833984375,"y":2484.041748046875,"z":44.62991333007812},"model":430324891}'),
(2464, 'Bolingbroke CellBlock7 1-20', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1773.6534423828126,"y":2482.205322265625,"z":44.62991333007812},"model":430324891}'),
(2465, 'Bolingbroke CellBlock7 1-21', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.6259765625,"y":2480.45751953125,"z":44.62991333007812},"model":430324891}'),
(2466, 'Bolingbroke CellBlock7 1-22', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1764.6597900390626,"y":2477.012939453125,"z":44.62991333007812},"model":430324891}'),
(2467, 'Bolingbroke CellBlock7 1-23', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1761.5074462890626,"y":2475.19287109375,"z":44.62991333007812},"model":430324891}'),
(2468, 'Bolingbroke CellBlock7 1-24', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1758.4669189453126,"y":2473.4375,"z":44.62991333007812},"model":430324891}'),
(2469, 'Bolingbroke CellBlock7 1-25', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1755.5296630859376,"y":2471.74169921875,"z":44.62991333007812},"model":430324891}'),
(2470, 'Bolingbroke CellBlock7 1-26', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1752.2935791015626,"y":2472.833251953125,"z":44.62634658813476},"model":430324891}'),
(2471, 'Bolingbroke CellBlock7 1-27', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1750.5325927734376,"y":2475.883544921875,"z":44.62634658813476},"model":430324891}'),
(2472, 'Bolingbroke CellBlock7 1-28', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1748.81591796875,"y":2478.85693359375,"z":44.62634658813476},"model":430324891}'),
(2473, 'Bolingbroke CellBlock7 1-29', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1747.1519775390626,"y":2481.73876953125,"z":44.62634658813476},"model":430324891}'),
(2474, 'Bolingbroke CellBlock7 1-30', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1749.989990234375,"y":2487.138671875,"z":44.62986373901367},"model":430324891}'),
(2475, 'Bolingbroke CellBlock7 1-31', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1753.05419921875,"y":2488.90771484375,"z":44.62986373901367},"model":430324891}'),
(2476, 'Bolingbroke CellBlock7 1-32', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1756.01708984375,"y":2490.618408203125,"z":44.62986373901367},"model":430324891}'),
(2477, 'Bolingbroke CellBlock7 2-1', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1762.3680419921876,"y":2494.286376953125,"z":47.77750778198242},"model":430324891}'),
(2478, 'Bolingbroke CellBlock7 2-2', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1765.5831298828126,"y":2496.142822265625,"z":47.77750778198242},"model":430324891}'),
(2479, 'Bolingbroke CellBlock7 2-3', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1768.6414794921876,"y":2497.908447265625,"z":47.77750778198242},"model":430324891}'),
(2480, 'Bolingbroke CellBlock7 2-4', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1771.560791015625,"y":2499.59375,"z":47.77750778198242},"model":430324891}'),
(2481, 'Bolingbroke CellBlock7 2-5', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1774.5894775390626,"y":2498.339599609375,"z":47.77750778198242},"model":430324891}'),
(2482, 'Bolingbroke CellBlock7 2-6', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1776.346923828125,"y":2495.295654296875,"z":47.77750778198242},"model":430324891}'),
(2483, 'Bolingbroke CellBlock7 2-7', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1778.0589599609376,"y":2492.330322265625,"z":47.77750778198242},"model":430324891}'),
(2484, 'Bolingbroke CellBlock7 2-8', '{"auto":true,"heading":120,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1779.724365234375,"y":2489.44580078125,"z":47.77750778198242},"model":430324891}'),
(2485, 'Bolingbroke CellBlock7 2-9', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1779.7308349609376,"y":2485.714111328125,"z":47.77750778198242},"model":430324891}'),
(2486, 'Bolingbroke CellBlock7 2-10', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1776.833984375,"y":2484.041748046875,"z":47.77750778198242},"model":430324891}'),
(2487, 'Bolingbroke CellBlock7 2-11', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1773.6534423828126,"y":2482.205322265625,"z":47.77750778198242},"model":430324891}'),
(2488, 'Bolingbroke CellBlock7 2-12', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1770.6259765625,"y":2480.45751953125,"z":47.77750778198242},"model":430324891}'),
(2489, 'Bolingbroke CellBlock7 2-13', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1764.6597900390626,"y":2477.012939453125,"z":47.77750778198242},"model":430324891}'),
(2490, 'Bolingbroke CellBlock7 2-14', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1761.5074462890626,"y":2475.19287109375,"z":47.77750778198242},"model":430324891}'),
(2491, 'Bolingbroke CellBlock7 2-15', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1758.4669189453126,"y":2473.4375,"z":47.77750778198242},"model":430324891}'),
(2492, 'Bolingbroke CellBlock7 2-16', '{"auto":true,"heading":30,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1755.5296630859376,"y":2471.74169921875,"z":47.77750778198242},"model":430324891}'),
(2493, 'Bolingbroke CellBlock7 2-17', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1752.2935791015626,"y":2472.833251953125,"z":47.77750778198242},"model":430324891}'),
(2494, 'Bolingbroke CellBlock7 2-18', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1750.5325927734376,"y":2475.883544921875,"z":47.77750778198242},"model":430324891}'),
(2495, 'Bolingbroke CellBlock7 2-19', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1748.81591796875,"y":2478.85693359375,"z":47.77750778198242},"model":430324891}'),
(2496, 'Bolingbroke CellBlock7 2-20', '{"auto":true,"heading":300,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1747.1536865234376,"y":2481.73583984375,"z":47.77750778198242},"model":430324891}'),
(2497, 'Bolingbroke CellBlock7 2-21', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1746.850341796875,"y":2485.325927734375,"z":47.77750778198242},"model":430324891}'),
(2498, 'Bolingbroke CellBlock7 2-22', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1749.989990234375,"y":2487.138671875,"z":47.77750778198242},"model":430324891}'),
(2499, 'Bolingbroke CellBlock7 2-23', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1753.05419921875,"y":2488.90771484375,"z":47.77750778198242},"model":430324891}'),
(2500, 'Bolingbroke CellBlock7 2-24', '{"auto":true,"heading":210,"maxDistance":2,"state":1,"doors":false,"coords":{"x":1756.01708984375,"y":2490.618408203125,"z":47.77750778198242},"model":430324891}'),

-- Bolingbroke Escape
(2501, 'Bolingbroke Escape 1-1', '{"coords":{"x":1557.38427734375,"y":2267.232421875,"z":74.48112487792969},"hideUi":true,"maxDistance":2,"doors":[{"coords":{"x":1557.38427734375,"y":2269.20703125,"z":74.48112487792969},"heading":270,"model":-2102230269},{"coords":{"x":1557.3843994140626,"y":2265.257568359375,"z":74.48112487792969},"heading":270,"model":-283452462}],"state":1}'),

-- Bolingbroke Roof Access
(2502, 'Bolingbroke Roof Access 1-1', '{"maxDistance":2,"autolock":5,"state":1,"groups":{"doc":1},"hideUi":true,"heading":270,"model":-1156020871,"coords":{"x":1744.6243896484376,"y":2563.190185546875,"z":46.26889038085937},"doors":false}'),
(2503, 'Bolingbroke Roof Access 1-2', '{"maxDistance":2,"autolock":5,"state":1,"groups":{"doc":1},"hideUi":true,"heading":270,"model":-1156020871,"coords":{"x":1708.6749267578126,"y":2565.80810546875,"z":46.26889038085937},"doors":false}'),
(2504, 'Bolingbroke Roof Access 1-3', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":270,"model":-1156020871,"coords":{"x":1680.965576171875,"y":2565.581787109375,"z":46.26889038085937},"doors":false}'),
(2505, 'Bolingbroke Roof Access 1-4', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":315,"model":-1156020871,"coords":{"x":1616.63330078125,"y":2575.579833984375,"z":46.26772689819336},"doors":false}'),
(2506, 'Bolingbroke Roof Access 1-5', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":225,"model":-1156020871,"coords":{"x":1617.971923828125,"y":2533.126220703125,"z":46.27000427246094},"doors":false}'),
(2507, 'Bolingbroke Roof Access 1-6', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":5,"model":-1156020871,"coords":{"x":1620.807861328125,"y":2518.938232421875,"z":46.26772308349609},"doors":false}'),
(2508, 'Bolingbroke Roof Access 1-7', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":275,"model":-1156020871,"coords":{"x":1654.072021484375,"y":2492.633056640625,"z":46.27026748657226},"doors":false}'),
(2509, 'Bolingbroke Roof Access 1-8', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":45,"model":-1156020871,"coords":{"x":1671.1497802734376,"y":2487.8134765625,"z":46.26771926879883},"doors":false}'),
(2510, 'Bolingbroke Roof Access 1-9', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":315,"model":-1156020871,"coords":{"x":1713.6500244140626,"y":2489.16455078125,"z":46.270263671875},"doors":false}'),
(2511, 'Bolingbroke Roof Access 1-10', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":75,"model":-1156020871,"coords":{"x":1726.343017578125,"y":2506.978515625,"z":46.26889038085937},"doors":false}'),
(2512, 'Bolingbroke Roof Access 1-11', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":345,"model":-1156020871,"coords":{"x":1762.3602294921876,"y":2529.237548828125,"z":46.26889038085937},"doors":false}'),
(2513, 'Bolingbroke Roof Access 1-12', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"coords":{"x":1697.400390625,"y":2545.931396484375,"z":46.26889038085937},"doors":[{"model":-1156020871,"heading":90,"coords":{"x":1697.400390625,"y":2544.255859375,"z":46.26889038085937}},{"model":-1156020871,"heading":270,"coords":{"x":1697.400390625,"y":2547.60693359375,"z":46.26889038085937}}]}'),
(2514, 'Bolingbroke Roof Access 2-1', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":90,"model":-1156020871,"coords":{"x":1668.4830322265626,"y":2621.64892578125,"z":46.27949142456055},"doors":false}'),
(2515, 'Bolingbroke Roof Access 2-2', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":90,"model":-1156020871,"coords":{"x":1695.74169921875,"y":2621.75537109375,"z":46.2652702331543},"doors":false}'),
(2516, 'Bolingbroke Roof Access 2-3', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":90,"model":-1156020871,"coords":{"x":1731.7000732421876,"y":2651.6318359375,"z":46.2428092956543},"doors":false}'),
(2517, 'Bolingbroke Roof Access 2-4', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":190,"model":-1156020871,"coords":{"x":1780.863037109375,"y":2650.103271484375,"z":46.21867752075195},"doors":false}'),
(2518, 'Bolingbroke Roof Access 2-5', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":100,"model":-1156020871,"coords":{"x":1745.44921875,"y":2673.42431640625,"z":46.27022552490234},"doors":false}'),
(2519, 'Bolingbroke Roof Access 2-6', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":225,"model":-1156020871,"coords":{"x":1732.795654296875,"y":2677.656005859375,"z":46.29333114624023},"doors":false}'),
(2520, 'Bolingbroke Roof Access 2-7', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":135,"model":-1156020871,"coords":{"x":1690.17041015625,"y":2676.501708984375,"z":46.27016448974609},"doors":false}'),
(2521, 'Bolingbroke Roof Access 2-8', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":275,"model":-1156020871,"coords":{"x":1678.833740234375,"y":2673.802978515625,"z":46.24878692626953},"doors":false}'),
(2522, 'Bolingbroke Roof Access 2-9', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"heading":185,"model":-1156020871,"coords":{"x":1652.2037353515626,"y":2640.507080078125,"z":46.270263671875},"doors":false}'),
(2524, 'Bolingbroke Roof Access 2-10', '{"maxDistance":2,"autolock":5,"state":1,"hideUi":true,"coords":{"x":1684.6058349609376,"y":2640.81982421875,"z":46.22626876831055},"doors":[{"model":-1156020871,"heading":270,"coords":{"x":1684.6058349609376,"y":2642.4609375,"z":46.22626876831055}},{"model":-1156020871,"heading":90,"coords":{"x":1684.6058349609376,"y":2639.1787109375,"z":46.22626876831055}}]}');
```

{% hint style="warning" %}
Don’t edit IDs or JSON structure unless you know your door manager’s exact schema.\
The above is ready for **ox\_doorlock** as-is.
{% endhint %}
{% endtab %}

{% tab title="Troubleshooting & Support" %}
#### Common Checks

* **Map not loading?** Ensure the folder name is exactly `[Prompt_Prison_Completed]` and it’s started in `server.cfg`.
* **Doorlocks not working?** Confirm the SQL imported successfully and your doorlock script (e.g., **ox\_doorlock**) is running.
* **Conflicts**: If you run other prison mods, verify there are no overlapping YMAPs or IPL edits in the same area.

#### Need help?

* Open a ticket on your server’s support channel with: **resource name**, **server artifacts version**, and any **console errors**.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endtab %}
{% endtabs %}
