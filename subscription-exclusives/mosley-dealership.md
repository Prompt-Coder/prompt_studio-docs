# 🚘 Mosley Dealership

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/hlemEwpRJ78" %}

The **Mosley Dealership** is a highly detailed and immersive map designed for FiveM servers, offering a realistic car dealership environment for roleplay scenarios. Located in the industrial area of Los Santos, this map provides a fully functional dealership with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Mosley Dealership** is located at the following coordinates:

* **Position**: `-54.44, -1678.97, 30.58`

***

### 🚪 Doorlock System

The **Mosley Dealership** map includes a customizable doorlock system to restrict access to specific areas. Below is an example SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(DEFAULT, 'Mosley Dealership E-1', '{"coords":{"x":-40.3743667602539,"y":-1674.2440185546876,"z":29.62456703186035},"maxDistance":2,"state":1,"doors":[{"heading":320,"model":288089934,"coords":{"x":-39.4085693359375,"y":-1675.054443359375,"z":29.62456703186035}},{"heading":320,"model":32360658,"coords":{"x":-41.34016036987305,"y":-1673.43359375,"z":29.62456703186035}}]}'),
	(DEFAULT, 'Mosley Dealership E-2', '{"coords":{"x":-43.11420059204101,"y":-1661.8682861328126,"z":29.72961807250976},"maxDistance":2,"state":1,"doors":[{"heading":50,"model":-1490873538,"coords":{"x":-44.04762268066406,"y":-1662.980712890625,"z":29.72961807250976}},{"heading":50,"model":-647891013,"coords":{"x":-42.18077850341797,"y":-1660.755859375,"z":29.72961807250976}}]}'),
	(DEFAULT, 'Mosley Dealership G-1', '{"coords":{"x":-30.90956115722656,"y":-1647.5404052734376,"z":30.53314590454101},"heading":230,"model":-937747387,"maxDistance":2,"state":1,"doors":false}'),
	(DEFAULT, 'Mosley Dealership 1-1', '{"coords":{"x":-33.95782852172851,"y":-1663.5966796875,"z":29.67400169372558},"heading":50,"model":-2051651622,"maxDistance":2,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Mosley Dealership** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_mosley_dealership` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_mosley_dealership
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-54.44, -1678.97, 30.58` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Mosley Dealership** on your FiveM server! 🚗🏁
