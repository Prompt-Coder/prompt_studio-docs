# 🚚 Truck You Repairs

{% embed url="https://fivem.prompt-mods.com/package/5862517" %}

{% embed url="https://youtu.be/nSrBNDIMKGg" %}

The **Truck You Repairs** map is a detailed and immersive repair shop environment designed for FiveM servers. It includes multiple locations across Los Santos, Paleto Bay, and Sandy Shores, complete with interactive elements like TVs, chairs, and a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

#### There are 2 version of this map you will get after the purchase.

* **Prompt's Mods - Truck\_you\_Repairs** (you cannot change the logo because it's 3d here. Use this if you want to keep the logo as is)
* **Prompt's Mods - Custom\_Truck\_you\_Repairs** (use this version in order to be able to put any logo you want by changing the .ytd file)

***

### 🗺️ Map Locations

The **Truck You Repairs** map is available at the following coordinates:

* **Los Santos**: `939.64, -1024.79, 40.83`
* **Paleto Bay**: `-634.01, 5701.94, 36.88`
* **Sandy Shores**: `2684.43, 3373.65, 57.20`



Locations can be removed by simple deleting the folder with the location name inside the stream folder of the resource.

***

### 🪑 Chairs

The map includes chairs for added realism. Below are the chair models used in the map:

* `prop_couch_lg_05`
* `v_med_p_deskchair`
* `v_med_cor_medstool`
* `v_res_j_dinechair`

***

### 📺 TVs

The map features TVs to enhance the environment. The following TV models are used:

* `prop_tv_flat_michael`
* `prop_tv_cabinet_03`

***

### ⛽ Gas

The map includes gas-related props for added detail:

* `prop_gas_airunit01`

***

### 🚪 Doorlock System

