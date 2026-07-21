# 🚓 Rockford Police Department

{% embed url="https://fivem.prompt-mods.com/package/5153364" %}

{% embed url="https://youtu.be/jFkSgaOibyk" %}

The **Rockford Police Department** is a custom map designed for FiveM servers, offering a fully immersive police station environment for roleplay, law enforcement, and emergency response scenarios. This map features a detailed interior and exterior, complete with interactive props, seating arrangements, and a robust doorlock system for enhanced gameplay. Below, you’ll find all the necessary details to install and configure this map on your server.



***

### 🚒+🚔 Compatibility with Rockford PD <a href="#compatibility-with-rockford-pd" id="compatibility-with-rockford-pd"></a>

In order for this map to work with our other map [Rockford Fire Station](rockford-fire-department.md#compatibility-with-rockford-pd) you must install resource named as **Prompt's Mods - rockford\_police\_department (fd compatible)** and **Prompt's Mods - prompt\_los\_santos\_fire\_station (pd compatible)** from keymaster or portal. They will only work together if you use those 2 versions.

***

### 📍 **Map Location**

The Rockford Police Department is located at the following coordinates:\
&#xNAN;**-555.57, -135.89, 38.28**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The map includes a variety of chairs and props to create a realistic police station environment. Below is a list of the chairs included:

* `prompt_pd_chair_detective`
* `prompt_pd_chair_kitchen`
* `prompt_pd_chairs_enter`
* `prompt_pd_locker_seat`
* `prompt_pd_student_chair`
* `prompt_pd_prison_beds`
* `prop_off_chair_01`
* `prop_off_chair_04_s`
* `prop_wait_bench_01`
* `v_ret_gc_chair02`
* `v_ret_gc_chair03`
* `v_ilev_chair02_ped`
* `prop_toilet_01`
* `v_club_officechair`
* `p_armchair_01_s`
* `hei_heist_stn_sofa3seat_02`
* `apa_mp_h_yacht_sofa_02`
* `ex_prop_offchair_exec_01`
* `xm_prop_x17_avengerchair_02`
* `hei_heist_stn_sofa3seat_06`
* `hei_heist_stn_sofa3seat_01`
* `apa_mp_h_yacht_barstool_01`
* `sum_mp_h_yacht_armchair_01`
* `v_med_cor_medstool`
* `bkr_prop_biker_boardchair01`
* `bkr_prop_clubhouse_sofa_01a`
* `v_corp_bk_chair2`

***

#### 📺 **TV**

The map includes a TV for added realism:

* `apa_mp_h_str_avunits_01`

***

#### 🚪 **Doorlock System**

The Rockford Police Department map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Rockford Police Department G-1', '{"maxDistance":2,"state":1,"model":769870942,"doors":false,"coords":{"x":-579.4329833984375,"y":-124.66803741455078,"z":34.65650939941406},"heading":23}'),
(DEFAULT, 'Rockford Police Department G-2', '{"maxDistance":2,"state":1,"model":769870942,"doors":false,"coords":{"x":-584.7935791015625,"y":-126.94384765625,"z":34.65879821777344},"heading":23}'),
(DEFAULT, 'Rockford Police Department E-1', '{"coords":{"x":-557.7818603515625,"y":-128.04429626464845,"z":38.1182632446289},"maxDistance":2,"state":1,"doors":[{"heading":23,"model":-223920905,"coords":{"x":-556.8018188476563,"y":-127.63514709472656,"z":38.11901473999023}},{"heading":203,"model":-223920905,"coords":{"x":-558.7618408203125,"y":-128.4534454345703,"z":38.11751174926758}}]}'),
(DEFAULT, 'Rockford Police Department E-2', '{"maxDistance":2,"doors":[{"model":-1338294381,"coords":{"x":-561.0794677734375,"y":-130.25990295410157,"z":38.74447631835937},"heading":23},{"model":-1338294381,"coords":{"x":-563.045654296875,"y":-131.07432556152345,"z":38.74447631835937},"heading":203}],"coords":{"x":-562.0625610351563,"y":-130.6671142578125,"z":38.74447631835937},"state":0}'),
(DEFAULT, 'Rockford Police Department E-3', '{"coords":{"x":-566.980224609375,"y":-131.83961486816407,"z":38.11536407470703},"maxDistance":2,"state":1,"doors":[{"heading":23,"model":-223920905,"coords":{"x":-566.000732421875,"y":-131.43019104003907,"z":38.11536407470703}},{"heading":203,"model":-223920905,"coords":{"x":-567.959716796875,"y":-132.24903869628907,"z":38.11536407470703}}]}'),
(DEFAULT, 'Rockford Police Department 1-1', '{"coords":{"x":-571.5455322265625,"y":-128.55128479003907,"z":37.40618896484375},"maxDistance":2,"state":1,"doors":[{"heading":293,"model":-1225363909,"coords":{"x":-571.8327026367188,"y":-127.8579330444336,"z":37.40618896484375}},{"heading":112,"model":-1225363909,"coords":{"x":-571.25830078125,"y":-129.24464416503907,"z":37.40618896484375}}]}'),
(DEFAULT, 'Rockford Police Department E-4', '{"maxDistance":2,"doors":[{"model":-1338294381,"coords":{"x":-541.9861450195313,"y":-131.59951782226563,"z":39.11523056030273},"heading":23},{"model":-1338294381,"coords":{"x":-543.9446411132813,"y":-132.41073608398438,"z":39.11523056030273},"heading":203}],"coords":{"x":-542.9653930664063,"y":-132.005126953125,"z":39.11523056030273},"state":0}'),
(DEFAULT, 'Rockford Police Department 1-2', '{"coords":{"x":-552.7528686523438,"y":-118.7061538696289,"z":37.69427108764648},"maxDistance":2,"state":1,"doors":[{"heading":23,"model":108017676,"coords":{"x":-552.36669921875,"y":-118.54618835449219,"z":37.69427108764648}},{"heading":203,"model":108017676,"coords":{"x":-553.1390380859375,"y":-118.86611938476563,"z":37.69427108764648}}]}'),
(DEFAULT, 'Rockford Police Department 1-3', '{"maxDistance":2,"doors":[{"model":108017676,"coords":{"x":-549.7468872070313,"y":-117.46170043945313,"z":37.69427108764648},"heading":23},{"model":108017676,"coords":{"x":-550.519287109375,"y":-117.7816390991211,"z":37.69427108764648},"heading":203}],"coords":{"x":-550.133056640625,"y":-117.62167358398438,"z":37.69427108764648},"state":0}'),
(DEFAULT, 'Rockford Police Department 1-4', '{"maxDistance":2,"doors":[{"model":924110090,"coords":{"x":-550.6034545898438,"y":-115.43992614746094,"z":37.51140594482422},"heading":23},{"model":924110090,"coords":{"x":-553.0623779296875,"y":-116.47884368896485,"z":37.51140594482422},"heading":203}],"coords":{"x":-551.8328857421875,"y":-115.95938110351563,"z":37.51140594482422},"state":0}'),
(DEFAULT, 'Rockford Police Department 1-5', '{"coords":{"x":-556.1270141601563,"y":-111.67930603027344,"z":38.60493469238281},"heading":23,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-1', '{"maxDistance":2,"doors":[{"model":1313927514,"coords":{"x":-578.8805541992188,"y":-116.18084716796875,"z":32.8191032409668},"heading":113},{"model":1313927514,"coords":{"x":-577.7158813476563,"y":-118.94220733642578,"z":32.8191032409668},"heading":293}],"coords":{"x":-578.2982177734375,"y":-117.5615234375,"z":32.8191032409668},"state":0}'),
(DEFAULT, 'Rockford Police Department 0-2', '{"coords":{"x":-572.9036254882813,"y":-110.74264526367188,"z":33.85123825073242},"heading":293,"model":-1357407713,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-3', '{"coords":{"x":-576.5724487304688,"y":-101.83441162109375,"z":33.82674789428711},"maxDistance":2,"state":1,"doors":[{"heading":293,"model":-1357407713,"coords":{"x":-576.1089477539063,"y":-102.96070098876953,"z":33.82674789428711}},{"heading":112,"model":-1357407713,"coords":{"x":-577.0359497070313,"y":-100.70811462402344,"z":33.82674789428711}}]}'),
(DEFAULT, 'Rockford Police Department 0-4', '{"coords":{"x":-585.74365234375,"y":-99.71932983398438,"z":33.81260681152344},"maxDistance":2,"state":1,"doors":[{"heading":203,"model":-1357407713,"coords":{"x":-586.8680419921875,"y":-100.1850357055664,"z":33.81260681152344}},{"heading":23,"model":-1357407713,"coords":{"x":-584.6193237304688,"y":-99.25361633300781,"z":33.81260681152344}}]}'),
(DEFAULT, 'Rockford Police Department 0-5', '{"coords":{"x":-592.8909912109375,"y":-102.66239929199219,"z":33.86140823364258},"heading":23,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-6', '{"coords":{"x":-598.3673706054688,"y":-104.69992065429688,"z":32.6710319519043},"maxDistance":2,"state":1,"doors":[{"heading":23,"model":-1647363618,"coords":{"x":-597.466552734375,"y":-104.32649993896485,"z":32.6710319519043}},{"heading":203,"model":1232343333,"coords":{"x":-599.2681884765625,"y":-105.07334899902344,"z":32.6710319519043}}]}'),
(DEFAULT, 'Rockford Police Department 0-7', '{"coords":{"x":-610.5416259765625,"y":-110.62037658691406,"z":33.86969757080078},"heading":113,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-8', '{"coords":{"x":-561.2625122070313,"y":-91.86186981201172,"z":32.67623138427734},"heading":112,"model":-1798639645,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-9', '{"coords":{"x":-563.0897827148438,"y":-87.45028686523438,"z":32.67623138427734},"heading":112,"model":-1798639645,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-10', '{"coords":{"x":-564.9179077148438,"y":-83.03669738769531,"z":32.67623138427734},"heading":112,"model":-1798639645,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-11', '{"coords":{"x":-566.7450561523438,"y":-78.62559509277344,"z":32.67623138427734},"heading":112,"model":-1798639645,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-12', '{"coords":{"x":-568.67041015625,"y":-88.38733673095703,"z":33.86761093139648},"heading":112,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-13', '{"coords":{"x":-573.041015625,"y":-83.23936462402344,"z":33.85836410522461},"heading":203,"model":-2023754432,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-14', '{"coords":{"x":-576.1963500976563,"y":-84.54381561279297,"z":33.85855484008789},"heading":23,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-15', '{"coords":{"x":-579.0067749023438,"y":-85.69232177734375,"z":33.82425308227539},"heading":203,"model":-2023754432,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 0-16', '{"coords":{"x":-582.1521606445313,"y":-87.0145034790039,"z":33.86378479003906},"heading":23,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 2-1', '{"coords":{"x":-554.9573974609375,"y":-112.12147521972656,"z":44.64352416992187},"maxDistance":2,"state":1,"doors":[{"heading":203,"model":-364937765,"coords":{"x":-556.0182495117188,"y":-112.56087493896485,"z":44.64352416992187}},{"heading":23,"model":-364937765,"coords":{"x":-553.8966064453125,"y":-111.68207550048828,"z":44.64352416992187}}]}'),
(DEFAULT, 'Rockford Police Department 2-2', '{"coords":{"x":-550.6250610351563,"y":-124.03079986572266,"z":44.8275260925293},"heading":203,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 2-3', '{"coords":{"x":-544.8136596679688,"y":-124.83219909667969,"z":44.8556022644043},"heading":293,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 2-4', '{"coords":{"x":-546.0374755859375,"y":-119.16471099853516,"z":43.68090057373047},"maxDistance":2,"state":1,"doors":[{"heading":23,"model":1093938460,"coords":{"x":-545.3858642578125,"y":-118.89481353759766,"z":43.68090057373047}},{"heading":203,"model":1093938460,"coords":{"x":-546.6890869140625,"y":-119.43460845947266,"z":43.68090057373047}}]}'),
(DEFAULT, 'Rockford Police Department 2-5', '{"coords":{"x":-556.6710205078125,"y":-121.03850555419922,"z":44.7915153503418},"heading":23,"model":2014573897,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 2-6', '{"coords":{"x":-560.41650390625,"y":-125.30409240722656,"z":44.64434051513672},"maxDistance":2,"state":1,"doors":[{"heading":112,"model":-364937765,"coords":{"x":-560.85546875,"y":-124.24424743652344,"z":44.64434051513672}},{"heading":293,"model":-364937765,"coords":{"x":-559.9775390625,"y":-126.36394500732422,"z":44.64434051513672}}]}'),
(DEFAULT, 'Rockford Police Department 2-7', '{"coords":{"x":-574.3419799804688,"y":-136.50794982910157,"z":41.85536575317383},"maxDistance":2,"state":1,"doors":[{"heading":112,"model":-1225363909,"coords":{"x":-574.0562133789063,"y":-137.19790649414063,"z":41.85536575317383}},{"heading":293,"model":-1225363909,"coords":{"x":-574.6277465820313,"y":-135.8179931640625,"z":41.85536575317383}}]}'),
(DEFAULT, 'Rockford Police Department 2-8', '{"coords":{"x":-596.2781982421875,"y":-150.8641815185547,"z":42.83048629760742},"maxDistance":2,"state":1,"doors":[{"heading":203,"model":-364937765,"coords":{"x":-597.3389282226563,"y":-151.30355834960938,"z":42.83048629760742}},{"heading":23,"model":-364937765,"coords":{"x":-595.2174072265625,"y":-150.4248046875,"z":42.83048629760742}}]}'),
(DEFAULT, 'Rockford Police Department 2-9', '{"coords":{"x":-602.1114501953125,"y":-149.4393310546875,"z":42.97473526000976},"heading":112,"model":2014573897,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 2-10', '{"coords":{"x":-558.1412353515625,"y":-99.75003051757813,"z":44.76831817626953},"heading":112,"model":2014573897,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 3-1', '{"coords":{"x":-559.470458984375,"y":-96.8044662475586,"z":48.24392318725586},"heading":42,"model":-1357407713,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 3-2', '{"coords":{"x":-556.2528686523438,"y":-110.04706573486328,"z":48.2117919921875},"maxDistance":2,"state":1,"doors":[{"heading":203,"model":1242124150,"coords":{"x":-557.453857421875,"y":-110.5445327758789,"z":48.2117919921875}},{"heading":23,"model":1242124150,"coords":{"x":-555.0518798828125,"y":-109.54959869384766,"z":48.2117919921875}}]}'),
(DEFAULT, 'Rockford Police Department 3-3', '{"coords":{"x":-559.5848999023438,"y":-119.90181732177735,"z":47.71407699584961},"heading":23,"model":-908284348,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 3-4', '{"coords":{"x":-565.0298461914063,"y":-122.17720794677735,"z":47.7130012512207},"heading":23,"model":-908284348,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Rockford Police Department 3-5', '{"coords":{"x":-574.555419921875,"y":-136.6026153564453,"z":46.9156608581543},"maxDistance":2,"state":1,"doors":[{"heading":112,"model":-1225363909,"coords":{"x":-574.268310546875,"y":-137.29571533203126,"z":46.9156608581543}},{"heading":293,"model":-1225363909,"coords":{"x":-574.842529296875,"y":-135.90951538085938,"z":46.9156608581543}}]}'),
(DEFAULT, 'Rockford Police Department E-5', '{"coords":{"x":-578.6076049804688,"y":-130.3820037841797,"z":51.01509475708008},"maxDistance":2,"state":1,"doors":[{"heading":293,"model":-1225363909,"coords":{"x":-578.9010009765625,"y":-129.69082641601563,"z":51.01509475708008}},{"heading":113,"model":-1225363909,"coords":{"x":-578.314208984375,"y":-131.07318115234376,"z":51.01509475708008}}]}');
```

***

### 🚀 **Installation Guide**

Follow these steps to install the Rockford Police Department map on your FiveM server:

1. **Download the Map Resource**
   * Ensure the `rockford_police_department` resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start rockford_police_department
       ```
3. **Set Up Doorlocks**
   * Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**
   * Restart your server and visit the map location at **-555.57, -135.89, 38.28** to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Rockford Police Department** on your FiveM server! 🚀
