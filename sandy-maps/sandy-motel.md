# 🛎️ Sandy Motel

{% embed url="https://store.prompt-mods.com/store/" %}

## Sandy Shores **Motel** :bellhop:

The **Sandy Motel** is a feature-rich and immersive map designed to elevate roleplay in the heart of Sandy Shores. With 26 motel rooms and hidden surprises like a secret poker room and tunnel-access jail cells, it’s perfect for civilian, crime, or police storylines alike.



{% embed url="https://youtu.be/qX13YKdOXMw" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 Map Position

Located at coordinates: **1628.05, 3787.72, 35.57**

***

<details>

<summary>🏨 Main Features</summary>



* 🛏️ 26 Motel Rooms – Each includes furniture and seating props
* 🛎️ Reception with Bar & Lounge – Social hub with drinks and casual seating
* 🧑‍💼 Manager's Office – Accessible on the second floor, perfect for administrative RP
* ♠️ Secret Poker Room – Hidden behind dynamic props
* 🚪 Secret Tunnel – Leads to an underground area with jail cells



### 🧱 Reworked Exterior

* Designed for immersive motel parking and lounging
* Outdoor seating areas with benches and tables
* Realistic asset placement for casual or criminal RP

</details>

<details>

<summary>🪑 Custom Props &#x26; Interactables</summary>

📍 In Motel Rooms

* **Prop to lay**: `prompt_sandy_motel_room_bed`
* **Props to sit**:
  * `prompt_sandy_motel_couche`
  * `prompt_sandy_motel_room_chair`
  * `prop_toilet_01`
* **Misc**:
  * `prompt_sandy_motel_room_wardrobe`
  * `prop_tv_flat_michael`
  * `prop_laptop_02_closed`

#### 📍 Exterior

* **Props to sit**:
  * `prop_bench_01a`
  * `prop_table_02_chr`
  * `prop_chateau_chair_01`
  * `hei_heist_din_chair_05`
* **ATM**: `prop_atm_01`

#### 📍 Reception Area

* **Props to sit**:
  * `prompt_sandy_motel_rec_rest_chair_chester`
  * `prompt_sandy_motel_rec_rest_bench`
  * `prompt_sandy_motel_rec_corner`
  * `prompt_sandy_motel_rec_sofa_left`
  * `prompt_sandy_motel_rec_armchair`
  * `prompt_sandy_motel_rec_rest_chair`
  * `prompt_sandy_motel_rec_rest_barstool`
* **Misc**:
  * `prop_pooltable_02`
  * `prop_pool_rack_01`
  * `prompt_sandy_motel_rec_tablemenu`

#### 📍 Manager's Office (Second Floor)

* **Props to sit**:
  * `prompt_sandy_motel_rec_sofa`
  * `prompt_sandy_motel_rec_armchair`
  * `chuz_is_poker_chair_motel`
  * `ch_prop_casino_chair_01c`

***

### 🕳️ Secret Doors

* `chuz_is_shelf_door_pocker_b`
* `chuz_is_old_mirror_poker_b`

</details>

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f6aa">🚪</span>Doorlock System</summary>



This map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Doorlock Configuration**

Add the following SQL lines to your database to configure the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (1117, 'Sandy Shores Motel G-1', '{"maxDistance":2,"doors":false,"coords":{"x":1616.4639892578126,"y":3787.65478515625,"z":35.05494689941406},"state":1,"heading":218,"model":718415028}'),
    (1118, 'Sandy Shores Motel G-2', '{"maxDistance":2,"doors":false,"coords":{"x":1612.069091796875,"y":3784.28759765625,"z":35.05494689941406},"state":1,"heading":218,"model":718415028}'),
    (1119, 'Sandy Shores Motel G-3', '{"maxDistance":2,"doors":false,"coords":{"x":1607.6707763671876,"y":3780.892822265625,"z":35.05494689941406},"state":1,"heading":218,"model":718415028}'),
    (1120, 'Sandy Shores Motel G-4', '{"maxDistance":2,"doors":false,"coords":{"x":1603.28515625,"y":3777.527587890625,"z":35.05494689941406},"state":1,"heading":218,"model":718415028}'),
    (1121, 'Sandy Shores Motel G-5', '{"maxDistance":2,"doors":false,"coords":{"x":1584.8594970703126,"y":3763.412353515625,"z":35.05878067016601},"state":1,"heading":218,"model":718415028}'),
    (1122, 'Sandy Shores Motel G-6', '{"maxDistance":2,"doors":false,"coords":{"x":1579.904296875,"y":3759.614501953125,"z":35.05878067016601},"state":1,"heading":217,"model":718415028}'),
    (1123, 'Sandy Shores Motel G-7', '{"maxDistance":2,"doors":false,"coords":{"x":1623.28125,"y":3774.53125,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1124, 'Sandy Shores Motel G-8', '{"maxDistance":2,"doors":false,"coords":{"x":1618.3240966796876,"y":3770.7275390625,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1125, 'Sandy Shores Motel G-9', '{"maxDistance":2,"doors":false,"coords":{"x":1613.3477783203126,"y":3766.9091796875,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1126, 'Sandy Shores Motel G-10', '{"maxDistance":2,"doors":false,"coords":{"x":1608.3729248046876,"y":3763.091796875,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1127, 'Sandy Shores Motel G-11', '{"maxDistance":2,"doors":false,"coords":{"x":1603.40185546875,"y":3759.27734375,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1128, 'Sandy Shores Motel G-12', '{"maxDistance":2,"doors":false,"coords":{"x":1598.4222412109376,"y":3755.456298828125,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1129, 'Sandy Shores Motel G-13', '{"maxDistance":2,"doors":false,"coords":{"x":1593.4525146484376,"y":3751.642822265625,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1130, 'Sandy Shores Motel G-14', '{"maxDistance":2,"doors":false,"coords":{"x":1588.8453369140626,"y":3748.107666015625,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1131, 'Sandy Shores Motel G-15', '{"maxDistance":2,"doors":false,"coords":{"x":1584.32421875,"y":3744.637939453125,"z":35.04315185546875},"state":1,"heading":38,"model":718415028}'),
    (1132, 'Sandy Shores Motel G-16', '{"maxDistance":2,"doors":[{"coords":{"x":1577.6634521484376,"y":3747.125244140625,"z":35.13037109375},"model":-1087242187,"heading":128},{"coords":{"x":1576.1572265625,"y":3749.08837890625,"z":35.13037109375},"model":-1087242187,"heading":308}],"coords":{"x":1576.910400390625,"y":3748.10693359375,"z":35.13037109375},"state":1}'),
    (1133, 'Sandy Shores Motel G-17', '{"maxDistance":2,"doors":false,"coords":{"x":1573.8060302734376,"y":3740.1240234375,"z":35.13277816772461},"state":1,"heading":37,"model":-2094971262}'),
    (1134, 'Sandy Shores Motel 1-1', '{"maxDistance":2,"doors":false,"coords":{"x":1616.4639892578126,"y":3787.65478515625,"z":38.65202713012695},"state":1,"heading":218,"model":718415028}'),
    (1135, 'Sandy Shores Motel 1-2', '{"maxDistance":2,"doors":false,"coords":{"x":1612.09619140625,"y":3784.30712890625,"z":38.65202713012695},"state":1,"heading":218,"model":718415028}'),
    (1136, 'Sandy Shores Motel 1-3', '{"maxDistance":2,"doors":false,"coords":{"x":1607.700927734375,"y":3780.92578125,"z":38.65202713012695},"state":1,"heading":218,"model":718415028}'),
    (1137, 'Sandy Shores Motel 1-4', '{"maxDistance":2,"doors":false,"coords":{"x":1603.243408203125,"y":3777.501220703125,"z":38.65202713012695},"state":1,"heading":218,"model":718415028}'),
    (1138, 'Sandy Shores Motel 1-5', '{"maxDistance":2,"doors":false,"coords":{"x":1582.2303466796876,"y":3761.370361328125,"z":38.65202713012695},"state":1,"heading":218,"model":718415028}'),
    (1139, 'Sandy Shores Motel 1-6', '{"maxDistance":2,"doors":false,"coords":{"x":1577.269775390625,"y":3757.58642578125,"z":38.65202713012695},"state":1,"heading":218,"model":718415028}'),
    (1140, 'Sandy Shores Motel 1-7', '{"maxDistance":2,"doors":false,"coords":{"x":1572.290283203125,"y":3753.769775390625,"z":38.65202713012695},"state":1,"heading":218,"model":718415028}'),
    (1141, 'Sandy Shores Motel 1-8', '{"maxDistance":2,"doors":false,"coords":{"x":1623.2734375,"y":3774.52490234375,"z":38.65088653564453},"state":1,"heading":38,"model":718415028}'),
    (1142, 'Sandy Shores Motel 1-9', '{"maxDistance":2,"doors":false,"coords":{"x":1618.3192138671876,"y":3770.723388671875,"z":38.65088653564453},"state":1,"heading":38,"model":718415028}'),
    (1143, 'Sandy Shores Motel 1-10', '{"maxDistance":2,"doors":false,"coords":{"x":1613.355224609375,"y":3766.914306640625,"z":38.65088653564453},"state":1,"heading":38,"model":718415028}'),
    (1144, 'Sandy Shores Motel 1-11', '{"doors":false,"state":1,"coords":{"x":1608.390625,"y":3763.10498046875,"z":38.65088653564453},"model":718415028,"maxDistance":2,"heading":38}'),
    (1145, 'Sandy Shores Motel 1-12', '{"doors":false,"state":1,"coords":{"x":1603.4102783203126,"y":3759.283447265625,"z":38.65088653564453},"model":718415028,"maxDistance":2,"heading":38}'),
    (1146, 'Sandy Shores Motel 1-13', '{"doors":false,"state":1,"coords":{"x":1598.4281005859376,"y":3755.46044921875,"z":38.65088653564453},"model":718415028,"maxDistance":2,"heading":38}'),
    (1147, 'Sandy Shores Motel 1-14', '{"doors":false,"state":1,"coords":{"x":1593.4371337890626,"y":3751.630859375,"z":38.65088653564453},"model":718415028,"maxDistance":2,"heading":38}'),
    (1148, 'Sandy Shores Motel 1-15', '{"doors":false,"state":1,"coords":{"x":1588.4732666015626,"y":3747.822021484375,"z":38.65088653564453},"model":718415028,"maxDistance":2,"heading":38}'),
    (1149, 'Sandy Shores Motel 1-16', '{"doors":false,"state":1,"coords":{"x":1583.494384765625,"y":3744.00146484375,"z":38.6529655456543},"model":718415028,"maxDistance":2,"heading":38}'),
    (1150, 'Sandy Shores Motel 1-17', '{"doors":[{"model":-1087242187,"coords":{"x":1575.7420654296876,"y":3745.677001953125,"z":38.70522689819336},"heading":128},{"model":-1087242187,"coords":{"x":1574.2257080078126,"y":3747.640380859375,"z":38.70522689819336},"heading":308}],"state":1,"coords":{"x":1574.98388671875,"y":3746.65869140625,"z":38.70522689819336},"maxDistance":2}'),
    (1151, 'Sandy Shores Motel 1-18', '{"doors":false,"state":1,"coords":{"x":1571.0679931640626,"y":3748.385498046875,"z":38.72258758544922},"model":-738528475,"maxDistance":2,"heading":37}'),
    (1152, 'Sandy Shores Motel 1-19', '{"doors":false,"state":1,"coords":{"x":1575.3251953125,"y":3742.169921875,"z":38.75629806518555},"model":-2094971262,"maxDistance":2,"heading":38}'),
    (1153, 'Sandy Shores Motel Secret-1', '{"doors":false,"hideUi":true,"state":1,"coords":{"x":1578.78369140625,"y":3737.6748046875,"z":37.65934371948242},"model":476235269,"maxDistance":2,"heading":218}'),
    (1154, 'Sandy Shores Motel Secret-2', '{"doors":false,"hideUi":true,"state":1,"coords":{"x":1566.1815185546876,"y":3750.52099609375,"z":37.66647338867187},"model":1358887135,"maxDistance":2,"heading":219}'),
    (1155, 'Sandy Shores Motel B-1', '{"doors":false,"state":1,"coords":{"x":1590.11328125,"y":3740.513916015625,"z":31.5613784790039},"model":-1259829481,"maxDistance":2,"heading":38}'),
    (1156, 'Sandy Shores Motel B-2', '{"doors":false,"state":0,"coords":{"x":1593.438232421875,"y":3743.063720703125,"z":31.5802059173584},"model":-1259829481,"maxDistance":2,"heading":38}');
```

</details>

<details>

<summary>🚀 Installation Guide</summary>

To install the Sandy Mechanic map on your FiveM server, follow these steps:

1. **Download the Map Resource**
   * Ensure the **prompt\_sandy\_motel** resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start prompt_sandy_motel
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map at it's location to ensure everything is working correctly.

</details>

***

For further assistance, contact support. Enjoy using Sandy Motel on your FiveM server! 🚀
