# ⛽ Gas Station

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

The **Gas Station** is a detailed and immersive map designed for FiveM servers, offering a realistic fueling and convenience store environment for roleplay scenarios. Located in the scenic area of Sandy Shores, this map provides a fully functional gas station with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Gas Station** is located at the following coordinates:

* **Position**: `2000.23, 3776.39, 32.18`

***

### 🪑 Chairs

The **Gas Station** map includes the following chair prop:

* **Chair**:
  * `prop_ld_toilet_01`

***

### 🚪 Doorlock System

The **Gas Station** map includes a customizable doorlock system to restrict access to specific areas. Below is an example SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES 
	(DEFAULT, 'Sandy Gas Station 1-1', '{"doors":false,"model":-495720969,"coords":{"x":1997.496826171875,"y":3783.47802734375,"z":32.34941482543945},"heading":120,"state":1,"maxDistance":2}'),
	(DEFAULT, 'Sandy Gas Station E-1', '{"doors":[{"coords":{"x":2001.9114990234376,"y":3780.602294921875,"z":32.3482780456543},"model":-98391585,"heading":210},{"coords":{"x":2000.4759521484376,"y":3779.773193359375,"z":32.3482780456543},"model":-606311141,"heading":30}],"coords":{"x":2001.1937255859376,"y":3780.187744140625,"z":32.3482780456543},"state":1,"maxDistance":2}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Gas Station** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_sandy_gas_station` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_sandy_gas_station
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `2000.23, 3776.39, 32.18` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Gas Station** on your FiveM server! ⛽🚗
