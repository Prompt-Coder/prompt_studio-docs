# 🥷 Gang Hideout El-Burro

{% embed url="https://fivem.prompt-mods.com/package/5460876" %}

{% embed url="https://youtu.be/EkL_mrWCHbU" %}

The **Gang Hideout El-Burro** is a gritty and immersive map designed for FiveM servers. Located in the El-Burro Heights neighborhood of Los Santos, this map provides a realistic environment for roleplay scenarios, complete with seating areas, a TV, and a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Gang Hideout El-Burro** is located at the following coordinates:

* **Position**: `1435.28, -1497.95, 63.22`

***

### 🪑 Chairs

The map includes a variety of chairs and sofas for added realism. Below are the chair models used in the map:

* `prop_torture_ch_01`
* `v_res_tt_bed`
* `v_res_tt_sofa`
* `prop_off_chair_04`
* `prop_table_06_chr`
* `v_ret_fh_chair01`
* `prop_bench_11`
* `v_res_j_sofa`
* `prop_toilet_01`

***

### 📺 TV

The map features a TV to enhance the environment. The following TV model is used:

* `v_ret_gc_tv`

***

### 🚪 Doorlock System

The **Gang Hideout El-Burro** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Gang Hideout / El Burro E-1', '{"maxDistance":2,"coords":{"x":1437.5860595703126,"y":-1491.52001953125,"z":63.77627563476562},"state":1,"doors":[{"model":262671971,"coords":{"x":1438.635986328125,"y":-1491.846435546875,"z":63.77627563476562},"heading":163},{"model":1504256620,"coords":{"x":1436.5361328125,"y":-1491.193603515625,"z":63.77627563476562},"heading":343}]}'),
(DEFAULT, 'Gang Hideout / El Burro E-2', '{"maxDistance":2,"model":262671971,"coords":{"x":1439.330322265625,"y":-1480.5023193359376,"z":63.78522872924805},"heading":343,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / El Burro 1-1', '{"maxDistance":2,"model":-1186396713,"coords":{"x":1441.078369140625,"y":-1490.13427734375,"z":63.77946853637695},"heading":73,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / El Burro 1-2', '{"maxDistance":2,"model":103339342,"coords":{"x":1441.8800048828126,"y":-1487.609619140625,"z":63.77902221679687},"heading":252,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / El Burro 1-3', '{"maxDistance":2,"model":103339342,"coords":{"x":1442.7642822265626,"y":-1482.8558349609376,"z":66.78407287597656},"heading":73,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / El Burro 1-4', '{"maxDistance":2,"model":-1186396713,"coords":{"x":1441.0762939453126,"y":-1490.1749267578126,"z":66.78370666503906},"heading":254,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / El Burro 1-5', '{"maxDistance":2,"model":-1186396713,"coords":{"x":1440.7945556640626,"y":-1490.9676513671876,"z":66.7834701538086},"heading":73,"state":1,"doors":false}'),
(DEFAULT, 'Gang Hideout / El Burro E-3', '{"maxDistance":2,"coords":{"x":1435.815185546875,"y":-1491.0771484375,"z":66.79662322998047},"state":1,"doors":[{"model":1504256620,"coords":{"x":1434.761474609375,"y":-1490.758056640625,"z":66.79662322998047},"heading":343},{"model":262671971,"coords":{"x":1436.8687744140626,"y":-1491.396240234375,"z":66.79662322998047},"heading":163}]}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Gang Hideout El-Burro** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_gang_hideout_el_burro` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    plaintextCopy

    ```
    start cfx_prompt_gang_hideout_el_burro
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `1435.28, -1497.95, 63.22` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Gang Hideout El-Burro** on your FiveM server! 🚀
