# 🎭 Abandoned Theater

The **Abandoned Theater** is a detailed and atmospheric map designed for FiveM servers. Located in Los Santos, this map provides a unique environment for roleplay scenarios, complete with seating areas, a customizable doorlock system, and a variety of props to enhance immersion. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Abandoned Theater** is located at the following coordinates:

* **Position**: `459.38, -1452.86, 29.22`

***

### 🪑 Chairs

The map includes a variety of chairs and sofas for added realism. Below are the chair models used in the map:

* `v_res_tre_sofa_mess_a`
* `v_club_ch_briefchair`
* `v_corp_offchairfd`
* `prop_gc_chair02`
* `prop_clown_chair`
* `v_med_p_sofa`
* `ch_chint02_flat_toilet`
* `prop_bar_stool_01`
* `v_ret_fh_chair01`
* `prop_rub_couch01`
* `prop_rub_couch04`
* `prop_chair_06`
* `v_club_ch_briefchair`
* `v_res_j_sofa`
* `prop_rub_matress_03`

***

### 🚪 Doorlock System

The **Abandoned Theater** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Abandoned Theater E-1', '{"doors":[{"heading":15,"model":-1467927765,"coords":{"x":459.524658203125,"y":-1458.4884033203126,"z":29.37477874755859}},{"heading":195,"model":515013440,"coords":{"x":461.4029846191406,"y":-1457.966796875,"z":29.37696075439453}}],"maxDistance":2,"coords":{"x":460.46380615234377,"y":-1458.2275390625,"z":29.37586975097656},"state":1}'),
(DEFAULT, 'Abandoned Theater E-2', '{"doors":[{"heading":15,"model":-1467927765,"coords":{"x":461.4469909667969,"y":-1457.9501953125,"z":29.37477874755859}},{"heading":195,"model":515013440,"coords":{"x":463.3295593261719,"y":-1457.4351806640626,"z":29.37696075439453}}],"maxDistance":2,"coords":{"x":462.3882751464844,"y":-1457.692626953125,"z":29.37586975097656},"state":1}'),
(DEFAULT, 'Abandoned Theater 1-1', '{"doors":[{"heading":104,"model":-515032007,"coords":{"x":461.196533203125,"y":-1468.2510986328126,"z":29.38607788085937}},{"heading":284,"model":-515032007,"coords":{"x":461.9132385253906,"y":-1470.9388427734376,"z":29.38607788085937}}],"maxDistance":2,"coords":{"x":461.55487060546877,"y":-1469.594970703125,"z":29.38607788085937},"state":1}'),
(DEFAULT, 'Abandoned Theater 1-2', '{"doors":false,"maxDistance":2,"heading":15,"coords":{"x":457.0133361816406,"y":-1478.88525390625,"z":29.45929336547851},"model":-1082864116,"state":1}'),
(DEFAULT, 'Abandoned Theater E-3', '{"doors":[{"heading":297,"model":-973311781,"coords":{"x":466.40301513671877,"y":-1514.403076171875,"z":29.32433700561523}},{"heading":117,"model":816137771,"coords":{"x":465.5633850097656,"y":-1512.74462890625,"z":29.32433700561523}}],"maxDistance":2,"coords":{"x":465.98321533203127,"y":-1513.5738525390626,"z":29.32433700561523},"state":1}'),
(DEFAULT, 'Abandoned Theater G-1', '{"doors":false,"maxDistance":2,"heading":15,"coords":{"x":475.02557373046877,"y":-1514.190185546875,"z":29.54345703125},"model":-394365140,"state":1}'),
(DEFAULT, 'Abandoned Theater G-2', '{"doors":false,"maxDistance":2,"heading":15,"coords":{"x":478.3542175292969,"y":-1513.272216796875,"z":29.54356384277343},"model":1019042346,"state":1}'),
(DEFAULT, 'Abandoned Theater E-4', '{"doors":[{"heading":106,"model":-973311781,"coords":{"x":485.1081848144531,"y":-1507.2802734375,"z":29.34361267089843}},{"heading":286,"model":816137771,"coords":{"x":485.60791015625,"y":-1509.07080078125,"z":29.35664367675781}}],"maxDistance":2,"coords":{"x":485.3580322265625,"y":-1508.175537109375,"z":29.35012817382812},"state":1}'),
(DEFAULT, 'Abandoned Theater 1-3', '{"doors":[{"heading":15,"model":2114132590,"coords":{"x":461.6162109375,"y":-1483.0712890625,"z":29.3945026397705}},{"heading":195,"model":2114132590,"coords":{"x":464.1243591308594,"y":-1482.38671875,"z":29.3945026397705}}],"maxDistance":2,"coords":{"x":462.87030029296877,"y":-1482.72900390625,"z":29.3945026397705},"state":1}'),
(DEFAULT, 'Abandoned Theater 1-4', '{"doors":[{"heading":14,"model":2114132590,"coords":{"x":471.6172180175781,"y":-1480.359375,"z":29.39441108703613}},{"heading":194,"model":2114132590,"coords":{"x":474.12939453125,"y":-1479.69384765625,"z":29.39441108703613}}],"maxDistance":2,"coords":{"x":472.873291015625,"y":-1480.026611328125,"z":29.39441108703613},"state":1}'),
(DEFAULT, 'Abandoned Theater 1-5', '{"doors":false,"maxDistance":2,"heading":15,"coords":{"x":474.4897155761719,"y":-1474.1746826171876,"z":29.45929336547851},"model":-823676600,"state":1}'),
(DEFAULT, 'Abandoned Theater 3-1', '{"doors":false,"maxDistance":2,"heading":285,"coords":{"x":462.5486145019531,"y":-1483.3873291015626,"z":36.49530792236328},"model":-976663736,"state":1}'),
(DEFAULT, 'Abandoned Theater 3-2', '{"doors":false,"maxDistance":2,"heading":105,"coords":{"x":473.38616943359377,"y":-1481.5867919921876,"z":36.49530792236328},"model":-976663736,"state":1}'),
(DEFAULT, 'Abandoned Theater 2-1', '{"doors":false,"maxDistance":2,"heading":286,"coords":{"x":461.66461181640627,"y":-1481.3631591796876,"z":32.70326995849609},"model":-92540141,"state":1}'),
(DEFAULT, 'Abandoned Theater 2-2', '{"doors":[{"heading":14,"model":2114132590,"coords":{"x":458.76092529296877,"y":-1488.851318359375,"z":32.71543884277344}},{"heading":194,"model":2114132590,"coords":{"x":461.2673034667969,"y":-1488.2083740234376,"z":32.71543884277344}}],"maxDistance":2,"coords":{"x":460.01409912109377,"y":-1488.52978515625,"z":32.71543884277344},"state":1}'),
(DEFAULT, 'Abandoned Theater 2-3', '{"doors":[{"heading":14,"model":2114132590,"coords":{"x":476.5036315917969,"y":-1484.056884765625,"z":32.71543884277344}},{"heading":194,"model":2114132590,"coords":{"x":479.02166748046877,"y":-1483.4107666015626,"z":32.71543884277344}}],"maxDistance":2,"coords":{"x":477.76263427734377,"y":-1483.73388671875,"z":32.71543884277344},"state":1}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Abandoned Theater** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `chuz_abandoned_theater` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    plaintextCopy

    ```
    start chuz_abandoned_theater
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `459.38, -1452.86, 29.22` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Abandoned Theater** on your FiveM server! 🚀
