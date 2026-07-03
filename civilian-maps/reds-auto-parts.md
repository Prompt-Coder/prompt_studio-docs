# 🚗 Red's Auto Parts

{% embed url="https://fivem.prompt-mods.com/package/6266567" %}

{% embed url="https://youtu.be/C0B87NWbEZM" %}

The **Red's Auto Parts** is a detailed and immersive auto repair shop map designed for FiveM servers. Located in Los Santos, this map provides a realistic environment for roleplay scenarios, complete with seating areas, lifts, vending machines, and a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Red's Auto Parts** is located at the following coordinates:

* **Position**: `-508.58, -1733.44, 19.72`

***

### 🪑 Chairs

The map includes a variety of chairs and stools for added realism. Below are the chair models used in the map:

* `v_res_tre_stool_scuz`
* `m23_2_int4_m232_sofa_01`
* `m23_2_int4_m232_int_sub_bed`

***

### 🚗 Lifts

The map features functional car lifts for vehicle repairs. Below are the lift models used in the map:

* `m23_2_int4_m232_car_lift_01_down`
* `m23_2_int4_m232_car_lift_02_down`

***

### 🥤 Vending Machines

The map includes vending machines for added convenience. Below is the vending machine model used in the map:

* `m23_2_prop_m32_vend_drink_01a`

***

### 🚪 Doorlock System

The **Red's Auto Parts** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(532, 'Red\'s AutoParts G-1', '{"doors":false,"maxDistance":2,"heading":145,"coords":{"x":-512.9033203125,"y":-1739.1495361328126,"z":20.12289237976074},"model":-190780785,"state":1}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Red's Auto Parts** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_reds_repair_shop` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    plaintextCopy

    ```
    start prompt_reds_repair_shop
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-508.58, -1733.44, 19.72` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Red's Auto Parts** on your FiveM server! 🚀
