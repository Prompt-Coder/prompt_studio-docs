# 🛠️ Repair Shops

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/hlemEwpRJ78" %}

The **Repair Shops** is a comprehensive map designed for FiveM servers, offering multiple realistic repair shop environments for roleplay scenarios. This map includes detailed interiors and exteriors for various repair shops, complete with functional lifts, seating, and other immersive elements. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Overview

The **Repair Shops** map includes multiple locations, each with its own unique setup. The map features:

* **Position:** \
  **1:** `1153.89, -775.50, 57.60`\
  2: `537.29, -173.51, 54.50`
* **Chairs**:
  * `bkr_prop_clubhouse_sofa_01a`
  * `prop_off_chair_05`
  * `v_corp_offchair`
* **TV**:
  * `fluorine4305_cto_tv_stand`
* **Lifts**:
  * `fluorine4305_cto_carlift1`
  * `fluorine4305_cto_carlift2`

***

### 🚪 Doorlock System

The **Repair Shops** map includes a customizable doorlock system to restrict access to specific areas. Below is an example SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES 

```

***

### 🚀 Installation Guide

Follow these steps to install the **Repair Shops** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_repair_stations` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_repair_stations
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system for each repair shop.
4. **Test the Map**\
   Restart your server and visit the repair shop locations to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Repair Shops** on your FiveM server! 🛠️🚗
