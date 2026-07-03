# 🍙 Japanese Restaurant

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/C0B87NWbEZM" %}

The **Japanese Restaurant** is a beautifully designed map for FiveM servers, offering a serene and authentic dining experience for roleplay scenarios. Located in the bustling city of Los Santos, this map provides a fully functional restaurant with detailed interiors and exteriors, perfect for immersive roleplay. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Japanese Restaurant** is located at the following coordinates:

* **Position**: `-169.64, 275.84, 94.38`

### 🗺️ Map Features

**Chairs**:

* `fluorine4305_chair_001`
* `prop_torture_ch_01`
* `v_ilev_chair02_ped`

**TV**:

* `prop_tv_flat_michael`

***

### 🚪 Doorlock System

The **Japanese Restaurant** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (533, 'Japanese Restaurant E-1', '{"doors":[{"heading":0,"model":2012678195,"coords":{"x":-168.76629638671876,"y":285.9325866699219,"z":93.95906066894531}},{"heading":0,"model":-965106369,"coords":{"x":-170.99729919433595,"y":285.9325866699219,"z":93.95906066894531}}],"maxDistance":2,"coords":{"x":-169.88180541992188,"y":285.9325866699219,"z":93.95906066894531},"state":1}'),
    (534, 'Japanese Restaurant E-2', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-166.6422882080078,"y":285.9216003417969,"z":93.9600601196289},"model":-369464256,"state":1}'),
    (535, 'Japanese Restaurant E-3', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-153.15528869628907,"y":287.3235778808594,"z":93.9600601196289},"model":-1653288146,"state":1}'),
    (536, 'Japanese Restaurant E-4', '{"doors":[{"heading":0,"model":-1093560853,"coords":{"x":-150.498291015625,"y":294.818603515625,"z":99.09606170654297}},{"heading":0,"model":-726253128,"coords":{"x":-152.8032989501953,"y":294.818603515625,"z":99.09606170654297}}],"maxDistance":2,"coords":{"x":-151.65078735351563,"y":294.818603515625,"z":99.09606170654297},"state":1}'),
    (537, 'Japanese Restaurant 1-1', '{"doors":[{"heading":180,"model":-1089711493,"coords":{"x":-168.7952880859375,"y":299.99859619140627,"z":93.9150619506836}},{"heading":0,"model":-1089711493,"coords":{"x":-171.24530029296876,"y":299.99859619140627,"z":93.9150619506836}}],"maxDistance":2,"coords":{"x":-170.02029418945313,"y":299.99859619140627,"z":93.9150619506836},"state":1}'),
    (538, 'Japanese Restaurant 1-2', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-159.4425506591797,"y":300.1082763671875,"z":93.91758728027344},"model":-2012426746,"state":1}'),
    (539, 'Japanese Restaurant 1-3', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-159.04241943359376,"y":300.1082763671875,"z":93.91758728027344},"model":-868476758,"state":1}'),
    (540, 'Japanese Restaurant G-1', '{"doors":false,"maxDistance":2,"heading":270,"coords":{"x":-178.2048797607422,"y":319.30084228515627,"z":98.36776733398438},"model":-1274314914,"state":1}'),
    (541, 'Japanese Restaurant 2-1', '{"doors":false,"maxDistance":2,"heading":90,"coords":{"x":-171.3477020263672,"y":302.71099853515627,"z":97.61006927490235},"model":-2023754432,"state":1}'),
    (542, 'Japanese Restaurant 2-2', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-171.36883544921876,"y":317.8489074707031,"z":98.14335632324219},"model":-49034954,"state":1}'),
    (543, 'Japanese Restaurant 2-3', '{"doors":[{"heading":180,"model":-1407669096,"coords":{"x":-164.21829223632813,"y":299.9575500488281,"z":99.04405975341797}},{"heading":0,"model":-1407669096,"coords":{"x":-166.20529174804688,"y":299.95758056640627,"z":99.04405975341797}}],"maxDistance":2,"coords":{"x":-165.2117919921875,"y":299.95758056640627,"z":99.04405975341797},"state":1}'),
    (544, 'Japanese Restaurant 2-4', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-159.44131469726563,"y":300.0574951171875,"z":99.04840850830078},"model":-1177931392,"state":1}'),
    (545, 'Japanese Restaurant 2-5', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-159.04241943359376,"y":300.0574951171875,"z":99.04840850830078},"model":-1164053138,"state":1}'),
    (546, 'Japanese Restaurant 2-6', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-149.5572967529297,"y":299.39959716796877,"z":99.02205657958985},"model":-862441096,"state":1}'),
    (547, 'Japanese Restaurant 2-7', '{"doors":false,"maxDistance":2,"heading":0,"coords":{"x":-142.96730041503907,"y":299.39959716796877,"z":99.02205657958985},"model":423873230,"state":1}'),
    (548, 'Japanese Restaurant 3-1', '{"doors":false,"maxDistance":2,"heading":90,"coords":{"x":-171.31900024414063,"y":302.71063232421877,"z":101.07380676269531},"model":-2023754432,"state":1}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Japanese Restaurant** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_japanese_restaurant` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_japanese_restaurant
    ```
3. **Set Up Doorlocks**\
   Once the doorlock configuration is available, execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-169.64, 275.84, 94.38` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Japanese Restaurant** on your FiveM server! 🍣🍜
