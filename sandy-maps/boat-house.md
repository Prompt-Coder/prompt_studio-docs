# ⛵ Boat House

{% embed url="https://fivem.prompt-mods.com/package/6276364" %}

{% embed url="https://youtu.be/sClnFtxMFFY" %}

The **Boat House** is a detailed and immersive map designed for FiveM servers, located in Sandy Shores. This map provides a cozy and functional environment for roleplay scenarios, complete with seating areas, TVs, and a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Boat House** is located at the following coordinates:

* **Position**: `1533.20, 3776.65, 34.51`

***

### 🪑 Chairs

The map includes a variety of chairs and sofas for added realism. Below are the chair models used in the map:

* `prop_yaught_sofa_01`
* `prop_yaught_chair_01`
* `prop_table_05_chr`
* `prop_couch_lg_08`
* `v_corp_bk_chair3`
* `apa_mp_h_stn_chairstrip_07`
* `prop_toilet_01`
* `prop_clown_chair`
* `chuz_is_blue_chair_rm7`
* `chuz_is_onl1_table_7rm`
* `chuz_is_bar_chairs_around`
* `chuz_is_bar_chairs_around2`

***

### 📺 TVs

The map features a TV to enhance the environment. The following TV model is used:

* `prop_tv_flat_michael`

***

### 🚪 Doorlock System

The **Boat House** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(203, 'Sandy Boat House E-1', '{"doors":[{"coords":{"x":1530.4393310546876,"y":3779.90966796875,"z":34.99489974975586},"model":-1102142939,"heading":35},{"coords":{"x":1528.1531982421876,"y":3778.298583984375,"z":34.99489974975586},"model":-1102142939,"heading":215}],"coords":{"x":1529.2962646484376,"y":3779.10400390625,"z":34.99489974975586},"state":1,"maxDistance":2}'),
(204, 'Sandy Boat House E-2', '{"doors":false,"model":-893114122,"coords":{"x":1515.5010986328126,"y":3784.512451171875,"z":34.93637466430664},"heading":135,"state":1,"maxDistance":2}'),
(205, 'Sandy Boat House E-3', '{"doors":false,"model":-893114122,"coords":{"x":1528.989990234375,"y":3793.86328125,"z":34.94539642333984},"heading":114,"state":1,"maxDistance":2}'),
(207, 'Sandy Boat House E-4', '{"doors":[{"coords":{"x":1549.996337890625,"y":3800.39501953125,"z":34.57147979736328},"model":-502195954,"heading":117},{"coords":{"x":1551.152587890625,"y":3798.24951171875,"z":34.57147979736328},"model":-502195954,"heading":297}],"coords":{"x":1550.574462890625,"y":3799.322265625,"z":34.57147979736328},"state":1,"maxDistance":2}'),
(208, 'Sandy Boat House E-5', '{"doors":[{"coords":{"x":1527.3138427734376,"y":3790.969970703125,"z":38.4559326171875},"model":-1454760130,"heading":297},{"coords":{"x":1528.3065185546876,"y":3789.00439453125,"z":38.45648574829101},"model":-1454760130,"heading":117}],"coords":{"x":1527.8101806640626,"y":3789.9873046875,"z":38.45620727539062},"state":0,"maxDistance":2}'),
(209, 'Sandy Boat House 1-1', '{"doors":[{"coords":{"x":1535.8624267578126,"y":3792.3935546875,"z":34.78372573852539},"model":1480370527,"heading":298},{"coords":{"x":1534.558837890625,"y":3794.8779296875,"z":34.78372573852539},"model":1480370527,"heading":118}],"coords":{"x":1535.210693359375,"y":3793.6357421875,"z":34.78372573852539},"state":1,"maxDistance":2}'),
(210, 'Sandy Boat House 1-2', '{"doors":[{"coords":{"x":1545.009521484375,"y":3796.369873046875,"z":34.65959167480469},"model":-1498975473,"heading":116},{"coords":{"x":1543.869384765625,"y":3798.70751953125,"z":34.65959167480469},"model":-1498975473,"heading":296}],"coords":{"x":1544.439453125,"y":3797.53857421875,"z":34.65959167480469},"state":1,"maxDistance":2}'),
(211, 'Sandy Boat House 1-3', '{"doors":false,"model":827574885,"coords":{"x":1525.9193115234376,"y":3791.329833984375,"z":34.73612213134765},"heading":31,"state":1,"maxDistance":2}'),
(212, 'Sandy Boat House 2-1', '{"doors":false,"model":1044811355,"coords":{"x":1522.598388671875,"y":3792.52685546875,"z":37.25511932373047},"heading":301,"state":1,"maxDistance":2}'),
(213, 'Sandy Boat House 2-2', '{"doors":false,"model":-2030220382,"coords":{"x":1518.04296875,"y":3790.938232421875,"z":38.34967041015625},"heading":125,"state":1,"maxDistance":2}'),
(214, 'Sandy Boat House 2-3', '{"doors":false,"model":-2030220382,"coords":{"x":1519.9874267578126,"y":3788.14453125,"z":38.34419631958008},"heading":305,"state":1,"maxDistance":2}'),
(215, 'Sandy Boat House 2-4', '{"doors":false,"model":827574885,"coords":{"x":1517.829345703125,"y":3781.9111328125,"z":38.43782424926758},"heading":312,"state":1,"maxDistance":2}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Boat House** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_chuz_sandy_shores_boat_house` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    plaintextCopy

    ```
    start cfx_chuz_sandy_shores_boat_house
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**\
   Restart your server and visit the map location at `1533.20, 3776.65, 34.51` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Boat House** on your FiveM server! 🚀
