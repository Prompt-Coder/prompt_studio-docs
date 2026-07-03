# 🧺 Sandy Market

## Sandy Shores Market

{% embed url="https://fivem.prompt-mods.com/package/XXXXXXX" %}

{% embed url="https://www.youtube.com/watch?v=XXhdG0iWpbw" %}

The **Sandy Shores Market** brings a vibrant commercial hub to your FiveM server — blending certified storefronts, a community-run farmers market, and optional stall-based expansions through a built-in IPL management system.

Designed for immersive and flexible economy roleplay, players can buy groceries, camping gear, prescriptions, or sell their own goods and services (both legal and illegal). The market includes an accessible backroom for secure storage and a manager’s office.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

#### 📍 Map Position

**1921.21, 3816.21, 32.3**

***

<details>

<summary>🏪 Market Stores</summary>

* 🚗 **Autoshop**
* 💊 **Pharmacy**
* 🖥️ **Digital Den**
* 🛒 **Grocery Store**
* 🔫 **Ammu-Nation Outdoors** (camping/hunting supplies)
* 📦 B**ackroom storage & Staff-only Management room**

</details>

<details>

<summary>🌾 Farmers Market IPL Script</summary>

Custom IPL Manager script allows toggling pre-made stall setups.

**Included IPLs:**

```lua
Config.IPLs = {
    { name = "Arcade Stalls",     ipl = "box55_s_market_stalls_arcade" },
    { name = "Boat Stalls",       ipl = "box55_s_market_stalls_boats" },
    { name = "Clothing Stalls",   ipl = "box55_s_market_stalls_clothing" },
    { name = "Crafting Stalls",   ipl = "box55_s_market_stalls_crafting" },
    { name = "Junk Stalls",       ipl = "box55_s_market_stalls_junk" },
    { name = "Plant Stalls",      ipl = "box55_s_market_stalls_plants" },
    { name = "Tattoo Stalls",     ipl = "box55_s_market_stalls_tattoo" },
    { name = "Vending Stalls",    ipl = "box55_s_market_stalls_vending" },
    { name = "Wholesale Stalls",  ipl = "box55_s_market_stalls_wholesale" }
}
```

**Script Usage:**

* 🧭 Menu Access: `/marketipls` (top-right, title: Sandy Market IPL Manager)
* 🔧 Fallback: IPLs auto-load if ox\_lib is missing
* 🔐 Permissions: Unrestricted by default, configurable to admin-only

</details>

<details>

<summary>🛠️ Requirements</summary>

* [sandy-mapdata.md](sandy-mapdata.md "mention")

</details>

<details>

<summary>🪑 Custom Props &#x26; Interactables</summary>

## 🪑 Custom Props & Interactables — Sandy Shores Market

### 📍 Seats (Vanilla, sit/lay)

* **Chairs (sit):**
  * `v_corp_bk_chair3`
  * `v_ret_gc_chair01`
  * `prop_off_chair_03`

***

### 🧭 Simple Categories (for quick reference)

#### Counters & Shelving

`i45pt_sandymarket_room06_counter`, `i45pt_sandymarket_dd_counter`, `i45pt_sandymarket_as_counter`,\
`i45pt_sandymarket_counterset_01/02/03`, `i45pt_sandymarket_ph_shelf_01`, `i45pt_sandymarket_room06_cupboard_ped`

#### Retail Racks & Clothes

`i45pt_sandymarket_room06_clothset_01/02/03/05`, `i45pt_sandymarket_room06_cloth_stand`,\
`i45pt_sandymarket_room06_boot_stand`, `i45pt_sandymarket_room06_basket_rack`

#### Food/Fridge/Small Items

`i45pt_sandymarket_fridge_01`, `i45pt_sandymarket_fridgeset_01`, `i45pt_sandymarket_room06_donuts`,\
`i45pt_sandymarket_main_donuts_box`, `i45pt_sandymarket_counter_paper`, `i45pt_sandymarket_ph_bootles_drug_01`,\
`i45pt_sandymarket_oil_01/02/03/04`

#### Electronics & Boxes

`i45pt_sandymarket_dd_laptop_set_01`, `i45pt_sandymarket_dd_tablets`, `i45pt_sandymarket_dd_phones`,\
`i45pt_sandymarket_dd_monitors`, `i45pt_sandymarket_dd_cardbox_01`,\
`i45pt_sandymarket_dd_box_m_01a/b/c`, `i45pt_sandymarket_dd_box_b_01a/b/c`,\
`i45pt_sandymarket_dd_cardboxes`, `i45pt_sandymarket_dd_cardboxes_02`

