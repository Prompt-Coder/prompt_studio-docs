# 🏥 Pillbox Hill Medical Center

{% embed url="https://store.prompt-mods.com/store/package/7698320" %}
**Official asset for FiveM — available on CFX Portal and Prompt's Mods Store**
{% endembed %}

{% embed url="https://youtu.be/BczUGncSNA8" %}

A full rework of **Pillbox Hill Medical Center**: a new exterior and five connected interiors across four floors, two basements, the main floor and the rooftop helipad. It ships with two scripted features, a working **MRI scanner** and **teleport elevators** with a floor-select panel.

{% hint style="info" %}
**ox\_lib** is the only requirement. Framework (Qbox / QBCore / ESX / standalone) and target (ox\_target / qb-target) are detected automatically. Without a target resource, interactions fall back to an on-screen `[E]` prompt.
{% endhint %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Install the map

Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Pillbox+Hospital).

After downloading, **you will get a folder named**:

<pre><code><strong>prompt_pillbox_hospital
</strong></code></pre>

Drag and drop it inside your `resources` directory. When done, the full path should look like this:

<pre><code><strong>resources/prompt_pillbox_hospital
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Add to your server.cfg

Start it **after** ox\_lib, and after your framework and target resource if you use them:

<pre class="language-cfg"><code class="lang-cfg">start ox_lib
<strong>start prompt_pillbox_hospital
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 3 — Restart your server

Restart and go to **292.89, -584.39, 44.3**. Type `/pillbox` in chat. It prints which framework, target, language and modules were detected. If the building loads and the report looks right, installation was successful ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

### Additional Information

{% tabs %}
{% tab title="Features" %}
#### 🧲 MRI scanner

A patient lies on the MRI bed. An operator at the control-room console slides the bed into the bore and runs the scan (pulsing bore light and progress circle), then slides it back out.

* One patient at a time.
* Fully synced: every nearby player sees the same smooth movement.
* The patient pose is adjustable live with `/pillbox_mri_offset` (debug mode).

#### 🛗 Elevators

Two elevator shafts, each with four floors:

| Button | Floor |
| --- | --- |
| `-2` | Basement B2 |
| `-1` | Basement B1 |
| `1` | Main floor |
| `R` | Rooftop (helipad) |

Step into a cabin, press **E** and pick a floor on the button panel. The trip is fade → teleport → fade. There's no cabin prop, so nothing extra needs to stream.

#### 🧩 Built for any server

* **Frameworks:** Qbox, QBCore, ESX, standalone, or your own via `custom`.
* **Targets:** ox\_target and qb-target, or `custom`. With no target resource, an `[E]` prompt is used.
* **Notifications & text UI:** ox\_lib, QB or ESX, or `custom`.
* **12 languages:** English, Arabic, Chinese, Finnish, French, German, Korean, Norwegian, Portuguese, Russian, Spanish and Swedish.
* **Hooks & exports** let you gate every interaction or react to it (see **For Developers**).
{% endtab %}

{% tab title="Configuration" %}
All configuration files are **open** (not escrowed).

| File | What it controls |
| --- | --- |
| `config.lua` | Modules on/off, language, framework / target / notify / text-UI selection, staff access, debug |
| `config/mri.lua` | Bed positions, interaction zones, slide and scan timings, scan light, patient pose |
| `config/elevator.lua` | Floors, the two shafts' cabin points, interaction radius, staff-only toggle |
| `localization/<lang>.lua` | Every player-facing text (English is the fallback for missing keys) |
| `hooks/hooks_*.lua` | Your own gates and reactions (created from the `.example` files on first start) |
| `bridge/*.lua` | Framework / target / notify / text-UI adapters, including `custom` hooks |

#### Staff-only access

Everything is **open to everyone** by default. To limit the MRI controls or the elevators to medical staff:

1. Set `Config.MRI.operatorAccess = true` and/or `Config.Elevator.access = true`.
2. Put your EMS job names in `Config.access.jobs` (default: `ambulance`, `ems`, `doctor`). You can also set `minGrade` and `requireOnDuty`.
3. **Standalone servers:** grant the ACE instead:

```cfg
add_ace group.admin pillbox.access allow
```

Patients never need access. Anyone can lie on the MRI bed.

#### Language

Set `Config.language` to a code from `localization/` (e.g. `'de'`), or `'auto'` to follow your server's `setr ox:locale`.

