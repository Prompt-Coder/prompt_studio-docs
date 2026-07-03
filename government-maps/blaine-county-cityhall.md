# 🏢 Blaine County Cityhall

{% embed url="https://fivem.prompt-mods.com/package/5641745" %}

{% embed url="https://youtu.be/3DRLonOmmYk" %}

The **Blaine County City Hall** is a custom map designed for FiveM servers, offering a fully immersive government and administrative environment for roleplay, city management, and public service scenarios. This map features a detailed interior and exterior, complete with interactive props, seating arrangements, and a robust doorlock system for enhanced gameplay. Below, you’ll find all the necessary details to install and configure this map on your server.

***

### 📍 Map Location

The **Blaine County City Hall** is located at the following coordinates:\
**328.74, 6619.56, 28.61**

***

### 🛠️ Features

#### 🪑 Chairs and Props

The map includes a variety of chairs and props to create a realistic city hall environment. Below is a list of the chairs included:

* `sf_prop_sf_chair_stool_09a`
* `v_ret_chair_white`
* `p_yacht_chair_01_s`
* `v_ret_chair`
* `h4_prop_battle_club_chair_01`
* `hei_heist_stn_sofa2seat_06`
* `p_dinechair_01_s`
* `imp_prop_impexp_offchair_01a`
* `prop_sol_chair`
* `tr_int1_mod_sofa_009`
* `prop_bench_01c`
* `hei_heist_stn_chairarm_04`
* `apa_mp_h_stn_chairarm_09`
* `v_res_fa_chair01`
* `ba_prop_battle_club_chair_01`
* `apa_mp_h_yacht_sofa_02`
* `prompt_cityhall_court_chair`
* `prompt_cityhall_library_chair`
* `prop_toilet_02`
* `prompt_cityhall_court_seating`

***

#### 📺 TV

The map includes TVs for added realism:

* `xm_prop_x17_tv_flat_01`
* `prop_tv_flat_michael`

***

#### 🚪 Doorlock System

