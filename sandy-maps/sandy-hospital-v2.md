# 🏥 Sandy Hospital V2

{% embed url="https://store.prompt-mods.com/store/packages/7277536" %}
Official asset for FiveM - available on Prompt's Mods Store (Bundle)
{% endembed %}

The **Sandy Shores Hospital V2** is a fully reimagined medical facility featuring a detailed exterior and a comprehensive multi-room interior. From the reception and ICU to the MRI suite, operating room, pharmacy, morgue, cafeteria, and upper offices - every area has been designed to support immersive medical and emergency roleplay. The hospital includes a **built-in elevator system** with teleport functionality for seamless floor-to-floor navigation. Built as part of the Sandy Shores V2 project, this hospital sets a new standard for healthcare interiors.

{% embed url="https://youtu.be/6iRM42sYWy8" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

#### Installation Instructions

{% stepper %}
{% step %}
### Step 1 - Add the resource

Place the `prompt_sandy_hospital2` folder inside your `resources` directory.

<pre><code><strong>resources/prompt_sandy_hospital2
</strong></code></pre>
{% endstep %}

{% step %}
### Step 2 - Add to your server.cfg

Insert the following line to ensure the map loads automatically:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_hospital2
</strong></code></pre>
{% endstep %}

{% step %}
### Step 3 - Install ox\_lib (Required)

This resource requires [**ox\_lib**](https://github.com/overextended/ox_lib) for the elevator teleport system.\
Make sure `ox_lib` is installed and started **before** this resource in your `server.cfg`.

<pre class="language-cfg"><code class="lang-cfg"><strong>start ox_lib
</strong></code></pre>
{% endstep %}

{% step %}
### Step 4 - Set up MapData

Make sure you have the correct **Sandy MapData** installed and started before this resource.
{% endstep %}

{% step %}
### Step 5 - Test the map

Restart your server and visit the **Sandy Hospital** location.\
If the map and interiors load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

{% hint style="info" %}
🔔 Tip: Always restart your server after adding new resources — especially when adding multiple Sandy area maps.
{% endhint %}

***

:round\_pushpin:Location: **1765.53, 3618.79, 35.54**

***

<details>

<summary><strong>Interactive Props</strong></summary>

<br>

| Category                | Prop Name                              | Description                       |
| ----------------------- | -------------------------------------- | --------------------------------- |
| **Medical Equipment**   | `i45pt_s_hsp_prop_operationbed_01`     | Operating room bed                |
|                         | `i45pt_s_hsp_prop_mri_machine_bed`     | MRI ped part (movable via script) |
|                         | `i45_s_hsp_prop_cardiomonitor`         | Cardiac monitor                   |
|                         | `i45pt_s_hsp_bed_01`                   | Hospital bed (standard)           |
|                         | `i45pt_s_hsp_bed_02`                   | Hospital bed (alternate)          |
|                         | `i45pt_s_hsp_prop_deskmri`             | MRI control desk                  |
|                         | `i45pt_s_hsp_prop_mri_machine`         | MRI scanner machine               |
|                         | `i45pt_s_hsp_prop_trolley_01`          | Medical trolley                   |
|                         | `i45pt_s_hsp_prop_trolley_02`          | Medical trolley (alternate)       |
| **Furniture & Seating** | `i45pt_s_hsp_chair_01a`                | Standard hospital chair           |
|                         | `i45pt_s_hsp_bench_01`                 | Bench seating                     |
|                         | `i45pt_s_hsp_prop_dinnerchair_01`      | Cafeteria chair                   |
|                         | `i45pt_s_hsp_prop_dinnertable_01`      | Cafeteria table                   |
|                         | `i45pt_hosp_sandy_ex_office_02b_sofa2` | Office sofa                       |
| **Storage & Shelving**  | `i45pt_s_hsp_prop_locker_01`           | Staff locker                      |
|                         | `i45pt_s_hsp_shelves_01`               | Storage shelves                   |
|                         | `i45pt_s_hsp_prop_cupboard_01`         | Cupboard                          |
|                         | `i45pt_s_hsp_caprack_01`               | Cap / coat rack                   |
|                         | `i45pt_s_hsp_pharm_shelf`              | Pharmacy shelf                    |
|                         | `i45pt_s_hsp_countershelf_dinner`      | Cafeteria counter shelf           |
| **Office & Service**    | `i45pt_s_hsp_officedesk_01`            | Office desk                       |
|                         | `i45pt_s_hsp_pharmacy_window`          | Pharmacy service window           |
|                         | `i45pt_s_hsp_prop_stufftv_01`          | Staff TV                          |
|                         | `i45pt_s_hsp_till_01`                  | Cash register                     |
|                         | `i45pt_s_hsp_tillpay`                  | NFC payment terminal              |
| **Kitchen & Cafeteria** | `i45pt_s_hsp_kitchen_furniture_01`     | Kitchen furniture set             |
|                         | `i45pt_s_hsp_kitchen_grill_prop_01`    | Kitchen grill                     |
| **Doors**               | `i45pt_s_hsp_maindoor_r`               | Main entrance door (right)        |
|                         | `i45pt_s_hsp_maindoor_l`               | Main entrance door (left)         |
|                         | `i45pt_s_hsp_door_double_01`           | Double interior door              |
|                         | `i45pt_s_hsp_door_wood_single`         | Single wood interior door         |
|                         | `i45pt_s_hsp_balcony_door_l`           | Balcony door (left)               |
|                         | `i45pt_s_hsp_balcony_door_r`           | Balcony door (right)              |
|                         | `i45pt_s_hsp_garage_gate`              | Ambulance garage gate             |
| **Other**               | `i45pt_s_hsp_shower_cabines`           | Shower cabins                     |

</details>

<details>

<summary><i class="fa-stethoscope">:stethoscope:</i> <strong>MRI Scanner System</strong></summary>

{% file src="../.gitbook/assets/mritest.mp4" %}



The hospital includes a **fully functional MRI scanner** with two-role interaction — **patient** and **operator**.

**Patient:**

* Any player can lie on the MRI bed (no job restriction by default)
* Player is attached to the bed with a lying animation
* Press `BACKSPACE` to get up at any time
* Progress circle shown during the scan

**Operator:**

* Controlled by a configurable job/permission check (`canOperate` in config)
* Opens a context menu at the MRI control desk with options:
  * **Move Bed Inside** — slides the bed into the MRI tube
  * **Start MRI Scan** — begins the scan with progress bar and blue flashing light
  * **Move Bed Outside** — slides the bed back out
  * **Release Patient** — forces the patient off the bed
* Menu options are contextual — only relevant actions appear

**Scan Light Effect:**

* Blue pulsing light inside the MRI bore during scans
* Visible to all nearby players
* Configurable color, intensity, flash speed, and range

**Operator Permission Setup**

The `canOperate` function in `config.lua` controls who can operate the MRI. By default it returns `true` (no restriction).

**ESX:**

```lua
canOperate = function(source)
    local xPlayer = ESX.GetPlayerFromId(source)
    return xPlayer and xPlayer.getJob().name == 'ambulance'
end,
```

**QBCore / QBox:**

```lua
canOperate = function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    return Player and Player.PlayerData.job.name == 'ambulance'
end,
```

**Admin Test Commands**

Both commands require the ACE permission:

```
add_ace group.admin command.testmri allow
```

| Command         | Description                                                                          |
| --------------- | ------------------------------------------------------------------------------------ |
| `/testmri`      | Runs the full MRI sequence solo — lies down, moves bed in, scans, moves out, gets up |
| `/testoperator` | Simulates an operator while you are already on the bed — move in, scan, move out     |

</details>

***

<details>

<summary><strong>Doorlock SQL</strong></summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(2717, 'Sandy Hospital V2 E-1', '{"maxDistance":2,"coords":{"x":1761.9771728515626,"y":3622.92822265625,"z":34.79059219360351},"doors":[{"coords":{"x":1762.99462890625,"y":3623.5166015625,"z":34.79059219360351},"heading":30,"model":-99789842},{"coords":{"x":1760.959716796875,"y":3622.339599609375,"z":34.79059219360351},"heading":210,"model":-1809250257}],"state":0}'),
	(2718, 'Sandy Hospital V2 E-2', '{"auto":true,"coords":{"x":1732.3043212890626,"y":3607.672607421875,"z":36.26321411132812},"doors":false,"state":1,"heading":30,"model":783802132,"maxDistance":6}'),
	(2719, 'Sandy Hospital V2 E-3', '{"maxDistance":2,"coords":{"x":1728.7200927734376,"y":3605.84912109375,"z":35.1361198425293},"doors":false,"state":1,"heading":210,"model":1552570442}'),
	(2720, 'Sandy Hospital V2 E-4', '{"maxDistance":2,"coords":{"x":1712.2318115234376,"y":3631.67578125,"z":35.09859466552734},"doors":false,"state":1,"heading":30,"model":1552570442}'),
	(2721, 'Sandy Hospital V2 E-5', '{"auto":true,"coords":{"x":1716.4967041015626,"y":3634.338623046875,"z":36.22335433959961},"doors":false,"state":1,"heading":210,"model":783802132,"maxDistance":6}'),
	(2722, 'Sandy Hospital V2 E-6', '{"maxDistance":2,"coords":{"x":1745.169677734375,"y":3638.820556640625,"z":34.79059219360351},"doors":[{"coords":{"x":1744.5811767578126,"y":3639.838134765625,"z":34.79059219360351},"heading":120,"model":-99789842},{"coords":{"x":1745.758056640625,"y":3637.802978515625,"z":34.79059219360351},"heading":300,"model":-1809250257}],"state":1}'),
	(2723, 'Sandy Hospital V2 E-7', '{"maxDistance":2,"coords":{"x":1755.684326171875,"y":3633.8544921875,"z":34.79059219360351},"doors":[{"coords":{"x":1754.666748046875,"y":3633.265869140625,"z":34.79059219360351},"heading":210,"model":-99789842},{"coords":{"x":1756.7017822265626,"y":3634.443115234375,"z":34.79059219360351},"heading":30,"model":-1809250257}],"state":1}'),
	(2724, 'Sandy Hospital V2 E-8', '{"maxDistance":2,"coords":{"x":1756.7181396484376,"y":3645.47998046875,"z":34.79059219360351},"doors":[{"coords":{"x":1757.306640625,"y":3644.46240234375,"z":34.79059219360351},"heading":300,"model":-99789842},{"coords":{"x":1756.129638671875,"y":3646.497314453125,"z":34.79059219360351},"heading":120,"model":-1809250257}],"state":1}'),
	(2725, 'Sandy Hospital V2 E-9', '{"maxDistance":2,"coords":{"x":1778.0595703125,"y":3652.1162109375,"z":34.29669189453125},"doors":[{"coords":{"x":1777.263671875,"y":3653.492431640625,"z":34.29669189453125},"heading":120,"model":-184565622},{"coords":{"x":1778.85546875,"y":3650.73974609375,"z":34.29669189453125},"heading":120,"model":687450237}],"state":1}'),
	(2726, 'Sandy Hospital V2 1-1', '{"maxDistance":2,"coords":{"x":1747.09423828125,"y":3627.17236328125,"z":34.70506286621094},"doors":[{"coords":{"x":1747.6060791015626,"y":3626.267822265625,"z":34.70505142211914},"heading":120,"model":-851388712},{"coords":{"x":1746.582275390625,"y":3628.07666015625,"z":34.70507431030273},"heading":300,"model":-851388712}],"state":1}'),
	(2727, 'Sandy Hospital V2 1-2', '{"maxDistance":2,"coords":{"x":1746.3023681640626,"y":3624.79931640625,"z":34.73498916625976},"doors":false,"state":1,"heading":210,"model":-1318231787}'),
	(2728, 'Sandy Hospital V2 1-3', '{"maxDistance":2,"coords":{"x":1746.5748291015626,"y":3620.677734375,"z":34.73392486572265},"doors":false,"state":1,"heading":120,"model":-1318231787}'),
	(2729, 'Sandy Hospital V2 1-4', '{"maxDistance":2,"coords":{"x":1741.0999755859376,"y":3623.730712890625,"z":34.70507431030273},"doors":[{"coords":{"x":1740.5880126953126,"y":3624.635009765625,"z":34.70508575439453},"heading":300,"model":-851388712},{"coords":{"x":1741.6119384765626,"y":3622.826416015625,"z":34.70506286621094},"heading":120,"model":-851388712}],"state":1}'),
	(2730, 'Sandy Hospital V2 1-5', '{"maxDistance":2,"coords":{"x":1738.0244140625,"y":3623.753662109375,"z":34.70512390136719},"doors":[{"coords":{"x":1738.9287109375,"y":3624.265625,"z":34.70513534545898},"heading":210,"model":-851388712},{"coords":{"x":1737.1199951171876,"y":3623.24169921875,"z":34.70511245727539},"heading":30,"model":-851388712}],"state":1}'),
	(2731, 'Sandy Hospital V2 1-6', '{"maxDistance":2,"coords":{"x":1736.483154296875,"y":3621.6376953125,"z":34.73403549194336},"doors":false,"state":1,"heading":120,"model":-1318231787}'),
	(2732, 'Sandy Hospital V2 1-7', '{"maxDistance":2,"coords":{"x":1735.339599609375,"y":3630.6455078125,"z":34.73392486572265},"doors":false,"state":1,"heading":30,"model":-1318231787}'),
	(2733, 'Sandy Hospital V2 1-8', '{"maxDistance":2,"coords":{"x":1731.2236328125,"y":3630.725830078125,"z":34.70528793334961},"doors":[{"coords":{"x":1731.7362060546876,"y":3629.82177734375,"z":34.70527648925781},"heading":120,"model":-851388712},{"coords":{"x":1730.711181640625,"y":3631.6298828125,"z":34.7052993774414},"heading":300,"model":-851388712}],"state":1}'),
	(2734, 'Sandy Hospital V2 1-9', '{"maxDistance":2,"coords":{"x":1732.10791015625,"y":3633.63427734375,"z":34.73403549194336},"doors":false,"state":1,"heading":210,"model":-1318231787}'),
	(2735, 'Sandy Hospital V2 1-10', '{"maxDistance":2,"coords":{"x":1737.6083984375,"y":3631.984375,"z":34.70507431030273},"doors":[{"coords":{"x":1736.7041015625,"y":3631.47265625,"z":34.70508575439453},"heading":30,"model":-851388712},{"coords":{"x":1738.5128173828126,"y":3632.496337890625,"z":34.70506286621094},"heading":210,"model":-851388712}],"state":1}'),
	(2736, 'Sandy Hospital V2 1-11', '{"maxDistance":2,"coords":{"x":1745.974853515625,"y":3629.149169921875,"z":34.72350692749023},"doors":false,"state":1,"heading":300,"model":-1318231787}'),
	(2737, 'Sandy Hospital V2 1-12', '{"maxDistance":2,"coords":{"x":1769.5772705078126,"y":3637.82421875,"z":34.71339416503906},"doors":[{"coords":{"x":1768.6728515625,"y":3637.312255859375,"z":34.71338272094726},"heading":30,"model":-851388712},{"coords":{"x":1770.481689453125,"y":3638.336181640625,"z":34.71340560913086},"heading":210,"model":-851388712}],"state":1}'),
	(2738, 'Sandy Hospital V2 1-13', '{"maxDistance":2,"coords":{"x":1773.289794921875,"y":3634.901611328125,"z":34.73513793945312},"doors":false,"state":1,"heading":300,"model":-1318231787}'),
	(2739, 'Sandy Hospital V2 1-14', '{"maxDistance":2,"coords":{"x":1773.273193359375,"y":3639.927978515625,"z":34.73392486572265},"doors":false,"state":1,"heading":30,"model":-1318231787}'),
	(2740, 'Sandy Hospital V2 1-15', '{"maxDistance":2,"coords":{"x":1776.4959716796876,"y":3636.755615234375,"z":34.73513793945312},"doors":false,"state":1,"heading":300,"model":-1318231787}'),
	(2741, 'Sandy Hospital V2 1-16', '{"maxDistance":2,"coords":{"x":1775.720703125,"y":3641.369873046875,"z":34.71339416503906},"doors":[{"coords":{"x":1774.816650390625,"y":3640.857421875,"z":34.71338272094726},"heading":30,"model":-851388712},{"coords":{"x":1776.624755859375,"y":3641.88232421875,"z":34.71340560913086},"heading":210,"model":-851388712}],"state":1}'),
	(2742, 'Sandy Hospital V2 1-17', '{"maxDistance":2,"coords":{"x":1776.4390869140626,"y":3644.266845703125,"z":34.73403549194336},"doors":false,"state":1,"heading":300,"model":-1318231787}'),
	(2743, 'Sandy Hospital V2 1-18', '{"maxDistance":2,"coords":{"x":1771.2596435546876,"y":3653.18408203125,"z":34.73403549194336},"doors":false,"state":1,"heading":300,"model":-1318231787}'),
	(2744, 'Sandy Hospital V2 1-19', '{"maxDistance":2,"coords":{"x":1767.4720458984376,"y":3649.263916015625,"z":34.71339416503906},"doors":[{"coords":{"x":1768.37646484375,"y":3649.77587890625,"z":34.71340560913086},"heading":210,"model":-851388712},{"coords":{"x":1766.567626953125,"y":3648.751953125,"z":34.71338272094726},"heading":30,"model":-851388712}],"state":1}'),
	(2745, 'Sandy Hospital V2 1-20', '{"maxDistance":2,"coords":{"x":1762.813720703125,"y":3646.54248046875,"z":34.73377990722656},"doors":false,"state":1,"heading":30,"model":-1318231787}'),
	(2746, 'Sandy Hospital V2 1-21', '{"maxDistance":2,"coords":{"x":1760.6602783203126,"y":3651.652099609375,"z":34.73513793945312},"doors":false,"state":1,"heading":300,"model":-1318231787}'),
	(2747, 'Sandy Hospital V2 1-22', '{"maxDistance":2,"coords":{"x":1757.88037109375,"y":3652.492431640625,"z":34.73392486572265},"doors":false,"state":1,"heading":210,"model":-1318231787}'),
	(2748, 'Sandy Hospital V2 1-23', '{"maxDistance":2,"coords":{"x":1762.1005859375,"y":3655.468505859375,"z":34.70506286621094},"doors":[{"coords":{"x":1762.612548828125,"y":3654.564208984375,"z":34.70507431030273},"heading":120,"model":-851388712},{"coords":{"x":1761.588623046875,"y":3656.372802734375,"z":34.70505142211914},"heading":300,"model":-851388712}],"state":1}'),
	(2749, 'Sandy Hospital V2 1-24', '{"auto":true,"coords":{"x":1760.037353515625,"y":3655.9228515625,"z":33.53993988037109},"doors":[{"coords":{"x":1760.6865234375,"y":3656.29833984375,"z":33.53993988037109},"heading":30,"model":1219957182},{"coords":{"x":1759.3880615234376,"y":3655.54736328125,"z":33.53993988037109},"heading":30,"model":-1225363909}],"state":1,"maxDistance":2}'),
	(2750, 'Sandy Hospital V2 2-1', '{"maxDistance":2,"coords":{"x":1757.0369873046876,"y":3628.328857421875,"z":39.1791877746582},"doors":false,"state":1,"heading":120,"model":-1318231787}'),
	(2751, 'Sandy Hospital V2 2-2', '{"maxDistance":2,"coords":{"x":1759.738525390625,"y":3630.421142578125,"z":39.1791877746582},"doors":false,"state":1,"heading":300,"model":-1318231787}'),
	(2752, 'Sandy Hospital V2 2-3', '{"maxDistance":2,"coords":{"x":1755.220703125,"y":3631.4697265625,"z":39.1791877746582},"doors":false,"state":1,"heading":120,"model":-1318231787}'),
	(2753, 'Sandy Hospital V2 2-4', '{"maxDistance":2,"coords":{"x":1755.792724609375,"y":3634.0439453125,"z":39.25869369506836},"doors":[{"coords":{"x":1756.7698974609376,"y":3634.60888671875,"z":39.25869369506836},"heading":30,"model":1588600532},{"coords":{"x":1754.8154296875,"y":3633.478759765625,"z":39.25869369506836},"heading":30,"model":141488719}],"state":1}');
```

</details>

***

#### Notes

* Fully compatible with other **Sandy Shores** maps and the MapData system.
* **Requires** [**ox\_lib**](https://github.com/overextended/ox_lib) for the built-in elevator teleport script.
* Designed for easy integration with hospital job scripts, ambulance systems, and target frameworks.
* Optimized exterior and interior with minimal performance impact.
* Also available as part of the [**Sandy Fire Station & Hospital Bundle**](https://store.prompt-mods.com/store/packages/7256055).

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/prompt)