#### Elevator interaction

`Config.Elevator.interaction = 'prompt'` (default) shows an `[E] Use elevator` prompt inside the cabin. `'target'` puts a target sphere on the cabin instead.
{% endtab %}

{% tab title="Compatibility" %}
Pillbox Hill Medical Center rebuilds the vanilla hospital block. It edits these **base-game files**:

* `dt1_06_0.ybn`, `hi@dt1_06_0.ybn` (block collision)
* `hei_dt1_06_strm_0.ymap`, `hei_dt1_06_long_0.ymap` (removes the vanilla hospital)
* `hei_dt1_occl_07.ymap` (occlusion)
* `vw_lodlights_small031.ymap`, `vw_distlodlights_small031.ymap` (distant lights)

Only one version of each file can load. Any other resource that ships one of these files needs a **merged version**.

#### Our Pillbox Fire Department & Bus Station — pre-merged, included

The resource ships ready-merged files in the `compatibility` folder:

| You own | Folder | Files |
| --- | --- | --- |
| Pillbox Fire Department | `compatibility/pillbox_fire_department` | `dt1_06_0.ybn`, `hi@dt1_06_0.ybn` |
| Bus Station | `compatibility/bus_station` | `hei_dt1_occl_07.ymap` |

1. Copy the files into **both** resources: `prompt_pillbox_hospital/stream/` and the other map's `stream/unlocked/` folder.
2. Replace the existing files with the same name, then restart.

Own both maps? Use both folders; they contain different files. Both resources then carry the same merged file, so the start order doesn't matter.

#### Any other map

