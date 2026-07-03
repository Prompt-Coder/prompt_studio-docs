# 🚒 Paleto Fire Department

{% embed url="https://fivem.prompt-mods.com/package/5203442" %}

{% embed url="https://youtu.be/KSaXWUpU3ac" %}

The **Paleto Fire Department** is a custom map designed for FiveM servers, offering a fully immersive fire station environment for roleplay, emergency response, and firefighting scenarios. This map features a detailed interior and exterior, complete with interactive props, seating arrangements, and a robust doorlock system for enhanced gameplay. Below, you’ll find all the necessary details to install and configure this map on your server.

***

### 📍 **Map Location**

The Paleto Fire Department is located at the following coordinates:\
&#xNAN;**-381.10, 6120.57, 31.47**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The map includes a variety of chairs and props to create a realistic fire station environment. Below is a list of the chairs included:

* `prop_bench_06`
* `prop_stool_01`
* `v_club_officechair`
* `prop_off_chair_03`
* `v_res_fa_chair01`
* `v_res_fh_kitnstool`
* `prop_chair_02`
* `prop_toilet_01`
* `prompt_paleto_sleep_bed`
* `prompt_paleto_blanket_1`
* `prompt_paleto_blanket_2`
* `prompt_paleto_chair_custom`
* `prompt_paleto_street_bench`

***

#### 📺 **TV**

The map includes a TV for added realism:

* `prop_tv_flat_02b`

***

#### 🚪 **Doorlock System**

