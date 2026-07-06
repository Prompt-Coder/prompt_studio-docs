# 🚒 Sandy Fire Station V2

{% embed url="https://store.prompt-mods.com/store/packages/7277533" %}
Official asset for FiveM - available on Prompt's Mods Store (Bundle)
{% endembed %}

The **Sandy Shores Fire Station V2** is a complete ground-up rebuild of the fire department, combining a fully detailed exterior with a richly furnished interior. Every room has been designed with roleplay functionality in mind — from the gym and briefing room to the gear lockers, observation tower, and multi-bay garage. Built to complement the Sandy Shores V2 project, this fire station brings a polished, lived-in feel to your emergency services.

{% embed url="https://youtu.be/6iRM42sYWy8" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

#### Installation Instructions

{% stepper %}
{% step %}
### Step 1 - Add the resource

Place the `prompt_sandy_fire2` folder inside your `resources` directory.

<pre><code><strong>resources/prompt_sandy_fire2
</strong></code></pre>
{% endstep %}

{% step %}
### Step 2 - Add to your server.cfg

Insert the following line to ensure the map loads automatically:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_fire2
</strong></code></pre>
{% endstep %}

{% step %}
### Step 3 - Set up MapData

Make sure you have the correct **Sandy MapData** installed and started before this resource.
{% endstep %}

{% step %}
### Step 4 - Test the map

Restart your server and visit the **Sandy Fire Station** location.\
If the map and interiors load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

{% hint style="info" %}
🔔 Tip: Always restart your server after adding new resources — especially when adding multiple Sandy area maps.
{% endhint %}

***

:round\_pushpin:Location: **1699.17, 3582.51, 35.61**

***

<details>

<summary><strong>Interactive Props</strong></summary>

<br>

| Category                 | Prop Name                                | Description                                          |
| ------------------------ | ---------------------------------------- | ---------------------------------------------------- |
| **Entrance & Reception** | `escobar_sandy_fd_int_door_entrance`     | Main entrance door                                   |
|                          | `escobar_sandy_fd_int_reception_desk`    | Front reception desk                                 |
|                          | `escobar_sandy_fd_int_wallofhonor`       | Wall of honor display                                |
|                          | `escobar_sandy_fd_int_reception_cabinet` | Cabinet behind reception                             |
| **Furniture & Office**   | `escobar_sandy_fd_int_bench_01`          | Interior bench seating                               |
|                          | `escobar_sandy_fd_int_sideboard2`        | Sideboard storage furniture                          |
|                          | `escobar_sandy_fd_int_old_cabinet01`     | Vintage storage cabinet                              |
|                          | `escobar_sandy_fd_int_desk_01`           | Office desk                                          |
|                          | `escobar_sandy_fd_int_folders_cabinet`   | Filing / folders cabinet                             |
|                          | `escobar_sandy_fd_int_04_side_table`     | Side table                                           |
|                          | `escobar_sandy_fd_int_old_cabinet02`     | Secondary vintage cabinet                            |
| **Briefing Room**        | `escobar_sandy_fd_int_briefing_chair`    | Briefing room table (named "chair" but is the table) |
|                          | `escobar_sandy_fd_int_briefing_chair02`  | Briefing room chair (actual seating)                 |
|                          | `escobar_sandy_fd_int_briefing_table`    | Briefing standing desk                               |
| **Kitchen**              | `escobar_sandy_fd_int_kitchen_table`     | Kitchen table                                        |
|                          | `escobar_sandy_fd_int_kitchen_det`       | Kitchen detail props                                 |
| **Gear & Equipment**     | `escobar_sandy_fd_int_jacket_001`        | Firefighter jacket on rack                           |
|                          | `escobar_sandy_fd_int_rack`              | Equipment rack                                       |
|                          | `escobar_sandy_fd_int_pants`             | Firefighter pants                                    |
|                          | `escobar_sandy_fd_inti_locker_02`        | Gear locker                                          |
|                          | `escobar_sandy_fd_int_outfit_foundry`    | Outfit foundry / gear station                        |
|                          | `escobar_sandy_fd_int_helmet`            | Firefighter helmet                                   |
|                          | `escobar_sandy_fd_int_scba`              | SCBA (Self-Contained Breathing Apparatus)            |
|                          | `escobar_sandy_fd_int_showers_det`       | Showers detail props                                 |
| **Doors & Garage**       | `escobar_sandy_fd_int_door_wc`           | Restroom door                                        |
|                          | `escobar_sandy_fd_int_door_exit`         | Exit door                                            |
|                          | `escobar_sandy_fd_int_garage_vacuum_01`  | Garage vacuum / cleaning station                     |
|                          | `escobar_sandy_fd_int_garage_gate`       | Main garage gate                                     |

</details>

***

<details>

<summary><strong>Doorlock SQL</strong></summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(2754, 'Sandy Fire Station V2 E-1', '{"state":0,"maxDistance":2,"doors":[{"model":-357310701,"coords":{"x":1686.1673583984376,"y":3577.319580078125,"z":35.96624755859375},"heading":210},{"model":-357310701,"coords":{"x":1684.4959716796876,"y":3576.3544921875,"z":35.96624755859375},"heading":30}],"coords":{"x":1685.3316650390626,"y":3576.8369140625,"z":35.96624755859375}}'),
	(2755, 'Sandy Fire Station V2 E-2', '{"state":1,"heading":30,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1701.57861328125,"y":3591.819091796875,"z":36.19905853271484}}'),
	(2756, 'Sandy Fire Station V2 E-3', '{"state":1,"heading":30,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1705.789306640625,"y":3594.23974609375,"z":36.19821548461914}}'),
	(2757, 'Sandy Fire Station V2 E-4', '{"state":1,"heading":30,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1710.026123046875,"y":3596.697509765625,"z":36.19449996948242}}'),
	(2758, 'Sandy Fire Station V2 E-5', '{"state":1,"heading":30,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1714.1348876953126,"y":3599.077880859375,"z":36.19931030273437}}'),
	(2759, 'Sandy Fire Station V2 E-6', '{"state":1,"heading":210,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1699.97802734375,"y":3623.610107421875,"z":36.20360565185547}}'),
	(2760, 'Sandy Fire Station V2 E-7', '{"state":1,"heading":210,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1695.8553466796876,"y":3621.252685546875,"z":36.20722961425781}}'),
	(2761, 'Sandy Fire Station V2 E-8', '{"state":1,"heading":210,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1691.62158203125,"y":3618.7900390625,"z":36.20738983154297}}'),
	(2762, 'Sandy Fire Station V2 E-9', '{"state":1,"heading":210,"model":1089597390,"maxDistance":6,"auto":true,"doors":false,"coords":{"x":1687.412841796875,"y":3616.36181640625,"z":36.20612716674805}}'),
	(2763, 'Sandy Fire Station V2 E-10', '{"state":1,"heading":30,"model":477095373,"maxDistance":2,"doors":false,"coords":{"x":1679.9840087890626,"y":3600.341796875,"z":35.9226188659668}}'),
	(2764, 'Sandy Fire Station V2 1-1', '{"state":1,"heading":210,"model":-1946200364,"maxDistance":2,"doors":false,"coords":{"x":1676.6488037109376,"y":3579.114990234375,"z":35.92396926879883}}'),
	(2765, 'Sandy Fire Station V2 1-2', '{"state":1,"maxDistance":2,"doors":[{"model":-1946200364,"coords":{"x":1670.6778564453126,"y":3581.424560546875,"z":35.92822265625},"heading":300},{"model":-1946200364,"coords":{"x":1671.6417236328126,"y":3579.754638671875,"z":35.92822265625},"heading":120}],"coords":{"x":1671.1597900390626,"y":3580.589599609375,"z":35.92822265625}}'),
	(2766, 'Sandy Fire Station V2 1-3', '{"state":1,"maxDistance":2,"doors":[{"model":777428071,"coords":{"x":1666.7669677734376,"y":3588.098876953125,"z":35.92822265625},"heading":300},{"model":-1258051157,"coords":{"x":1667.729248046875,"y":3586.421142578125,"z":35.92822265625},"heading":300}],"coords":{"x":1667.248046875,"y":3587.260009765625,"z":35.92822265625}}'),
	(2767, 'Sandy Fire Station V2 1-4', '{"state":1,"maxDistance":2,"doors":[{"model":-1946200364,"coords":{"x":1669.3837890625,"y":3590.2412109375,"z":35.92822265625},"heading":120},{"model":-1946200364,"coords":{"x":1668.416748046875,"y":3591.91650390625,"z":35.92822265625},"heading":300}],"coords":{"x":1668.9002685546876,"y":3591.078857421875,"z":35.92822265625}}'),
	(2768, 'Sandy Fire Station V2 1-5', '{"state":1,"heading":300,"model":-1946200364,"maxDistance":2,"doors":false,"coords":{"x":1684.6715087890626,"y":3590.796875,"z":35.91157531738281}}'),
	(2769, 'Sandy Fire Station V2 1-6', '{"state":1,"heading":300,"model":1538388438,"maxDistance":2,"doors":false,"coords":{"x":1680.3172607421876,"y":3598.39453125,"z":35.92030334472656}}'),
	(2770, 'Sandy Fire Station V2 1-7', '{"state":1,"maxDistance":2,"doors":[{"model":-1946200364,"coords":{"x":1695.48046875,"y":3590.664306640625,"z":35.91793060302734},"heading":120},{"model":-1946200364,"coords":{"x":1694.513916015625,"y":3592.3388671875,"z":35.91793060302734},"heading":300}],"coords":{"x":1694.9971923828126,"y":3591.50146484375,"z":35.91793060302734}}');
```

</details>

***

#### Notes

* Fully compatible with other **Sandy Shores** maps and the MapData system.
* Designed for easy integration with fire department job scripts and target systems.
* Optimized exterior and interior with minimal performance impact.
* Also available as part of the [**Sandy Fire Station & Hospital Bundle**](https://store.prompt-mods.com/store/packages/7256055).

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/prompt)
