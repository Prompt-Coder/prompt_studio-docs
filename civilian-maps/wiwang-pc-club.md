# 💻 Wiwang PC Club

{% embed url="https://fivem.prompt-mods.com/package/4609356" %}

{% embed url="https://youtu.be/IRlw3RjuVvk" %}

The **Wiwang PC Club** is a highly detailed and immersive PC gaming lounge designed for FiveM servers. Located in Los Santos, this map features a variety of chairs, TVs, and a customizable doorlock system to enhance the gaming experience. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Wiwang PC Club** is located at the following coordinates:

* **Position**: `-828.66, -734.19, 28.05`

***

### 🪑 Chairs

The map includes a variety of chairs for added realism. Below are the chair models used in the map:

* `xm_lab_sofa_02`
* `apa_mp_h_stn_chairstrip_07`
* `bkr_prop_clubhouse_armchair_01a`
* `xm_lab_chairarm_26`
* `v_corp_facebeanbagd`
* `prop_toilet_02`
* `gr_prop_highendchair_gr_01a`
* `hei_prop_heist_off_chair`
* `apa_mp_h_stn_sofacorn_09`
* `ba_prop_int_glam_stool`
* `vw_prop_vw_offchair_02`

***

### 📺 TVs

The map features TVs to enhance the environment. The following TV models are used:

* `vw_prop_vw_cinema_tv_01`
* `xm_prop_x17_tv_ceiling_01`
* `ex_prop_ex_tv_flat_01`

***

### 🚪 Doorlock System

The **Wiwang PC Club** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Wiwang PC Club E-1', '{"maxDistance":2,"coords":{"x":-826.4222412109375,"y":-696.910888671875,"z":28.47396659851074},"state":1,"doors":[{"model":218840560,"coords":{"x":-826.4214477539063,"y":-698.0077514648438,"z":28.47396659851074},"heading":270},{"model":218840560,"coords":{"x":-826.4230346679688,"y":-695.81396484375,"z":28.47396659851074},"heading":90}]}'),
(DEFAULT, 'Wiwang PC Club E-2', '{"maxDistance":2,"coords":{"x":-826.4219970703125,"y":-699.8438720703125,"z":28.46998977661132},"state":1,"doors":[{"model":218840560,"coords":{"x":-826.4219970703125,"y":-700.941162109375,"z":28.46998977661132},"heading":270},{"model":218840560,"coords":{"x":-826.4219970703125,"y":-698.7466430664063,"z":28.46998977661132},"heading":90}]}'),
(DEFAULT, 'Wiwang PC Club E-3', '{"maxDistance":2,"coords":{"x":-826.406982421875,"y":-691.4998779296875,"z":28.4649600982666},"state":1,"doors":[{"model":218840560,"coords":{"x":-826.40576171875,"y":-692.5967407226563,"z":28.4649600982666},"heading":270},{"model":218840560,"coords":{"x":-826.408203125,"y":-690.4030151367188,"z":28.4649600982666},"heading":90}]}'),
(DEFAULT, 'Wiwang PC Club E-4', '{"maxDistance":2,"coords":{"x":-826.4144287109375,"y":-688.5641479492188,"z":28.47199630737304},"state":1,"doors":[{"model":218840560,"coords":{"x":-826.4137573242188,"y":-689.6616821289063,"z":28.47199630737304},"heading":270},{"model":218840560,"coords":{"x":-826.4151000976563,"y":-687.4666137695313,"z":28.47199630737304},"heading":90}]}'),
(DEFAULT, 'Wiwang PC Club E-5', '{"maxDistance":2,"coords":{"x":-810.063232421875,"y":-698.3272705078125,"z":28.47211074829101},"state":1,"doors":[{"model":218840560,"coords":{"x":-810.063232421875,"y":-697.230224609375,"z":28.47211074829101},"heading":90},{"model":218840560,"coords":{"x":-810.063232421875,"y":-699.4242553710938,"z":28.47211074829101},"heading":270}]}'),
(DEFAULT, 'Wiwang PC Club 1-1', '{"maxDistance":2,"model":-2611446,"coords":{"x":-822.1166381835938,"y":-704.763427734375,"z":27.10039901733398},"heading":180,"state":1,"doors":false}'),
(DEFAULT, 'Wiwang PC Club E-6', '{"maxDistance":2,"coords":{"x":-828.4703369140625,"y":-731.1858520507813,"z":28.48112869262695},"state":1,"doors":[{"model":218840560,"coords":{"x":-827.369384765625,"y":-731.1858520507813,"z":28.48112869262695},"heading":0},{"model":218840560,"coords":{"x":-829.5712280273438,"y":-731.1858520507813,"z":28.48112869262695},"heading":180}]}'),
(DEFAULT, 'Wiwang PC Club E-7', '{"maxDistance":2,"coords":{"x":-825.5386962890625,"y":-731.1972045898438,"z":28.47762870788574},"state":1,"doors":[{"model":218840560,"coords":{"x":-824.4431762695313,"y":-731.1972045898438,"z":28.47762870788574},"heading":0},{"model":218840560,"coords":{"x":-826.63427734375,"y":-731.1972045898438,"z":28.47762870788574},"heading":180}]}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Wiwang PC Club** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_pc_club` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_pc_club
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-828.66, -734.19, 28.05` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Wiwang PC Club** on your FiveM server! 🚀
