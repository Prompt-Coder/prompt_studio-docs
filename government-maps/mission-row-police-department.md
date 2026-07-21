# 🚓 Mission Row Police Department

<!-- TODO: replace with the real store package embed, e.g. {% embed url="https://fivem.prompt-mods.com/package/PACKAGE_ID" %} -->

<!-- TODO: add a showcase video, e.g. {% embed url="https://youtu.be/VIDEO_ID" %} -->

The **Mission Row Police Department** is a fully detailed MLO for FiveM — a complete police station with a reworked interior and exterior, built for roleplay, law enforcement, and emergency-response scenarios. It ships as a standalone map and pairs with the **MRPD Police Feature Pack** for interactive features.

***

### 🚀 Installation

{% stepper %}
{% step %}
#### Step 1 — Add the resource

Place `prompt_mrpd` inside your `resources` folder:

```
resources/prompt_mrpd
```
{% endstep %}

{% step %}
#### Step 2 — Add to server.cfg

```
ensure prompt_mrpd
```

Adding the Full pack too? Start it **after** the map (and after `ox_lib`):

```
ensure ox_lib
ensure prompt_mrpd
ensure prompt_mrpd_scripts
```
{% endstep %}

{% step %}
#### Step 3 — Restart & verify

Restart the server and teleport to **455.91, -999.01, 27.47** to confirm the interior loads ✅
{% endstep %}
{% endstepper %}

***

### 🧩 Base vs Full

| Tier | Resource | What you get |
| --- | --- | --- |
| **Base** | `prompt_mrpd` | The map — interiors, exterior, garage, elevator shell. Runs on its own. |
| **Full** | `+ prompt_mrpd_scripts` | Adds training, custody, gym, animations, audio, and banners. |

When the **Full** pack runs, the map's standalone layer steps aside automatically. → [**MRPD Police Feature Pack**](../scripts/mrpd/README.md)

***

### 📍 Map Location

Mission Row Police Department. Teleport inside the station to verify the load:\
**455.91, -999.01, 27.47**

***

### 🛠️ Features

* Detailed **interior** — briefing room, holding cells, garage, gym area, and offices
* Reworked **exterior** building, decals, and signage
* Scripted **garage** door
* Multi-floor **elevator** shell
* Animated props, PA audio, and banners *(with the [Full pack](../scripts/mrpd/README.md))*

***

### 🚪 Doorlock System

