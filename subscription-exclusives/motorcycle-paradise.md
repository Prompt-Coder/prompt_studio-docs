# 🏍️ Motorcycle Paradise

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/hlemEwpRJ78" %}

The **Motorcycle Paradise** is a sleek and immersive map designed for FiveM servers, offering a stylish and functional environment for motorcycle enthusiasts. Located in the heart of Los Santos, this map provides a fully equipped motorcycle showroom with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Motorcycle Paradise** is located at the following coordinates:

* **Position**: `287.31, -1141.62, 30.46`

***

### 🪑 Chairs

The **Motorcycle Paradise** map includes the following chair prop:

* **Chair**:
  * `xm_lab_chairarm_12`

***

### 🚪 Doorlock System

The **Motorcycle Paradise** map includes a customizable doorlock system to restrict access to specific areas. Below is an example SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (1026, 'Bike Shop Door 1026', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_csr_door_r","coords":{"x":287.8423,"y":-1149.089,"z":29.51102},"state":1}'),
    (1027, 'Bike Shop Door 1027', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_csr_door_l","coords":{"x":285.8636,"y":-1149.089,"z":29.51102},"state":1}'),
    (1028, 'Bike Shop Door 1028', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_csr_door_r","coords":{"x":269.334,"y":-1154.351,"z":29.51004},"state":1}'),
    (1029, 'Bike Shop Door 1029', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_csr_door_l","coords":{"x":269.334,"y":-1156.329,"z":29.51004},"state":1}'),
    (1030, 'Bike Shop Door 1030', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_15_garg_delta_doordown","coords":{"x":269.2986,"y":-1159.701,"z":29.94192},"state":1}'),
    (1031, 'Bike Shop Door 1031', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_15_garg_delta_doordown2","coords":{"x":304.3455,"y":-1162.837,"z":29.13172},"state":1}'),
    (1032, 'Bike Shop Door 1032', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_cbankcountdoor02","coords":{"x":288.3299,"y":-1167.492,"z":29.54739},"state":1}'),
    (1033, 'Bike Shop Door 1033', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_cbankcountdoor01","coords":{"x":288.3299,"y":-1165.246,"z":29.54739},"state":1}'),
    (1034, 'Bike Shop Door 1034', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_cbankcountdoor02","coords":{"x":282.758,"y":-1156.719,"z":29.54646},"state":1}'),
    (1035, 'Bike Shop Door 1035', '{"maxDistance":2.0,"heading":0.0,"doors":false,"model":"honey_5m_bikeshop_v_ilev_cbankcountdoor01","coords":{"x":280.5119,"y":-1156.719,"z":29.54646},"state":1}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Motorcycle Paradise** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_motorcycle_paradise` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_motorcycle_paradise
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `287.31, -1141.62, 30.46` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Motorcycle Paradise** on your FiveM server! 🏍️✨
