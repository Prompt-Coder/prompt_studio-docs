# 👮 Paleto Sheriff

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/TtAdLFJ-2zM" %}

The **Paleto Sheriff Department** is a meticulously designed map for FiveM servers, offering a realistic law enforcement environment for roleplay scenarios. Located in the serene town of Paleto Bay, this map provides a fully functional sheriff's office with detailed interiors and exteriors. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Paleto Sheriff Department** is located at the following coordinates:

* **Position**: `-427.55, 6019.88, 31.47`

***

### 🚪 Doorlock System

The **Paleto Sheriff Department** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(654, 'Paleto Sheriff E-1', '{"maxDistance":2,"model":-1567414359,"coords":{"x":-434.37493896484377,"y":6012.3935546875,"z":32.09313201904297},"heading":315,"state":1,"doors":false}'),
	(655, 'Paleto Sheriff 1-1', '{"maxDistance":2,"model":-2123373213,"coords":{"x":-439.149658203125,"y":6007.55419921875,"z":32.06966018676758},"heading":135,"state":1,"doors":false}'),
	(656, 'Paleto Sheriff 1-2', '{"maxDistance":2,"model":1697656036,"coords":{"x":-436.6623229980469,"y":6004.42724609375,"z":32.0988540649414},"heading":135,"state":1,"doors":false}'),
	(657, 'Paleto Sheriff 1-3', '{"maxDistance":2,"model":1697656036,"coords":{"x":-433.3275146484375,"y":6001.07275390625,"z":32.09967803955078},"heading":135,"state":1,"doors":false}'),
	(658, 'Paleto Sheriff 1-4', '{"maxDistance":2,"model":1697656036,"coords":{"x":-436.76776123046877,"y":5998.63134765625,"z":32.09854125976562},"heading":315,"state":1,"doors":false}'),
	(659, 'Paleto Sheriff 1-5', '{"maxDistance":2,"model":1697656036,"coords":{"x":-441.85247802734377,"y":6001.16845703125,"z":32.09762573242187},"heading":45,"state":1,"doors":false}'),
	(660, 'Paleto Sheriff 1-6', '{"maxDistance":2,"model":1697656036,"coords":{"x":-448.274658203125,"y":6011.56201171875,"z":32.10568618774414},"heading":315,"state":1,"doors":false}'),
	(661, 'Paleto Sheriff 1-8', '{"maxDistance":2,"model":1697656036,"coords":{"x":-447.5762634277344,"y":6016.373046875,"z":32.09729385375976},"heading":225,"state":1,"doors":false}'),
	(662, 'Paleto Sheriff 1-7', '{"maxDistance":2,"model":1697656036,"coords":{"x":-446.95465087890627,"y":6014.72265625,"z":32.106201171875},"heading":135,"state":1,"doors":false}'),
	(663, 'Paleto Sheriff 1-9', '{"maxDistance":2,"model":1697656036,"coords":{"x":-452.1437683105469,"y":6015.998046875,"z":32.09511184692383},"heading":225,"state":1,"doors":false}'),
	(664, 'Paleto Sheriff 1-10', '{"maxDistance":2,"model":1697656036,"coords":{"x":-451.7818298339844,"y":6013.6357421875,"z":32.09706497192383},"heading":315,"state":1,"doors":false}'),
	(665, 'Paleto Sheriff E-2', '{"maxDistance":2,"model":863717779,"coords":{"x":-442.7430419921875,"y":5990.17529296875,"z":32.0947151184082},"heading":225,"state":1,"doors":false}'),
	(666, 'Paleto Sheriff 1-12', '{"maxDistance":2,"model":400691809,"coords":{"x":-441.51800537109377,"y":5987.12744140625,"z":32.10067749023437},"heading":45,"state":1,"doors":false}'),
	(667, 'Paleto Sheriff 1-11', '{"maxDistance":2,"model":400691809,"coords":{"x":-440.1981201171875,"y":5988.47265625,"z":32.09803771972656},"heading":225,"state":1,"doors":false}'),
	(668, 'Paleto Sheriff 0-1', '{"maxDistance":2,"model":472981945,"coords":{"x":-437.66253662109377,"y":5997.57177734375,"z":28.34415054321289},"heading":315,"state":1,"doors":false}'),
	(669, 'Paleto Sheriff 0-2', '{"maxDistance":2,"model":472981945,"coords":{"x":-433.2354431152344,"y":5999.1689453125,"z":28.34118270874023},"heading":225,"state":1,"doors":false}'),
	(670, 'Paleto Sheriff 0-3', '{"maxDistance":2,"model":472981945,"coords":{"x":-434.4946594238281,"y":6001.85986328125,"z":28.34299850463867},"heading":45,"state":1,"doors":false}'),
	(671, 'Paleto Sheriff 0-4', '{"maxDistance":2,"model":-871983225,"coords":{"x":-436.0227355957031,"y":6003.6875,"z":28.37539482116699},"heading":45,"state":1,"doors":false}'),
	(672, 'Paleto Sheriff 0-5', '{"maxDistance":2,"coords":{"x":-443.4676513671875,"y":5999.91845703125,"z":28.34253883361816},"state":1,"doors":[{"model":1113619785,"coords":{"x":-442.62249755859377,"y":6000.763671875,"z":28.34253883361816},"heading":225},{"model":1113619785,"coords":{"x":-444.31280517578127,"y":5999.0732421875,"z":28.34253883361816},"heading":45}]}'),
	(673, 'Paleto Sheriff 0-6', '{"maxDistance":2,"model":878277124,"coords":{"x":-447.5989685058594,"y":6006.0595703125,"z":27.19585227966308},"heading":225,"state":1,"doors":false}'),
	(674, 'Paleto Sheriff 0-7', '{"maxDistance":2,"model":878277124,"coords":{"x":-447.1788330078125,"y":6007.47802734375,"z":27.19647407531738},"heading":315,"state":1,"doors":false}'),
	(675, 'Paleto Sheriff 0-8', '{"maxDistance":2,"model":878277124,"coords":{"x":-445.3467712402344,"y":6009.31005859375,"z":27.19547843933105},"heading":315,"state":1,"doors":false}'),
	(676, 'Paleto Sheriff 0-9', '{"maxDistance":2,"model":878277124,"coords":{"x":-443.18212890625,"y":6011.474609375,"z":27.19707679748535},"heading":315,"state":1,"doors":false}'),
	(677, 'Paleto Sheriff 0-10', '{"maxDistance":2,"model":472981945,"coords":{"x":-447.10845947265627,"y":6001.58447265625,"z":28.34185028076172},"heading":135,"state":1,"doors":false}'),
	(678, 'Paleto Sheriff 0-11', '{"maxDistance":2,"model":472981945,"coords":{"x":-449.4573059082031,"y":6003.93310546875,"z":28.34185028076172},"heading":135,"state":1,"doors":false}'),
	(679, 'Paleto Sheriff 0-12', '{"maxDistance":2,"model":472981945,"coords":{"x":-448.51861572265627,"y":5993.3759765625,"z":27.33387374877929},"heading":45,"state":1,"doors":false}'),
	(680, 'Paleto Sheriff 0-13', '{"maxDistance":2,"model":472981945,"coords":{"x":-450.47564697265627,"y":5991.4052734375,"z":27.32875251770019},"heading":45,"state":1,"doors":false}'),
	(681, 'Paleto Sheriff 0-14', '{"maxDistance":2,"coords":{"x":-450.1090087890625,"y":5987.6796875,"z":27.33162689208984},"state":1,"doors":[{"model":1113619785,"coords":{"x":-450.9541931152344,"y":5988.52490234375,"z":27.33162689208984},"heading":315},{"model":1113619785,"coords":{"x":-449.2638244628906,"y":5986.8349609375,"z":27.33162689208984},"heading":135}]}'),
	(682, 'Paleto Sheriff 0-15', '{"maxDistance":2,"model":472981945,"coords":{"x":-454.0626525878906,"y":5985.6875,"z":27.32840919494629},"heading":45,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Paleto Sheriff Department** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_tuco_paleto_sheriff` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_tuco_paleto_sheriff
    ```
3. **Set Up Doorlocks**\
   Once the doorlock configuration is available, execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-427.55, 6019.88, 31.47` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Paleto Sheriff Department** on your FiveM server! 🚀