The station is fully compatible with [`ox_doorlock`](https://github.com/overextended/ox_doorlock). Community-submitted door positions for the whole station are below — import the SQL into your database and restart `ox_doorlock`.

{% hint style="info" %}
The SQL uses `DEFAULT` for the `id` column, so your database assigns free IDs automatically on import — it won't conflict with doorlocks you already have.
{% endhint %}

<details>

<summary><strong>MRPD Doorlock SQL (85 doors)</strong></summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(DEFAULT, 'MRPD G-1', '{"model":-1985598920,"auto":true,"heading":90,"doors":false,"coords":{"x":410.58624267578127,"y":-1022.4909057617188,"z":29.4594669342041},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD G-2', '{"model":-280093660,"auto":true,"heading":270,"doors":false,"coords":{"x":488.911376953125,"y":-1011.3807373046875,"z":28.57465171813965},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD G-3', '{"model":1487728468,"auto":true,"heading":270,"doors":false,"coords":{"x":488.9114074707031,"y":-1022.1572265625,"z":28.57465171813965},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD G-4', '{"model":1926169436,"auto":true,"heading":187,"doors":false,"coords":{"x":479.66741943359377,"y":-1026.9671630859376,"z":29.03641319274902},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD G-5', '{"model":-744294672,"auto":true,"heading":0,"doors":false,"coords":{"x":485.28143310546877,"y":-991.5838012695313,"z":28.44295692443847},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD G-6', '{"model":-744294672,"auto":true,"heading":0,"doors":false,"coords":{"x":478.5071716308594,"y":-991.6021118164063,"z":28.44295692443847},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD E-1', '{"doors":[{"model":1061735503,"heading":270,"coords":{"x":426.10382080078127,"y":-991.7098388671875,"z":30.02359199523925}},{"model":-218647638,"heading":270,"coords":{"x":426.10382080078127,"y":-988.8495483398438,"z":30.02359199523925}}],"coords":{"x":426.10382080078127,"y":-990.2796630859375,"z":30.02359199523925},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD E-2', '{"model":-630812075,"heading":270,"doors":false,"coords":{"x":426.0972595214844,"y":-1015.0638427734375,"z":29.54476928710937},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD E-3', '{"model":1307469158,"heading":90,"doors":false,"coords":{"x":473.6332092285156,"y":-1005.4370727539063,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD E-4', '{"model":-1033001619,"heading":270,"doors":false,"coords":{"x":465.2098693847656,"y":-984.54052734375,"z":44.76824188232422},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-1', '{"model":726043835,"heading":180,"doors":false,"coords":{"x":432.30035400390627,"y":-985.7879638671875,"z":29.13741493225097},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-2', '{"model":1307469158,"heading":90,"doors":false,"coords":{"x":431.1378173828125,"y":-983.9158325195313,"z":29.66619110107422},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-3', '{"model":1307469158,"heading":90,"doors":false,"coords":{"x":434.54547119140627,"y":-983.9158325195313,"z":29.66619110107422},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-4', '{"doors":[{"model":1148670743,"heading":0,"coords":{"x":433.6834411621094,"y":-994.720458984375,"z":29.66790008544922}},{"model":1869424902,"heading":0,"coords":{"x":435.6834411621094,"y":-994.720458984375,"z":29.66790008544922}}],"coords":{"x":434.6834411621094,"y":-994.720458984375,"z":29.66790008544922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-5', '{"doors":[{"model":1869424902,"heading":180,"coords":{"x":433.6834411621094,"y":-1003.893798828125,"z":29.66790008544922}},{"model":1148670743,"heading":180,"coords":{"x":435.6834411621094,"y":-1003.893798828125,"z":29.66790008544922}}],"coords":{"x":434.6834411621094,"y":-1003.893798828125,"z":29.66790008544922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-6', '{"model":841592293,"heading":180,"doors":false,"coords":{"x":438.9002380371094,"y":-1008.2346801757813,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-7', '{"model":726043835,"heading":90,"doors":false,"coords":{"x":440.6407165527344,"y":-1005.5096435546875,"z":28.73353576660156},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-8', '{"model":726043835,"heading":180,"doors":false,"coords":{"x":442.7796630859375,"y":-1003.7410278320313,"z":28.73353576660156},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-9', '{"model":1551275764,"heading":0,"doors":false,"coords":{"x":443.8717346191406,"y":-1008.2318115234375,"z":28.12579536437988},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-10', '{"model":1307469158,"heading":270,"doors":false,"coords":{"x":447.0243835449219,"y":-1002.3245239257813,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-11', '{"model":726043835,"heading":0,"doors":false,"coords":{"x":443.4212341308594,"y":-992.71728515625,"z":28.73353576660156},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-12', '{"model":726043835,"heading":0,"doors":false,"coords":{"x":449.8029479980469,"y":-985.8875732421875,"z":28.73353576660156},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-13', '{"model":726043835,"heading":0,"doors":false,"coords":{"x":449.8029479980469,"y":-981.1334228515625,"z":28.73353576660156},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-14', '{"model":726043835,"heading":180,"doors":false,"coords":{"x":443.86773681640627,"y":-979.1590576171875,"z":28.73353576660156},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-15', '{"doors":[{"model":1307469158,"heading":90,"coords":{"x":441.0804748535156,"y":-973.839111328125,"z":29.26231002807617}},{"model":841592293,"heading":90,"coords":{"x":441.0804748535156,"y":-976.428955078125,"z":29.26231002807617}}],"coords":{"x":441.0804748535156,"y":-975.134033203125,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-16', '{"model":1307469158,"heading":0,"doors":false,"coords":{"x":449.4596862792969,"y":-972.9990234375,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-17', '{"model":1307469158,"heading":0,"doors":false,"coords":{"x":454.6825866699219,"y":-977.328369140625,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-18', '{"doors":[{"model":-1056355503,"heading":180,"coords":{"x":460.04034423828127,"y":-972.8845825195313,"z":29.35942840576172}},{"model":-1056355503,"heading":0,"coords":{"x":462.36224365234377,"y":-972.8845825195313,"z":29.35942840576172}}],"coords":{"x":461.2012939453125,"y":-972.8845825195313,"z":29.35942840576172},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-19', '{"model":-1056355503,"heading":180,"doors":false,"coords":{"x":468.5730285644531,"y":-972.8836059570313,"z":29.35942840576172},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-20', '{"doors":[{"model":-1056355503,"heading":270,"coords":{"x":469.1961364746094,"y":-982.67431640625,"z":29.35973167419433}},{"model":-1056355503,"heading":90,"coords":{"x":469.19708251953127,"y":-980.3540649414063,"z":29.35973167419433}}],"coords":{"x":469.19659423828127,"y":-981.51416015625,"z":29.35973167419433},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-21', '{"model":1307469158,"heading":90,"doors":false,"coords":{"x":469.3443298339844,"y":-987.5093383789063,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-22', '{"doors":[{"model":841592293,"heading":90,"coords":{"x":469.3443298339844,"y":-998.650146484375,"z":29.26231002807617}},{"model":1307469158,"heading":90,"coords":{"x":469.3443298339844,"y":-996.060302734375,"z":29.26231002807617}}],"coords":{"x":469.3443298339844,"y":-997.355224609375,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-23', '{"model":841592293,"heading":180,"doors":false,"coords":{"x":466.08526611328127,"y":-1008.2346801757813,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-24', '{"model":841592293,"heading":180,"doors":false,"coords":{"x":459.5562438964844,"y":-1008.2346801757813,"z":29.26231002807617},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-25', '{"model":-1383516496,"heading":180,"doors":false,"coords":{"x":463.66973876953127,"y":-999.391845703125,"z":29.37309455871582},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-26', '{"model":-1383516496,"heading":180,"doors":false,"coords":{"x":459.9132385253906,"y":-999.391845703125,"z":29.37309455871582},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-27', '{"model":-1383516496,"heading":180,"doors":false,"coords":{"x":455.71673583984377,"y":-999.391845703125,"z":29.37309455871582},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-28', '{"model":-1383516496,"heading":180,"doors":false,"coords":{"x":451.9610290527344,"y":-999.391845703125,"z":29.39125633239746},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-29', '{"model":-1056355503,"heading":270,"doors":false,"coords":{"x":450.69720458984377,"y":-998.5325927734375,"z":29.37308502197265},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-30', '{"model":917741506,"heading":270,"doors":false,"coords":{"x":453.6883239746094,"y":-994.4948120117188,"z":28.13590621948242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-31', '{"model":917741506,"heading":270,"doors":false,"coords":{"x":453.6883239746094,"y":-990.0010986328125,"z":28.13590621948242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-32', '{"model":917741506,"heading":270,"doors":false,"coords":{"x":458.59375,"y":-994.4851684570313,"z":28.13590621948242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-33', '{"model":917741506,"heading":270,"doors":false,"coords":{"x":458.59375,"y":-990.0009765625,"z":28.13590621948242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-34', '{"model":917741506,"heading":90,"doors":false,"coords":{"x":460.6370544433594,"y":-993.196044921875,"z":28.13590621948242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 1-35', '{"model":917741506,"heading":90,"doors":false,"coords":{"x":460.6370544433594,"y":-988.7010498046875,"z":28.13590621948242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-1', '{"model":917741506,"heading":0,"doors":false,"coords":{"x":444.18658447265627,"y":-1017.4139404296875,"z":22.84865379333496},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-2', '{"model":917741506,"heading":0,"doors":false,"coords":{"x":444.18658447265627,"y":-1020.0380859375,"z":22.84865379333496},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-3', '{"doors":[{"model":1913294703,"heading":0,"coords":{"x":439.5635986328125,"y":-970.9515380859375,"z":23.55029296875}},{"model":1913294703,"heading":180,"coords":{"x":437.2239685058594,"y":-970.9515380859375,"z":23.55029296875}}],"coords":{"x":438.393798828125,"y":-970.9515380859375,"z":23.55029296875},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-4', '{"doors":[{"model":1913294703,"heading":90,"coords":{"x":434.9832458496094,"y":-973.1681518554688,"z":23.5438003540039}},{"model":1913294703,"heading":270,"coords":{"x":434.9832458496094,"y":-975.5078125,"z":23.5438003540039}}],"coords":{"x":434.9832458496094,"y":-974.3380126953125,"z":23.5438003540039},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-5', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":434.9832458496094,"y":-1005.91259765625,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-6', '{"model":1913294703,"heading":180,"doors":false,"coords":{"x":432.1129150390625,"y":-1003.9345703125,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-7', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":430.4124450683594,"y":-999.90087890625,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-8', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":430.4124450683594,"y":-992.9820556640625,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-9', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":430.4124450683594,"y":-983.95556640625,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-10', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":430.4124450683594,"y":-979.9239501953125,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-11', '{"model":1913294703,"heading":180,"doors":false,"coords":{"x":422.7593688964844,"y":-976.530029296875,"z":23.5438003540039},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-12', '{"model":1913294703,"heading":0,"doors":false,"coords":{"x":429.6031799316406,"y":-982.6538696289063,"z":23.5438003540039},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-13', '{"model":1913294703,"heading":180,"doors":false,"coords":{"x":420.2186584472656,"y":-998.0829467773438,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-14', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":430.4124450683594,"y":-1006.881591796875,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-15', '{"model":1913294703,"heading":0,"doors":false,"coords":{"x":421.3884582519531,"y":-1016.8500366210938,"z":23.54380226135254},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-16', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":410.33953857421877,"y":-1015.2628784179688,"z":18.27972221374511},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-17', '{"model":1913294703,"heading":90,"doors":false,"coords":{"x":410.33953857421877,"y":-998.5003051757813,"z":18.27972221374511},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD B-18', '{"doors":[{"model":1913294703,"heading":180,"coords":{"x":431.5290832519531,"y":-1018.2992553710938,"z":20.12190246582031}},{"model":1913294703,"heading":0,"coords":{"x":433.86871337890627,"y":-1018.2992553710938,"z":20.12190246582031}}],"coords":{"x":432.69891357421877,"y":-1018.2992553710938,"z":20.12190246582031},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 2-1', '{"model":-1913454337,"heading":90,"doors":false,"coords":{"x":456.55908203125,"y":-971.3486938476563,"z":37.03873443603515},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-1', '{"model":1510632809,"heading":90,"doors":false,"coords":{"x":448.7169189453125,"y":-974.1781005859375,"z":40.01218032836914},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-2', '{"model":1510632809,"heading":0,"doors":false,"coords":{"x":444.5018005371094,"y":-977.7491455078125,"z":39.68485641479492},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-3', '{"doors":[{"model":-389936422,"heading":270,"coords":{"x":439.2229919433594,"y":-975.3307495117188,"z":39.80807876586914}},{"model":-389936422,"heading":90,"coords":{"x":439.23773193359377,"y":-973.1897583007813,"z":39.80807876586914}}],"coords":{"x":439.2303466796875,"y":-974.26025390625,"z":39.80807876586914},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-4', '{"doors":[{"model":-389936422,"heading":90,"coords":{"x":449.7645263671875,"y":-969.4492797851563,"z":40.12647247314453}},{"model":-389936422,"heading":270,"coords":{"x":449.7503967285156,"y":-971.5869140625,"z":40.12647247314453}}],"coords":{"x":449.7574462890625,"y":-970.51806640625,"z":40.12647247314453},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-5', '{"model":1510632809,"heading":0,"doors":false,"coords":{"x":452.40240478515627,"y":-972.307861328125,"z":40.00357818603515},"state":1,"hideUi":true,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-6', '{"model":1510632809,"heading":0,"doors":false,"coords":{"x":457.7463073730469,"y":-972.307861328125,"z":40.00357818603515},"state":1,"hideUi":true,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-7', '{"model":1510632809,"heading":90,"doors":false,"coords":{"x":459.52276611328127,"y":-969.8014526367188,"z":40.00357818603515},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-8', '{"model":1510632809,"heading":90,"doors":false,"coords":{"x":463.3553466796875,"y":-970.3564453125,"z":40.01286697387695},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-9', '{"model":1510632809,"heading":90,"doors":false,"coords":{"x":463.3521728515625,"y":-975.5791625976563,"z":40.00571823120117},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-10', '{"model":1510632809,"heading":0,"doors":false,"coords":{"x":461.9283752441406,"y":-977.991943359375,"z":40.00357818603515},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-11', '{"model":1510632809,"heading":270,"doors":false,"coords":{"x":434.38818359375,"y":-972.272216796875,"z":39.68955993652344},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-12', '{"model":1510632809,"heading":270,"doors":false,"coords":{"x":434.3832702636719,"y":-978.423583984375,"z":39.69026184082031},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-13', '{"doors":[{"model":-389936422,"heading":0,"coords":{"x":437.5257263183594,"y":-981.1627197265625,"z":39.80828475952148}},{"model":-389936422,"heading":180,"coords":{"x":435.3888854980469,"y":-981.1486206054688,"z":39.80828475952148}}],"coords":{"x":436.4573059082031,"y":-981.1556396484375,"z":39.80828475952148},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-14', '{"model":1510632809,"heading":270,"doors":false,"coords":{"x":434.37506103515627,"y":-985.5111694335938,"z":39.68958282470703},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-15', '{"model":1510632809,"heading":270,"doors":false,"coords":{"x":434.3801574707031,"y":-990.2555541992188,"z":40.00774765014648},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-16', '{"model":1510632809,"heading":90,"doors":false,"coords":{"x":438.6420593261719,"y":-988.4932250976563,"z":40.00435256958008},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-17', '{"doors":[{"model":-389936422,"heading":0,"coords":{"x":437.5054016113281,"y":-991.8422241210938,"z":40.12934112548828}},{"model":-389936422,"heading":180,"coords":{"x":435.3634948730469,"y":-991.8291625976563,"z":40.12934112548828}}],"coords":{"x":436.4344482421875,"y":-991.835693359375,"z":40.12934112548828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-18', '{"model":-317254784,"heading":270,"doors":false,"coords":{"x":430.1753845214844,"y":-991.8195190429688,"z":40.12738037109375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-19', '{"model":-317254784,"heading":270,"doors":false,"coords":{"x":430.1753845214844,"y":-997.28173828125,"z":40.12738037109375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-20', '{"model":-317254784,"heading":0,"doors":false,"coords":{"x":430.29388427734377,"y":-1007.0596313476563,"z":40.13219451904297},"state":1,"maxDistance":2}'),
	(DEFAULT, 'MRPD 3-21', '{"model":1510632809,"heading":90,"doors":false,"coords":{"x":434.393798828125,"y":-1009.3743896484375,"z":39.99874877929687},"state":1,"maxDistance":2}');
```

</details>

***

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
