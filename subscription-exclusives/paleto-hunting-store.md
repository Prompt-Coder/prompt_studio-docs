# 🔫 Paleto Hunting Store

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/JVSkrBivsgI" %}

The **Paleto Hunting Store** is a detailed and immersive map designed for FiveM servers, offering a rustic and functional hunting store environment for roleplay scenarios. Located in the tranquil town of Paleto Bay, this map provides a fully equipped store with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Paleto Hunting Store** is located at the following coordinates:

* **Position**: `-685.92, 5834.45, 19.08`

***

### 🚪 Doorlock System

The **Paleto Hunting Store** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (570, 'Paleto Hunting Store E-1', '{"doors":false,"maxDistance":2,"heading":315,"coords":{"x":-678.3617553710938,"y":5834.16015625,"z":17.42280578613281},"model":-1563799200,"state":1}'),
    (571, 'Paleto Hunting Store 1-1', '{"doors":false,"maxDistance":2,"heading":45,"coords":{"x":-674.2617797851563,"y":5833.1474609375,"z":17.47189712524414},"model":-2023754432,"state":1}'),
    (572, 'Paleto Hunting Store 1-2', '{"doors":false,"maxDistance":2,"heading":135,"coords":{"x":-670.0435180664063,"y":5831.2919921875,"z":17.48620986938476},"model":-1033001619,"state":1}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Paleto Hunting Store** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_paleto_hunting_store` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_paleto_hunting_store
    ```
3. **Set Up Doorlocks**\
   Once the doorlock configuration is available, execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-685.92, 5834.45, 19.08` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Paleto Hunting Store** on your FiveM server!