Merge it with the [**Vertex Hub Merger**](https://app.vertex-hub.com/merger).

{% hint style="success" %}
Merging Prompt Studio maps with each other in Vertex Hub is **completely free**. No subscription required.
{% endhint %}

#### Not compatible with

* **Other Pillbox Hospital MLOs.** They replace the same building. Use one Pillbox only.
* Decoration packs made for the **vanilla** Pillbox (e.g. Christmas decorations). Their props are placed for the old building and will clip into this one.
{% endtab %}

{% tab title="Doorlock SQL" %}
Ready-to-import **ox\_doorlock** config: **64 doors (95 door leaves)**, generated from the map files and verified against every door in the map.

**Door names** follow the floors:

| Prefix | Floor |
| --- | --- |
| `1-` | Basement B2 |
| `2-` | Basement B1 |
| `3-` | Main floor |
| `4-` | Rooftop |
| `E-` | Exterior doors and gates |

* The two garage gates (`E-3`, `E-4`) open automatically for vehicles (`"auto": true`).
* **Not included on purpose:** the toilet stall doors and the elevator cabin doors. Players must be able to walk into the cabin to use the elevator.
* Every door starts **locked**. Set `"state":0` on any door you want unlocked by default.

{% hint style="info" %}
The ids use `DEFAULT`, so the SQL never collides with doors you already have. Import it as is.
{% endhint %}

<details>

<summary>Pillbox Hill Medical Center — ox_doorlock SQL (64 doors)</summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(DEFAULT, 'Pillbox Hill Medical Center 1-1', '{"doors":[{"model":976958139,"heading":160,"coords":{"x":309.4266357421875,"y":-586.2832641601562,"z":28.81767463684082}},{"model":-1808144713,"heading":160,"coords":{"x":307.2653503417969,"y":-585.4966430664062,"z":28.81767463684082}}],"coords":{"x":308.3459777832031,"y":-585.8899536132812,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-2', '{"model":-1484824604,"heading":350,"doors":false,"coords":{"x":313.8243103027344,"y":-581.59375,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-3', '{"model":-1484824604,"heading":335,"doors":false,"coords":{"x":314.6109924316406,"y":-579.4324340820312,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-4', '{"model":605414426,"heading":340,"doors":false,"coords":{"x":317.26971435546875,"y":-565.503662109375,"z":28.89190101623535},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-5', '{"doors":[{"model":-1484824604,"heading":250,"coords":{"x":319.1585998535156,"y":-583.4945678710938,"z":28.81767463684082}},{"model":-1484824604,"heading":70,"coords":{"x":319.94525146484375,"y":-581.3333129882812,"z":28.81767463684082}}],"coords":{"x":319.55194091796875,"y":-582.4139404296875,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-6', '{"doors":[{"model":1683753785,"heading":340,"coords":{"x":318.5955810546875,"y":-574.4564208984375,"z":28.892040252685547}},{"model":-1461709756,"heading":160,"coords":{"x":321.03875732421875,"y":-575.3456420898438,"z":28.89200210571289}}],"coords":{"x":319.8171691894531,"y":-574.9010009765625,"z":28.89202117919922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-7', '{"model":-627063124,"heading":340,"doors":false,"coords":{"x":324.12567138671875,"y":-581.2870483398438,"z":28.816308975219727},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-8', '{"doors":[{"model":-1484824604,"heading":250,"coords":{"x":329.03204345703125,"y":-587.0881958007812,"z":28.81767463684082}},{"model":-1484824604,"heading":70,"coords":{"x":329.8186950683594,"y":-584.9269409179688,"z":28.81767463684082}}],"coords":{"x":329.42535400390625,"y":-586.007568359375,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-9', '{"doors":[{"model":-1484824604,"heading":340,"coords":{"x":332.0890197753906,"y":-592.1318359375,"z":28.81767463684082}},{"model":-1484824604,"heading":160,"coords":{"x":329.927734375,"y":-591.3451538085938,"z":28.81767463684082}}],"coords":{"x":331.0083923339844,"y":-591.738525390625,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-10', '{"doors":[{"model":1683753785,"heading":250,"coords":{"x":332.8651428222656,"y":-580.6002197265625,"z":29.991941452026367}},{"model":-1461709756,"heading":70,"coords":{"x":331.9759216308594,"y":-583.0433959960938,"z":29.99190330505371}}],"coords":{"x":332.4205322265625,"y":-581.82177734375,"z":29.99192237854004},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-11', '{"doors":[{"model":1683753785,"heading":70,"coords":{"x":350.1663513183594,"y":-572.1798095703125,"z":28.891942977905273}},{"model":-1461709756,"heading":250,"coords":{"x":351.0555725097656,"y":-569.736572265625,"z":28.891904830932617}}],"coords":{"x":350.6109619140625,"y":-570.9581909179688,"z":28.891923904418945},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-12', '{"model":-627063124,"heading":340,"doors":false,"coords":{"x":351.1618347167969,"y":-577.1300048828125,"z":28.81680679321289},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-13', '{"doors":[{"model":-1484824604,"heading":340,"coords":{"x":357.588134765625,"y":-579.8839111328125,"z":28.81767463684082}},{"model":-1484824604,"heading":160,"coords":{"x":355.4268798828125,"y":-579.0972900390625,"z":28.81767463684082}}],"coords":{"x":356.50750732421875,"y":-579.4906005859375,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 1-14', '{"doors":[{"model":976958139,"heading":340,"coords":{"x":356.3988037109375,"y":-567.0584716796875,"z":28.76188850402832}},{"model":-1808144713,"heading":340,"coords":{"x":358.56011962890625,"y":-567.8451538085938,"z":28.76188850402832}}],"coords":{"x":357.4794616699219,"y":-567.4518432617188,"z":28.76188850402832},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-1', '{"doors":[{"model":976958139,"heading":340,"coords":{"x":308.0015869140625,"y":-570.4531860351562,"z":38.27863311767578}},{"model":-1808144713,"heading":340,"coords":{"x":310.16290283203125,"y":-571.23974609375,"z":38.27863311767578}}],"coords":{"x":309.0822448730469,"y":-570.8464965820312,"z":38.27863311767578},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-2', '{"doors":[{"model":-552361277,"heading":160,"coords":{"x":311.8147277832031,"y":-577.0036010742188,"z":38.40187454223633}},{"model":777896278,"heading":160,"coords":{"x":309.39678955078125,"y":-576.1235961914062,"z":38.401424407958984}}],"coords":{"x":310.60577392578125,"y":-576.5635986328125,"z":38.401649475097656},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-3', '{"doors":[{"model":-552361277,"heading":340,"coords":{"x":313.7898254394531,"y":-572.6486206054688,"z":38.404117584228516}},{"model":777896278,"heading":340,"coords":{"x":316.2082824707031,"y":-573.5288696289062,"z":38.404117584228516}}],"coords":{"x":314.9990539550781,"y":-573.0887451171875,"z":38.404117584228516},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-4', '{"model":768711192,"heading":295,"doors":false,"coords":{"x":316.237548828125,"y":-589.23681640625,"z":38.279605865478516},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-5', '{"doors":[{"model":-552361277,"heading":250,"coords":{"x":323.3216247558594,"y":-568.3135375976562,"z":38.404117584228516}},{"model":777896278,"heading":250,"coords":{"x":322.4390563964844,"y":-570.7383422851562,"z":38.404117584228516}}],"coords":{"x":322.8803405761719,"y":-569.5259399414062,"z":38.404117584228516},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-6', '{"doors":[{"model":374758529,"heading":160,"coords":{"x":322.712890625,"y":-588.2477416992188,"z":38.46305465698242}},{"model":374758529,"heading":340,"coords":{"x":325.1377258300781,"y":-589.1303100585938,"z":38.46305465698242}}],"coords":{"x":323.9253234863281,"y":-588.6890258789062,"z":38.46305465698242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-7', '{"model":1247236899,"heading":340,"doors":false,"coords":{"x":327.9980773925781,"y":-595.4011840820312,"z":38.2861213684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-8', '{"model":-627063124,"heading":250,"doors":false,"coords":{"x":331.4422912597656,"y":-599.6043090820312,"z":38.279605865478516},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-9', '{"model":374758529,"heading":325,"doors":false,"coords":{"x":333.9986572265625,"y":-578.2005004882812,"z":38.46305465698242},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-10', '{"model":-627063124,"heading":160,"doors":false,"coords":{"x":351.981689453125,"y":-591.0543823242188,"z":37.1317253112793},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 2-11', '{"doors":[{"model":976958139,"heading":250,"coords":{"x":354.6928405761719,"y":-588.3085327148438,"z":37.13103103637695}},{"model":-1808144713,"heading":250,"coords":{"x":353.90618896484375,"y":-590.4698486328125,"z":37.13103103637695}}],"coords":{"x":354.2995300292969,"y":-589.38916015625,"z":37.13103103637695},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-1', '{"model":2063519972,"heading":70,"doors":false,"coords":{"x":302.6012878417969,"y":-596.4888305664062,"z":43.661865234375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-2', '{"model":768711192,"heading":70,"doors":false,"coords":{"x":302.6315002441406,"y":-579.565185546875,"z":43.21234893798828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-3', '{"doors":[{"model":1851759888,"heading":250,"coords":{"x":303.6517333984375,"y":-585.0853881835938,"z":43.31745147705078}},{"model":54085317,"heading":250,"coords":{"x":302.8631286621094,"y":-587.2520141601562,"z":43.31746292114258}}],"coords":{"x":303.2574157714844,"y":-586.168701171875,"z":43.31745529174805},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-4', '{"model":768711192,"heading":160,"doors":false,"coords":{"x":304.2323303222656,"y":-595.8696899414062,"z":43.21234893798828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-5', '{"model":768711192,"heading":70,"doors":false,"coords":{"x":305.40191650390625,"y":-571.9535522460938,"z":43.21234893798828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-6', '{"doors":[{"model":-1484824604,"heading":250,"coords":{"x":311.75531005859375,"y":-576.7769775390625,"z":43.21466064453125}},{"model":-1484824604,"heading":70,"coords":{"x":312.54193115234375,"y":-574.61572265625,"z":43.21466064453125}}],"coords":{"x":312.14862060546875,"y":-575.6963500976562,"z":43.21466064453125},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-7', '{"model":768711192,"heading":250,"doors":false,"coords":{"x":312.96783447265625,"y":-596.0215454101562,"z":43.21234893798828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-8', '{"model":2063519972,"heading":160,"doors":false,"coords":{"x":314.17205810546875,"y":-571.7991333007812,"z":43.21234893798828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-9', '{"model":768711192,"heading":340,"doors":false,"coords":{"x":317.05426025390625,"y":-591.4495849609375,"z":43.21234893798828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-10', '{"model":-627063124,"heading":250,"doors":false,"coords":{"x":322.1483459472656,"y":-599.4132080078125,"z":43.21234893798828},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-11', '{"model":768711192,"heading":340,"doors":false,"coords":{"x":325.7112121582031,"y":-569.8792724609375,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-12', '{"model":768711192,"heading":160,"doors":false,"coords":{"x":327.0382080078125,"y":-570.3621826171875,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-13', '{"model":768711192,"heading":205,"doors":false,"coords":{"x":329.04925537109375,"y":-590.8553466796875,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-14', '{"model":768711192,"heading":70,"doors":false,"coords":{"x":329.24554443359375,"y":-595.9805297851562,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-15', '{"model":768711192,"heading":340,"doors":false,"coords":{"x":330.3616027832031,"y":-600.1446533203125,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-16', '{"model":768711192,"heading":25,"doors":false,"coords":{"x":330.9773864746094,"y":-594.4044189453125,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-17', '{"model":768711192,"heading":250,"doors":false,"coords":{"x":334.2620849609375,"y":-592.4703369140625,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-18', '{"model":768711192,"heading":115,"doors":false,"coords":{"x":334.2945251464844,"y":-573.5206909179688,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-19', '{"model":768711192,"heading":160,"doors":false,"coords":{"x":337.7338562011719,"y":-584.8970336914062,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-20', '{"model":768711192,"heading":160,"doors":false,"coords":{"x":342.4524841308594,"y":-586.6144409179688,"z":43.21234130859375},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-21', '{"model":976958139,"heading":340,"doors":false,"coords":{"x":343.8365478515625,"y":-583.14892578125,"z":43.211856842041016},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-22', '{"doors":[{"model":976958139,"heading":250,"coords":{"x":345.9328308105469,"y":-584.674560546875,"z":43.214656829833984}},{"model":-1808144713,"heading":250,"coords":{"x":345.1462097167969,"y":-586.8358764648438,"z":43.214656829833984}}],"coords":{"x":345.5395202636719,"y":-585.7551879882812,"z":43.214656829833984},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-23', '{"doors":[{"model":374758529,"heading":70,"coords":{"x":355.7560729980469,"y":-588.1001586914062,"z":42.4188117980957}},{"model":374758529,"heading":250,"coords":{"x":354.87353515625,"y":-590.5250244140625,"z":42.4188117980957}}],"coords":{"x":355.3147888183594,"y":-589.3125610351562,"z":42.4188117980957},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-24', '{"doors":[{"model":374758529,"heading":160,"coords":{"x":355.7682189941406,"y":-595.7019653320312,"z":42.4188117980957}},{"model":374758529,"heading":340,"coords":{"x":358.1929931640625,"y":-596.58447265625,"z":42.4188117980957}}],"coords":{"x":356.9805908203125,"y":-596.1431884765625,"z":42.4188117980957},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 3-25', '{"model":-1043098365,"heading":205,"doors":false,"coords":{"x":357.6800537109375,"y":-584.73046875,"z":42.42325210571289},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 4-1', '{"doors":[{"model":976958139,"heading":115,"coords":{"x":316.3451232910156,"y":-579.1179809570312,"z":74.18585205078125}},{"model":-1808144713,"heading":115,"coords":{"x":315.3730773925781,"y":-577.033447265625,"z":74.18585205078125}}],"coords":{"x":315.8591003417969,"y":-578.0757446289062,"z":74.18585205078125},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center 4-2', '{"doors":[{"model":976958139,"heading":70,"coords":{"x":330.1136169433594,"y":-580.8297119140625,"z":74.18585205078125}},{"model":-1808144713,"heading":70,"coords":{"x":330.9002685546875,"y":-578.6683959960938,"z":74.18585205078125}}],"coords":{"x":330.5069274902344,"y":-579.7490844726562,"z":74.18585205078125},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-1', '{"doors":[{"model":-1808144713,"heading":340,"coords":{"x":310.1452941894531,"y":-571.2863159179688,"z":28.81767463684082}},{"model":976958139,"heading":340,"coords":{"x":307.9840393066406,"y":-570.4996948242188,"z":28.81767463684082}}],"coords":{"x":309.0646667480469,"y":-570.8930053710938,"z":28.81767463684082},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-2', '{"doors":[{"model":1683753785,"heading":205,"coords":{"x":321.0455322265625,"y":-559.9749755859375,"z":28.892040252685547}},{"model":-1461709756,"heading":25,"coords":{"x":318.689208984375,"y":-561.0737915039062,"z":28.89200210571289}}],"coords":{"x":319.86737060546875,"y":-560.5244140625,"z":28.89202117919922},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-3', '{"model":2112127930,"heading":160,"doors":false,"coords":{"x":328.0688171386719,"y":-560.898193359375,"z":29.9362850189209},"state":1,"maxDistance":2,"auto":true}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-4', '{"model":2112127930,"heading":160,"doors":false,"coords":{"x":338.9305114746094,"y":-564.8514404296875,"z":29.9362850189209},"state":1,"maxDistance":2,"auto":true}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-5', '{"doors":[{"model":275758382,"heading":70,"coords":{"x":354.4910583496094,"y":-597.1142578125,"z":28.921916961669922}},{"model":-1708896107,"heading":70,"coords":{"x":355.27960205078125,"y":-594.9476318359375,"z":28.921907424926758}}],"coords":{"x":354.8853454589844,"y":-596.0309448242188,"z":28.921911239624023},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-6', '{"doors":[{"model":275758382,"heading":70,"coords":{"x":358.60986328125,"y":-585.7977294921875,"z":28.921918869018555}},{"model":-1708896107,"heading":70,"coords":{"x":359.3984680175781,"y":-583.631103515625,"z":28.92190933227539}}],"coords":{"x":359.0041809082031,"y":-584.7144165039062,"z":28.921913146972656},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-7', '{"doors":[{"model":275758382,"heading":250,"coords":{"x":300.1308288574219,"y":-583.8038940429688,"z":43.38489532470703}},{"model":-1708896107,"heading":250,"coords":{"x":299.3422546386719,"y":-585.9705200195312,"z":43.38490295410156}}],"coords":{"x":299.7365417480469,"y":-584.88720703125,"z":43.3848991394043},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-8', '{"doors":[{"model":976958139,"heading":340,"coords":{"x":308.0015869140625,"y":-570.453125,"z":43.21466064453125}},{"model":-1808144713,"heading":340,"coords":{"x":310.16290283203125,"y":-571.2398071289062,"z":43.21466064453125}}],"coords":{"x":309.0822448730469,"y":-570.8464965820312,"z":43.21466064453125},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-9', '{"doors":[{"model":-1484824604,"heading":250,"coords":{"x":326.6166076660156,"y":-594.1528930664062,"z":43.21466064453125}},{"model":-1484824604,"heading":70,"coords":{"x":327.4031982421875,"y":-591.9915771484375,"z":43.21466064453125}}],"coords":{"x":327.0098876953125,"y":-593.0722045898438,"z":43.21466064453125},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-10', '{"doors":[{"model":-1484824604,"heading":160,"coords":{"x":328.4344482421875,"y":-577.1707763671875,"z":43.21466064453125}},{"model":-1484824604,"heading":340,"coords":{"x":330.59576416015625,"y":-577.9573974609375,"z":43.21466064453125}}],"coords":{"x":329.5151062011719,"y":-577.5640869140625,"z":43.21466064453125},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-11', '{"model":-627063124,"heading":160,"doors":false,"coords":{"x":351.98175048828125,"y":-591.0543212890625,"z":42.246768951416016},"state":1,"maxDistance":2}'),
	(DEFAULT, 'Pillbox Hill Medical Center E-12', '{"doors":[{"model":1683753785,"heading":249,"coords":{"x":338.95361328125,"y":-581.453369140625,"z":74.31600952148438}},{"model":-1461709756,"heading":69,"coords":{"x":338.0302429199219,"y":-583.8839111328125,"z":74.31596374511719}}],"coords":{"x":338.4919128417969,"y":-582.6686401367188,"z":74.31598663330078},"state":1,"maxDistance":2}');
```

</details>
{% endtab %}

{% tab title="Custom Props" %}
These props are **Static + Dynamic**, so target scripts can use them, for example ox\_target's `addModel`. **Model names are all you need**; no coordinates required.

#### Placed in the hospital

| Group | Model names |
| --- | --- |
| Beds | `prompt_pill_s_hsp_bed_01`, `prompt_pill_s_hsp_bed_02` |
| Medical equipment | `prompt_pill_s_hsp_prop_cardiomonitor` |
| Seating | `atx_emgcy_onechair`, `atx_emgcy_threechair`, `atx_emgcy_fivechair` |
| Waiting room | `atx_emgcy_electric_queue`, `atx_emgcy_tv_flat_01`, `atx_emgcy_coffeetable2` |
| Other | `atx_emgcy_medclothes02`, `atx_emgcy_1_bin1` |

#### Included but not placed

Your scripts can spawn these:

`prop_atx_med_bed2`, `atx_emgcy_emptybed`, `atx_emgcy_sidetable`, `atx_emgcy_medclothes01`, `prop_atx_emgcy_body`, `prop_atx_emgcy_small_body`

{% hint style="warning" %}
The MRI machine (`prompt_pill_s_hsp_prop_mri_machine`) and its bed (`prompt_pill_s_hsp_prop_mri_machine_bed`) are driven by the MRI script. Don't attach other interactions to them.
{% endhint %}
{% endtab %}

{% tab title="For Developers" %}
#### Hooks

Every interaction is **gated** (`can*`, return `false` to block) and **reported** (`on*`). Edit `hooks/hooks_server.lua` (server-authoritative), `hooks_client.lua` or `hooks_shared.lua`. Updates never overwrite them.

| Feature | Entry id | Gates | Reactions | Server ctx |
| --- | --- | --- | --- | --- |
| `mri` | `bed` | `canUse` | `onStart`, `onEnd { reason }` | `{ source }` |
| `mri` | `controls` | `canOperate` | `onScanStart`, `onScanComplete` | `{ source = operator, patient }` |
| `elevator` | `b2` `b1` `main` `roof` | `canAccess` | `onTravel` | `{ source, elevatorId, floor, fromFloor }` |

Example: rooftop helipad for medical staff only.

{% code title="hooks/hooks_server.lua" %}
```lua
elevator = {
    entries = {
        ['roof'] = { canAccess = function(ctx) return Framework.HasAccess(ctx.source) end },
    },
},
```
{% endcode %}

`onScanComplete` is the place to hand the result to your medical-records script.

#### Exports

| Side | Export | Returns |
| --- | --- | --- |
| server | `IsMedic(src)` | Staff per `Config.access` |
| server | `IsMriOccupied()` | `boolean` |
| server | `GetMriState()` | `{ patient, bedPosition, scanning }` |
| server | `ReleaseMriPatient()` | `boolean`, forces the current patient off the bed |
| client | `IsOnMri()` | `boolean` |
| client | `OpenElevator(elevatorId, floorId)` | Opens the panel as if standing in that cabin |
| client | `TeleportToFloor(elevatorId, floorId)` | Server-checked trip (player must be at that shaft) |

Elevator ids: `left`, `right`. Floor ids: `b2`, `b1`, `main`, `roof`.

#### Commands

| Command | Who | What |
| --- | --- | --- |
| `/pillbox` | Anyone | Framework / target / module / language report |
| `/pillboxtest notify\|ui\|target` | `Config.debug` | Bridge self-tests |
| `/pillbox_debugdump` | Console or ACE `command.pillbox_debugdump` | Support snapshot, paste it in your ticket |
| `/pillbox_mri_test` | ACE `command.pillbox_mri_test` | Solo MRI run: lie → in → scan → out → up |
| `/pillbox_mri_operator` | ACE `command.pillbox_mri_test` | Runs the operator sequence for whoever is on the bed |
| `/pillbox_mri_offset x y z [rx ry rz]` | `Config.debug`, while on the bed | Try a patient pose live, prints the config line |
{% endtab %}

{% tab title="Troubleshooting & Support" %}
<details>

<summary>The resource doesn't start</summary>

Make sure `ox_lib` starts **before** `prompt_pillbox_hospital`, and that the folder is named exactly `prompt_pillbox_hospital`.

</details>

<details>

<summary>No elevator prompt / target option</summary>

Stand inside the cabin (the prompt radius is `1.2` m). If you set `Config.Elevator.interaction = 'target'`, a target resource must be running. Otherwise the `[E]` prompt is used. Also check `Config.Elevator.access`: when it's `true`, only medical staff can use the elevators.

</details>

<details>

<summary>Floating props, missing walls or doubled geometry</summary>

Another resource edits the same base-game files (see **Compatibility**). Merge them in the [Vertex Hub Merger](https://app.vertex-hub.com/merger), or remove the other Pillbox map.

</details>

<details>

<summary>Anything else</summary>

Set `Config.debug = true` (or only `Config.Debug.mri` / `Config.Debug.elevator`), reproduce the problem, then run `/pillbox_debugdump` in the server console and send us the output on Discord.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)

</details>
{% endtab %}
{% endtabs %}