#### Ammu/Outdoors & Tools

`i45pt_sandymarket_amm_furniture`, `i45pt_sandymarket_amm_sell_details`, `i45pt_sandymarket_amm_boxes`,\
`i45pt_sandymarket_amm_weapons`, `i45pt_sandymarket_amm_toolboxes`, `i45pt_sandymarket_amm_hats`,\
`i45pt_sandymarket_as_workbench_tools`, `i45pt_sandymarket_as_oil_bootles`,\
`i45pt_sandymarket_prop_musket`, `i45pt_sandymarket_prop_singleshot`,\
`i45pt_sandymarket_prop_compactgl`, `i45pt_sandymarket_prop_hatchet`

#### Security & Misc

`i45_sandymarket_gate_alarm_01`, `i45pt_sandymarket_room06_mainfance`, `i45pt_sandymarket_room06_blind`,\
`i45pt_sandymarket_prop_climatronic`, `i45pt_sandymarket_main_coffee_counter`

### 🧩 Custom Props (FULL LIST)

> These are the Sandy Market custom archetypes that have `dynamic flag`. Use them for placement/interactions in your scripts.

```
i45pt_sandymarket_room07_fake_w
i45pt_sandymarket_fridge_01
i45pt_sandymarket_counterset_01
i45pt_sandymarket_counterset_02
i45pt_sandymarket_room06_basket_rack
i45pt_sandymarket_room06_mainfance
i45_sandymarket_gate_alarm_01
i45pt_sandymarket_room06_counter
i45pt_sandymarket_room06_donuts
i45pt_sandymarket_counterset_fruits
i45pt_sandymarket_counterset_03
i45pt_sandymarket_room06_boxes_det
i45pt_sandymarket_room06_cloth_detail
i45pt_sandymarket_room06_sub_lamps
i45pt_sandymarket_room06_pillar_clothdet
i45pt_sandymarket_room06_clothset_01
i45pt_sandymarket_room06_clothset_02
i45pt_sandymarket_room06_clothset_03
i45pt_sandymarket_room06_boot_stand
i45pt_sandymarket_room06_clothset_05
i45pt_sandymarket_room06_cloth_stand
i45pt_sandymarket_room06_cupboard_ped
i45pt_sandymarket_room06_blind
i45pt_sandymarket_prop_climatronic
i45pt_sandymarket_counter_paper
i45pt_sandymarket_dd_counter
i45pt_sandymarket_dd_laptop_set_01
i45pt_sandymarket_dd_cardbox_01
i45pt_sandymarket_dd_cardboxes_02
i45pt_sandymarket_dd_cardboxes
i45pt_sandymarket_dd_consoleshowcase
i45pt_sandymarket_dd_tablets
i45pt_sandymarket_dd_phones
i45pt_sandymarket_dd_monitors
i45pt_sandymarket_as_counter
i45pt_sandymarket_as_furniture_01
i45pt_sandymarket_as_boxes
i45pt_sandymarket_as_oil_bootles
i45pt_sandymarket_as_workbench_tools
i45pt_sandymarket_amm_furniture
i45pt_sandymarket_amm_sell_details
i45pt_sandymarket_amm_boxes
i45pt_sandymarket_amm_weapons
i45pt_sandymarket_amm_toolboxes
i45pt_sandymarket_amm_hats
i45pt_sandymarket_ph_drugs_boxes
i45pt_sandymarket_ph_shelf_01
i45pt_sandymarket_ph_furniture
i45pt_sandymarket_ph_bootles_drug_01
i45pt_sandymarket_main_coffee_counter
i45pt_sandymarket_main_donuts_box
i45pt_sandymarket_fridgeset_01
i45pt_sandymarket_oil_01
i45pt_sandymarket_oil_02
i45pt_sandymarket_oil_03
i45pt_sandymarket_oil_04
i45pt_sandymarket_dd_box_m_01a
i45pt_sandymarket_dd_box_m_01b
i45pt_sandymarket_dd_box_m_01c
i45pt_sandymarket_dd_box_b_01a
i45pt_sandymarket_dd_box_b_01b
i45pt_sandymarket_dd_box_b_01c
i45pt_sandymarket_prop_musket
i45pt_sandymarket_prop_singleshot
i45pt_sandymarket_prop_compactgl
i45pt_sandymarket_prop_hatchet
```

***

</details>

