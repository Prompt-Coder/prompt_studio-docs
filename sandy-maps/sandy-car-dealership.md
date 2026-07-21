# 🏎️ Sandy Car Dealership

{% embed url="https://fivem.prompt-mods.com/package/6254445" %}

{% embed url="https://www.youtube.com/watch?v=qSmwE2k9VJQ" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

The **Sandy Car Dealership** is a premium MLO map for FiveM. Its detailed showroom, comfy lounge zones, and business-ready layout support car sales, customer meetups, and job scripts. Realistic props and visuals make it ideal for any RP server.

***

#### 📍 Map Position

**1909, 3727.43, 33.06**

***

<details>

<summary>🛠️ Chairs and Props</summary>

**Seating / Interior Props**

* `v_res_j_dinechair`
* `v_res_study_chair`
* `prop_couch_sm2_07`
* `v_ind_meatbench`
* `prop_toilet_01`
* `prop_couch_lg_06`
* `int_cars_couch`

</details>

***

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f6aa">🚪</span> Doorlock System</summary>



Supports **ox\_doorlock**. Add this SQL:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (DEFAULT, 'Sandy Shores Classic Cars Door 1044', '{"maxDistance":2.0,"doors":false,"heading":-90.0,"model":"int_cars_staff_door_02","coords":{"x":-5.83804,"y":8.02756,"z":-1.1127398},"state":1}'),
    (DEFAULT, 'Sandy Shores Classic Cars Door 1045', '{"maxDistance":2.0,"doors":false,"heading":0.0,"model":"int_cars_staff_door_02","coords":{"x":9.801943,"y":-0.47020632,"z":-1.09695435},"state":1}'),
    (DEFAULT, 'Sandy Shores Classic Cars Door 1046', '{"maxDistance":2.0,"doors":false,"heading":180.0,"model":"int_cars_staff_door_01","coords":{"x":-0.7217621,"y":12.1200924,"z":-1.09695},"state":1}'),
    (DEFAULT, 'Sandy Shores Classic Cars Door 1047', '{"maxDistance":2.0,"doors":false,"heading":0.0,"model":"v_ilev_ss_door04","coords":{"x":4.86157227,"y":8.911865,"z":-1.09695435},"state":1}'),
    (DEFAULT, 'Sandy Shores Classic Cars Door 1048', '{"maxDistance":2.0,"doors":false,"heading":180.0,"model":"v_ilev_cs_door","coords":{"x":4.306383,"y":13.1777344,"z":-1.09695435},"state":1}'),
    (DEFAULT, 'Sandy Shores Classic Cars Door 1049', '{"maxDistance":2.0,"doors":false,"heading":-90.0,"model":"int_cars_staff_door_01","coords":{"x":8.060387,"y":6.80915,"z":-1.09695},"state":1}'),
    (DEFAULT, 'Sandy Shores Classic Cars Door 1050', '{"maxDistance":2.0,"doors":false,"heading":45.0,"model":"int_cars_gardoor","coords":{"x":-2.743375,"y":-2.74345684,"z":-0.757312834},"state":1}');
```

</details>

***

<details>

<summary>🚀 Installation Guide</summary>

1. Drop the folder `prompt_sandy_classic_car_dealership` in your `resources`
2. In `server.cfg`:

```cfg
start prompt_sandy_classic_car_dealership
```

3. Import the doorlock SQL above
4. Install MapData – see MapData Docs
5. Restart your server and verify map at **1909, 3727.43, 33.06**

</details>

***

Need help? Contact support and enjoy **Sandy Car Dealership** on your FiveM server! 🚗
