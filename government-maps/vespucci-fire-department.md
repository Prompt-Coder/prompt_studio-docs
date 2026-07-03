# 🚒 Vespucci Fire Department

{% embed url="https://fivem.prompt-mods.com/package/6023276" %}

{% embed url="https://youtu.be/RfSvV4g_F5o?si=LPHKckE0L07Tq6JB" %}

The **Vespucci Fire Department** is a custom map designed for FiveM servers, offering a fully immersive fire station environment for roleplay, emergency response, and firefighting scenarios. This map features a detailed interior and exterior, complete with interactive props, seating arrangements, and a robust doorlock system for enhanced gameplay. Below, you’ll find all the necessary details to install and configure this map on your server.

***

### 📍 **Map Location**

The Vespucci Fire Department is located at the following coordinates:\
&#xNAN;**-1042.60, -1382.17, 6.34**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The map includes a variety of chairs and props to create a realistic fire station environment. Below is a list of the chairs included:

* `ba_prop_int_edgy_stool`
* `imp_prop_impexp_offchair_01a`
* `prop_off_chair_01`
* `prop_off_chair_05`
* `prop_table_02_chr`
* `prop_table_06_chr`
* `prop_bench_07`
* `p_clb_officechair_s`
* `xm_prop_x17_corp_offchair`
* `prop_wheelchair_01_s`
* `v_res_fh_barcchair`
* `xm_lab_sofa_02`
* `v_corp_lazychair`
* `bkr_prop_clubhouse_sofa_01a`
* `ex_prop_offchair_exec_03`
* `prop_patio_lounger1`
* `prompt_vfd_hub_bench`
* `prompt_vfd_hub_bench_shorty`

***

#### 🚪 **Doorlock System**

