# 🏢 Vespucci CityHall

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/hlemEwpRJ78" %}

The **Vespucci CityHall** is a highly detailed and immersive map designed for FiveM servers, offering a realistic government building environment for roleplay scenarios. Located in the vibrant district of Vespucci, this map provides a fully functional city hall with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Vespucci CityHall** is located at the following coordinates:

* **Position**: `-1281.71, -563.34, 31.70`

### 🗺️ Map Features

**Chairs**:

* `prompt_vcityhall_toilet2`
* `prompt_vcityhall_toilet_1`
* `prompt_vcityhall_seating`
* `fluorine4305_cityholl_chairarm_01b`
* `fluorine4305_cityholl_prop_9_seat`
* `prop_off_chair_05`
* `v_corp_offchair`
* `bkr_prop_clubhouse_sofa_01a`
* `prop_chair_04b`
* `apa_mp_h_stn_chairarm_24`
* `ex_mp_h_off_sofa_02`
* `ex_prop_exec_bed_01`
* `xm_prop_x17_avengerchair_02`
* `vw_prop_vw_offchair_02`
* `prop_front_seat_row_01`

**TV**:

* `prop_tv_flat_michael`
* `prop_tv_flat_01`
* `prop_tv_flat_02`
* `xm_prop_x17_tv_ceiling_01`

***

### 🚪 Doorlock System

