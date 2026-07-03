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

<summary><strong>Doorlock SQL</strong></summary>

<pre class="language-sql"><code class="lang-sql"><strong>Door Positions are not yet collected for this project.
</strong><strong>If you have collected doors in the sql, please send them to us - 
</strong><strong>we will give u 20% discount for next purchase
</strong><strong>
</strong><strong>Index for the doors starts from: 2309
</strong></code></pre>

</details>

***

**Need help?** Open a ticket on our support Discord with the resource name, console errors, and a screenshot.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