The **Truck You Repairs** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(573, 'DOT Repairs / Truck Repairs 1-1-1', '{"doors":[{"heading":0,"model":964838196,"coords":{"x":938.6293334960938,"y":-1017.1438598632813,"z":42.28619384765625}},{"heading":180,"model":964838196,"coords":{"x":936.02880859375,"y":-1017.1438598632813,"z":42.28619384765625}}],"maxDistance":2,"coords":{"x":937.3291015625,"y":-1017.1438598632813,"z":42.28619384765625},"state":1}'),
(574, 'DOT Repairs / Truck Repairs 1-1-2', '{"doors":false,"maxDistance":2,"heading":90,"coords":{"x":939.5059814453125,"y":-1013.5996704101563,"z":42.28765487670898},"model":-952356348,"state":1}'),
(575, 'DOT Repairs / Truck Repairs 1-E-1', '{"doors":[{"heading":180,"model":-1212951353,"coords":{"x":936.0236206054688,"y":-1011.4185791015625,"z":42.2885513305664}},{"heading":0,"model":-1212951353,"coords":{"x":938.623779296875,"y":-1011.4185791015625,"z":42.2885513305664}}],"maxDistance":2,"coords":{"x":937.32373046875,"y":-1011.4185791015625,"z":42.2885513305664},"state":1}'),
(576, 'DOT Repairs / Truck Repairs 1-1-3', '{"doors":[{"heading":90,"model":964838196,"coords":{"x":926.1654663085938,"y":-1020.9387817382813,"z":40.98083114624023}},{"heading":270,"model":964838196,"coords":{"x":926.1654663085938,"y":-1023.5384521484375,"z":40.98083114624023}}],"maxDistance":2,"coords":{"x":926.1654663085938,"y":-1022.2386474609375,"z":40.98083114624023},"state":1}'),
(577, 'DOT Repairs / Truck Repairs 1-1-4', '{"doors":[{"heading":90,"model":964838196,"coords":{"x":922.7977905273438,"y":-1030.461181640625,"z":40.98283004760742}},{"heading":270,"model":964838196,"coords":{"x":922.7977905273438,"y":-1033.062744140625,"z":40.98283004760742}}],"maxDistance":2,"coords":{"x":922.7977905273438,"y":-1031.761962890625,"z":40.98283004760742},"state":1}'),
(578, 'DOT Repairs / Truck Repairs 1-G-1', '{"doors":false,"maxDistance":2,"heading":90,"coords":{"x":962.6578979492188,"y":-1014.1070556640625,"z":42.11402893066406},"model":140742819,"state":1}'),
(579, 'DOT Repairs / Truck Repairs 1-G-2', '{"doors":false,"maxDistance":2,"heading":90,"coords":{"x":962.6578979492188,"y":-1019.7545166015625,"z":42.11402893066406},"model":140742819,"state":1}'),
(580, 'DOT Repairs / Truck Repairs 1-G-3', '{"doors":false,"maxDistance":2,"heading":90,"coords":{"x":962.6578979492188,"y":-1025.4339599609376,"z":42.11402893066406},"model":140742819,"state":1}'),
(581, 'DOT Repairs / Truck Repairs 1-G-4', '{"doors":false,"maxDistance":2,"heading":90,"coords":{"x":962.6578979492188,"y":-1031.1181640625,"z":42.11402893066406},"model":140742819,"state":1}'),
(582, 'DOT Repairs / Truck Repairs 2-E-1', '{"doors":[{"heading":247,"model":-1212951353,"coords":{"x":2670.194580078125,"y":3376.906005859375,"z":58.662353515625}},{"heading":67,"model":-1212951353,"coords":{"x":2671.210693359375,"y":3379.29931640625,"z":58.662353515625}}],"maxDistance":2,"coords":{"x":2670.70263671875,"y":3378.1025390625,"z":58.662353515625},"state":1}'),
(583, 'DOT Repairs / Truck Repairs 2-1-1', '{"doors":[{"heading":67,"model":964838196,"coords":{"x":2676.483154296875,"y":3377.0673828125,"z":58.65999603271484}},{"heading":247,"model":964838196,"coords":{"x":2675.467041015625,"y":3374.673583984375,"z":58.65999603271484}}],"maxDistance":2,"coords":{"x":2675.97509765625,"y":3375.87060546875,"z":58.65999603271484},"state":1}'),
(584, 'DOT Repairs / Truck Repairs 2-1-2', '{"doors":false,"maxDistance":2,"heading":157,"coords":{"x":2673.563232421875,"y":3379.25927734375,"z":58.66145706176758},"model":-952356348,"state":1}'),
(585, 'DOT Repairs / Truck Repairs 2-1-3', '{"doors":[{"heading":157,"model":964838196,"coords":{"x":2675.106201171875,"y":3364.111572265625,"z":57.35463333129883}},{"heading":337,"model":964838196,"coords":{"x":2677.499267578125,"y":3363.095947265625,"z":57.35463333129883}}],"maxDistance":2,"coords":{"x":2676.302734375,"y":3363.603759765625,"z":57.35463333129883},"state":1}'),
(586, 'DOT Repairs / Truck Repairs 2-1-4', '{"doors":[{"heading":157,"model":964838196,"coords":{"x":2682.5556640625,"y":3357.290771484375,"z":57.35663223266601}},{"heading":337,"model":964838196,"coords":{"x":2684.950439453125,"y":3356.2744140625,"z":57.35663223266601}}],"maxDistance":2,"coords":{"x":2683.7529296875,"y":3356.78271484375,"z":57.35663223266601},"state":1}'),
(587, 'DOT Repairs / Truck Repairs 2-G-1', '{"doors":false,"maxDistance":2,"heading":157,"coords":{"x":2683.076416015625,"y":3400.372314453125,"z":58.48783111572265},"model":140742819,"state":1}'),
(588, 'DOT Repairs / Truck Repairs 2-G-2', '{"doors":false,"maxDistance":2,"heading":157,"coords":{"x":2688.27490234375,"y":3398.165771484375,"z":58.48783111572265},"model":140742819,"state":1}'),
(589, 'DOT Repairs / Truck Repairs 2-G-3', '{"doors":false,"maxDistance":2,"heading":157,"coords":{"x":2693.5029296875,"y":3395.946533203125,"z":58.48783111572265},"model":140742819,"state":1}'),
(590, 'DOT Repairs / Truck Repairs 2-G-4', '{"doors":false,"maxDistance":2,"heading":157,"coords":{"x":2698.735107421875,"y":3393.7255859375,"z":58.48783111572265},"model":140742819,"state":1}'),
(591, 'DOT Repairs / Truck Repairs 3-E-1', '{"doors":[{"heading":154,"model":-1212951353,"coords":{"x":-629.8409423828125,"y":5715.79638671875,"z":38.34554290771484}},{"heading":334,"model":-1212951353,"coords":{"x":-627.50390625,"y":5714.65673828125,"z":38.34554290771484}}],"maxDistance":2,"coords":{"x":-628.6724243164063,"y":5715.2265625,"z":38.34554290771484},"state":1}'),
(592, 'DOT Repairs / Truck Repairs 3-1-1', '{"doors":[{"heading":334,"model":964838196,"coords":{"x":-630.0086669921875,"y":5709.50830078125,"z":38.34318542480469}},{"heading":154,"model":964838196,"coords":{"x":-632.3460693359375,"y":5710.6484375,"z":38.34318542480469}}],"maxDistance":2,"coords":{"x":-631.1773681640625,"y":5710.078125,"z":38.34318542480469},"state":1}'),
(593, 'DOT Repairs / Truck Repairs 3-1-2', '{"doors":false,"maxDistance":2,"heading":64,"coords":{"x":-627.6671142578125,"y":5712.3095703125,"z":38.34464645385742},"model":-952356348,"state":1}'),
(594, 'DOT Repairs / Truck Repairs 3-1-3', '{"doors":[{"heading":64,"model":964838196,"coords":{"x":-642.874755859375,"y":5711.5615234375,"z":37.03782272338867}},{"heading":244,"model":964838196,"coords":{"x":-644.0143432617188,"y":5709.224609375,"z":37.03782272338867}}],"maxDistance":2,"coords":{"x":-643.444580078125,"y":5710.39306640625,"z":37.03782272338867},"state":1}'),
(595, 'DOT Repairs / Truck Repairs 3-1-4', '{"doors":[{"heading":64,"model":964838196,"coords":{"x":-650.075927734375,"y":5704.478515625,"z":37.03982162475586}},{"heading":244,"model":964838196,"coords":{"x":-651.2163696289063,"y":5702.140625,"z":37.03982162475586}}],"maxDistance":2,"coords":{"x":-650.6461181640625,"y":5703.3095703125,"z":37.03982162475586},"state":1}'),
(596, 'DOT Repairs / Truck Repairs 3-G-1', '{"doors":false,"maxDistance":2,"heading":64,"coords":{"x":-607.0807495117188,"y":5701.7041015625,"z":38.1710205078125},"model":140742819,"state":1}'),
(597, 'DOT Repairs / Truck Repairs 3-G-2', '{"doors":false,"maxDistance":2,"heading":64,"coords":{"x":-609.5564575195313,"y":5696.62841796875,"z":38.1710205078125},"model":140742819,"state":1}'),
(598, 'DOT Repairs / Truck Repairs 3-G-3', '{"doors":false,"maxDistance":2,"heading":64,"coords":{"x":-612.046142578125,"y":5691.5234375,"z":38.1710205078125},"model":140742819,"state":1}'),
(599, 'DOT Repairs / Truck Repairs 3-G-4', '{"doors":false,"maxDistance":2,"heading":64,"coords":{"x":-614.5379638671875,"y":5686.41455078125,"z":38.1710205078125},"model":140742819,"state":1}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Truck You Repairs** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_custom_Truck_Repairs` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_custom_Truck_Repairs
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit one of the map locations (e.g., Los Santos: `939.64, -1024.79, 40.83`) to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Truck You Repairs** map on your FiveM server! 🚀
