# 🥷 Gang Hideout Davis

{% embed url="https://fivem.prompt-mods.com/package/5469127" %}

{% embed url="https://youtu.be/zh5ForQ0fdg" %}

The **Gang Hideout Davis** is a gritty and immersive map designed for FiveM servers. Located in the Davis neighborhood of Los Santos, this map provides a realistic environment for roleplay scenarios, complete with seating areas, an arcade machine, and a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Gang Hideout Davis** is located at the following coordinates:

* **Position**: `-212.95, -1602.00, 34.86`

***

### 🪑 Chairs

The map includes a variety of chairs and sofas for added realism. Below are the chair models used in the map:

* `prop_ld_toilet_01`
* `prop_torture_ch_01`
* `prop_chair_01b`
* `v_res_tt_bed`
* `v_res_tt_sofa`
* `prop_chair_09`
* `prop_off_chair_04`
* `prop_ld_farm_couch02`
* `prop_rub_couch03`
* `prop_ld_farm_chair01`
* `v_res_fa_chair01`
* `v_ret_fh_chair01`

***

### 🕹️ Arcade Machine

The map features an arcade machine for added interactivity. Below is the arcade machine model used in the map:

* **Model**: `prop_arcade_01`

***

### 🚪 Doorlock System

The **Gang Hideout Davis** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Gang Hideout / Davis E-1', '{"maxDistance":2,"model":-1515008170,"coords":{"x":-208.40997314453126,"y":-1601.147705078125,"z":35.20551300048828},"heading":349,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / Davis 1-1', '{"maxDistance":2,"model":-5479653,"coords":{"x":-205.0818634033203,"y":-1599.102783203125,"z":35.12880706787109},"heading":259,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / Davis 1-2', '{"maxDistance":2,"model":-5479653,"coords":{"x":-202.89698791503907,"y":-1587.802490234375,"z":35.13292694091797},"heading":259,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / Davis 1-3', '{"maxDistance":2,"model":-5479653,"coords":{"x":-198.39285278320313,"y":-1581.263916015625,"z":35.12630081176758},"heading":322,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / Davis 1-4', '{"maxDistance":2,"coords":{"x":-209.00485229492188,"y":-1577.760498046875,"z":35.1319465637207},"state":1,"doors":[{"model":-5479653,"coords":{"x":-210.01475524902345,"y":-1576.9427490234376,"z":35.1319465637207},"heading":140},{"model":-5479653,"coords":{"x":-207.99496459960938,"y":-1578.5782470703126,"z":35.1319465637207},"heading":321}]}'),
(DEFAULT, 'Gang Hideout / Davis 1-5', '{"maxDistance":2,"model":-5479653,"coords":{"x":-216.31967163085938,"y":-1571.656005859375,"z":35.12838745117187},"heading":320,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / Davis 1-6', '{"maxDistance":2,"model":-5479653,"coords":{"x":-215.82919311523438,"y":-1564.9404296875,"z":35.12830352783203},"heading":53,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / Davis 1-7', '{"maxDistance":2,"model":-5479653,"coords":{"x":-223.83892822265626,"y":-1575.6939697265626,"z":35.12640380859375},"heading":53,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Gang Hideout Davis** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_gang_hideout_davis` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    plaintextCopy

    ```
    start cfx_prompt_gang_hideout_davis
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-212.95, -1602.00, 34.86` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Gang Hideout Davis** on your FiveM server! 🚀
