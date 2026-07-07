# 👺 4 Dragons Casino & Triad HQ

A fully reimagined tribute to the **legendary Four Dragons Casino** from GTA: San Andreas — built from the ground up for FiveM.

This massive custom interior spans **3 levels:**

* **Public Casino Floor** — Open for all visitors to enjoy
* **VIP Hallways** — Private rooms, management offices, and exclusive access for upper-class visitors
* **Underground Triad HQ** — A fully illegal operation hidden behind a secretive entrance

{% updates format="full" %}
{% update date="2026-06-08" tags="script" %}
## <i class="fa-cards">:cards:</i> Added Casino Script

We have partnered with [Override Studio](https://override.studio/) to bring the seamless casino experience directly into your server.&#x20;

All map owners and subscribers now have access to the <mark style="color:$danger;">**limited**</mark> version of the casino script that allows to play games inside the Chinese Casino Map.

<i class="fa-memo-circle-info" style="color:blue;">:memo-circle-info:</i> **Read More:** [https://override.studio/docs/casino/installation](https://override.studio/docs/casino/installation)

<i class="fa-youtube" style="color:$danger;">:youtube:</i> [Video Showcase](https://youtu.be/MmvJSSHhUOE)
{% endupdate %}

{% update date="2026-06-08" tags="script" %}
## <i class="fa-poker-chip">:poker-chip:</i> Added Texas Hold'em Script

We also took our time to create a completely custom Texas Hold'em Script for the Chinese Casino map.

Users can use /pokercreator in order to create their own **custom** locations in their houses, different interiors and so on. Powered by a Chinese Casino (meaning the Texas Holdem <mark style="color:$danger;">**will not work without**</mark> Casino Map)

<i class="fa-youtube" style="color:$danger;">:youtube:</i> [Video Showcase](https://youtu.be/MmvJSSHhUOE)

<i class="fa-memo-circle-info" style="color:$primary;">:memo-circle-info:</i> **Read More:** [#texas-holdem](4-dragons-casino-and-triad-hq.md#texas-holdem "mention")
{% endupdate %}
{% endupdates %}



The interior is packed with **secrets and surprises** - hidden passages, escape routes, and a **members-only parking garage** with elevator access straight to the Triad HQ.

**3 toggleable VIP game rooms** — despawn the default props and place your own casino games or minigames. Comes with a built-in **dancer spawning system** with configurable payment.

Uses **standard GTA Diamond Casino props**, making it compatible with **any casino script** — including

* [**Override Studio Casino** ](https://override.studio/products/7323602)(use coupon "nihao" for 30% off)
* [**rcore Casino**](https://store.rcore.cz/package/5156878) (use coupon "RCORE-PROMPT-10-OFF" for 10% off)&#x20;
* Please reach out to us if you made your casino script compatible with this map :heart:



**Multi-framework support** with auto-detection - QBCore, QBox, ESX, Standalone.

{% embed url="https://youtu.be/XA69K_uRDDU" %}

{% embed url="https://youtu.be/QbBGG8JRMDE" %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### <i class="fa-download" style="color:$warning;">:download:</i> Download the resource from the [CFX Portal](https://portal.cfx.re/assets/created-assets?page=1\&sort=asset.id\&direction=desc\&search=Prompt%27s+-+Chinese+Casino+%7C+Secret+Triad+HQ).

After downloading, **you will get a folder named:**

```
prompt_chinese_casino
```

Drag and drop the downloaded folder inside your resources directory.\
When done, the full path should look like this:

<pre><code><strong>resources/prompt_chinese_casino
</strong></code></pre>
{% endstep %}

{% step %}
#### <i class="fa-folder-open" style="color:$warning;">:folder-open:</i> Open your `server.cfg` and add this line:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_chinese_casino
</strong></code></pre>

Save the file once done.
{% endstep %}

{% step %}
### <i class="fa-gear-code" style="color:$warning;">:gear-code:</i> Config

**Open `config.lua`** and adjust settings to your liking [#configuration](4-dragons-casino-and-triad-hq.md#configuration "mention").  Framework is **auto-detected** (QBCore, QBox, ESX). No extra setup needed unless you use a custom money system.
{% endstep %}

{% step %}
### <i class="fa-bottle-baby" style="color:$warning;">:bottle-baby:</i>Install Depencencies

| Dependency          | Required | Notes                                                                                           |
| ------------------- | -------- | ----------------------------------------------------------------------------------------------- |
| `ox_lib`            | Yes      | Required to use elevator and other script systems                                               |
| `ox_target`         | No       | Optional targeting system. Auto-detected. Falls back to E-key / `lib.zones.box` if not present. |
| `qb-target`         | No       | Alternative targeting system. Auto-detected via `Config.interactionMode`.                       |
| QBCore / QBox / ESX | No       | For payment and job restriction. Auto-detected. Standalone also supported.                      |
{% endstep %}

{% step %}
### <i class="fa-door-open">:door-open:</i> Doortuning | **Garage Door Setup**

The casino's garage has an animated door that requires **DoorTuning** registration to function properly.

Download the [Prompt's DoorTuning resource](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+DoorTuning) from the CFX Portal — it already includes the casino garage door entry

**or add these lines**

```xml
<Item>
   	  <ModelName>i45pt_ch_c_garage_gatedoor</ModelName>
   	  <TuningName>SupermodGarage</TuningName>
  	</Item>
```

to you existing `doortuning.ymt` file
{% endstep %}

{% step %}
#### <i class="fa-repeat" style="color:$warning;">:repeat:</i>  **Restart your server** and verify:

<table><thead><tr><th>Location</th><th>Coordinates</th></tr></thead><tbody><tr><td><strong>Casino:</strong> </td><td><pre><code>299.97, 198.58, 105.19
</code></pre></td></tr></tbody></table>

If interior appear, installation is complete ✅\
[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

<i class="fa-film">:film:</i> **Cinema Interior (Relocated)**

<details>

<summary>What changed</summary>

The default GTA cinema interior (`v_cinema`) conflicts with the casino's underground level. We've **relocated it** to a new position inside the building instead of removing it entirely.

|                  | Coordinates                        |
| ---------------- | ---------------------------------- |
| **Old position** | `320.5892, 264.133545, 85.25568`   |
| **New position** | `320.5892, 264.133545, 70.1300659` |

The original IPL (`hei_hw1_02_interior_v_cinema_milo_`) is still disabled via script as a fallback to prevent conflicts. The cinema interior loads at its new position automatically.

{% hint style="info" %}
If you use the cinema interior in your server, update your teleport/door coordinates to the new position above.
{% endhint %}

</details>

#### <i class="fa-gear-code" style="color:$primary;">:gear-code:</i> Configuration

<details>

<summary>Payment &#x26; Framework</summary>

Framework is auto-detected on startup. Force one manually if needed.

```lua
Config.framework       = 'auto'       -- 'auto' | 'qbcore' | 'qbox' | 'esx' | 'standalone'
```

Payment is handled automatically per framework. For standalone or custom money systems, edit `server/custom_check.lua` with your own logic. Variables `source`, `amount`, and `reason` are already in scope.

</details>

<details>

<summary>Job Restriction</summary>

Gate access behind a framework job check. Disabled by default.

```lua
Config.access = {
    job = {
        enabled       = false,
        allowed       = { 'triad' },    -- list of allowed job names
        requireOnDuty = false,           -- QBCore/QBox only
    },
    item = {
        enabled  = false,
        name     = 'triad_keycard',      -- item required to access
    },
    custom = {
        enabled = false,                 -- define your own logic in server/custom_check.lua
    },
}
```

All enabled checks use **AND logic** — if both job and item are enabled, the player must pass both.

</details>

<details>

<summary>Interaction &#x26; UI</summary>

```lua
Config.interactionMode = 'auto'    -- 'auto' | 'ox_target' | 'qb-target' | 'ox_lib'
```

| Setting     | Effect                                                       |
| ----------- | ------------------------------------------------------------ |
| `auto`      | Detects ox\_target → qb-target → ox\_lib zones → raw markers |
| `ox_target` | Force ox\_target interaction                                 |
| `qb-target` | Force qb-target interaction                                  |
| `ox_lib`    | Force ox\_lib E-key zones                                    |

</details>

***

#### <i class="fa-cards" style="color:$success;">:cards:</i>  **Texas Hold'em**

<details>

<summary>Currency &#x26; Economy</summary>

```lua
Config.CurrencyMode    = 'auto'          -- 'auto' | 'money' | 'casino_chips'
Config.MoneyType       = 'cash'          -- 'cash' | 'bank' (when not using chips)
Config.CasinoChipsItem = 'casino_chips'  -- chip item used when the casino isn't running
```

| Mode           | Behavior                                                                                                    |
| -------------- | ----------------------------------------------------------------------------------------------------------- |
| `auto`         | Mirror the casino's live currency if it's running, else framework cash/bank, else free play. _Recommended._ |
| `money`        | Always cash/bank — works fully **without** the casino.                                                      |
| `casino_chips` | Force the chip item (casino's live name when present).                                                      |

Per-table override: `Config.Defaults.currencyMode = 'auto' | 'free' | 'money' | 'casino_chips'`.

</details>

<details>

<summary>Framework &#x26; Inventory</summary>

Auto-detected on startup. Inventories: `ox_inventory`, `qs-inventory`, `ps-inventory`, `codem-inventory`, `qb-inventory`.

```lua
Config.Framework = 'auto'   -- 'auto' | 'qbcore' | 'qbox' | 'esx' | 'standalone'
```

</details>

<details>

<summary>Free Play</summary>

Free chips, no real money — for standalone/demo servers. **Off in release.**

```lua
Config.Defaults.freePlay = false   -- true = free chips (also per-table via currencyMode = 'free')
```

</details>

<details>

<summary>Diagnostics</summary>

Read-only support snapshot — players run it in F8 and send the output:

```
/pokerdiag
```

Net-zero economy self-test (registered only when `Config.Debug = true`):

```
/pokertest
```

</details>

***

#### <i class="fa-elevator" style="color:$primary;">:elevator:</i> TP Elevator System

<details>

<summary>How it works</summary>

A two-point teleport elevator connecting the **private members-only parking garage** to the **Triad HQ underground level**.

1. Walk into the elevator zone at either level and interact.
2. Screen fades to black (500ms), holds for streaming (600ms), then fades back in.
3. Player is teleported to the other level.

| Level            | Location        | Z Height  |
| ---------------- | --------------- | --------- |
| **Garage Level** | Private parking | `105.543` |
| **Triad HQ**     | Underground     | `89.034`  |

Access is controlled by the same job/item/custom checks from the Configuration section above. If all checks are disabled, the elevator is open to everyone.

</details>

***

#### <i class="fa-dice" style="color:$danger;">:dice:</i> VIP Game Rooms (Entity Sets)

<details>

<summary>How it works</summary>

The casino has **3 VIP game rooms** with toggleable props. Each room can be activated or deactivated independently — despawn the default furniture to place your own casino games, minigames, or scripts.

| Room       | Entity Set  |
| ---------- | ----------- |
| VIP Room 1 | `vipgame01` |
| VIP Room 2 | `vipgame02` |
| VIP Room 3 | `vipgame03` |

**Toggle methods:**

* **In-game:** Walk into a VIP room and interact with the toggle zone
* **Server console:** `/entityset vipgame01`

Room states are **persistent** — saved to `data/entitysets_state.json` and survive server restarts. All clients see changes in real-time via GlobalState sync.

{% hint style="info" %}
This is where you place your casino script props. Despawn a VIP room, then use rcore Casino, Override Studio, or any other script to spawn game tables in the empty space.
{% endhint %}

</details>

***

#### <i class="fa-music" style="color:yellow;">:music:</i> Dancer System

<details>

<summary>Pole Dancers</summary>

3 pole dancer stations across the VIP rooms. Interact with a station to spawn a dancer.

```lua
Config.dancers.poleDancers = {
    cost     = 500,        -- price per dancer (0 = free)
    duration = 0,          -- seconds (0 = stays forever)
    model    = 's_f_y_stripper_01',
}
```

3 animation sets cycle automatically: `pd_dance_01`, `pd_dance_02`, `pd_dance_03`.

</details>

<details>

<summary>Private Dancers</summary>

3 private table locations for personal entertainment. Higher cost, timed duration.

```lua
Config.dancers.privateDancers = {
    cost     = 1000,       -- price per dancer
    duration = 300,        -- 5 minutes
}
```

3-part animation sequence: `priv_dance_p1` → `priv_dance_p2` → `priv_dance_p3`. Dancer auto-despawns when the timer expires.

</details>

<details>

<summary>Persistence</summary>

Dancer states are saved to `data/dancers_state.json` and survive server restarts. All spawns/despawns sync to all clients via GlobalState. Expired dancers are automatically cleaned up on resource start.

</details>

#### <i class="fa-chair" style="color:blue;">:chair:</i> Supplemental Info

<details>

<summary><strong>Custom Props</strong></summary>



### Seating

* `i45pt_ch_casino_barchair_01a`
* `i45pt_ch_casino_chair_01a`
* `i45pt_ch_casino_officechair_01a`
* `i45pt_ch_casino_sofa_01a`
* `i45pt_ch_casino_sofa_02a`
* `i45pt_ch_casino_sofa_02b`
* `i45pt_ch_casino_sofa_02c`
* `i45pt_ch_casino_sofa_03a`
* `i45pt_ch_ctr_bench_prop_01a`
* `i45pt_ctr_seat_tea_01`

### Tables / counters

* `i45pt_ch_casino_table_01a`
* `i45pt_ch_casino_table_02a`
* `i45pt_ch_casino_table_03a`
* `i45pt_ch_casino_conftable_01a`
* `i45pt_ch_casino_tabletop_01a`
* `i45pt_ch_casino_woodcounter_01a`
* `i45pt_ch_casino_woodcounter_01b`
* `i45pt_ctr_tables_tea`
* `prompt_chinese_teapot`
* `prompt_chinese_tea_cup`

### Gambling props

* `i45pt_ch_casino_slotmachine_01a`
* `i45pt_ch_casino_gametable_01a`
* `i45pt_ch_casino_gametable_01b`
* `i45pt_ch_casino_gametable_01c`
* `i45pt_ch_casino_rulette_area`
* `prompt_china_casino_vw_prop_vw_luckywheel_01a`

### Cashier / money

* `i45pt_ch_casino_prop_till_01`
* `i45pt_ch_casino_prop_tillpay_01`
* `i45pt_ch_casino_prop_token_trolly`

### Screens / electronics

* `i45pt_ch_casino_tv_main`
* `i45pt_ch_casino_screen`
* `i45pt_ctr_prop_security_monitor`
* `i45pt_ctr_prop_security_monitor_screens`
* `i45pt_ctr_prop_tv_01a`

### Office / desk

* `i45pt_ch_casino_desk_set_01a`
* `i45pt_ch_casino_prop_deskoffice_01a`
* `i45pt_ctr_prop_deskcttv_01`

### Utility / appliances

* `i45pt_ch_casino_berrmachine_01a`
* `i45pt_ch_casino_kitchen_fridge_01`
* `i45pt_ch_casino_kitchen_grill_01a`
* `i45pt_ch_casino_laundry_machine_01`

### Maybe needed

* `i45pt_ch_casino_box_prop_01a`
* `i45pt_ch_casino_box_01a`
* `i45pt_ch_casino_box_01b`
* `i45pt_ch_casino_box_01c`
* `i45pt_ch_casino_woodshelf_01a`
* `i45pt_ch_casino_woodshelf_01b`
* `i45pt_ctr_prop_box_01a`
* `i45pt_ctr_prop_shelf_01a`

</details>

<details>

<summary><strong>Doorlock SQL (60 doors)</strong></summary>

Community-submitted [`ox_doorlock`](https://github.com/overextended/ox_doorlock) positions for all three levels. Import into your database and restart `ox_doorlock`. Door IDs use the range **2313–2372** — renumber if those are taken in your table.

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(2852, '4 Dragons E-1', '{"state":1,"maxDistance":2,"coords":{"x":299.77532958984377,"y":204.7957763671875,"z":104.64308166503906},"doors":[{"coords":{"x":299.15020751953127,"y":205.5425567626953,"z":104.64308166503906},"heading":310,"model":1888438146},{"coords":{"x":300.4004211425781,"y":204.04898071289063,"z":104.64308166503906},"heading":310,"model":272205552}]}'),
	(2853, '4 Dragons E-2', '{"state":1,"maxDistance":2,"coords":{"x":301.6708984375,"y":203.4922637939453,"z":104.639892578125},"doors":[{"coords":{"x":300.7557678222656,"y":203.82534790039063,"z":104.639892578125},"heading":340,"model":1888438146},{"coords":{"x":302.5860595703125,"y":203.1591796875,"z":104.639892578125},"heading":340,"model":272205552}]}'),
	(2854, '4 Dragons E-3', '{"state":1,"maxDistance":2,"coords":{"x":303.95916748046877,"y":203.2717742919922,"z":104.64308166503906},"doors":[{"coords":{"x":303.000244140625,"y":203.10183715820313,"z":104.64308166503906},"heading":10,"model":1888438146},{"coords":{"x":304.9180908203125,"y":203.44171142578126,"z":104.64308166503906},"heading":10,"model":272205552}]}'),
	(2855, '4 Dragons E-4', '{"state":1,"heading":250,"maxDistance":2,"model":-774905227,"coords":{"x":317.33489990234377,"y":297.0877380371094,"z":105.6104507446289},"doors":false,"hideUi":true}'),
	(2856, '4 Dragons E-5', '{"state":1,"heading":70,"maxDistance":2,"model":1606121205,"coords":{"x":287.8294677734375,"y":310.7496032714844,"z":104.44112396240235},"doors":false,"auto":true}'),
	(2857, '4 Dragons 1-1', '{"state":1,"maxDistance":2,"coords":{"x":307.46588134765627,"y":219.3436279296875,"z":103.37159729003906},"doors":[{"coords":{"x":309.15545654296877,"y":218.72850036621095,"z":103.37159729003906},"heading":340,"model":1347067975},{"coords":{"x":305.77630615234377,"y":219.958740234375,"z":103.3716049194336},"heading":340,"model":-451524128}]}'),
	(2858, '4 Dragons 1-2', '{"state":1,"maxDistance":2,"coords":{"x":335.9305725097656,"y":281.84686279296877,"z":97.91573333740235},"doors":[{"coords":{"x":334.7210693359375,"y":282.3009948730469,"z":97.91573333740235},"heading":339,"model":-971357243},{"coords":{"x":337.14007568359377,"y":281.3927307128906,"z":97.91573333740235},"heading":159,"model":-971357243}]}'),
	(2859, '4 Dragons 1-3', '{"state":1,"heading":339,"maxDistance":2,"model":181091411,"coords":{"x":318.6636962890625,"y":288.13970947265627,"z":97.90916442871094},"doors":false,"hideUi":true}'),
	(2860, '4 Dragons 1-4', '{"state":1,"maxDistance":2,"coords":{"x":281.9024658203125,"y":321.380126953125,"z":92.48456573486328},"doors":[{"coords":{"x":281.52764892578127,"y":320.3818359375,"z":92.48456573486328},"heading":249,"model":-1240554578},{"coords":{"x":282.2773132324219,"y":322.3784484863281,"z":92.48456573486328},"heading":69,"model":-1240554578}]}'),
	(2861, '4 Dragons 1-5', '{"state":1,"maxDistance":2,"coords":{"x":313.9703063964844,"y":309.0483093261719,"z":104.54113006591797},"doors":[{"coords":{"x":314.6750793457031,"y":308.7917785644531,"z":104.54113006591797},"heading":160,"model":-1240156945},{"coords":{"x":313.2655334472656,"y":309.3048400878906,"z":104.54113006591797},"heading":340,"model":-1240156945}],"auto":true}'),
	(2862, '4 Dragons -1-1', '{"state":1,"heading":159,"maxDistance":2,"model":-2037125726,"coords":{"x":303.2580871582031,"y":247.0953826904297,"z":93.03118896484375},"doors":false}'),
	(2863, '4 Dragons -1-2', '{"state":1,"heading":159,"maxDistance":2,"model":-1479997661,"coords":{"x":297.52874755859377,"y":242.36614990234376,"z":92.92080688476563},"doors":false}'),
	(2864, '4 Dragons -1-3', '{"state":1,"heading":48,"maxDistance":2,"model":-1479997661,"coords":{"x":301.966552734375,"y":237.9559783935547,"z":93.8359146118164},"doors":false}'),
	(2865, '4 Dragons -1-4', '{"state":1,"heading":339,"maxDistance":2,"model":-1479997661,"coords":{"x":308.2054443359375,"y":218.92071533203126,"z":93.82503509521485},"doors":false}'),
	(2866, '4 Dragons -1-5', '{"state":1,"heading":249,"maxDistance":2,"model":-1520917551,"coords":{"x":302.3948669433594,"y":219.41104125976563,"z":94.2270736694336},"doors":false}'),
	(2867, '4 Dragons -1-6', '{"state":1,"heading":91,"maxDistance":2,"model":-1479997661,"coords":{"x":324.2381896972656,"y":229.67459106445313,"z":93.8351058959961},"doors":false}'),
	(2868, '4 Dragons -1-7', '{"state":1,"heading":159,"maxDistance":2,"model":-1479997661,"coords":{"x":329.2530517578125,"y":230.44882202148438,"z":92.92362976074219},"doors":false}'),
	(2869, '4 Dragons -1-8', '{"state":1,"heading":159,"maxDistance":2,"model":-2037125726,"coords":{"x":328.3010559082031,"y":237.6923370361328,"z":93.03118896484375},"doors":false}'),
	(2870, '4 Dragons -1-9', '{"state":1,"heading":48,"maxDistance":2,"model":-1479997661,"coords":{"x":357.08941650390627,"y":234.23135375976563,"z":92.9186019897461},"doors":false}'),
	(2871, '4 Dragons -1-10', '{"state":1,"maxDistance":2,"coords":{"x":350.484130859375,"y":237.98196411132813,"z":92.90713500976563},"doors":[{"coords":{"x":349.56182861328127,"y":237.07814025878907,"z":92.90713500976563},"heading":44,"model":-971357243},{"coords":{"x":351.40643310546877,"y":238.88577270507813,"z":92.90713500976563},"heading":224,"model":-971357243}]}'),
	(2872, '4 Dragons -1-11', '{"state":1,"heading":228,"maxDistance":2,"model":601770753,"coords":{"x":358.22479248046877,"y":228.03440856933595,"z":92.93177032470703},"doors":false}'),
	(2873, '4 Dragons -1-12', '{"state":1,"heading":228,"maxDistance":2,"model":601770753,"coords":{"x":355.2314453125,"y":224.69873046875,"z":92.93177032470703},"doors":false}'),
	(2874, '4 Dragons -1-13', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":361.7763977050781,"y":243.154541015625,"z":92.9329605102539},"doors":false}'),
	(2875, '4 Dragons -1-14', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":364.73602294921877,"y":251.0489501953125,"z":92.91815948486328},"doors":false}'),
	(2876, '4 Dragons -1-15', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":367.5681457519531,"y":258.595947265625,"z":92.91815948486328},"doors":false}'),
	(2877, '4 Dragons -1-16', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":370.5143127441406,"y":266.33038330078127,"z":92.91854858398438},"doors":false}'),
	(2878, '4 Dragons -1-17', '{"state":1,"maxDistance":2,"coords":{"x":364.1876525878906,"y":272.20904541015627,"z":92.91932678222656},"doors":[{"coords":{"x":364.5625,"y":273.20733642578127,"z":92.91932678222656},"heading":69,"model":-1240554578},{"coords":{"x":363.81280517578127,"y":271.21075439453127,"z":92.91932678222656},"heading":249,"model":-1240554578}]}'),
	(2879, '4 Dragons -1-18', '{"state":1,"heading":159,"maxDistance":2,"model":-1479997661,"coords":{"x":342.7220458984375,"y":284.71673583984377,"z":92.93014526367188},"doors":false}'),
	(2880, '4 Dragons -1-19', '{"state":1,"maxDistance":2,"coords":{"x":299.8144226074219,"y":296.37969970703127,"z":92.91932678222656},"doors":[{"coords":{"x":300.18927001953127,"y":297.37799072265627,"z":92.91932678222656},"heading":69,"model":-1240554578},{"coords":{"x":299.4395751953125,"y":295.38140869140627,"z":92.91932678222656},"heading":249,"model":-1240554578}]}'),
	(2881, '4 Dragons -1-20', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":288.5132751464844,"y":289.1357421875,"z":92.92011260986328},"doors":false}'),
	(2882, '4 Dragons -1-21', '{"state":1,"heading":339,"maxDistance":2,"model":-1479997661,"coords":{"x":287.9805908203125,"y":294.8419189453125,"z":92.91943359375},"doors":false}'),
	(2883, '4 Dragons -1-22', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":284.8910217285156,"y":279.4886779785156,"z":92.92011260986328},"doors":false}'),
	(2884, '4 Dragons -1-23', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":282.2326354980469,"y":272.40863037109377,"z":92.92304229736328},"doors":false}'),
	(2885, '4 Dragons -1-24', '{"state":1,"heading":85,"maxDistance":2,"model":-1479997661,"coords":{"x":280.2535705566406,"y":265.2146911621094,"z":92.91999053955078},"doors":false}'),
	(2886, '4 Dragons -1-25', '{"state":1,"heading":104,"maxDistance":2,"model":-1479997661,"coords":{"x":280.60107421875,"y":258.1936950683594,"z":92.92034149169922},"doors":false}'),
	(2887, '4 Dragons -1-26', '{"state":1,"heading":124,"maxDistance":2,"model":-1479997661,"coords":{"x":283.482666015625,"y":251.27589416503907,"z":92.92155456542969},"doors":false}'),
	(2888, '4 Dragons -1-27', '{"state":1,"heading":124,"maxDistance":2,"model":601770753,"coords":{"x":282.2583312988281,"y":244.18618774414063,"z":92.93021392822266},"doors":false}'),
	(2889, '4 Dragons -1-28', '{"state":1,"heading":124,"maxDistance":2,"model":601770753,"coords":{"x":284.7969055175781,"y":240.49267578125,"z":92.93021392822266},"doors":false}'),
	(2890, '4 Dragons -1-29', '{"state":1,"maxDistance":2,"coords":{"x":330.7259521484375,"y":281.0399475097656,"z":90.91191101074219},"doors":[{"coords":{"x":331.93487548828127,"y":280.5860290527344,"z":90.91191101074219},"heading":159,"model":-971357243},{"coords":{"x":329.51702880859377,"y":281.4938659667969,"z":90.91191101074219},"heading":339,"model":-971357243}]}'),
	(2891, '4 Dragons -1-30', '{"state":1,"maxDistance":2,"coords":{"x":345.01202392578127,"y":296.6722412109375,"z":92.90802001953125},"doors":[{"coords":{"x":345.2645263671875,"y":297.3441467285156,"z":92.91007995605469},"heading":69,"model":-198090717},{"coords":{"x":344.759521484375,"y":296.0003662109375,"z":92.90595245361328},"heading":69,"model":-1700451060}],"hideUi":true}'),
	(2892, '4 Dragons -2-1', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":335.9372863769531,"y":300.74432373046877,"z":89.19331359863281},"doors":false}'),
	(2893, '4 Dragons -2-2', '{"state":1,"heading":339,"maxDistance":2,"model":-1479997661,"coords":{"x":327.0096435546875,"y":300.8387145996094,"z":89.19293975830078},"doors":false}'),
	(2894, '4 Dragons -2-3', '{"state":1,"heading":69,"maxDistance":2,"model":-1479997661,"coords":{"x":324.7711181640625,"y":300.688232421875,"z":89.19293975830078},"doors":false}'),
	(2895, '4 Dragons -2-4', '{"state":1,"heading":339,"maxDistance":2,"model":-1479997661,"coords":{"x":320.48468017578127,"y":303.2886962890625,"z":89.19293975830078},"doors":false}'),
	(2896, '4 Dragons -2-5', '{"state":1,"heading":249,"maxDistance":2,"model":-1479997661,"coords":{"x":321.5022277832031,"y":310.4333801269531,"z":89.19831848144531},"doors":false}'),
	(2897, '4 Dragons -2-6', '{"state":1,"heading":249,"maxDistance":2,"model":-1479997661,"coords":{"x":318.58245849609377,"y":311.5296936035156,"z":89.19831848144531},"doors":false}'),
	(2898, '4 Dragons -2-7', '{"state":1,"heading":249,"maxDistance":2,"model":-1479997661,"coords":{"x":324.33184814453127,"y":317.969482421875,"z":89.19692993164063},"doors":false}'),
	(2899, '4 Dragons -2-8', '{"state":1,"heading":249,"maxDistance":2,"model":-1479997661,"coords":{"x":328.83795166015627,"y":316.27691650390627,"z":89.19224548339844},"doors":false}'),
	(2900, '4 Dragons -2-9', '{"state":1,"heading":249,"maxDistance":2,"model":-1479997661,"coords":{"x":326.1446838378906,"y":322.797607421875,"z":89.1968002319336},"doors":false}'),
	(2901, '4 Dragons -2-10', '{"state":1,"maxDistance":2,"coords":{"x":329.4447021484375,"y":324.7364501953125,"z":89.18840789794922},"doors":[{"coords":{"x":328.4464111328125,"y":325.1112976074219,"z":89.18840789794922},"heading":159,"model":-1240554578},{"coords":{"x":330.4430236816406,"y":324.36163330078127,"z":89.18840789794922},"heading":339,"model":-1240554578}]}'),
	(2902, '4 Dragons -2-11', '{"state":1,"heading":339,"maxDistance":2,"model":-1479997661,"coords":{"x":313.2784729003906,"y":305.99444580078127,"z":89.19293975830078},"doors":false}'),
	(2903, '4 Dragons -2-12', '{"state":1,"maxDistance":2,"coords":{"x":307.34112548828127,"y":310.7919921875,"z":89.18840789794922},"doors":[{"coords":{"x":306.96630859375,"y":309.7936706542969,"z":89.18840789794922},"heading":249,"model":-1240554578},{"coords":{"x":307.7159729003906,"y":311.790283203125,"z":89.18840789794922},"heading":69,"model":-1240554578}]}'),
	(2904, '4 Dragons -2-13', '{"state":1,"maxDistance":2,"coords":{"x":308.15386962890627,"y":306.90234375,"z":88.03445434570313},"doors":[{"coords":{"x":308.8559875488281,"y":306.6387023925781,"z":88.03445434570313},"heading":159,"model":-1240156945},{"coords":{"x":307.45172119140627,"y":307.16595458984377,"z":88.03445434570313},"heading":339,"model":-1240156945}],"auto":true}'),
	(2905, '4 Dragons -3-1', '{"state":1,"heading":159,"maxDistance":2,"model":-1013515293,"coords":{"x":315.5712585449219,"y":325.51336669921877,"z":85.40650939941406},"doors":false}'),
	(2906, '4 Dragons -3-2', '{"state":1,"heading":159,"maxDistance":2,"model":-1013515293,"coords":{"x":310.8903503417969,"y":327.2709655761719,"z":85.40650939941406},"doors":false}'),
	(2907, '4 Dragons -3-3', '{"state":1,"heading":339,"maxDistance":2,"model":-1013515293,"coords":{"x":310.8836669921875,"y":331.1547546386719,"z":85.40650939941406},"doors":false}'),
	(2908, '4 Dragons -3-4', '{"state":1,"heading":339,"maxDistance":2,"model":-1013515293,"coords":{"x":315.5645751953125,"y":329.397216796875,"z":85.40650939941406},"doors":false}'),
	(2909, '4 Dragons -3-5', '{"state":1,"maxDistance":2,"coords":{"x":287.57061767578127,"y":311.44537353515627,"z":85.459228515625},"doors":[{"coords":{"x":288.56890869140627,"y":311.070556640625,"z":85.459228515625},"heading":339,"model":-1240554578},{"coords":{"x":286.5722961425781,"y":311.8202209472656,"z":85.459228515625},"heading":159,"model":-1240554578}]}'),
	(2910, '4 Dragons -3-6', '{"state":1,"maxDistance":2,"coords":{"x":280.61981201171877,"y":316.4676513671875,"z":85.44142150878906},"doors":[{"coords":{"x":281.0345458984375,"y":317.46734619140627,"z":85.44142150878906},"heading":69,"model":419599283},{"coords":{"x":280.2050476074219,"y":315.4679260253906,"z":85.44142150878906},"heading":249,"model":419599283}]}'),
	(2911, '4 Dragons -3-7', '{"state":1,"maxDistance":2,"coords":{"x":277.127197265625,"y":307.16583251953127,"z":85.44142150878906},"doors":[{"coords":{"x":276.7124328613281,"y":306.1661071777344,"z":85.44142150878906},"heading":249,"model":419599283},{"coords":{"x":277.54193115234377,"y":308.16552734375,"z":85.44142150878906},"heading":69,"model":419599283}]}');
```

</details>

***

**Need help?** Open a ticket on our support Discord with the resource name, console errors, and a screenshot.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