The Paleto Fire Department map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(292, 'Paleto Bay Fire Department G-1', '{"doors":false,"model":1789636489,"coords":{"x":-366.82147216796877,"y":6130.6796875,"z":33.03107833862305},"heading":225,"state":1,"maxDistance":2}'),
(293, 'Paleto Bay Fire Department G-2', '{"doors":false,"model":1789636489,"coords":{"x":-363.3889465332031,"y":6134.078125,"z":33.02942657470703},"heading":225,"state":1,"maxDistance":2}'),
(294, 'Paleto Bay Fire Department G-3', '{"doors":false,"model":1789636489,"coords":{"x":-360.0032653808594,"y":6137.45947265625,"z":33.03010940551758},"heading":225,"state":1,"maxDistance":2}'),
(295, 'Paleto Bay Fire Department G-4', '{"doors":false,"model":1789636489,"coords":{"x":-356.5881652832031,"y":6140.87744140625,"z":33.03178405761719},"heading":225,"state":1,"maxDistance":2}'),
(296, 'Paleto Bay Fire Department G-5', '{"doors":false,"model":1789636489,"coords":{"x":-344.1676940917969,"y":6128.46142578125,"z":33.03068161010742},"heading":45,"state":1,"maxDistance":2}'),
(297, 'Paleto Bay Fire Department G-6', '{"doors":false,"model":1789636489,"coords":{"x":-347.5775146484375,"y":6125.03857421875,"z":33.03019332885742},"heading":45,"state":1,"maxDistance":2}'),
(298, 'Paleto Bay Fire Department G-7', '{"doors":false,"model":1789636489,"coords":{"x":-350.9595947265625,"y":6121.650390625,"z":33.03315353393555},"heading":45,"state":1,"maxDistance":2}'),
(299, 'Paleto Bay Fire Department G-8', '{"doors":false,"model":1789636489,"coords":{"x":-354.38116455078127,"y":6118.2314453125,"z":33.0260009765625},"heading":45,"state":1,"maxDistance":2}'),
(300, 'Paleto Bay Fire Department E-1', '{"doors":[{"coords":{"x":-380.1513671875,"y":6117.697265625,"z":31.53499984741211},"model":1482185401,"heading":225},{"coords":{"x":-378.6073303222656,"y":6119.3046875,"z":31.53499984741211},"model":1482185401,"heading":45}],"coords":{"x":-379.37933349609377,"y":6118.5009765625,"z":31.53499984741211},"state":1,"maxDistance":2}'),
(301, 'Paleto Bay Fire Department E-2', '{"doors":false,"model":1482185401,"coords":{"x":-378.9424743652344,"y":6106.13037109375,"z":31.53713417053222},"heading":135,"state":1,"maxDistance":2}'),
(302, 'Paleto Bay Fire Department 1-1', '{"doors":false,"model":-246927995,"coords":{"x":-379.2972412109375,"y":6108.32275390625,"z":31.69684982299804},"heading":225,"state":1,"maxDistance":2}'),
(303, 'Paleto Bay Fire Department 1-2', '{"doors":false,"model":-246927995,"coords":{"x":-376.8049621582031,"y":6110.900390625,"z":31.7124080657959},"heading":225,"state":1,"maxDistance":2}'),
(304, 'Paleto Bay Fire Department 1-3', '{"doors":false,"model":964838196,"coords":{"x":-375.1997375488281,"y":6113.0830078125,"z":31.59394454956054},"heading":315,"state":1,"maxDistance":2}'),
(305, 'Paleto Bay Fire Department 1-4', '{"doors":false,"model":-246927995,"coords":{"x":-375.0607604980469,"y":6120.1142578125,"z":31.69972229003906},"heading":315,"state":1,"maxDistance":2}'),
(306, 'Paleto Bay Fire Department 1-5', '{"doors":false,"model":-246927995,"coords":{"x":-359.1754150390625,"y":6116.6552734375,"z":31.71304130554199},"heading":315,"state":1,"maxDistance":2}'),
(307, 'Paleto Bay Fire Department 1-6', '{"doors":false,"model":-246927995,"coords":{"x":-365.7249755859375,"y":6115.06787109375,"z":31.70168113708496},"heading":225,"state":1,"maxDistance":2}'),
(308, 'Paleto Bay Fire Department 1-7', '{"doors":false,"model":-246927995,"coords":{"x":-367.2385559082031,"y":6124.953125,"z":31.72744941711425},"heading":315,"state":1,"maxDistance":2}'),
(309, 'Paleto Bay Fire Department 1-8', '{"doors":false,"model":823116083,"coords":{"x":-368.6300354003906,"y":6120.20556640625,"z":31.70638656616211},"heading":315,"state":1,"maxDistance":2}'),
(310, 'Paleto Bay Fire Department 1-9', '{"doors":false,"model":823116083,"coords":{"x":-367.34735107421877,"y":6118.9228515625,"z":31.70638656616211},"heading":315,"state":1,"maxDistance":2}'),
(311, 'Paleto Bay Fire Department 1-10', '{"doors":false,"model":-246927995,"coords":{"x":-370.9203796386719,"y":6109.86669921875,"z":31.70896911621093},"heading":225,"state":1,"maxDistance":2}'),
(312, 'Paleto Bay Fire Department 1-11', '{"doors":false,"model":-246927995,"coords":{"x":-373.6807556152344,"y":6107.10302734375,"z":31.70515632629394},"heading":225,"state":1,"maxDistance":2}'),
(313, 'Paleto Bay Fire Department 1-12', '{"doors":false,"model":-246927995,"coords":{"x":-375.8838195800781,"y":6104.90869140625,"z":31.70618438720703},"heading":225,"state":1,"maxDistance":2}'),
(314, 'Paleto Bay Fire Department 0-1', '{"doors":false,"model":-246927995,"coords":{"x":-367.2890319824219,"y":6117.1552734375,"z":27.95434761047363},"heading":45,"state":1,"maxDistance":2}'),
(315, 'Paleto Bay Fire Department 0-2', '{"doors":false,"model":-246927995,"coords":{"x":-366.56317138671877,"y":6121.0107421875,"z":27.95622253417968},"heading":45,"state":1,"maxDistance":2}'),
(316, 'Paleto Bay Fire Department 0-3', '{"doors":false,"model":-246927995,"coords":{"x":-362.5422668457031,"y":6121.90478515625,"z":27.94985580444336},"heading":45,"state":1,"maxDistance":2}');
```

***

### 🚀 **Installation Guide**

Follow these steps to install the Paleto Fire Department map on your FiveM server:

1. **Download the Map Resource**
   * Ensure the **`paleto_bay_fire_station`** resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start paleto_bay_fire_station
       ```
3. **Set Up Doorlocks**
   * Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**
   * Restart your server and visit the map location at **-381.10, 6120.57, 31.47** to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Paleto Fire Department** on your FiveM server! 🚀
