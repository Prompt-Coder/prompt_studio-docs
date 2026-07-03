# 🏦 Sandy Bank

## Sandy Bank

{% embed url="https://fivem.prompt-mods.com/package/XXXXXXXX" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**
{% endembed %}

The **Sandy Shores Bank** is a compact, fully reworked interior that fits the restored 1980s desert-town style while adding a polished, functional space for everyday banking and high-stakes roleplay. Inside, players get teller counters, meeting rooms, staff areas, and a detailed vault designed for both legitimate transactions and immersive heist scenarios.

Supported Robbery Scripts: \
2\. [https://www.youtube.com/watch?v=XR3tYCygYKs](https://www.youtube.com/watch?v=XR3tYCygYKs) \
1\. [https://store.fearlessdev.me/package/6963949](https://store.fearlessdev.me/package/6963949) (USE CODE: "PROMPTBANK50" FOR 50% OFF)

{% embed url="https://www.youtube.com/watch?v=wEYiFR6KQKA" %}

***

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Add the resource

Place the `prompt_sandy_bank` folder inside your `resources` directory.

<pre><code><strong>resources/prompt_sandy_bank
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Add to your server.cfg

Insert the following line to ensure the map loads automatically:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_bank
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 3 — Set up MapData

Make sure you have the correct [**Sandy MapData**](sandy-mapdata.md) installed.
{% endstep %}

{% step %}
#### Step 4 — Test the map

Restart your server and visit the **Sandy Bank** location.\
If the map and interiors load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

{% hint style="info" %}
💡 **Tip:** Always restart your server after adding new resources — especially when adding multiple Sandy area maps.
{% endhint %}

***

:round\_pushpin:Location: **1854.77, 3863.07, 36.7**

***

### Interactive Props

| Category               | Prop Name                 | Description                                        |
| ---------------------- | ------------------------- | -------------------------------------------------- |
| **Seating**            | `d1n_sandy_bank_bench_01` | Bench seating inside lobby                         |
|                        | `d1n_sb_sofa_01`          | Sofa seating area                                  |
| **Bank Worker Table**  | `d1n_sandy_bank_table_01` | Desk used by bank staff                            |
| **Bank Counter Table** | `d1n_sandy_bank_table_02` | Counter area (supports targeting for bank systems) |
| **Vault Door**         | `v_ilev_bk_vaultdoor`     | Vault entry door (non-interactive by default)      |

***

### Doorlock SQL

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1900, 'Sandy Shores Bank 1-1', '{"coords":{"x":1851.5235595703126,"y":3861.71728515625,"z":36.28575134277344},"state":0,"doors":[{"coords":{"x":1852.1131591796876,"y":3860.489501953125,"z":36.28575134277344},"model":-30651409,"heading":116},{"coords":{"x":1850.9339599609376,"y":3862.945068359375,"z":36.28575134277344},"model":-30651409,"heading":296}],"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1901, 'Sandy Shores Bank 1-2', '{"coords":{"x":1852.8316650390626,"y":3852.276123046875,"z":36.00296783447265},"state":0,"model":2067875351,"heading":206,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1902, 'Sandy Shores Bank 1-3', '{"coords":{"x":1838.5985107421876,"y":3846.30908203125,"z":36.00296783447265},"state":0,"model":2067875351,"heading":116,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1903, 'Sandy Shores Bank 1-4', '{"coords":{"x":1819.7872314453126,"y":3856.920166015625,"z":35.99913787841797},"state":0,"model":2067875351,"heading":116,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1904, 'Sandy Shores Bank 1-5', '{"coords":{"x":1831.896240234375,"y":3860.265869140625,"z":36.00296783447265},"state":0,"model":2067875351,"heading":116,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1905, 'Sandy Shores Bank 2-1', '{"coords":{"x":1852.8836669921876,"y":3852.16796875,"z":41.00100708007812},"state":0,"model":2067875351,"heading":206,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1906, 'Sandy Shores Bank 2-2', '{"coords":{"x":1836.21240234375,"y":3844.16259765625,"z":41.00100708007812},"state":0,"model":2067875351,"heading":206,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1907, 'Sandy Shores Bank 2-3', '{"coords":{"x":1826.712646484375,"y":3842.498291015625,"z":41.00100708007812},"state":0,"model":2067875351,"heading":116,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1908, 'Sandy Shores Bank 2-4', '{"coords":{"x":1824.2440185546876,"y":3845.0693359375,"z":41.00100708007812},"state":0,"model":2067875351,"heading":206,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1909, 'Sandy Shores Bank 2-5', '{"coords":{"x":1823.8621826171876,"y":3848.434326171875,"z":41.00100708007812},"state":0,"doors":[{"coords":{"x":1824.370361328125,"y":3847.376220703125,"z":41.00100708007812},"model":2067875351,"heading":116},{"coords":{"x":1823.35400390625,"y":3849.492431640625,"z":41.00100708007812},"model":2067875351,"heading":296}],"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1910, 'Sandy Shores Bank 2-6', '{"coords":{"x":1819.3326416015626,"y":3855.29736328125,"z":41.00100708007812},"state":0,"model":2067875351,"heading":206,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1911, 'Sandy Shores Bank 2-7', '{"coords":{"x":1818.923583984375,"y":3858.718994140625,"z":41.00100708007812},"state":0,"model":2067875351,"heading":116,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1912, 'Sandy Shores Bank 2-8', '{"coords":{"x":1820.884033203125,"y":3857.20654296875,"z":41.00100708007812},"state":0,"model":2067875351,"heading":26,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1913, 'Sandy Shores Bank 2-9', '{"coords":{"x":1827.3489990234376,"y":3860.31103515625,"z":41.00100708007812},"state":0,"model":2067875351,"heading":206,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1914, 'Sandy Shores Bank 2-10', '{"coords":{"x":1843.86328125,"y":3868.240966796875,"z":41.00100708007812},"state":0,"model":2067875351,"heading":26,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1915, 'Sandy Shores Bank 0-1', '{"coords":{"x":1821.70556640625,"y":3843.97216796875,"z":33.49150466918945},"state":0,"model":2067875351,"heading":206,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1916, 'Sandy Shores Bank 0-2', '{"coords":{"x":1819.6312255859376,"y":3840.685302734375,"z":34.10546493530273},"state":0,"model":-1627599682,"heading":296,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1917, 'Sandy Shores Bank 0-3', '{"coords":{"x":1834.3983154296876,"y":3859.997802734375,"z":31.96230697631836},"state":0,"model":961976194,"heading":296,"doors":false,"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1918, 'Sandy Shores Bank G-1', '{"coords":{"x":1806.99169921875,"y":3835.034423828125,"z":33.04075622558594},"state":0,"doors":[{"coords":{"x":1803.8599853515626,"y":3840.458740234375,"z":33.15008544921875},"model":1939805166,"heading":120},{"coords":{"x":1810.1234130859376,"y":3829.610107421875,"z":32.93142700195312},"model":1939805166,"heading":300}],"maxDistance":5,"doorRate":0.5}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1919, 'Sandy Shores Bank G-2', '{"coords":{"x":1815.6173095703126,"y":3838.5185546875,"z":34.36040496826172},"state":0,"doors":[{"coords":{"x":1814.760498046875,"y":3840.33642578125,"z":34.35607528686523},"model":1526539404,"heading":295},{"coords":{"x":1816.47412109375,"y":3836.700927734375,"z":34.3647346496582},"model":1526539404,"heading":115}],"maxDistance":2}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (1920, 'Sandy Shores Bank G-3', '{"coords":{"x":1816.619384765625,"y":3842.127197265625,"z":34.36013793945312},"state":0,"model":1526539404,"heading":205,"doors":false,"maxDistance":2}');

```

***

### Notes

* Fully compatible with other **Sandy Shores** maps and MapData system.
* Designed for easy integration with custom banking scripts or target systems.
* Optimized interior with minimal performance impact.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
