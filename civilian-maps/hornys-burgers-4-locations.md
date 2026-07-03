# 🍔 Horny's Burgers (4 locations)

## Prompt’s Horny's Burgers

{% embed url="https://portal.cfx.re/assets/granted-assets?page=1&sort=asset.updated_at&direction=asc&search=Prompt%27s+-+Gym+%28with+Animations%29" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**
{% endembed %}

{% embed url="https://www.youtube.com/watch?v=YvIBmrv-oYI" %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Install the map

Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Gym+%28with+Animations%29).

After downloading, **you will get a zip with a folder named**:

<pre><code><strong>prompt_hornys || prompt_hornys_sandy_only (depends on your version)
</strong></code></pre>

Drag and drop the downloaded folder inside your `resources` directory.\
When done, the full path should look like this:

<pre><code><strong>resources/prompt_hornys || resources/prompt_hornys (depends on your version)
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Restart your server

If the map has been started successfully -> you will see the Map Data message in the end of the server console.\
Please Follow the directions of those messages (for **Paleto** and **Sandy** Map Datas).

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

### Additional Information

{% tabs %}
{% tab title="Compatibility & Locations" %}
**✅ Compatible Resources**

* [Utility Kitchen](https://forum.cfx.re/t/utility-kitchen/5292505) — If you want to have cooking experience for the burger place

***

&#x20;**Horny's Locations**

{% hint style="info" %}
To remove a specific Horny's location:

1. Navigate to the `/stream` directory.
2. Delete the folder for the desired horny's location.
{% endhint %}

| Area            | Coordinates              |
| --------------- | ------------------------ |
| Sandy Shores    | 1847.24, 3767.86, 33.82  |
| Mirror Park     | 1240.78, -370.39, 69.92  |
| Ghetto Location | -187.98, -1428.51, 33.27 |
| Paleto Bay      | -362.35, 6050.57, 33.38  |

> The Sandy Shores Horny's and Paleto Bay Horny's integrates seamlessly with other Sandy Shores and Paleto Maps maps using the shared map data system.
{% endtab %}

{% tab title="Doorlock SQL" %}


```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES

	-- Sandy Shores Horny
	(1965, 'Sandy Shores Horny E-1', '{"coords":{"x":1845.299560546875,"y":3779.7646484375,"z":33.48891067504883},"doors":[{"coords":{"x":1845.9287109375,"y":3778.628173828125,"z":33.48891067504883},"model":-285040094,"heading":120},{"coords":{"x":1844.6702880859376,"y":3780.9013671875,"z":33.48891067504883},"model":-951201095,"heading":300}],"maxDistance":2,"state":1}'),
	(1966, 'Sandy Shores Horny E-2', '{"coords":{"x":1848.681884765625,"y":3792.423583984375,"z":33.48908996582031},"doors":[{"coords":{"x":1849.8184814453126,"y":3793.052734375,"z":33.48908996582031},"model":-951201095,"heading":210},{"coords":{"x":1847.54541015625,"y":3791.79443359375,"z":33.48908996582031},"model":-285040094,"heading":30}],"maxDistance":2,"state":1}'),
	(1967, 'Sandy Shores Horny E-3', '{"coords":{"x":1859.7623291015626,"y":3787.63134765625,"z":33.32556915283203},"heading":303,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(1968, 'Sandy Shores Horny 1-1', '{"coords":{"x":1855.5821533203126,"y":3779.783935546875,"z":33.32556915283203},"heading":30,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(1969, 'Sandy Shores Horny 1-2', '{"coords":{"x":1857.3046875,"y":3787.066162109375,"z":33.32556915283203},"heading":30,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),

	-- Mirror Park Horny
	(1970, 'Mirror Park Horny E-1', '{"coords":{"x":1241.724853515625,"y":-366.34051513671877,"z":69.46353912353516},"doors":[{"coords":{"x":1240.476318359375,"y":-365.9818115234375,"z":69.46353912353516},"model":-951201095,"heading":345},{"coords":{"x":1242.973388671875,"y":-366.6992492675781,"z":69.46353912353516},"model":-285040094,"heading":165}],"maxDistance":2,"state":1}'),
	(1971, 'Mirror Park Horny E-2', '{"coords":{"x":1235.16552734375,"y":-354.9976806640625,"z":69.46371459960938},"doors":[{"coords":{"x":1234.8067626953126,"y":-356.2462158203125,"z":69.46371459960938},"model":-285040094,"heading":75},{"coords":{"x":1235.5242919921876,"y":-353.7491760253906,"z":69.46371459960938},"model":-951201095,"heading":255}],"maxDistance":2,"state":1}'),
	(1972, 'Mirror Park Horny E-3', '{"coords":{"x":1246.3890380859376,"y":-350.5511169433594,"z":69.3001937866211},"heading":348,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(1973, 'Mirror Park Horny 1-1', '{"coords":{"x":1248.982421875,"y":-359.0560607910156,"z":69.3001937866211},"heading":75,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(1974, 'Mirror Park Horny 1-2', '{"coords":{"x":1245.0509033203126,"y":-352.6887512207031,"z":69.3001937866211},"heading":75,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),

	-- Ghetto Horny
	(1975, 'Ghetto Horny E-1', '{"coords":{"x":-182.5804443359375,"y":-1432.696044921875,"z":31.59699249267578},"doors":[{"coords":{"x":-181.72769165039063,"y":-1431.716064453125,"z":31.59699249267578},"model":-951201095,"heading":230},{"coords":{"x":-183.43321228027345,"y":-1433.676025390625,"z":31.59699249267578},"model":-285040094,"heading":50}],"maxDistance":2,"state":1}'),
	(1976, 'Ghetto Horny E-2', '{"coords":{"x":-181.42938232421876,"y":-1445.748291015625,"z":31.59681320190429},"doors":[{"coords":{"x":-182.40931701660157,"y":-1444.8955078125,"z":31.59681320190429},"model":-951201095,"heading":320},{"coords":{"x":-180.449462890625,"y":-1446.60107421875,"z":31.59681320190429},"model":-285040094,"heading":140}],"maxDistance":2,"state":1}'),
	(1977, 'Ghetto Horny E-3', '{"coords":{"x":-170.5293426513672,"y":-1433.409423828125,"z":31.43347358703613},"heading":323,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(1978, 'Ghetto Horny 1-1', '{"coords":{"x":-171.7733154296875,"y":-1442.21337890625,"z":31.43347358703613},"heading":50,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(1979, 'Ghetto Horny 1-2', '{"coords":{"x":-172.64537048339845,"y":-1434.78125,"z":31.43347358703613},"heading":50,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),

	-- Paleto Bay Horny
	(1980, 'Paleto Bay Horny E-1', '{"coords":{"x":-367.57537841796877,"y":6051.5703125,"z":31.87233734130859},"doors":[{"coords":{"x":-366.67352294921877,"y":6050.6357421875,"z":31.87233734130859},"model":-951201095,"heading":135},{"coords":{"x":-368.4772644042969,"y":6052.50537109375,"z":31.87233734130859},"model":-285040094,"heading":315}],"maxDistance":2,"state":1}'),
	(1982, 'Paleto Bay Horny E-2', '{"coords":{"x":-380.67828369140627,"y":6051.5615234375,"z":31.87215805053711},"doors":[{"coords":{"x":-381.61322021484377,"y":6050.65966796875,"z":31.87215805053711},"model":-285040094,"heading":45},{"coords":{"x":-379.74334716796877,"y":6052.46337890625,"z":31.87215805053711},"model":-951201095,"heading":225}],"maxDistance":2,"state":1}'),
	(1983, 'Paleto Bay Horny E-3', '{"coords":{"x":-369.3363342285156,"y":6039.62744140625,"z":31.70881843566894},"heading":228,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(1984, 'Paleto Bay Horny 1-1', '{"coords":{"x":-377.99847412109377,"y":6041.6337890625,"z":31.70881843566894},"heading":315,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(1985, 'Paleto Bay Horny 1-2', '{"coords":{"x":-370.5185852050781,"y":6041.85498046875,"z":31.70881843566894},"heading":315,"doors":false,"maxDistance":2,"state":1,"model":1710114873}');
```
{% endtab %}

{% tab title="Custom Props" %}
## Props that you may want to use in your script



1. Seating & Furniture

* `i45pt_hornys_chair_01`
* `i45pt_hornys_seat_01`
* `i45pt_hornys_seat_02`
* `i45pt_hornys_chairbar_01`

2\. Food & Ingredients

* `i45pt_hornys_food_frites`
* `i45pt_hornys_food_burger_pack`
* `i45pt_hornys_food_burger_pack_02`
* `i45pt_hornys_food_burger_pack_03`
* `i45pt_hornys_food_sandwitch_pack_01`
* `i45pt_hornys_food_misc`
* `i45pt_hornys_food_burgermeet_01` (Meat)
* `i45pt_hornys_food_burgermeet_02` (Meat)
* `i45pt_hornys_food_burgermeet_03` (Meat)
* `i45pt_hornys_food_bag_b`
* `i45pt_hornys_food_bag_s`

3\. Script Props (Tills, Trays, Tools, Bins)

* `i45pt_hornys_till_01`
* `i45pt_hornys_tillpay`
* `i45pt_hornys_prop_bin_01`
* `i45pt_hornys_cutlery`
* `i45pt_hornys_tray_01`
* `i45pt_hornys_food_bs_tray_01`
* `i45pt_hornys_food_bs_tray_02`
* `i45pt_hornys_prop_tools_fryer`
* `i45pt_hornys_kitchen_tool_grill_01`
* `i45pt_hornys_prop_tools_frye_mesh`
{% endtab %}

{% tab title="Troubleshooting & Support" %}
**Common Issues**

* Have gta objects overlapping with the map? -> Usually this means you are using wrong map data or have a conflict with other maps around.

**Need Help?**

Open a ticket with:

* Resource name: **prompt\_hornys**
* Server artifact version
* Console error logs (if any)

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endtab %}
{% endtabs %}
