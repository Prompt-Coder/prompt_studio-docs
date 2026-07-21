# 🏡 Dynasty 8

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/psJL7W7U0do" %}

The **Dynasty 8 Real Estate** is a beautifully designed map for FiveM servers, offering a professional and modern real estate office environment for roleplay scenarios. Located in the heart of Los Santos, this map provides a fully functional office space with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Dynasty 8 Real Estate** is located at the following coordinates:

* **Position**: `-839.15, -331.78, 38.68`

### 🗺️ Map Features

**Chairs**:

* `prop_off_chair_01`
* `prop_sol_chair`
* `xm_lab_sofa_02`
* `ex_office_03c_recepchair_1`
* `vw_prop_vw_offchair_03`
* `v_corp_offchair`
* `apa_mp_h_stn_chairarm_26`

***

### 🚪 Doorlock System

The **Dynasty 8 Real Estate** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (DEFAULT, 'Dynasty 8 E-1', '{"doors":[{"heading":117,"model":-98018355,"coords":{"x":-842.8986206054688,"y":-333.65985107421877,"z":38.87641143798828}},{"heading":297,"model":-98018355,"coords":{"x":-841.734619140625,"y":-335.9458312988281,"z":38.87641143798828}}],"maxDistance":2,"coords":{"x":-842.316650390625,"y":-334.8028564453125,"z":38.87641143798828},"state":1}'),
    (DEFAULT, 'Dynasty 8 1-1', '{"doors":false,"maxDistance":2,"heading":207,"coords":{"x":-855.5955200195313,"y":-348.5436096191406,"z":38.81884384155273},"model":-551608542,"state":1}'),
    (DEFAULT, 'Dynasty 8 2-1', '{"doors":false,"maxDistance":2,"heading":342,"coords":{"x":-840.8136596679688,"y":-334.41082763671877,"z":44.85441589355469},"model":1111157749,"state":1}'),
    (DEFAULT, 'Dynasty 8 2-2', '{"doors":false,"maxDistance":2,"heading":117,"coords":{"x":-846.0596313476563,"y":-340.2448425292969,"z":44.86441421508789},"model":-551608542,"state":1}'),
    (DEFAULT, 'Dynasty 8 2-3', '{"doors":false,"maxDistance":2,"heading":27,"coords":{"x":-849.8776245117188,"y":-339.9818420410156,"z":44.86141204833984},"model":-551608542,"state":1}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Dynasty 8 Real Estate** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_nm_dynasty8` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_nm_dynasty8
    ```
3. **Set Up Doorlocks**\
   Once the doorlock configuration is available, execute the provided SQL configuration in your database to enable the doorlock system.
4.
5. **Test the Map**\
   Restart your server and visit the map location at `-839.15, -331.78, 38.68` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Dynasty 8 Real Estate** on your FiveM server! 🚀