The **Blaine County City Hall** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(259, 'Blaine County City Hall E-1', '{"doors":[{"coords":{"x":346.807861328125,"y":6628.49462890625,"z":29.08551025390625},"model":1503255960,"heading":134},{"coords":{"x":345.4643249511719,"y":6629.8857421875,"z":29.08551025390625},"model":1503255960,"heading":314}],"coords":{"x":346.1361083984375,"y":6629.1904296875,"z":29.08551025390625},"state":1,"maxDistance":2}'),
(260, 'Blaine County City Hall E-2', '{"doors":[{"coords":{"x":357.399169921875,"y":6603.50732421875,"z":33.87639236450195},"model":1503255960,"heading":90},{"coords":{"x":357.399169921875,"y":6605.4462890625,"z":33.87639236450195},"model":1503255960,"heading":270}],"coords":{"x":357.399169921875,"y":6604.4765625,"z":33.87639236450195},"state":1,"maxDistance":2}'),
(261, 'Blaine County City Hall 1-1', '{"doors":[{"coords":{"x":353.5418395996094,"y":6626.822265625,"z":29.00247001647949},"model":-462932014,"heading":46},{"coords":{"x":355.3249816894531,"y":6628.6689453125,"z":29.00247001647949},"model":467392331,"heading":226}],"coords":{"x":354.43341064453127,"y":6627.74560546875,"z":29.00247001647949},"state":1,"maxDistance":2}'),
(262, 'Blaine County City Hall 1-2', '{"doors":[{"coords":{"x":340.56500244140627,"y":6645.72998046875,"z":29.0040111541748},"model":-462932014,"heading":270},{"coords":{"x":340.56500244140627,"y":6643.1611328125,"z":29.0040111541748},"model":467392331,"heading":90}],"coords":{"x":340.56500244140627,"y":6644.4453125,"z":29.0040111541748},"state":1,"maxDistance":2}'),
(263, 'Blaine County City Hall 1-3', '{"doors":false,"model":1697869588,"coords":{"x":344.6764831542969,"y":6650.044921875,"z":28.8560791015625},"heading":180,"state":1,"maxDistance":2}'),
(264, 'Blaine County City Hall 1-4', '{"doors":false,"model":1697869588,"coords":{"x":356.0912170410156,"y":6630.07470703125,"z":28.85216903686523},"heading":67,"state":1,"maxDistance":2}'),
(265, 'Blaine County City Hall 1-5', '{"doors":false,"model":1697869588,"coords":{"x":352.70452880859377,"y":6636.4267578125,"z":28.84871864318847},"heading":136,"state":1,"maxDistance":2}'),
(266, 'Blaine County City Hall 1-6', '{"doors":false,"model":1697869588,"coords":{"x":351.6114196777344,"y":6640.57568359375,"z":28.84848022460937},"heading":358,"state":1,"maxDistance":2}'),
(267, 'Blaine County City Hall 1-7', '{"doors":false,"model":1697869588,"coords":{"x":355.1504211425781,"y":6646.74072265625,"z":28.85601043701172},"heading":0,"state":1,"maxDistance":2}'),
(268, 'Blaine County City Hall 1-8', '{"doors":false,"model":1697869588,"coords":{"x":358.3002624511719,"y":6650.82666015625,"z":28.85614776611328},"heading":180,"state":1,"maxDistance":2}'),
(269, 'Blaine County City Hall 1-9', '{"doors":[{"coords":{"x":353.0509338378906,"y":6647.1875,"z":29.00420570373535},"model":-462932014,"heading":90},{"coords":{"x":353.0509338378906,"y":6649.75537109375,"z":29.00420570373535},"model":467392331,"heading":270}],"coords":{"x":353.0509338378906,"y":6648.4716796875,"z":29.00420570373535},"state":1,"maxDistance":2}'),
(270, 'Blaine County City Hall 1-10', '{"doors":[{"coords":{"x":359.5584716796875,"y":6619.63671875,"z":29.00368309020996},"model":467392331,"heading":180},{"coords":{"x":356.9895324707031,"y":6619.63671875,"z":29.00368309020996},"model":-462932014,"heading":0}],"coords":{"x":358.27398681640627,"y":6619.63671875,"z":29.00368309020996},"state":1,"maxDistance":2}'),
(271, 'Blaine County City Hall 1-11', '{"doors":[{"coords":{"x":370.0412292480469,"y":6623.5791015625,"z":29.00335121154785},"model":-462932014,"heading":180},{"coords":{"x":367.47210693359377,"y":6623.58251953125,"z":29.00335121154785},"model":467392331,"heading":0}],"coords":{"x":368.75665283203127,"y":6623.5810546875,"z":29.00335121154785},"state":1,"maxDistance":2}'),
(272, 'Blaine County City Hall 1-12', '{"doors":false,"model":1697869588,"coords":{"x":369.3527526855469,"y":6616.58447265625,"z":28.8460693359375},"heading":0,"state":1,"maxDistance":2}'),
(273, 'Blaine County City Hall 1-13', '{"doors":false,"model":1697869588,"coords":{"x":362.56829833984377,"y":6616.0673828125,"z":28.85303878784179},"heading":90,"state":1,"maxDistance":2}'),
(274, 'Blaine County City Hall 1-14', '{"doors":false,"model":1697869588,"coords":{"x":353.9618225097656,"y":6612.94091796875,"z":28.85210037231445},"heading":90,"state":1,"maxDistance":2}'),
(275, 'Blaine County City Hall 1-15', '{"doors":[{"coords":{"x":354.510986328125,"y":6607.85107421875,"z":29.00323486328125},"model":-462932014,"heading":0},{"coords":{"x":357.0801086425781,"y":6607.85107421875,"z":29.00323486328125},"model":467392331,"heading":180}],"coords":{"x":355.7955322265625,"y":6607.85107421875,"z":29.00323486328125},"state":1,"maxDistance":2}'),
(276, 'Blaine County City Hall 1-16', '{"doors":[{"coords":{"x":359.3512878417969,"y":6607.85107421875,"z":29.00323486328125},"model":-462932014,"heading":0},{"coords":{"x":361.92041015625,"y":6607.85107421875,"z":29.00323486328125},"model":467392331,"heading":180}],"coords":{"x":360.6358642578125,"y":6607.85107421875,"z":29.00323486328125},"state":1,"maxDistance":2}'),
(277, 'Blaine County City Hall 2-1', '{"doors":[{"coords":{"x":356.9852600097656,"y":6619.63720703125,"z":33.41431045532226},"model":-462932014,"heading":0},{"coords":{"x":359.5523681640625,"y":6619.63720703125,"z":33.41431045532226},"model":467392331,"heading":180}],"coords":{"x":358.268798828125,"y":6619.63720703125,"z":33.41431045532226},"state":1,"maxDistance":2}'),
(278, 'Blaine County City Hall 2-2', '{"doors":[{"coords":{"x":359.55670166015627,"y":6626.3916015625,"z":33.41536712646484},"model":-462932014,"heading":180},{"coords":{"x":356.9853820800781,"y":6626.3916015625,"z":33.41536712646484},"model":467392331,"heading":0}],"coords":{"x":358.27105712890627,"y":6626.3916015625,"z":33.41536712646484},"state":1,"maxDistance":2}'),
(279, 'Blaine County City Hall 2-3', '{"doors":[{"coords":{"x":364.3415222167969,"y":6621.7880859375,"z":33.41564559936523},"model":-462932014,"heading":90},{"coords":{"x":364.3415222167969,"y":6624.35693359375,"z":33.41564559936523},"model":467392331,"heading":270}],"coords":{"x":364.3415222167969,"y":6623.072265625,"z":33.41564559936523},"state":1,"maxDistance":2}'),
(280, 'Blaine County City Hall 2-4', '{"doors":false,"model":1697869588,"coords":{"x":353.9590759277344,"y":6612.9365234375,"z":33.25247192382812},"heading":90,"state":1,"maxDistance":2}'),
(281, 'Blaine County City Hall 2-5', '{"doors":false,"model":1697869588,"coords":{"x":362.5890808105469,"y":6613.12451171875,"z":33.26037979125976},"heading":90,"state":1,"maxDistance":2}'),
(282, 'Blaine County City Hall 2-6', '{"doors":false,"model":1697869588,"coords":{"x":364.4462890625,"y":6628.63037109375,"z":33.25836563110351},"heading":90,"state":1,"maxDistance":2}'),
(283, 'Blaine County City Hall 2-7', '{"doors":[{"coords":{"x":356.85003662109377,"y":6630.56787109375,"z":33.4148063659668},"model":467392331,"heading":270},{"coords":{"x":356.85003662109377,"y":6628.00244140625,"z":33.4148063659668},"model":-462932014,"heading":90}],"coords":{"x":356.85003662109377,"y":6629.28515625,"z":33.4148063659668},"state":1,"maxDistance":2}'),
(284, 'Blaine County City Hall 2-8', '{"doors":[{"coords":{"x":353.91912841796877,"y":6638.78369140625,"z":33.41851425170898},"model":-462932014,"heading":270},{"coords":{"x":353.91912841796877,"y":6636.21337890625,"z":33.41851425170898},"model":467392331,"heading":90}],"coords":{"x":353.91912841796877,"y":6637.49853515625,"z":33.41851425170898},"state":1,"maxDistance":2}'),
(285, 'Blaine County City Hall 2-9', '{"doors":[{"coords":{"x":356.65631103515627,"y":6640.6416015625,"z":33.41511154174805},"model":-462932014,"heading":180},{"coords":{"x":354.08636474609377,"y":6640.6416015625,"z":33.41511154174805},"model":467392331,"heading":360}],"coords":{"x":355.371337890625,"y":6640.6416015625,"z":33.41511154174805},"state":1,"maxDistance":2}'),
(286, 'Blaine County City Hall 2-10', '{"doors":false,"model":-538477509,"coords":{"x":352.093017578125,"y":6635.97509765625,"z":33.27661514282226},"heading":0,"state":1,"maxDistance":2}'),
(287, 'Blaine County City Hall 2-11', '{"doors":false,"model":-538477509,"coords":{"x":344.6212158203125,"y":6641.6220703125,"z":33.27661514282226},"heading":90,"state":1,"maxDistance":2}'),
(288, 'Blaine County City Hall 2-12', '{"doors":false,"model":1242124150,"coords":{"x":347.6073303222656,"y":6653.67919921875,"z":33.21811294555664},"heading":270,"state":1,"maxDistance":2}'),
(289, 'Blaine County City Hall 2-13', '{"doors":false,"model":1697869588,"coords":{"x":351.8662109375,"y":6652.94677734375,"z":33.2578239440918},"heading":90,"state":1,"maxDistance":2}'),
(290, 'Blaine County City Hall 2-14', '{"doors":false,"model":1697869588,"coords":{"x":350.4627380371094,"y":6649.8603515625,"z":33.2681655883789},"heading":0,"state":1,"maxDistance":2}'),
(291, 'Blaine County City Hall 2-15', '{"doors":[{"coords":{"x":350.6369323730469,"y":6645.9423828125,"z":33.41606140136719},"model":467392331,"heading":180},{"coords":{"x":348.0672912597656,"y":6645.9423828125,"z":33.41606140136719},"model":-462932014,"heading":0}],"coords":{"x":349.35211181640627,"y":6645.9423828125,"z":33.41606140136719},"state":1,"maxDistance":2}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Blaine County City Hall** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_blaine_county_city_hall` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start cfx_prompt_blaine_county_city_hall
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at **328.74, 6619.56, 28.61** to ensure everything is functioning correctly.

For further assistance, contact support. Enjoy using the **Blaine County City Hall** on your FiveM server! 🚀
