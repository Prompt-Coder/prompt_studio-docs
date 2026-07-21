# 🚒 Rockford Fire Department

{% embed url="https://fivem.prompt-mods.com/package/4701837" %}

{% embed url="https://youtu.be/tF8gEADdbVA" %}

The **Rockford Fire Department** is a custom map designed for FiveM servers, offering a fully immersive fire station environment for roleplay, emergency response, and firefighting scenarios. This map features a detailed interior and exterior, complete with interactive props, seating arrangements, and a robust doorlock system for enhanced gameplay. Below, you’ll find all the necessary details to install and configure this map on your server.

***

## 🚒+🚔 Compatibility with Rockford PD

In order for this map to work with our other map [Rockford Police Department](rockford-police-department.md) you must install resource named as **Prompt's Mods - rockford\_police\_department (fd compatible)** and **Prompt's Mods - prompt\_los\_santos\_fire\_station (pd compatible)** from keymaster or portal.  They will only work together if you use those 2 versions.

***

### 📍 **Map Location**

The Rockford Fire Department is located at the following coordinates:\
&#xNAN;**-662.27, -73.37, 38.55**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The map includes a variety of chairs and props to create a realistic fire station environment. Below is a list of the chairs included:

* `gr_prop_bunker_bed_01`
* `v_corp_offchair`
* `v_ret_chair`
* `prop_sol_chair`
* `v_res_study_chair`
* `v_res_fa_chair01`
* `xm_base_cia_seats_long`
* `ex_mp_h_stn_chairstrip_010`
* `v_med_p_deskchair`
* `prop_toilet_01`
* `prop_couch_03`
* `p_v_med_p_sofa_s`
* `prop_off_chair_01`
* `bkr_prop_clubhouse_sofa_01a`
* `v_res_mbchair`

***

#### 📺 **TV**

The map includes a TV for added realism:

* `prop_tv_flat_01`

***

#### 🚪 **Doorlock System**

