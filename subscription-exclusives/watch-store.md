# ⌚ Watch Store

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

The **Watch Store** is a meticulously designed map for FiveM servers, offering a luxurious and immersive retail environment for roleplay scenarios. Located in the upscale district of Los Santos, this map provides a fully functional watch store with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Watch Store** is located at the following coordinates:

* **Position**: `-648.8801, -276.9714, 35.6846`

***

### 🪑 Chairs

The **Watch Store** map includes the following chair prop:

* **Chair**:
  * `v_ret_chair_white`

***

### 🚪 Doorlock System

The **Watch Store** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES 
(DEFAULT, 'Watch Store E-1', '{"maxDistance":2,"coords":{"x":-647.3912353515625,"y":-275.84326171875,"z":36.26143264770508},"state":1,"doors":[{"model":-1368194430,"coords":{"x":-646.8906860351563,"y":-276.71136474609377,"z":36.26143264770508},"heading":300},{"model":-1368194430,"coords":{"x":-647.891845703125,"y":-274.9751892089844,"z":36.26143264770508},"heading":120}]}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Watch Store** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_watch_store` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_watch_store
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-648.8801, -276.9714, 35.6846` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Watch Store** on your FiveM server! ⌚✨