The Vespucci Fire Department map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(317, 'Vespucci Fire Department G-1', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1042.60302734375,"y":-1382.174560546875,"z":6.34271955490112},"model":2099529766}'),
(318, 'Vespucci Fire Department G-2', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1041.072998046875,"y":-1376.43505859375,"z":6.35107469558715},"model":2099529766}'),
(319, 'Vespucci Fire Department G-3', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1039.51416015625,"y":-1370.689453125,"z":6.34585952758789},"model":2099529766}'),
(320, 'Vespucci Fire Department G-4', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1037.9786376953126,"y":-1364.9696044921876,"z":6.34458971023559},"model":2099529766}'),
(321, 'Vespucci Fire Department G-5', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1036.0843505859376,"y":-1357.871337890625,"z":6.34455490112304},"model":2099529766}'),
(322, 'Vespucci Fire Department G-6', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1034.546630859375,"y":-1352.1510009765626,"z":6.34552764892578},"model":2099529766}'),
(323, 'Vespucci Fire Department G-7', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1033.02392578125,"y":-1346.4239501953126,"z":6.34038972854614},"model":2099529766}'),
(324, 'Vespucci Fire Department G-8', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1031.4998779296876,"y":-1340.68896484375,"z":6.3428726196289},"model":2099529766}'),
(325, 'Vespucci Fire Department E-1', '{"doors":[{"model":-446668741,"heading":255,"coords":{"x":-1047.3890380859376,"y":-1399.4742431640626,"z":5.36098861694335}},{"model":981961352,"heading":75,"coords":{"x":-1046.9969482421876,"y":-1397.6175537109376,"z":5.36098861694335}}],"state":1,"maxDistance":2,"coords":{"x":-1047.1929931640626,"y":-1398.5458984375,"z":5.36098861694335}}'),
(326, 'Vespucci Fire Department 1-1', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1030.3692626953126,"y":-1389.2620849609376,"z":5.1203646659851},"model":1768829057}'),
(327, 'Vespucci Fire Department 1-2', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1040.64892578125,"y":-1386.4697265625,"z":5.12314558029174},"model":2123924634}'),
(328, 'Vespucci Fire Department 1-3', '{"doors":false,"state":1,"maxDistance":2,"heading":115,"coords":{"x":-1035.1334228515626,"y":-1393.7008056640626,"z":5.13264846801757},"model":1768829057}'),
(329, 'Vespucci Fire Department 1-4', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1034.353759765625,"y":-1399.0274658203126,"z":5.11662244796752},"model":1082476365}'),
(330, 'Vespucci Fire Department 1-5', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1028.3604736328126,"y":-1407.545166015625,"z":5.11692762374877},"model":1082476365}'),
(331, 'Vespucci Fire Department 1-6', '{"doors":false,"state":1,"maxDistance":2,"heading":165,"coords":{"x":-1033.369384765625,"y":-1410.505859375,"z":5.11659240722656},"model":1082476365}'),
(332, 'Vespucci Fire Department 1-7', '{"doors":[{"model":1082476365,"heading":345,"coords":{"x":-1041.158447265625,"y":-1394.639892578125,"z":5.11992645263671}},{"model":-122095133,"heading":165,"coords":{"x":-1043.607421875,"y":-1393.9837646484376,"z":5.11992645263671}}],"state":1,"maxDistance":2,"coords":{"x":-1042.3829345703126,"y":-1394.311767578125,"z":5.11992645263671}}'),
(333, 'Vespucci Fire Department 1-8', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1036.6185302734376,"y":-1403.6026611328126,"z":5.2386474609375},"model":1082476365}'),
(334, 'Vespucci Fire Department 1-9', '{"doors":[{"model":70673596,"heading":345,"coords":{"x":-1038.98046875,"y":-1404.679931640625,"z":5.22185468673706}},{"model":2120988497,"heading":165,"coords":{"x":-1041.427001953125,"y":-1404.019287109375,"z":5.22355270385742}}],"state":1,"maxDistance":2,"coords":{"x":-1040.2037353515626,"y":-1404.349609375,"z":5.22270393371582}}'),
(335, 'Vespucci Fire Department 1-10', '{"doors":false,"state":1,"maxDistance":2,"heading":75,"coords":{"x":-1042.806396484375,"y":-1406.3590087890626,"z":5.11878156661987},"model":1082476365}'),
(336, 'Vespucci Fire Department 1-11', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1040.601806640625,"y":-1414.87548828125,"z":5.12189865112304},"model":1082476365}'),
(337, 'Vespucci Fire Department 1-12', '{"doors":[{"model":-1821777087,"heading":165,"coords":{"x":-1045.8787841796876,"y":-1421.2117919921876,"z":5.13346481323242}},{"model":-1821777087,"heading":345,"coords":{"x":-1043.3680419921876,"y":-1421.884521484375,"z":5.13346481323242}}],"state":1,"maxDistance":2,"coords":{"x":-1044.6234130859376,"y":-1421.548095703125,"z":5.13346481323242}}'),
(338, 'Vespucci Fire Department 1-13', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1048.5880126953126,"y":-1425.60546875,"z":5.12553453445434},"model":70673596}'),
(339, 'Vespucci Fire Department 1-14', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1049.685302734375,"y":-1429.6177978515626,"z":5.12297487258911},"model":70673596}'),
(340, 'Vespucci Fire Department 1-15', '{"doors":false,"state":1,"maxDistance":2,"heading":120,"coords":{"x":-1050.38818359375,"y":-1432.7462158203126,"z":5.12207078933715},"model":70673596}'),
(341, 'Vespucci Fire Department 1-16', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1046.2830810546876,"y":-1434.914306640625,"z":5.12403440475463},"model":70673596}'),
(342, 'Vespucci Fire Department 1-17', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1043.44189453125,"y":-1435.675537109375,"z":5.12403440475463},"model":70673596}'),
(343, 'Vespucci Fire Department 1-18', '{"doors":false,"state":1,"maxDistance":2,"heading":30,"coords":{"x":-1039.8148193359376,"y":-1435.5919189453126,"z":5.11739349365234},"model":70673596}'),
(344, 'Vespucci Fire Department 1-19', '{"doors":false,"state":1,"maxDistance":2,"heading":75,"coords":{"x":-1038.553955078125,"y":-1431.39013671875,"z":5.1212887763977},"model":70673596}'),
(345, 'Vespucci Fire Department 1-20', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1037.87109375,"y":-1428.840087890625,"z":5.11952257156372},"model":70673596}'),
(346, 'Vespucci Fire Department 1-21', '{"doors":false,"state":1,"maxDistance":2,"heading":300,"coords":{"x":-1036.9476318359376,"y":-1424.96826171875,"z":5.11579179763793},"model":70673596}'),
(347, 'Vespucci Fire Department 1-22', '{"doors":false,"state":1,"maxDistance":2,"heading":75,"coords":{"x":-1037.4990234375,"y":-1421.76513671875,"z":5.11902284622192},"model":749848321}'),
(348, 'Vespucci Fire Department 1-23', '{"doors":false,"state":1,"maxDistance":2,"heading":165,"coords":{"x":-1035.0880126953126,"y":-1416.9979248046876,"z":5.11657762527465},"model":-1821777087}'),
(349, 'Vespucci Fire Department 1-24', '{"doors":false,"state":1,"maxDistance":2,"heading":75,"coords":{"x":-1032.43359375,"y":-1414.088623046875,"z":5.11580276489257},"model":70673596}'),
(350, 'Vespucci Fire Department 0-1', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1032.6435546875,"y":-1413.4180908203126,"z":2.05276441574096},"model":1082476365}'),
(351, 'Vespucci Fire Department E-2', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1047.44091796875,"y":-1430.358642578125,"z":10.6980504989624},"model":1082476365}'),
(352, 'Vespucci Fire Department 2-1', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1046.01318359375,"y":-1429.6475830078126,"z":10.64230346679687},"model":-610054759}'),
(353, 'Vespucci Fire Department 2-2', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1044.9951171875,"y":-1425.9014892578126,"z":10.64102935791015},"model":-610054759}'),
(354, 'Vespucci Fire Department 2-3', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1044.0296630859376,"y":-1422.085693359375,"z":10.63891220092773},"model":-610054759}'),
(355, 'Vespucci Fire Department 2-4', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1042.9805908203126,"y":-1418.3731689453126,"z":10.64637756347656},"model":-610054759}'),
(356, 'Vespucci Fire Department 2-5', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1041.990966796875,"y":-1414.5999755859376,"z":10.6425666809082},"model":-610054759}'),
(357, 'Vespucci Fire Department 2-6', '{"doors":false,"state":1,"maxDistance":2,"heading":255,"coords":{"x":-1040.9700927734376,"y":-1410.8197021484376,"z":10.63846969604492},"model":-610054759}'),
(358, 'Vespucci Fire Department 2-7', '{"doors":false,"state":1,"maxDistance":2,"heading":165,"coords":{"x":-1042.5806884765626,"y":-1407.4185791015626,"z":10.70503997802734},"model":70673596}'),
(359, 'Vespucci Fire Department 2-8', '{"doors":false,"state":1,"maxDistance":2,"heading":75,"coords":{"x":-1039.4261474609376,"y":-1399.9044189453126,"z":11.37910842895507},"model":1082476365}'),
(360, 'Vespucci Fire Department 2-9', '{"doors":false,"state":1,"maxDistance":2,"heading":165,"coords":{"x":-1031.754150390625,"y":-1388.864501953125,"z":11.37970352172851},"model":1082476365}'),
(361, 'Vespucci Fire Department 2-10', '{"doors":[{"model":-325753126,"heading":255,"coords":{"x":-1033.4110107421876,"y":-1390.677001953125,"z":11.52967071533203}},{"model":-325753126,"heading":75,"coords":{"x":-1032.9375,"y":-1388.9097900390626,"z":11.52967071533203}}],"state":1,"maxDistance":2,"coords":{"x":-1033.17431640625,"y":-1389.79345703125,"z":11.52967071533203}}'),
(362, 'Vespucci Fire Department 2-11', '{"doors":[{"model":-325753126,"heading":255,"coords":{"x":-1035.00390625,"y":-1396.6219482421876,"z":11.52967071533203}},{"model":-325753126,"heading":75,"coords":{"x":-1034.5299072265626,"y":-1394.852783203125,"z":11.52967071533203}}],"state":1,"maxDistance":2,"coords":{"x":-1034.766845703125,"y":-1395.7373046875,"z":11.52967071533203}}'),
(363, 'Vespucci Fire Department 2-12', '{"doors":false,"state":1,"maxDistance":2,"heading":345,"coords":{"x":-1035.755615234375,"y":-1396.7874755859376,"z":11.38071060180664},"model":1082476365}'),
(364, 'Vespucci Fire Department E-3', '{"doors":[{"model":-446668741,"heading":75,"coords":{"x":-1027.6297607421876,"y":-1408.9068603515626,"z":5.23744964599609}},{"model":981961352,"heading":255,"coords":{"x":-1028.028564453125,"y":-1410.763916015625,"z":5.23744964599609}}],"state":1,"maxDistance":2,"coords":{"x":-1027.8291015625,"y":-1409.83544921875,"z":5.23744964599609}}');
```

***

### 🚀 **Installation Guide**

Follow these steps to install the Vespucci Fire Department map on your FiveM server:

1. **Download the Map Resource**
   * Ensure the `cfx_vfd` resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start cfx_vfd
       ```
3. **Set Up Doorlocks**
   * Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**
   * Restart your server and visit the map location at **-1042.60, -1382.17, 6.34** to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using Sandy Fire Department on your FiveM server! 🚀
