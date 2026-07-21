# 🏍️ Sandy Lost MC

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/psJL7W7U0do" %}

The **Sandy Shores Lost MC Biker Club** is a highly detailed and immersive map designed for FiveM servers. Located in the desert town of Sandy Shores, this map provides a gritty and atmospheric biker club environment for roleplay scenarios. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Sandy Shores Lost MC Biker Club** is located at the following coordinates:

* **Position**: `102.33, 3691.12, 39.72`

***

### 🚪 Doorlock System

The **Sandy Shores Lost MC Biker Club** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

<pre class="language-sql"><code class="lang-sql">INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
<strong>    (DEFAULT, 'Sandy Lost MC G-1', '{"doors":false,"model":1237855335,"coords":{"x":110.03023529052735,"y":3689.74755859375,"z":38.74575424194336},"heading":80,"state":1,"maxDistance":2}'),
</strong><strong>    (DEFAULT, 'Sandy Lost MC E-1', '{"doors":false,"model":-710818483,"coords":{"x":111.23632049560547,"y":3696.550537109375,"z":40.11320114135742},"heading":80,"state":1,"maxDistance":2}'),
</strong><strong>    (DEFAULT, 'Sandy Lost MC 1-1', '{"doors":false,"model":-710818483,"coords":{"x":120.47178649902344,"y":3685.7451171875,"z":40.11320114135742},"heading":170,"state":1,"maxDistance":2}'),
</strong>    (DEFAULT, 'Sandy Lost MC 1-2', '{"doors":false,"model":-710818483,"coords":{"x":128.62110900878907,"y":3697.467041015625,"z":40.10647201538086},"heading":170,"state":1,"maxDistance":2}'),
    (DEFAULT, 'Sandy Lost MC 1-3', '{"doors":false,"model":-710818483,"coords":{"x":119.28607177734375,"y":3699.18359375,"z":40.11320114135742},"heading":170,"state":1,"maxDistance":2}'),
    (DEFAULT, 'Sandy Lost MC 1-4', '{"doors":false,"model":1544229216,"coords":{"x":115.50468444824219,"y":3701.398193359375,"z":40.24978637695312},"heading":350,"state":1,"maxDistance":2}');
</code></pre>

***

### 🚀 Installation Guide

Follow these steps to install the **Sandy Shores Lost MC Biker Club** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_d1n-stab-city-lost-mc` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_d1n-stab-city-lost-mc
    ```
3. **Set Up Doorlocks**\
   Once the doorlock configuration is available, execute the provided SQL configuration in your database to enable the doorlock system.
4. Install MapData (if required)\
   For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](../sandy-maps/sandy-mapdata.md) for detailed instructions.
5. **Test the Map**\
   Restart your server and visit the map location at `102.33, 3691.12, 39.72` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Sandy Shores Lost MC Biker Club** on your FiveM server!&#x20;
