# 🚗 Rockford Dealership

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/hlemEwpRJ78" %}

The **Rockford Dealership** is a highly detailed and immersive map designed for FiveM servers, offering a realistic car dealership environment for roleplay scenarios. Located in the bustling Rockford Hills district, this map provides a fully functional dealership with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Rockford Dealership** is located at the following coordinates:

* **Position**: `-323.18, -257.58, 34.39`

### 🗺️ Map Features

**Chairs**:

* `prompt_rdealer_chilling_spot`
* `apa_mpa2_din_chair_00`
* `hei_prop_heist_off_chair`
* `sum_mp_h_yacht_sofa_02`

**Lifts**:

* `prompt_rdealer_carlift`

***

### 🚪 Doorlock System

The **Rockford Dealership** map includes a customizable doorlock system to restrict access to specific areas. Below is an example SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES 
	(DEFAULT, 'Rockford Dealership G-1', '{"coords":{"x":-354.4662170410156,"y":-232.13206481933595,"z":36.23910903930664},"heading":54,"model":1281492173,"maxDistance":2,"state":1,"doors":false}'),
	(DEFAULT, 'Rockford Dealership G-2', '{"coords":{"x":-351.11285400390627,"y":-227.54046630859376,"z":36.24414825439453},"heading":54,"model":1281492173,"maxDistance":2,"state":1,"doors":false}'),
	(DEFAULT, 'Rockford Dealership E-2', '{"coords":{"x":-317.12506103515627,"y":-226.3603057861328,"z":36.97378921508789},"maxDistance":2,"state":1,"doors":[{"heading":325,"model":424177038,"coords":{"x":-317.9437561035156,"y":-225.78704833984376,"z":36.97378921508789}},{"heading":145,"model":424177038,"coords":{"x":-316.3063659667969,"y":-226.93356323242188,"z":36.97378921508789}}]}'),
	(DEFAULT, 'Rockford Dealership E-1', '{"coords":{"x":-327.3249816894531,"y":-254.08030700683595,"z":34.55200576782226},"maxDistance":2,"state":1,"doors":[{"heading":55,"model":1861302034,"coords":{"x":-326.7520446777344,"y":-253.26206970214845,"z":34.55200576782226}},{"heading":55,"model":424177038,"coords":{"x":-327.8979187011719,"y":-254.89854431152345,"z":34.55200576782226}}]}'),
	(DEFAULT, 'Rockford Dealership 1-1', '{"coords":{"x":-324.9126892089844,"y":-226.91445922851563,"z":36.98732376098633},"heading":325,"model":946508663,"maxDistance":2,"state":1,"doors":false}'),
	(DEFAULT, 'Rockford Dealership 1-2', '{"coords":{"x":-328.8351135253906,"y":-224.1824951171875,"z":36.98762130737305},"heading":325,"model":946508663,"maxDistance":2,"state":1,"doors":false}'),
	(DEFAULT, 'Rockford Dealership 1-3', '{"coords":{"x":-332.7995300292969,"y":-221.50550842285157,"z":36.98852157592773},"heading":325,"model":946508663,"maxDistance":2,"state":1,"doors":false}'),
	(DEFAULT, 'Rockford Dealership 1-4', '{"coords":{"x":-343.9602355957031,"y":-222.73057556152345,"z":37.4089469909668},"heading":325,"model":-1726818330,"maxDistance":2,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Rockford Dealership** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_rdealer` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_rdealer
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-323.18, -257.58, 34.39` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Rockford Dealership** on your FiveM server! 🚗🏁