The Rockford Fire Department map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Rockford Fire Department G-1', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-630.6298217773438,"y":-113.97341918945313,"z":39.08005905151367},"heading":263}'),
(DEFAULT, 'Rockford Fire Department G-2', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-629.6058349609375,"y":-105.84209442138672,"z":39.08163070678711},"heading":262}'),
(DEFAULT, 'Rockford Fire Department G-3', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-628.5516967773438,"y":-97.72549438476563,"z":39.08761215209961},"heading":263}'),
(DEFAULT, 'Rockford Fire Department G-4', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-655.0746459960938,"y":-100.28689575195313,"z":38.9916877746582},"heading":300}'),
(DEFAULT, 'Rockford Fire Department G-5', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-659.061767578125,"y":-93.40306091308594,"z":39.00727844238281},"heading":300}'),
(DEFAULT, 'Rockford Fire Department G-6', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-640.803466796875,"y":-70.37983703613281,"z":41.09241485595703},"heading":177}'),
(DEFAULT, 'Rockford Fire Department G-7', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-632.8696899414063,"y":-70.92486572265625,"z":41.08790969848633},"heading":177}'),
(DEFAULT, 'Rockford Fire Department G-8', '{"maxDistance":2,"state":1,"model":-1511111260,"doors":false,"coords":{"x":-625.1746215820313,"y":-71.40992736816406,"z":41.0860595703125},"heading":178}'),
(DEFAULT, 'Rockford Fire Department E-1', '{"maxDistance":2,"state":0,"doors":[{"coords":{"x":-661.0494995117188,"y":-78.00564575195313,"z":39.09143447875976},"model":-96416801,"heading":30},{"coords":{"x":-659.1735229492188,"y":-76.97418212890625,"z":39.09143447875976},"model":-625902714,"heading":28}],"coords":{"x":-660.1115112304688,"y":-77.48991394042969,"z":39.09143447875976}}'),
(DEFAULT, 'Rockford Fire Department E-2', '{"maxDistance":2,"state":0,"doors":[{"coords":{"x":-632.286376953125,"y":-122.9828109741211,"z":39.42330551147461},"model":-2021949952,"heading":260},{"coords":{"x":-631.965087890625,"y":-120.96527862548828,"z":39.42330551147461},"model":-2021949952,"heading":80}],"coords":{"x":-632.125732421875,"y":-121.97404479980469,"z":39.42330551147461}}'),
(DEFAULT, 'Rockford Fire Department E-3', '{"maxDistance":2,"state":0,"doors":[{"coords":{"x":-633.09375,"y":-127.80731201171875,"z":39.42167663574219},"model":-2021949952,"heading":260},{"coords":{"x":-632.77001953125,"y":-125.78953552246094,"z":39.42167663574219},"model":-2021949952,"heading":80}],"coords":{"x":-632.931884765625,"y":-126.79842376708985,"z":39.42167663574219}}'),
(DEFAULT, 'Rockford Fire Department 1-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-652.0358276367188,"y":-88.85348510742188,"z":38.88957977294922},"model":-2041685008,"heading":29},{"coords":{"x":-649.7578125,"y":-87.60139465332031,"z":38.88957977294922},"model":-2041685008,"heading":209}],"coords":{"x":-650.8968505859375,"y":-88.2274398803711,"z":38.88957977294922}}'),
(DEFAULT, 'Rockford Fire Department 1-2', '{"maxDistance":2,"state":1,"model":1242124150,"doors":false,"coords":{"x":-629.245361328125,"y":-85.38566589355469,"z":40.26640319824219},"heading":355}'),
(DEFAULT, 'Rockford Fire Department 1-3', '{"maxDistance":2,"state":1,"model":1242124150,"doors":false,"coords":{"x":-627.6679077148438,"y":-92.65962982177735,"z":40.22930145263672},"heading":172}'),
(DEFAULT, 'Rockford Fire Department 1-4', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-627.76318359375,"y":-119.02855682373047,"z":39.36922073364258},"model":964838196,"heading":352},{"coords":{"x":-630.3424682617188,"y":-118.6875228881836,"z":39.36922073364258},"model":964838196,"heading":172}],"coords":{"x":-629.0528564453125,"y":-118.85803985595703,"z":39.36922073364258}}'),
(DEFAULT, 'Rockford Fire Department 1-5', '{"maxDistance":2,"state":1,"model":964838196,"doors":false,"coords":{"x":-627.9164428710938,"y":-126.06578063964844,"z":39.37223434448242},"heading":352}'),
(DEFAULT, 'Rockford Fire Department 0-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-627.3859252929688,"y":-86.78646087646485,"z":34.91033172607422},"model":-1320876379,"heading":85},{"coords":{"x":-627.6557006835938,"y":-89.37895965576172,"z":34.91033172607422},"model":-1320876379,"heading":263}],"coords":{"x":-627.5208129882813,"y":-88.08271026611328,"z":34.91033172607422}}'),
(DEFAULT, 'Rockford Fire Department 0-2', '{"maxDistance":2,"state":1,"model":1242124150,"doors":false,"coords":{"x":-626.3673706054688,"y":-126.17216491699219,"z":36.1591796875},"heading":353}'),
(DEFAULT, 'Rockford Fire Department 0-3', '{"maxDistance":2,"state":1,"model":749848321,"doors":false,"coords":{"x":-624.3489990234375,"y":-124.35419464111328,"z":36.16632461547851},"heading":263}'),
(DEFAULT, 'Rockford Fire Department 2-1', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-627.6466674804688,"y":-86.78004455566406,"z":45.55057907104492},"model":-543497392,"heading":83},{"coords":{"x":-627.9727783203125,"y":-89.36128234863281,"z":45.55057907104492},"model":-543497392,"heading":263}],"coords":{"x":-627.8096923828125,"y":-88.07066345214844,"z":45.55057907104492}}'),
(DEFAULT, 'Rockford Fire Department 2-2', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-627.8391723632813,"y":-92.64289855957031,"z":45.6503791809082},"model":-543497392,"heading":172},{"coords":{"x":-625.2660522460938,"y":-93.00208282470703,"z":45.6503791809082},"model":-543497392,"heading":352}],"coords":{"x":-626.5526123046875,"y":-92.82249450683594,"z":45.6503791809082}}'),
(DEFAULT, 'Rockford Fire Department 2-3', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-623.285400390625,"y":-99.02505493164063,"z":45.64799118041992},"model":-2041685008,"heading":85},{"coords":{"x":-623.0536499023438,"y":-96.43830108642578,"z":45.64799118041992},"model":-2041685008,"heading":265}],"coords":{"x":-623.1695556640625,"y":-97.73167419433594,"z":45.64799118041992}}'),
(DEFAULT, 'Rockford Fire Department 2-4', '{"maxDistance":2,"state":0,"doors":[{"coords":{"x":-629.6240234375,"y":-96.81140899658203,"z":45.64404678344726},"model":-1821777087,"heading":84},{"coords":{"x":-629.9171142578125,"y":-99.39490509033203,"z":45.64404678344726},"model":-1821777087,"heading":264}],"coords":{"x":-629.7705688476563,"y":-98.10315704345703,"z":45.64404678344726}}'),
(DEFAULT, 'Rockford Fire Department 2-5', '{"maxDistance":2,"state":0,"doors":[{"coords":{"x":-629.5435180664063,"y":-100.49187469482422,"z":45.65087890625},"model":-1821777087,"heading":175},{"coords":{"x":-626.9542236328125,"y":-100.6955337524414,"z":45.65087890625},"model":-1821777087,"heading":355}],"coords":{"x":-628.2489013671875,"y":-100.59370422363281,"z":45.65087890625}}'),
(DEFAULT, 'Rockford Fire Department 2-6', '{"maxDistance":2,"state":1,"model":-1821777087,"doors":false,"coords":{"x":-633.68994140625,"y":-95.78797912597656,"z":45.65042495727539},"heading":354}'),
(DEFAULT, 'Rockford Fire Department 2-7', '{"maxDistance":2,"state":1,"model":-1821777087,"doors":false,"coords":{"x":-640.3739624023438,"y":-94.9888687133789,"z":45.65042495727539},"heading":354}'),
(DEFAULT, 'Rockford Fire Department 2-8', '{"maxDistance":2,"state":1,"model":-2041685008,"doors":false,"coords":{"x":-649.37939453125,"y":-96.35741424560547,"z":45.62529373168945},"heading":80}'),
(DEFAULT, 'Rockford Fire Department 2-9', '{"maxDistance":2,"state":1,"model":-538477509,"doors":false,"coords":{"x":-626.4992065429688,"y":-104.8864517211914,"z":45.64228057861328},"heading":265}'),
(DEFAULT, 'Rockford Fire Department 2-10', '{"maxDistance":2,"state":1,"model":-538477509,"doors":false,"coords":{"x":-627.046142578125,"y":-111.596923828125,"z":45.64289855957031},"heading":265}'),
(DEFAULT, 'Rockford Fire Department 2-11', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-630.4786376953125,"y":-118.40088653564453,"z":45.62514495849609},"model":-543497392,"heading":174},{"coords":{"x":-627.892822265625,"y":-118.65616607666016,"z":45.62514495849609},"model":-543497392,"heading":354}],"coords":{"x":-629.1857299804688,"y":-118.52852630615235,"z":45.62514495849609}}'),
(DEFAULT, 'Rockford Fire Department 2-12', '{"maxDistance":2,"state":1,"doors":[{"coords":{"x":-631.5808715820313,"y":-132.3054962158203,"z":43.37261581420898},"model":-2023754432,"heading":355},{"coords":{"x":-628.9940185546875,"y":-132.53182983398438,"z":43.37261581420898},"model":-2023754432,"heading":175}],"coords":{"x":-630.2874755859375,"y":-132.41867065429688,"z":43.37261581420898}}');
```

***

### 🚀 **Installation Guide**

Follow these steps to install the Rockford Fire Department map on your FiveM server:

1. **Download the Map Resource**
   * Ensure the `prompt_los_santos_fire_station` resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start prompt_los_santos_fire_station
       ```
3. **Set Up Doorlocks**
   * Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**
   * Restart your server and visit the map location at **-662.27, -73.37, 38.55** to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Paleto Fire Department** on your FiveM server! 🚀
