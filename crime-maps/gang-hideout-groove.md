# 🥷 Gang Hideout Groove

{% embed url="https://fivem.prompt-mods.com/package/5454131" %}

{% embed url="https://youtu.be/q5gm8F2apKQ" %}

The **Gang Hideout Groove** is a gritty and immersive map designed for FiveM servers. Located in the Groove Street neighborhood of Los Santos, this map provides a realistic environment for roleplay scenarios, complete with seating areas, a TV, a pool table, and a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Gang Hideout Groove** is located at the following coordinates:

* **Position**: `110.43, -1955.01, 20.74`

***

### 🪑 Chairs

The map includes a variety of chairs and sofas for added realism. Below are the chair models used in the map:

* `p_lestersbed_s`
* `v_ret_fh_chair01`
* `prop_ld_toilet_01`
* `v_res_j_sofa`
* `apa_mp_h_stn_chairarm_02`
* `prop_off_chair_04`
* `prop_bench_11`
* `prop_chair_07`
* `prop_skid_chair_03`
* `prop_torture_ch_01`

***

### 🎱 Pool Table

The map features a pool table for added interactivity. Below is the pool table model used in the map:

* **Model**: `prop_pooltable_02`
* **Position**: `-0.7917962, -0.68156, -1.801092`

**Note**: The pool table is not compatible with balls or cues by default. Additional scripting may be required for full functionality.

***

### 📺 TV

The map features a TV to enhance the environment. The following TV model is used:

* `v_ret_gc_tv`

***

### 🚪 Doorlock System

The **Gang Hideout Groove** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(634, 'Gang Hideout / Groove E-1', '{"maxDistance":2,"model":1956494919,"coords":{"x":115.04419708251953,"y":-1961.4080810546876,"z":21.46610260009765},"heading":21,"state":1,"doors":false}'),
(635, 'Gang Hideout / Groove 1-1', '{"maxDistance":2,"model":1575804630,"coords":{"x":116.25086975097656,"y":-1963.7001953125,"z":21.46792602539062},"heading":291,"state":1,"doors":false}'),
(636, 'Gang Hideout / Groove 1-2', '{"maxDistance":2,"model":-5479653,"coords":{"x":117.04507446289063,"y":-1965.848876953125,"z":21.40908622741699},"heading":111,"state":1,"doors":false}'),
(637, 'Gang Hideout / Groove 1-3', '{"maxDistance":2,"model":456661554,"coords":{"x":119.10846710205078,"y":-1971.2080078125,"z":21.41182518005371},"heading":111,"state":1,"doors":false}'),
(638, 'Gang Hideout / Groove E-2', '{"maxDistance":2,"coords":{"x":118.13166809082031,"y":-1973.97900390625,"z":21.47210693359375},"state":1,"doors":[{"model":1504256620,"coords":{"x":119.1586685180664,"y":-1973.5865478515626,"z":21.47307777404785},"heading":201},{"model":262671971,"coords":{"x":117.10466766357422,"y":-1974.3714599609376,"z":21.47113800048828},"heading":21}]}'),
(639, 'Gang Hideout / Groove 1-4', '{"maxDistance":2,"model":-5479653,"coords":{"x":116.66157531738281,"y":-1969.542236328125,"z":21.40915298461914},"heading":291,"state":1,"doors":false}'),
(640, 'Gang Hideout / Groove E-3', '{"maxDistance":2,"model":1956494919,"coords":{"x":112.80323028564453,"y":-1973.874755859375,"z":21.46607208251953},"heading":201,"state":1,"doors":false}'),
(641, 'Gang Hideout / Groove E-4', '{"maxDistance":2,"model":-1987474252,"coords":{"x":111.46031951904297,"y":-1979.27978515625,"z":20.01158332824707},"heading":111,"state":1,"doors":false}'),
(642, 'Gang Hideout / Groove E-5', '{"maxDistance":2,"model":-1987474252,"coords":{"x":104.68203735351563,"y":-1977.2952880859376,"z":20.01325416564941},"heading":22,"state":1,"doors":false}'),
(643, 'Gang Hideout / Groove E-6', '{"maxDistance":2,"coords":{"x":94.7374038696289,"y":-1985.291015625,"z":19.46135711669922},"state":1,"doors":[{"model":-1987474252,"coords":{"x":93.99517822265625,"y":-1984.4793701171876,"z":19.46128845214843},"heading":312},{"model":-1987474252,"coords":{"x":95.47962951660156,"y":-1986.102783203125,"z":19.46142578125},"heading":132}]}'),
(644, 'Gang Hideout / Groove E-6', '{"maxDistance":2,"model":-1987474252,"coords":{"x":105.79612731933594,"y":-1964.9716796875,"z":19.89338493347168},"heading":85,"state":1,"doors":false}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Gang Hideout Groove** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_gang_hideout_groove` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    plaintextCopy

    ```
    start cfx_prompt_gang_hideout_groove
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `110.43, -1955.01, 20.74` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Gang Hideout Groove** on your FiveM server! 🚀
