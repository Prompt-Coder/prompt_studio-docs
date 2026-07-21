# 🏢 NOOSE Department

{% embed url="https://fivem.prompt-mods.com/package/4350312" %}

{% embed url="https://youtu.be/DsVi64XbFmk" %}

The **NOOSE Department** is a custom map designed for FiveM servers, offering a fully immersive law enforcement and tactical operations environment for roleplay, emergency response, and high-stakes scenarios. This map features a detailed interior and exterior, complete with interactive props, seating arrangements, and a robust doorlock system for enhanced gameplay. Below, you’ll find all the necessary details to install and configure this map on your server.

***

### 📍 Map Location

The **NOOSE Department** is located at the following coordinates:\
**2485.98, -384.81, 93.73**

***

### 🛠️ Features

#### 🪑 Chairs and Props

The map includes a variety of chairs and props to create a realistic NOOSE headquarters environment. Below is a list of the chairs included:

* `prompt_bench`
* `prompt_chairs`
* `prompt_offchair`
* `prompt_prop_toilet_01`
* `apa_mp_h_yacht_strip_chair_01`
* `prop_off_chair_01`
* `prop_off_chair_04`
* `v_serv_ct_chair02`
* `v_ilev_p_easychair`
* `hei_heist_toilet03`
* `hei_heist_beds03`
* `xm_prop_x17_avengerchair_02`
* `prop_chair_04b`

***

#### 🚪 Doorlock System

The **NOOSE Department** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'NOOSE E-1', '{"coords":{"x":2559.614013671875,"y":-325.5557556152344,"z":94.1236343383789},"heading":180,"model":-43433986,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE E-2', '{"coords":{"x":2569.22119140625,"y":-325.56640625,"z":94.1236343383789},"heading":180,"model":-43433986,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE E-3', '{"coords":{"x":2491.8681640625,"y":-303.47833251953127,"z":91.99237823486328},"heading":0,"model":569833973,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE E-4', '{"coords":{"x":2485.088134765625,"y":-335.8421630859375,"z":91.98345184326172},"heading":180,"model":1185512375,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE E-5', '{"coords":{"x":2485.43701171875,"y":-432.71343994140627,"z":91.98345184326172},"heading":180,"model":1185512375,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE E-6', '{"coords":{"x":2494.07958984375,"y":-464.03363037109377,"z":93.93792724609375},"maxDistance":2,"state":1,"doors":[{"heading":45,"model":-43433986,"coords":{"x":2498.400634765625,"y":-459.546875,"z":93.93792724609375}},{"heading":225,"model":-43433986,"coords":{"x":2489.75830078125,"y":-468.5203552246094,"z":93.93792724609375}}]}'),
(DEFAULT, 'NOOSE E-7', '{"coords":{"x":2475.163330078125,"y":-384.12860107421877,"z":94.54077911376953},"maxDistance":2,"state":1,"doors":[{"heading":90,"model":90507927,"coords":{"x":2475.163330078125,"y":-382.9577941894531,"z":94.54077911376953}},{"heading":270,"model":90507927,"coords":{"x":2475.163330078125,"y":-385.2994079589844,"z":94.54077911376953}}]}'),
(DEFAULT, 'NOOSE E-8', '{"coords":{"x":2459.706298828125,"y":-371.46783447265627,"z":93.25444793701172},"maxDistance":2,"state":1,"doors":[{"heading":90,"model":-340230128,"coords":{"x":2459.706298828125,"y":-372.7655944824219,"z":93.25444793701172}},{"heading":270,"model":-340230128,"coords":{"x":2459.706298828125,"y":-370.1700744628906,"z":93.25444793701172}}]}'),
(DEFAULT, 'NOOSE E-9', '{"coords":{"x":2460.589599609375,"y":-384.1329040527344,"z":93.47164154052735},"maxDistance":2,"state":1,"doors":[{"heading":270,"model":90507927,"coords":{"x":2460.589599609375,"y":-385.3037109375,"z":93.47164154052735}},{"heading":90,"model":90507927,"coords":{"x":2460.589599609375,"y":-382.96209716796877,"z":93.47164154052735}}]}'),
(DEFAULT, 'NOOSE 1-1', '{"coords":{"x":2467.625244140625,"y":-390.55865478515627,"z":93.46343231201172},"heading":0,"model":-1249735563,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-2', '{"coords":{"x":2465.060546875,"y":-392.5187072753906,"z":93.47328186035156},"heading":270,"model":873979204,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-3', '{"coords":{"x":2471.470703125,"y":-392.5210266113281,"z":93.46107482910156},"heading":270,"model":-519068795,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-4', '{"coords":{"x":2467.626953125,"y":-395.5187683105469,"z":93.4790267944336},"heading":180,"model":-131296141,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-5', '{"coords":{"x":2470.62255859375,"y":-397.5276794433594,"z":93.46674346923828},"heading":90,"model":-2023754432,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-6', '{"coords":{"x":2468.981689453125,"y":-397.91058349609377,"z":93.46674346923828},"heading":0,"model":-2023754432,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-7', '{"coords":{"x":2463.776123046875,"y":-377.7229309082031,"z":93.46316528320313},"heading":0,"model":749848321,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-8', '{"coords":{"x":2462.052490234375,"y":-368.5664367675781,"z":93.46139526367188},"heading":180,"model":-1726331785,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-9', '{"coords":{"x":2466.395751953125,"y":-371.59259033203127,"z":93.4300537109375},"heading":270,"model":631614199,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-10', '{"coords":{"x":2469.129638671875,"y":-369.8166809082031,"z":93.45623016357422},"heading":0,"model":631614199,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-11', '{"coords":{"x":2469.965087890625,"y":-372.3875427246094,"z":93.4300537109375},"heading":270,"model":631614199,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-12', '{"coords":{"x":2471.81298828125,"y":-369.49261474609377,"z":93.45623016357422},"heading":0,"model":631614199,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 1-13', '{"coords":{"x":2473.397705078125,"y":-369.4039306640625,"z":93.45623016357422},"heading":180,"model":631614199,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 2-1', '{"coords":{"x":2474.382080078125,"y":-372.71868896484377,"z":97.6362533569336},"heading":270,"model":873979204,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 2-2', '{"coords":{"x":2471.77294921875,"y":-370.10498046875,"z":97.65463256835938},"heading":0,"model":-1119680854,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'NOOSE 2-3', '{"coords":{"x":2460.775146484375,"y":-370.2148742675781,"z":97.66027069091797},"heading":0,"model":-1119680854,"maxDistance":2,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **NOOSE Department** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_noose` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_noose
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at **2485.98, -384.81, 93.73** to ensure everything is functioning correctly.

For further assistance, contact support. Enjoy using the **NOOSE Department** on your FiveM server! 🚀
