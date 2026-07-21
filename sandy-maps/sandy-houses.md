# 🏠 Sandy Houses

## 🏠 Sandy Houses

{% embed url="https://fivem.prompt-mods.com/package/6499824" %}

{% embed url="https://www.youtube.com/watch?v=ZM3UJkVO5d8" %}

The **Sandy Houses** pack adds a cozy, realistic residential area to Sandy Shores, optimized for performance and perfect for FiveM roleplay servers.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

{% tabs %}
{% tab title="📍 Position" %}
View all house coordinates in the [Google Doc with images](https://docs.google.com/document/d/1gQmbMr4UM9sXeyJlnhip13QYw9eRuGHR_uzLfFLOiuk/edit?usp=sharing).
{% endtab %}

{% tab title=" ⚙️Modes" %}


## 🧰 Sandy Houses — Modes

This page explains the two user-facing modes and how the runtime chooses which entity sets to activate.

***

### Global Mode Switch

In `config.lua`:

```lua
-- Options: "shells_only", "furnished"
Config.HouseMode = "furnished"
```

* **shells\_only** → Activates only each interior’s `defaults.sets` (unfurnished shells).
* **furnished** → Activates `defaults.sets` **plus** `"furniture"` (if that set exists for the interior). If an interior doesn’t define `"furniture"`, it remains on its defaults only.

At runtime the script:

1. Collects `defaults.sets` for that interior
2. Conditionally appends `"furniture"` when `Config.HouseMode == "furnished"`
3. Deactivates **all** known sets for the interior, then **activates only** the chosen sets.

***

### Manual “No Interior” (Despawn)

To remove interiors entirely, manually replace:

```
prompt_sandy_houses_part1\nointeriors (read readme)\houseplacement
```

**into**

```
prompt_sandy_houses_part1\stream\houseplacement
```

***

### Optional Overrides and Map Types

* You can disable/force specific houses or modes via `Config.HouseOverrides`.
* All Sandy Shores houses are grouped under the `sandy_houses` map type.

***
{% endtab %}

{% tab title="🚪 Entity Sets" %}


## 🏠 Sandy Houses — Entity Sets Per Interior

This page lists **every available interior entity set** per entry — no shortening.

> **Tip:** Users pick between **shells\_only** (unfurnished) and **furnished** globally. At runtime, that translates to:\
> `defaults.sets` (unfurnished) or `defaults.sets` + `"furniture"` (furnished, if present).

***

### Houses 1–10 (Sandy)

#### House 1 — `prompts_sandy_house1` — **Coords:** (1812.367, 3762.021, 34.21988)

**Entity Sets (Label → Set):**

* Bathroom Light → `bathroomlight`
* Hall Light → `halllight`
* Bedroom Light → `bedroomlight`
* Master Bedroom Light → `masterbedroomlight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Master Bathroom 1 → `masterbathroom1`
* Master Bathroom 2 → `masterbathroom2`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Master Bedroom 1 → `masterbedroom1`
* Master Bedroom 2 → `masterbedroom2`
* Master Bedroom 3 → `masterbedroom3`
* Bath 1 → `bath1`
* Bath 2 → `bath2`
* Master Bath 1 → `masterbath1`
* Master Bath 2 → `masterbath2`
* Bedroom Dirt → `bedroomdirt`
* Hall Dirt → `halldirt`
* Master Bedroom Dirt → `masterbedroomdirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Upper Frame → `upframe`
* Radiator Place → `radiatorplace`
* Fireplace → `fireplace`

***

#### House 2 — `prompts_sandy_house2` — **Coords:** (1775.337, 3746.64, 34.72295)

**Entity Sets (Label → Set):**

* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bathroom 3 → `bathroom3`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Bedroom 4 → `bedroom4`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Upper Frame → `upframe`

***

#### House 3 — `prompts_sandy_house3` — **Coords:** (1353.875, 3598.896, 35.84079)

**Entity Sets (Label → Set):**

* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bathroom 3 → `bathroom3`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Bedroom 4 → `bedroom4`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Upper Frame → `upframe`

***

#### House 4 — `prompts_sandy_house4` — **Coords:** (1650.912, 3626.822, 36.44559)

**Entity Sets (Label → Set):**

* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bathroom 3 → `bathroom3`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Upper Frame → `upframe`
* Wall Light 1 → `walllight1`
* Wall Light 2 → `walllight2`

***

#### House 5 — `prompts_sandy_house5` — **Coords:** (1425.434, 3669.213, 35.62526)

**Entity Sets (Label → Set):**

* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Hall Light → `halllight`
* Bathroom Light → `bathroomlight`
* Master Bathroom Light → `masterbathroomlight`
* Master Bedroom Light → `masterbedroomlight`
* Bedroom Light → `bedroomlight`
* Master Bathroom 1 → `masterbathroom1`
* Master Bathroom 2 → `masterbathroom2`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Master Bedroom 1 → `masterbedroom1`
* Master Bedroom 2 → `masterbedroom2`
* Master Bedroom 3 → `masterbedroom3`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Master Bathroom Set 1 → `masterbath1`
* Master Bathroom Set 2 → `masterbath2`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Hall Dirt → `halldirt`
* Bedroom Dirt → `bedroomdirt`
* Master Bedroom Dirt → `masterbedroomdirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Upper Frame → `upframe`

***

#### House 6 — `prompts_sandy_house6` — **Coords:** (1794.129, 3717.376, 35.1188)

**Entity Sets (Label → Set):**

* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Hall Light → `halllight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bathroom 3 → `bathroom3`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Hall Dirt → `halldirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Upper Frame → `upframe`

***

#### House 7 — `prompts_sandy_house7` — **Coords:** (1644.035, 3660.563, 35.57352)

**Entity Sets (Label → Set):**

* Master Bedroom Light → `masterbedroomlight`
* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Hall Light → `halllight`
* Master Bathroom Light → `masterbathroomlight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Master Bedroom 1 → `masterbedroom1`
* Master Bedroom 2 → `masterbedroom2`
* Master Bedroom 3 → `masterbedroom3`
* Master Bedroom 4 → `masterbedroom4`
* Master Bathroom 1 → `masterbathroom1`
* Master Bathroom 2 → `masterbathroom2`
* Master Bathroom 3 → `masterbathroom3`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Master Bathroom Set 1 → `masterbath1`
* Master Bathroom Set 2 → `masterbath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Hall Dirt → `halldirt`
* Master Bedroom Dirt → `masterbedroomdirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Curtains → `curtains`
* Upper Frame → `upframe`
* Bathroom Blinds → `bathroomblinds`
* Curtains 2 → `curtains2`

***

#### House 8 — `prompts_sandy_house8` — **Coords:** (1384.889, 3610.139, 35.468)

**Entity Sets (Label → Set):**

* Master Bedroom Light → `masterbedroomlight`
* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Hall Light → `halllight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Master Bedroom 1 → `masterbedroom1`
* Master Bedroom 2 → `masterbedroom2`
* Master Bedroom 3 → `masterbedroom3`
* Master Bathroom 1 → `masterbathroom1`
* Master Bathroom 2 → `masterbathroom2`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Master Bathroom Set 1 → `masterbath1`
* Master Bathroom Set 2 → `masterbath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Hall Dirt → `halldirt`
* Master Bedroom Dirt → `masterbedroomdirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`
* Curtains → `curtains`

***

#### House 9 — `prompts_sandy_house9` — **Coords:** (1827.661, 3738.009, 32.46845)

**Entity Sets (Label → Set):**

* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Hall Light → `halllight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Hall Dirt → `halldirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`

***

#### House 10 — `prompts_sandy_house10` — **Coords:** (1677.48, 3653.435, 37.39836)

**Entity Sets (Label → Set):**

* Bathroom Light → `bathroomlight`
* Living Room Light → `livingroomlight`
* Kitchen Light → `kitchenlight`
* Bedroom Light → `bedroomlight`
* Hall Light → `halllight`
* Bathroom 1 → `bathroom1`
* Bathroom 2 → `bathroom2`
* Bedroom 1 → `bedroom1`
* Bedroom 2 → `bedroom2`
* Bedroom 3 → `bedroom3`
* Bathroom Set 1 → `bath1`
* Bathroom Set 2 → `bath2`
* Bedroom Dirt → `bedroomdirt`
* Living Room Dirt → `livingroomdirt`
* Kitchen Dirt → `kitchendirt`
* Hall Dirt → `halldirt`
* Door Frame 1 → `doorframe1`
* Door Frame 2 → `doorframe2`
* Window Frame 1 → `windowframe1`
* Window Frame 2 → `windowframe2`
* Wall Frame 1 → `wallframe1`
* Wall Frame 2 → `wallframe2`

***

### VA Houses 11–16

> These are defined in `config_va_houses.lua`. Each lists its available sets explicitly.

#### VA House 11 — `va_house11_interior` — **Coords:** (1667.42, 3677.586, 35.58788)

**Entity Sets (Label → Set):**

* Default → `default`
* Furniture → `furniture`
* Abandoned → `abandoned`

***

#### VA House 12 — `va_house12_interior` — **Coords:** (1434.828, 3627.759, 37.83353)

**Entity Sets (Label → Set):**

* Default → `default`
* Furniture → `furniture`
* Abandoned → `abandoned`

***

#### VA House 13 — `va_house13_interior` — **Coords:** (1434.823, 3627.772, 37.84808)

**Entity Sets (Label → Set):**

* Default → `default`
* Default Purple → `default_purple`
* Furniture → `furniture`
* Abandoned → `abandoned`

***

#### VA House 14 — `va_house14_interior` — **Coords:** (1337.252, 3636.468, 35.40242)

**Entity Sets (Label → Set):**

* Default → `default`
* Furniture → `furniture`
* Abandoned → `abandoned`

***

#### VA House 15 — `va_h15_interior` — **Coords:** (1366.957, 3645.899, 34.68516)

**Entity Sets (Label → Set):**

* Default → `default`
* Furniture → `furniture`
* Abandoned → `abandoned`

***

#### VA House 16 — `va_h16_interior` — **Coords:** (1394.258, 3655.665, 35.85954)

**Entity Sets (Label → Set):**

* Default → `default`
* Furniture → `furniture`
* Abandoned → `abandoned`

***

### Big Houses

#### Senora Apartments B — `rck_senora_apps_b` — **Coords:** (1705.158, 3853.854, 37.889)

**Entity Sets (Label → Set):**

* Default → `default`
* Furniture → `furniture`
* Hash 47D6D9CB → `hash_47D6D9CB`

***

#### Senora Apartments — `rck_senora_apps` — **Coords:** (1735.229, 3877.322, 37.781)

**Entity Sets (Label → Set):**

* Default → `default`
* Furniture → `furniture`
* Hash 47D6D9CB → `hash_47D6D9CB`
{% endtab %}

{% tab title="🧰 Scripts" %}
If you prefer free options and manual setup:

**🧱 Prop Placer**

[**KuzQuality Prop Placer**](https://kuzquality.com/package/6697203) — Free tool to populate interiors manually with your own props.

**🧩 Entity Sets Manager**

[**FS-InteriorManager**](https://github.com/FearlessNite345/FS-InteriorManager/releases/tag/v1.1.1) — Free and preconfigured for Prompt’s interiors, supports toggling between `default` and `furnished`.
{% endtab %}

{% tab title="🔒 Doorlock Feature" %}


```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 1-1', '{"heading":300,"doors":false,"model":-240243877,"coords":{"x":1813.5782470703126,"y":3765.904296875,"z":34.02345275878906},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 1-2', '{"heading":120,"doors":false,"model":-1504996201,"coords":{"x":1814.3546142578126,"y":3765.016845703125,"z":33.93904876708984},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 1-3', '{"heading":30,"doors":false,"model":-1504996201,"coords":{"x":1815.079345703125,"y":3762.95068359375,"z":33.9404411315918},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 1-4', '{"heading":300,"doors":false,"model":-1504996201,"coords":{"x":1809.7088623046876,"y":3760.833984375,"z":33.93901443481445},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 1-5', '{"heading":30,"doors":false,"model":-1504996201,"coords":{"x":1809.716552734375,"y":3758.97412109375,"z":33.93815994262695},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 2-1', '{"heading":30,"doors":false,"model":1956267088,"coords":{"x":1774.2281494140626,"y":3744.4765625,"z":34.63594818115234},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 2-2', '{"heading":210,"doors":false,"model":1494725493,"coords":{"x":1773.8829345703126,"y":3745.995361328125,"z":34.27357482910156},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 2-3', '{"heading":210,"doors":false,"model":1494725493,"coords":{"x":1774.6251220703126,"y":3749.87841796875,"z":34.2708511352539},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 2-4', '{"heading":30,"doors":false,"model":-2099191587,"coords":{"x":1777.5582275390626,"y":3752.31494140625,"z":34.27594757080078},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 3-1', '{"heading":20,"doors":false,"model":-2083705920,"coords":{"x":1355.5821533203126,"y":3593.178955078125,"z":35.37979125976562},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 3-2', '{"heading":110,"doors":false,"model":-350062849,"coords":{"x":1354.7469482421876,"y":3594.53759765625,"z":35.3729133605957},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 3-3', '{"heading":110,"doors":false,"model":-350062849,"coords":{"x":1352.3760986328126,"y":3601.05078125,"z":35.38884735107422},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 3-4', '{"heading":290,"doors":false,"model":-2083705920,"coords":{"x":1350.532958984375,"y":3603.824462890625,"z":35.37593078613281},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 4-1', '{"heading":300,"doors":false,"model":-1899145338,"coords":{"x":1653.111572265625,"y":3625.763916015625,"z":36.09358978271484},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 4-2', '{"heading":210,"doors":false,"model":974879756,"coords":{"x":1650.168701171875,"y":3625.450439453125,"z":36.0778923034668},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 4-3', '{"heading":300,"doors":false,"model":974879756,"coords":{"x":1651.47509765625,"y":3625.671142578125,"z":36.0815200805664},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 4-4', '{"heading":300,"doors":false,"model":-1667304663,"coords":{"x":1646.27880859375,"y":3629.496826171875,"z":36.12358856201172},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 5-1', '{"heading":200,"doors":false,"model":1231460896,"coords":{"x":1418.353515625,"y":3675.7470703125,"z":35.26320266723633},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 5-2', '{"heading":20,"doors":false,"model":-417873796,"coords":{"x":1428.614990234375,"y":3668.25439453125,"z":35.27370071411133},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 5-3', '{"heading":20,"doors":false,"model":-2077308227,"coords":{"x":1430.394287109375,"y":3663.43310546875,"z":35.26237487792969},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 5-4', '{"heading":20,"doors":false,"model":-2077308227,"coords":{"x":1427.8631591796876,"y":3662.888916015625,"z":35.2734146118164},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 5-5', '{"heading":110,"doors":false,"model":-417873796,"coords":{"x":1422.1129150390626,"y":3665.607421875,"z":35.27870941162109},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 5-6', '{"heading":20,"doors":false,"model":1231460896,"coords":{"x":1429.1646728515626,"y":3661.43603515625,"z":35.26604461669922},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 6-1', '{"heading":301,"doors":false,"model":1170790271,"coords":{"x":1791.85107421875,"y":3715.002197265625,"z":34.78307723999023},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 6-2', '{"heading":31,"doors":false,"model":1540585784,"coords":{"x":1796.7779541015626,"y":3715.62841796875,"z":34.80405807495117},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 6-3', '{"heading":66,"doors":false,"model":1540585784,"coords":{"x":1794.4241943359376,"y":3719.577880859375,"z":34.79203414916992},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 7-1', '{"heading":305,"doors":false,"model":-113351383,"coords":{"x":1641.2772216796876,"y":3667.733642578125,"z":35.38069152832031},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 7-2', '{"heading":125,"doors":false,"model":-1164028407,"coords":{"x":1642.942626953125,"y":3665.808837890625,"z":35.29967498779297},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 7-3', '{"heading":305,"doors":false,"model":-1678341339,"coords":{"x":1645.1429443359376,"y":3665.147216796875,"z":35.29660034179687},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 7-4', '{"heading":350,"doors":false,"model":-1164028407,"coords":{"x":1642.4154052734376,"y":3659.817138671875,"z":35.2990608215332},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 7-5', '{"heading":305,"doors":false,"model":-1678341339,"coords":{"x":1650.628662109375,"y":3658.5625,"z":35.2992935180664},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 7-6', '{"doors":[{"coords":{"x":1648.2867431640626,"y":3656.83154296875,"z":35.3056755065918},"model":-280156205,"heading":305},{"coords":{"x":1646.4603271484376,"y":3655.552978515625,"z":35.3056755065918},"model":-585989282,"heading":305}],"coords":{"x":1647.37353515625,"y":3656.1923828125,"z":35.3056755065918},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-H-1', '{"doors":[{"coords":{"x":1383.2052001953126,"y":3606.143798828125,"z":35.24193954467773},"model":-1644510439,"heading":200},{"coords":{"x":1384.953125,"y":3606.779541015625,"z":35.24193954467773},"model":684775619,"heading":200}],"coords":{"x":1384.0791015625,"y":3606.461669921875,"z":35.24193954467773},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-H-2', '{"heading":110,"doors":false,"model":2145842721,"coords":{"x":1388.36376953125,"y":3608.22705078125,"z":35.24419784545898},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-H-3', '{"heading":200,"doors":false,"model":2145842721,"coords":{"x":1387.202880859375,"y":3612.177734375,"z":35.24456024169922},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-H-4', '{"heading":290,"doors":false,"model":2145842721,"coords":{"x":1384.7906494140626,"y":3612.93310546875,"z":35.24340057373047},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-H-5', '{"heading":200,"doors":false,"model":2145842721,"coords":{"x":1384.76904296875,"y":3617.666259765625,"z":35.24127960205078},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-H-6', '{"heading":200,"doors":false,"model":105484157,"coords":{"x":1378.7579345703126,"y":3616.3564453125,"z":35.24007797241211},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-G-1', '{"heading":20,"doors":false,"model":244758292,"coords":{"x":1369.945556640625,"y":3602.319580078125,"z":34.8062629699707},"state":1,"doorRate":1,"auto":true,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 8-G-2', '{"heading":290,"doors":false,"model":-828066833,"coords":{"x":1372.08056640625,"y":3608.208251953125,"z":34.69247055053711},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 9-H-1', '{"heading":300,"doors":false,"model":-1531520890,"coords":{"x":1824.183349609375,"y":3742.526611328125,"z":34.83540344238281},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 9-H-2', '{"heading":300,"doors":false,"model":2010609611,"coords":{"x":1825.0599365234376,"y":3738.015869140625,"z":34.79949188232422},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 9-H-3', '{"heading":120,"doors":false,"model":2010609611,"coords":{"x":1830.447265625,"y":3735.835205078125,"z":34.79349517822265},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 9-H-4', '{"heading":300,"doors":false,"model":-943918681,"coords":{"x":1831.312255859375,"y":3727.832763671875,"z":34.78815841674805},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 10-1', '{"heading":120,"doors":false,"model":1688186522,"coords":{"x":1682.9111328125,"y":3657.186279296875,"z":36.91742706298828},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 10-2', '{"heading":300,"doors":false,"model":-889774987,"coords":{"x":1682.0596923828126,"y":3654.581787109375,"z":36.94482040405273},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 10-3', '{"heading":120,"doors":false,"model":-889774987,"coords":{"x":1681.4176025390626,"y":3658.06005859375,"z":36.93566513061523},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 10-4', '{"heading":300,"doors":false,"model":1688186522,"coords":{"x":1672.0611572265626,"y":3646.531005859375,"z":36.9248161315918},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 11-1', '{"heading":45,"doors":false,"model":-1989239478,"coords":{"x":1665.551025390625,"y":3682.0927734375,"z":34.82287979125976},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 11-2', '{"heading":45,"doors":false,"model":-1708094201,"coords":{"x":1667.875,"y":3684.3408203125,"z":34.80287933349609},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 11-3', '{"heading":45,"doors":false,"model":-1708094201,"coords":{"x":1670.321044921875,"y":3677.19677734375,"z":34.80287933349609},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 11-4', '{"heading":45,"doors":false,"model":-1708094201,"coords":{"x":1668.5030517578126,"y":3674.8349609375,"z":34.80287933349609},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 11-5', '{"doors":[{"coords":{"x":1672.6090087890626,"y":3672.31201171875,"z":34.82287979125976},"model":1441216297,"heading":45},{"coords":{"x":1674.1220703125,"y":3673.82373046875,"z":34.82287979125976},"model":1078504583,"heading":45}],"coords":{"x":1673.365478515625,"y":3673.06787109375,"z":34.82287979125976},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-1', '{"heading":200,"doors":false,"model":777065009,"coords":{"x":1446.8369140625,"y":3623.1396484375,"z":36.30707931518555},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-2', '{"heading":110,"doors":false,"model":-64988855,"coords":{"x":1447.7452392578126,"y":3625.22705078125,"z":36.26408004760742},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-3', '{"heading":285,"doors":false,"model":-64988855,"coords":{"x":1443.2530517578126,"y":3628.323974609375,"z":36.26408004760742},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-4', '{"heading":54,"doors":false,"model":-64988855,"coords":{"x":1445.172119140625,"y":3631.821533203125,"z":36.26408004760742},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-5', '{"heading":200,"doors":false,"model":-64988855,"coords":{"x":1445.484619140625,"y":3631.909912109375,"z":36.26408004760742},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-6', '{"heading":110,"doors":false,"model":360036898,"coords":{"x":1442.25390625,"y":3635.61767578125,"z":35.17308044433594},"state":1,"auto":true,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-7', '{"heading":110,"doors":false,"model":-64988855,"coords":{"x":1441.2830810546876,"y":3633.665771484375,"z":36.26408004760742},"state":1,"lockSound":"door_bolt","maxDistance":2,"unlockSound":"door_bolt"}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-8', '{"unlockSound":"door_bolt","heading":290,"state":1,"doors":false,"coords":{"x":1437.1795654296876,"y":3636.116943359375,"z":36.26408004760742},"lockSound":"door_bolt","maxDistance":2,"model":-64988855}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 12-9', '{"unlockSound":"door_bolt","heading":200,"state":1,"doors":false,"coords":{"x":1436.6756591796876,"y":3639.087158203125,"z":36.30707931518555},"lockSound":"door_bolt","maxDistance":2,"model":1535724378}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 13-1', '{"unlockSound":"door_bolt","heading":200,"state":1,"doors":false,"coords":{"x":1419.8277587890626,"y":3621.865234375,"z":35.50952911376953},"lockSound":"door_bolt","maxDistance":2,"model":1999534392}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 13-2', '{"unlockSound":"door_bolt","heading":200,"state":1,"doors":false,"coords":{"x":1420.2069091796876,"y":3628.0185546875,"z":35.52352905273437},"lockSound":"door_bolt","maxDistance":2,"model":877929284}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 13-3', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1421.046630859375,"y":3628.32421875,"z":35.52352905273437},"lockSound":"door_bolt","maxDistance":2,"model":877929284}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 13-4', '{"unlockSound":"door_bolt","heading":110,"state":1,"doors":false,"coords":{"x":1417.92529296875,"y":3628.3740234375,"z":35.42898178100586},"lockSound":"door_bolt","maxDistance":2,"model":450870767}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 14-1', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1333.625732421875,"y":3641.697021484375,"z":34.05141830444336},"lockSound":"door_bolt","maxDistance":2,"model":-530861634}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 14-2', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1333.248291015625,"y":3635.489990234375,"z":34.0294189453125},"lockSound":"door_bolt","maxDistance":2,"model":-247593452}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 14-3', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1331.1900634765626,"y":3634.740478515625,"z":34.0294189453125},"lockSound":"door_bolt","maxDistance":2,"model":-247593452}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 14-4', '{"unlockSound":"door_bolt","heading":290,"state":1,"doors":false,"coords":{"x":1335.5301513671876,"y":3635.134765625,"z":33.95042037963867},"lockSound":"door_bolt","maxDistance":2,"model":819472460}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 15-1', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1372.5570068359376,"y":3647.169921875,"z":34.44316101074219},"lockSound":"door_bolt","maxDistance":2,"model":71850351}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 15-2', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1368.5067138671876,"y":3645.16455078125,"z":34.47216033935547},"lockSound":"door_bolt","maxDistance":2,"model":2064121908}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 15-3', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1365.856689453125,"y":3644.2001953125,"z":34.47216033935547},"lockSound":"door_bolt","maxDistance":2,"model":2064121908}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 15-4', '{"unlockSound":"door_bolt","heading":110,"state":1,"doors":false,"coords":{"x":1361.789794921875,"y":3640.85107421875,"z":34.43416213989258},"lockSound":"door_bolt","maxDistance":2,"model":1486619153}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 16-1', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1391.6097412109376,"y":3658.897216796875,"z":34.41854095458984},"lockSound":"door_bolt","maxDistance":2,"model":152850925}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 16-2', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1393.3187255859376,"y":3659.538330078125,"z":34.41653823852539},"lockSound":"door_bolt","maxDistance":2,"model":-843852781}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 16-3', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1395.2198486328126,"y":3660.22998046875,"z":34.41653823852539},"lockSound":"door_bolt","maxDistance":2,"model":-843852781}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 16-4', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1393.453369140625,"y":3653.90234375,"z":34.41653823852539},"lockSound":"door_bolt","maxDistance":2,"model":-843852781}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 16-5', '{"unlockSound":"door_bolt","heading":200,"state":1,"doors":false,"coords":{"x":1400.47509765625,"y":3650.913818359375,"z":34.41653823852539},"lockSound":"door_bolt","maxDistance":2,"model":-843852781}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 16-6', '{"unlockSound":"door_bolt","heading":20,"state":1,"doors":false,"coords":{"x":1399.0484619140626,"y":3648.236572265625,"z":34.45253753662109},"lockSound":"door_bolt","maxDistance":2,"model":-686494241}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-1-1', '{"unlockSound":"door_bolt","heading":224,"state":1,"doors":false,"coords":{"x":1701.3082275390626,"y":3858.632080078125,"z":35.4400749206543},"lockSound":"door_bolt","maxDistance":2,"model":-1310003697}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-1-2', '{"unlockSound":"door_bolt","heading":314,"state":1,"doors":false,"coords":{"x":1698.4197998046876,"y":3849.652587890625,"z":35.37849807739258},"lockSound":"door_bolt","maxDistance":2,"model":-1310003697}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-1-3', '{"unlockSound":"door_bolt","heading":134,"state":1,"doors":false,"coords":{"x":1713.3011474609376,"y":3853.93994140625,"z":35.1542854309082},"lockSound":"door_bolt","maxDistance":2,"model":-1310003697}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-1-4', '{"doorRate":1,"unlockSound":"door_bolt","heading":44,"state":1,"doors":false,"coords":{"x":1712.7706298828126,"y":3849.67626953125,"z":35.38152694702148},"model":451581468,"maxDistance":2,"lockSound":"door_bolt","auto":true}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-1-5', '{"unlockSound":"door_bolt","heading":134,"state":1,"doors":false,"coords":{"x":1706.59912109375,"y":3851.1015625,"z":35.22723007202148},"lockSound":"door_bolt","maxDistance":2,"model":117389386}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-1-6', '{"doorRate":1,"unlockSound":"door_bolt","heading":44,"state":1,"doors":false,"coords":{"x":1707.7423095703126,"y":3844.83251953125,"z":35.38152694702148},"model":451581468,"maxDistance":2,"lockSound":"door_bolt","auto":true}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-1', '{"unlockSound":"door_bolt","heading":44,"state":1,"doors":false,"coords":{"x":1704.5181884765626,"y":3858.04638671875,"z":38.26993942260742},"lockSound":"door_bolt","maxDistance":2,"model":-1339547461}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-2', '{"unlockSound":"door_bolt","heading":134,"state":1,"doors":false,"coords":{"x":1707.9207763671876,"y":3852.614990234375,"z":38.50148773193359},"lockSound":"door_bolt","maxDistance":2,"model":117389386}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-3', '{"unlockSound":"door_bolt","heading":224,"state":1,"doors":false,"coords":{"x":1709.083984375,"y":3855.652587890625,"z":38.51443481445312},"lockSound":"door_bolt","maxDistance":2,"model":117389386}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-4', '{"unlockSound":"door_bolt","heading":314,"state":1,"doors":false,"coords":{"x":1708.6707763671876,"y":3851.97314453125,"z":38.50148773193359},"lockSound":"door_bolt","maxDistance":2,"model":117389386}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-5', '{"unlockSound":"door_bolt","heading":224,"state":1,"doors":false,"coords":{"x":1712.0640869140626,"y":3852.360107421875,"z":38.26896286010742},"lockSound":"door_bolt","maxDistance":2,"model":-1339547461}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-6', '{"unlockSound":"door_bolt","heading":44,"state":1,"doors":false,"coords":{"x":1705.372314453125,"y":3849.902587890625,"z":38.50148773193359},"lockSound":"door_bolt","maxDistance":2,"model":117389386}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-7', '{"unlockSound":"door_bolt","heading":134,"state":1,"doors":false,"coords":{"x":1704.9755859375,"y":3849.789306640625,"z":38.50148773193359},"lockSound":"door_bolt","maxDistance":2,"model":117389386}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-8', '{"unlockSound":"door_bolt","heading":134,"state":1,"doors":false,"coords":{"x":1705.6214599609376,"y":3847.173095703125,"z":38.51443099975586},"lockSound":"door_bolt","maxDistance":2,"model":117389386}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 17-2-9', '{"unlockSound":"door_bolt","heading":224,"state":1,"doors":false,"coords":{"x":1705.2349853515626,"y":3845.77978515625,"z":38.26993942260742},"lockSound":"door_bolt","maxDistance":2,"model":-1339547461}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-1', '{"unlockSound":"door_bolt","heading":124,"state":1,"doors":false,"coords":{"x":1736.884521484375,"y":3883.10009765625,"z":35.17720794677734},"lockSound":"door_bolt","maxDistance":2,"model":-955088610}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-2', '{"unlockSound":"door_bolt","heading":124,"state":1,"doors":false,"coords":{"x":1728.0712890625,"y":3877.20947265625,"z":35.17720794677734},"lockSound":"door_bolt","maxDistance":2,"model":-955088610}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-3', '{"unlockSound":"door_bolt","heading":124,"state":1,"doors":false,"coords":{"x":1735.887451171875,"y":3878.96240234375,"z":35.20692825317383},"lockSound":"door_bolt","maxDistance":2,"model":-541267183}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-4', '{"unlockSound":"door_bolt","heading":34,"state":1,"doors":false,"coords":{"x":1742.1202392578126,"y":3874.176513671875,"z":35.55001449584961},"lockSound":"door_bolt","maxDistance":2,"model":1992927314}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-5', '{"unlockSound":"door_bolt","heading":124,"state":1,"doors":false,"coords":{"x":1734.413330078125,"y":3877.98095703125,"z":35.20692825317383},"lockSound":"door_bolt","maxDistance":2,"model":-541267183}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-6', '{"doorRate":1,"unlockSound":"door_bolt","heading":34,"state":1,"doors":false,"coords":{"x":1737.444580078125,"y":3871.09130859375,"z":35.54217910766601},"model":-718252958,"maxDistance":2,"lockSound":"door_bolt","auto":true}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-7', '{"doorRate":1,"unlockSound":"door_bolt","heading":34,"state":1,"doors":false,"coords":{"x":1734.1741943359376,"y":3868.891845703125,"z":35.53545379638672},"model":1992927314,"maxDistance":2,"lockSound":"door_bolt","auto":true}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-1-8', '{"unlockSound":"door_bolt","heading":214,"state":1,"doors":false,"coords":{"x":1738.9617919921876,"y":3873.65283203125,"z":35.17351913452148},"lockSound":"door_bolt","maxDistance":2,"model":-955088610}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-1', '{"unlockSound":"door_bolt","heading":34,"state":1,"doors":false,"coords":{"x":1736.52392578125,"y":3879.364990234375,"z":38.17094802856445},"lockSound":"door_bolt","maxDistance":2,"model":-541267183}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-2', '{"unlockSound":"door_bolt","heading":34,"state":1,"doors":false,"coords":{"x":1737.686767578125,"y":3877.618408203125,"z":38.17094802856445},"lockSound":"door_bolt","maxDistance":2,"model":-541267183}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-3', '{"unlockSound":"door_bolt","heading":34,"state":1,"doors":false,"coords":{"x":1740.904052734375,"y":3873.30419921875,"z":38.07783508300781},"lockSound":"door_bolt","maxDistance":2,"model":1807171785}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-4', '{"unlockSound":"door_bolt","heading":124,"state":1,"doors":false,"coords":{"x":1738.1214599609376,"y":3875.303466796875,"z":38.17094802856445},"lockSound":"door_bolt","maxDistance":2,"model":-541267183}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-5', '{"unlockSound":"door_bolt","heading":214,"state":1,"doors":false,"coords":{"x":1737.1363525390626,"y":3874.104736328125,"z":38.16779327392578},"lockSound":"door_bolt","maxDistance":2,"model":-541267183}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-6', '{"unlockSound":"door_bolt","heading":124,"state":1,"doors":false,"coords":{"x":1734.7320556640626,"y":3873.046875,"z":38.17094802856445},"lockSound":"door_bolt","maxDistance":2,"model":-541267183}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-7', '{"unlockSound":"door_bolt","heading":34,"state":1,"doors":false,"coords":{"x":1733.337646484375,"y":3868.28076171875,"z":38.07783508300781},"lockSound":"door_bolt","maxDistance":2,"model":1807171785}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-8', '{"heading":214,"state":1,"doors":false,"coords":{"x":1731.610595703125,"y":3883.602783203125,"z":38.07291793823242},"maxDistance":2,"model":1807171785}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-9', '{"unlockSound":"door_bolt","heading":214,"state":1,"doors":false,"coords":{"x":1729.4854736328126,"y":3882.185791015625,"z":38.07291793823242},"lockSound":"door_bolt","maxDistance":2,"model":1807171785}');
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES (DEFAULT, 'Sandy Houses 18-2-10', '{"unlockSound":"door_bolt","heading":214,"state":1,"doors":false,"coords":{"x":1738.3631591796876,"y":3883.226318359375,"z":38.13893890380859},"lockSound":"door_bolt","maxDistance":2,"model":-955088610}');
```
{% endtab %}

{% tab title="⚙️ Installation Guide" %}
#### Step 1 — Download the Resource

Place `cfx_prompt_sandy_houses_part1` in your server’s `/resources` folder.

#### Step 2 — Add to `server.cfg`

```plaintext
start cfx_prompt_sandy_houses_part1
```

#### Step 3 — Install MapData (if required)

Make sure you have the correct **Sandy MapData** installed.\
See [MapData Documentation](https://prompt-studio.gitbook.io/prompt-studio/sandy-maps/sandy-mapdata).

#### Step 4 — Restart Server

Visit the location in-game and ensure interiors load correctly.

***

Enjoy the **Sandy Houses** experience — cozy, flexible, and designed for realistic roleplay.
{% endtab %}
{% endtabs %}