The **Vespucci CityHall** map includes a customizable doorlock system to restrict access to specific areas. Below is an example SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES 
(476, 'Vespucci City Hall E-1', '{"maxDistance":2,"doors":[{"model":-914307974,"coords":{"x":-1286.8631591796876,"y":-566.29541015625,"z":30.70686149597168},"heading":310},{"model":575108502,"coords":{"x":-1285.097412109375,"y":-568.3997192382813,"z":30.70686149597168},"heading":130}],"coords":{"x":-1285.980224609375,"y":-567.3475341796875,"z":30.70686149597168},"state":0}'),
	(477, 'Vespucci City Hall E-2', '{"coords":{"x":-1298.74365234375,"y":-578.076416015625,"z":30.72524261474609},"maxDistance":2,"state":1,"doors":[{"heading":310,"model":320433149,"coords":{"x":-1297.907958984375,"y":-579.072509765625,"z":30.72524261474609}},{"heading":310,"model":-1215222675,"coords":{"x":-1299.5794677734376,"y":-577.080322265625,"z":30.72524261474609}}]}'),
	(479, 'Vespucci City Hall E-3', '{"coords":{"x":-1278.555419921875,"y":-603.2868041992188,"z":23.10353469848632},"maxDistance":2,"state":1,"doors":[{"heading":40,"model":-752989555,"coords":{"x":-1276.1419677734376,"y":-601.263427734375,"z":23.10609054565429}},{"heading":220,"model":-752989555,"coords":{"x":-1280.968994140625,"y":-605.3101806640625,"z":23.10098075866699}}]}'),
	(480, 'Vespucci City Hall 0-1', '{"coords":{"x":-1306.4715576171876,"y":-558.6986083984375,"z":19.80200004577636},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1305.8968505859376,"y":-558.2164306640625,"z":19.80200004577636}},{"heading":40,"model":-1240156945,"coords":{"x":-1307.0462646484376,"y":-559.1808471679688,"z":19.80200004577636}}]}'),
	(481, 'Vespucci City Hall 0-2', '{"coords":{"x":-1308.4951171875,"y":-560.3965454101563,"z":19.80200004577636},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1307.9205322265626,"y":-559.9143676757813,"z":19.80200004577636}},{"heading":40,"model":-1240156945,"coords":{"x":-1309.0697021484376,"y":-560.8787231445313,"z":19.80200004577636}}]}'),
	(482, 'Vespucci City Hall 1-1', '{"coords":{"x":-1306.2943115234376,"y":-563.155029296875,"z":29.58938217163086},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1305.72021484375,"y":-562.67333984375,"z":29.58938217163086}},{"heading":40,"model":-1240156945,"coords":{"x":-1306.868408203125,"y":-563.63671875,"z":29.58938217163086}}]}'),
	(483, 'Vespucci City Hall 1-2', '{"coords":{"x":-1308.317626953125,"y":-564.8527221679688,"z":29.58937644958496},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1307.743896484375,"y":-564.371337890625,"z":29.58937072753906}},{"heading":40,"model":-1240156945,"coords":{"x":-1308.8912353515626,"y":-565.3341064453125,"z":29.58938217163086}}]}'),
	(484, 'Vespucci City Hall 1-3', '{"coords":{"x":-1304.732666015625,"y":-554.6472778320313,"z":30.719482421875},"heading":40,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(485, 'Vespucci City Hall 1-4', '{"coords":{"x":-1309.44482421875,"y":-558.5824584960938,"z":30.719482421875},"heading":220,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(486, 'Vespucci City Hall 1-5', '{"coords":{"x":-1299.342041015625,"y":-562.3377075195313,"z":30.72140121459961},"heading":130,"model":1266543998,"maxDistance":2,"state":1,"doors":false}'),
	(487, 'Vespucci City Hall 2-1', '{"coords":{"x":-1286.8013916015626,"y":-584.6476440429688,"z":34.52389144897461},"heading":130,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(488, 'Vespucci City Hall 2-2', '{"coords":{"x":-1291.35693359375,"y":-579.2185668945313,"z":34.52389144897461},"heading":130,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(489, 'Vespucci City Hall 2-3', '{"coords":{"x":-1298.6427001953126,"y":-570.5357666015625,"z":34.52389144897461},"heading":310,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(490, 'Vespucci City Hall 2-4', '{"coords":{"x":-1306.291015625,"y":-563.1615600585938,"z":33.37770462036133},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1305.7169189453126,"y":-562.6798095703125,"z":33.37770462036133}},{"heading":40,"model":-1240156945,"coords":{"x":-1306.864990234375,"y":-563.643310546875,"z":33.37770462036133}}]}'),
	(491, 'Vespucci City Hall 2-5', '{"coords":{"x":-1308.343505859375,"y":-564.8837890625,"z":33.37770462036133},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1307.7685546875,"y":-564.4014282226563,"z":33.37770462036133}},{"heading":40,"model":-1240156945,"coords":{"x":-1308.9183349609376,"y":-565.3662109375,"z":33.37770462036133}}]}'),
	(492, 'Vespucci City Hall 3-1', '{"coords":{"x":-1306.303955078125,"y":-563.1495361328125,"z":36.37886047363281},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1305.7296142578126,"y":-562.6675415039063,"z":36.37886047363281}},{"heading":40,"model":-1240156945,"coords":{"x":-1306.8782958984376,"y":-563.6315307617188,"z":36.37886047363281}}]}'),
	(493, 'Vespucci City Hall 3-2', '{"coords":{"x":-1308.325927734375,"y":-564.84619140625,"z":36.37886047363281},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-1240156945,"coords":{"x":-1307.7528076171876,"y":-564.3652954101563,"z":36.37886047363281}},{"heading":40,"model":-1240156945,"coords":{"x":-1308.8990478515626,"y":-565.3270263671875,"z":36.37886047363281}}]}'),
	(494, 'Vespucci City Hall 3-3', '{"coords":{"x":-1298.6475830078126,"y":-570.5299682617188,"z":37.53782272338867},"heading":310,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(495, 'Vespucci City Hall 3-4', '{"coords":{"x":-1291.35546875,"y":-579.2203369140625,"z":37.53782272338867},"heading":130,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(496, 'Vespucci City Hall 3-5', '{"coords":{"x":-1286.798583984375,"y":-584.6510620117188,"z":37.53782272338867},"heading":130,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(497, 'Vespucci City Hall 4-2', '{"coords":{"x":-1291.9468994140626,"y":-584.87158203125,"z":41.33245849609375},"heading":220,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(498, 'Vespucci City Hall 4-1', '{"coords":{"x":-1289.125,"y":-574.31201171875,"z":41.33634567260742},"maxDistance":2,"state":1,"doors":[{"heading":220,"model":-88942360,"coords":{"x":-1290.1190185546876,"y":-575.1461181640625,"z":41.33634567260742}},{"heading":40,"model":-88942360,"coords":{"x":-1288.131103515625,"y":-573.4779663085938,"z":41.33634567260742}}]}'),
	(499, 'Vespucci City Hall 4-3', '{"coords":{"x":-1292.2572021484376,"y":-568.2954711914063,"z":41.33634567260742},"heading":40,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(500, 'Vespucci City Hall 4-4', '{"coords":{"x":-1295.631591796875,"y":-563.8184814453125,"z":41.33470153808594},"heading":130,"model":-88942360,"maxDistance":2,"state":1,"doors":false}'),
	(501, 'Vespucci City Hall 4-5', '{"coords":{"x":-1293.296630859375,"y":-566.2974853515625,"z":41.33470153808594},"heading":220,"model":-88942360,"maxDistance":2,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Vespucci CityHall** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_vespucci_cityhall` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_vespucci_cityhall
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-1281.71, -563.34, 31.70` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Vespucci CityHall** on your FiveM server! 🏛️🚀
