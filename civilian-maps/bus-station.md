# 🚏 Bus Station

{% embed url="https://fivem.prompt-mods.com/package/4450080" %}

{% embed url="https://youtu.be/aL75ZFeJGHg" %}

The **Los Santos Bus Station** is a detailed and functional bus station map designed for FiveM servers. Located in the heart of Los Santos, this map provides a realistic environment for roleplay scenarios, complete with seating areas and a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Los Santos Bus Station** is located at the following coordinates:

* **Position**: `433.96, -623.20, 28.50`

***

### 🪑 Chairs

The map includes benches and chairs for added realism. Below are the chair models used in the map:

* `v_ilev_ph_bench`
* `xm_int_lev_sub_chair_01`

***

### 🚪 Doorlock System

The **Los Santos Bus Station** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(600, 'Bus Station E-1', '{"maxDistance":2,"coords":{"x":436.82586669921877,"y":-645.9771728515625,"z":27.75592613220215},"state":1,"doors":[{"model":-1484815118,"coords":{"x":436.73028564453127,"y":-647.0697631835938,"z":27.75592613220215},"heading":265},{"model":-1484815118,"coords":{"x":436.92144775390627,"y":-644.8846435546875,"z":27.75592613220215},"heading":85}]}'),
(601, 'Bus Station E-2', '{"maxDistance":2,"coords":{"x":438.79779052734377,"y":-624.50634765625,"z":27.70729637145996},"state":1,"doors":[{"model":-1484815118,"coords":{"x":438.70208740234377,"y":-625.6000366210938,"z":27.70729637145996},"heading":265},{"model":-1484815118,"coords":{"x":438.8934631347656,"y":-623.4126586914063,"z":27.70729637145996},"heading":85}]}'),
(602, 'Bus Station 1-1', '{"maxDistance":2,"model":-2023754432,"coords":{"x":442.11285400390627,"y":-648.146240234375,"z":28.68785858154297},"heading":175,"state":1,"doors":false}'),
(603, 'Bus Station 1-2', '{"maxDistance":2,"model":-2023754432,"coords":{"x":443.39337158203127,"y":-648.2509765625,"z":28.68785858154297},"heading":355,"state":1,"doors":false}'),
(604, 'Bus Station 1-3', '{"maxDistance":2,"model":-2023754432,"coords":{"x":443.96087646484377,"y":-641.764404296875,"z":28.68785858154297},"heading":355,"state":1,"doors":false}'),
(605, 'Bus Station 1-4', '{"maxDistance":2,"model":-2023754432,"coords":{"x":442.6809387207031,"y":-641.6529541015625,"z":28.68785858154297},"heading":175,"state":1,"doors":false}'),
(606, 'Bus Station 1-5', '{"maxDistance":2,"model":-2023754432,"coords":{"x":443.4207458496094,"y":-633.197021484375,"z":28.68785858154297},"heading":175,"state":1,"doors":false}'),
(607, 'Bus Station 1-6', '{"maxDistance":2,"model":-2023754432,"coords":{"x":444.69378662109377,"y":-633.3872680664063,"z":28.68785858154297},"heading":355,"state":1,"doors":false}'),
(608, 'Bus Station 1-7', '{"maxDistance":2,"model":-2023754432,"coords":{"x":445.25958251953127,"y":-626.9205322265625,"z":28.68785858154297},"heading":355,"state":1,"doors":false}'),
(609, 'Bus Station 1-8', '{"maxDistance":2,"model":-2023754432,"coords":{"x":443.97991943359377,"y":-626.8056030273438,"z":28.68785858154297},"heading":175,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Los Santos Bus Station** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `bus_station` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start bus_station
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `433.96, -623.20, 28.50` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Los Santos Bus Station** on your FiveM server! 🚀
