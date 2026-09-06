# 🍔 Horny's Burgers (4 locations)

## Prompt’s Horny's Burgers

{% embed url="https://portal.cfx.re/assets/granted-assets?page=1&sort=asset.updated_at&direction=asc&search=Prompt%27s+-+Gym+%28with+Animations%29" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**
{% endembed %}

{% embed url="https://www.youtube.com/watch?v=YvIBmrv-oYI" %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Install the map

Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Gym+%28with+Animations%29).

After downloading, **you will get a zip with a folder named**:

<pre><code><strong>prompt_hornys || prompt_hornys_sandy_only (depends on your version)
</strong></code></pre>

Drag and drop the downloaded folder inside your `resources` directory.\
When done, the full path should look like this:

<pre><code><strong>resources/prompt_hornys || resources/prompt_hornys (depends on your version)
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Restart your server

If the map has been started successfully -> you will see the Map Data message in the end of the server console.\
Please Follow the directions of those messages (for **Paleto** and **Sandy** Map Datas).

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

### Additional Information

{% tabs %}
{% tab title="Compatibility & Locations" %}
**✅ Compatible Resources**

* [**MXC Utility Kitchen**](https://forum.cfx.re/t/utility-kitchen/5292505) — full cooking gameplay for all four locations. **Ready-made config included** → see the **Utility Kitchen** tab.

***

&#x20;**Horny's Locations**

{% hint style="info" %}
To remove a specific Horny's location:

1. Navigate to the `/stream` directory.
2. Delete the folder for the desired horny's location.
{% endhint %}

| Area            | Coordinates              |
| --------------- | ------------------------ |
| Sandy Shores    | 1847.24, 3767.86, 33.82  |
| Mirror Park     | 1240.78, -370.39, 69.92  |
| Ghetto Location | -187.98, -1428.51, 33.27 |
| Paleto Bay      | -362.35, 6050.57, 33.38  |

> The Sandy Shores Horny's and Paleto Bay Horny's integrates seamlessly with other Sandy Shores and Paleto Maps maps using the shared map data system.
{% endtab %}

{% tab title="Utility Kitchen" %}
Horny's is **ready to go** with [**MXC Utility Kitchen**](https://forum.cfx.re/t/utility-kitchen/5292505) — a full kitchen layout for all four locations ships below, so you paste one config entry and every restaurant has working fryers, griddles and prep tables.

Works with **any version** of Horny's.

{% stepper %}
{% step %}
#### Step 1 — Open the kitchen config

In your `utility_kitchen` resource, open `configs/kitchens.lua` and find the `Config.Kitchens` table.
{% endstep %}

{% step %}
#### Step 2 — Paste the entry below

Add the `["prompt-hornys"]` entry inside `Config.Kitchens`, alongside any kitchens you already have.
{% endstep %}

{% step %}
#### Step 3 — Set the job

At the top of the entry, uncomment the `jobs` line and put the job name your server uses for the restaurant. Leave it empty to let anyone use the kitchen.
{% endstep %}

{% step %}
#### Step 4 — Restart

Restart `utility_kitchen`. Every location gets its kitchen — fryers, griddle, drop tables, patty warmers and bins — in place.
{% endstep %}
{% endstepper %}

<details>

<summary><strong>Horny's kitchen config (all 4 locations)</strong></summary>

```lua
-- Prompt Studio Horny's x MXC utility_kitchen
-- Paste into Config.Kitchens (configs/kitchens.lua).
-- Covers all 4 locations: mirror-park, sandy, ghetto, paleto-bay

    ["prompt-hornys"] = {
        jobs = {
            -- ["hornys"] = 0, -- [job_name] = job_grade
            --
            -- OR
            --
            -- "hornys", -- job_name
        },
        required = {
            resource = "prompt_hornys"
        },
        exec = function()
            -- MIRROR-PARK  (MLO 1243.696, -358.959, 71.091  yaw -15.00)
            CreateBin(vec3(1250.742, -354.145, 68.211), vec3(0.000, 0.000, 74.876), {tableHidden = false})
            CreateEntityHider(vec3(1249.165, -356.253, 69.122), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(1249.525, -356.533, 69.201), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_b"})
            CreateEntityHider(vec3(1248.960, -356.482, 69.122), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(1248.008, -355.798, 69.150), vec3(0, 0, 0), {model = "prop_cs_clothes_box"})
            CreateEntityHider(vec3(1251.416, -352.652, 69.125), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1251.444, -352.497, 69.125), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1251.503, -352.342, 69.135), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1251.654, -352.417, 69.125), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(1251.626, -352.560, 69.125), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(1251.578, -352.713, 69.125), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1251.748, -352.716, 69.125), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1251.795, -352.553, 69.125), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(1252.018, -352.515, 69.133), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1251.947, -352.757, 69.133), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1252.150, -352.811, 69.133), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1252.221, -352.570, 69.133), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1252.381, -352.633, 69.120), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(1252.583, -352.770, 69.120), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(1252.425, -352.904, 69.120), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(1246.370, -355.343, 69.122), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(1246.770, -355.441, 69.136), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(1251.911, -352.907, 68.841), vec3(0, 0, 0), {model = "i45pt_hornys_kitchen_tool_grill_01"})
            CreateGriddle(vec3(1251.925, -352.748, 68.728), vec3(0.000, 0.000, 75.491), {tableHidden = false})
            CreateBurgerTable(vec3(1249.276, -356.254, 68.547), vec3(0.000, 0.000, -104.805), {tableHidden = true})
            CreateEntityHider(vec3(1247.622, -355.583, 69.218), vec3(0, 0, 0), {model = "i45pt_hornys_food_box_01b"})
            CreateEntityHider(vec3(1247.671, -355.978, 69.159), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(1247.671, -355.978, 69.112), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(1247.220, -355.787, 69.110), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01b"})
            CreateEntityHider(vec3(1248.463, -355.959, 69.121), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreateDropTable(vec3(1247.640, -355.795, 68.553), vec3(0.000, 0.000, -104.430), {tableHidden = true})
            CreateEntityHider(vec3(1246.518, -355.553, 68.862), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_fryer"})
            CreateFryer(vec3(1246.511, -355.436, 68.949), vec3(0.000, 0.000, 75.470), {tableHidden = false})
            CreateEntityHider(vec3(1253.255, -352.861, 69.146), vec3(0, 0, 0), {model = "v_ind_cftrayfillets"})
            CreateMeatContainer(vec3(1252.978, -352.909, 69.168), vec3(0.000, 0.000, 74.384), {tableHidden = false})
            CreateMeatContainer(vec3(1253.266, -353.023, 69.177), vec3(0.000, 0.000, 74.384), {tableHidden = false})
            CreateSpatula(vec3(1252.686, -352.975, 69.114), vec3(0.000, 0.000, 164.948), {tableHidden = false})
            CreateSpatula(vec3(1251.092, -351.965, 69.119), vec3(0.000, 0.000, 83.761), {tableHidden = false})
            CreateEntityHider(vec3(1253.825, -353.823, 69.110), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreatePattyWarmer(vec3(1253.859, -353.824, 69.206), vec3(0.000, 0.000, -13.146), {tableHidden = false})

            -- SANDY  (MLO 1851.913, 3783.590, 35.117  yaw -60.00)
            CreateBin(vec3(1860.299, 3782.012, 32.236), vec3(0.000, 0.000, 29.876), {tableHidden = false})
            CreateEntityHider(vec3(1857.693, 3781.637, 33.147), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(1857.750, 3781.184, 33.226), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_b"})
            CreateEntityHider(vec3(1857.387, 3781.620, 33.147), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(1857.197, 3782.777, 33.175), vec3(0, 0, 0), {model = "prop_cs_clothes_box"})
            CreateEntityHider(vec3(1861.831, 3782.591, 33.150), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1861.961, 3782.681, 33.150), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1862.112, 3782.749, 33.160), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1862.166, 3782.589, 33.150), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(1862.045, 3782.508, 33.150), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(1861.903, 3782.434, 33.150), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1862.021, 3782.311, 33.150), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(1862.169, 3782.393, 33.150), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(1862.354, 3782.263, 33.158), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1862.133, 3782.142, 33.158), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1862.238, 3781.960, 33.158), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1862.459, 3782.080, 33.158), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(1862.527, 3781.922, 33.145), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(1862.573, 3781.683, 33.145), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(1862.367, 3781.700, 33.145), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(1856.361, 3784.257, 33.147), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(1856.574, 3783.904, 33.161), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(1862.001, 3782.061, 32.866), vec3(0, 0, 0), {model = "i45pt_hornys_kitchen_tool_grill_01"})
            CreateGriddle(vec3(1862.123, 3782.164, 32.753), vec3(0.000, 0.000, 30.491), {tableHidden = false})
            CreateBurgerTable(vec3(1857.771, 3781.558, 32.572), vec3(0.000, 0.000, -149.805), {tableHidden = true})
            CreateEntityHider(vec3(1857.076, 3783.202, 33.243), vec3(0, 0, 0), {model = "i45pt_hornys_food_box_01b"})
            CreateEntityHider(vec3(1856.831, 3782.888, 33.184), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(1856.831, 3782.888, 33.137), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(1856.648, 3783.342, 33.135), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01b"})
            CreateEntityHider(vec3(1857.405, 3782.341, 33.146), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreateDropTable(vec3(1856.939, 3783.039, 32.578), vec3(0.000, 0.000, -149.430), {tableHidden = true})
            CreateEntityHider(vec3(1856.317, 3784.003, 32.887), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_fryer"})
            CreateFryer(vec3(1856.395, 3784.091, 32.974), vec3(0.000, 0.000, 30.470), {tableHidden = false})
            CreateEntityHider(vec3(1862.984, 3781.143, 33.171), vec3(0, 0, 0), {model = "v_ind_cftrayfillets"})
            CreateMeatContainer(vec3(1862.754, 3781.305, 33.193), vec3(0.000, 0.000, 29.384), {tableHidden = false})
            CreateMeatContainer(vec3(1862.877, 3781.021, 33.202), vec3(0.000, 0.000, 29.384), {tableHidden = false})
            CreateSpatula(vec3(1862.501, 3781.465, 33.139), vec3(0.000, 0.000, 119.948), {tableHidden = false})
            CreateSpatula(vec3(1862.088, 3783.306, 33.144), vec3(0.000, 0.000, 38.761), {tableHidden = false})
            CreateEntityHider(vec3(1862.707, 3780.060, 33.135), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreatePattyWarmer(vec3(1862.730, 3780.035, 33.231), vec3(0.000, 0.000, -58.146), {tableHidden = false})

            -- GHETTO  (MLO -176.523, -1439.892, 33.225  yaw -40.00)
            CreateBin(vec3(-168.103, -1438.506, 30.344), vec3(0.000, 0.000, 49.876), {tableHidden = false})
            CreateEntityHider(vec3(-170.423, -1439.750, 31.255), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(-170.215, -1440.156, 31.334), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_b"})
            CreateEntityHider(vec3(-170.706, -1439.871, 31.255), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(-171.279, -1438.849, 31.283), vec3(0, 0, 0), {model = "prop_cs_clothes_box"})
            CreateEntityHider(vec3(-166.861, -1437.438, 31.258), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-166.770, -1437.309, 31.258), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-166.651, -1437.194, 31.268), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-166.546, -1437.326, 31.258), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(-166.632, -1437.443, 31.258), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(-166.740, -1437.562, 31.258), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-166.587, -1437.636, 31.258), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-166.476, -1437.508, 31.258), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(-166.258, -1437.568, 31.266), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-166.424, -1437.757, 31.266), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-166.263, -1437.892, 31.266), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-166.097, -1437.704, 31.266), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-165.979, -1437.829, 31.253), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(-165.853, -1438.038, 31.253), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(-166.053, -1438.093, 31.253), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(-172.572, -1437.744, 31.255), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(-172.251, -1438.002, 31.269), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(-166.520, -1437.878, 30.974), vec3(0, 0, 0), {model = "i45pt_hornys_kitchen_tool_grill_01"})
            CreateGriddle(vec3(-166.440, -1437.740, 30.861), vec3(0.000, 0.000, 50.491), {tableHidden = false})
            CreateBurgerTable(vec3(-170.323, -1439.798, 30.680), vec3(0.000, 0.000, -129.805), {tableHidden = true})
            CreateEntityHider(vec3(-171.538, -1438.491, 31.351), vec3(0, 0, 0), {model = "i45pt_hornys_food_box_01b"})
            CreateEntityHider(vec3(-171.661, -1438.870, 31.292), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(-171.661, -1438.870, 31.245), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(-171.989, -1438.506, 31.243), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01b"})
            CreateEntityHider(vec3(-170.935, -1439.187, 31.254), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreateDropTable(vec3(-171.612, -1438.691, 30.686), vec3(0.000, 0.000, -129.430), {tableHidden = true})
            CreateEntityHider(vec3(-172.526, -1437.997, 30.995), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_fryer"})
            CreateFryer(vec3(-172.483, -1437.888, 31.082), vec3(0.000, 0.000, 50.470), {tableHidden = false})
            CreateEntityHider(vec3(-165.283, -1438.405, 31.279), vec3(0, 0, 0), {model = "v_ind_cftrayfillets"})
            CreateMeatContainer(vec3(-165.554, -1438.331, 31.301), vec3(0.000, 0.000, 49.384), {tableHidden = false})
            CreateMeatContainer(vec3(-165.341, -1438.556, 31.310), vec3(0.000, 0.000, 49.384), {tableHidden = false})
            CreateSpatula(vec3(-165.847, -1438.267, 31.247), vec3(0.000, 0.000, 139.948), {tableHidden = false})
            CreateSpatula(vec3(-166.864, -1436.678, 31.252), vec3(0.000, 0.000, 58.761), {tableHidden = false})
            CreateEntityHider(vec3(-165.173, -1439.517, 31.243), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreatePattyWarmer(vec3(-165.142, -1439.533, 31.339), vec3(0.000, 0.000, -38.146), {tableHidden = false})

            -- PALETO-BAY  (MLO -375.271, 6046.164, 33.500  yaw -135.00)
            CreateBin(vec3(-374.625, 6037.654, 30.620), vec3(0.000, 0.000, -45.124), {tableHidden = false})
            CreateEntityHider(vec3(-375.662, 6040.074, 31.531), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(-376.085, 6039.902, 31.610), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_b"})
            CreateEntityHider(vec3(-375.758, 6040.366, 31.531), vec3(0, 0, 0), {model = "i45pt_hornys_food_bag_s"})
            CreateEntityHider(vec3(-374.690, 6040.849, 31.559), vec3(0, 0, 0), {model = "prop_cs_clothes_box"})
            CreateEntityHider(vec3(-373.669, 6036.324, 31.534), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-373.549, 6036.223, 31.534), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-373.444, 6036.094, 31.544), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-373.585, 6036.001, 31.534), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(-373.695, 6036.096, 31.534), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(-373.803, 6036.214, 31.534), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-373.891, 6036.069, 31.534), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_03"})
            CreateEntityHider(vec3(-373.773, 6035.947, 31.534), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_01"})
            CreateEntityHider(vec3(-373.852, 6035.734, 31.542), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-374.026, 6035.917, 31.542), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-374.174, 6035.768, 31.542), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-374.001, 6035.586, 31.542), vec3(0, 0, 0), {model = "prop_cs_steak"})
            CreateEntityHider(vec3(-374.135, 6035.479, 31.529), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(-374.355, 6035.373, 31.529), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(-374.392, 6035.576, 31.529), vec3(0, 0, 0), {model = "i45pt_hornys_food_burgermeet_02"})
            CreateEntityHider(vec3(-373.477, 6042.040, 31.531), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(-373.762, 6041.742, 31.545), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_frye_mesh"})
            CreateEntityHider(vec3(-374.138, 6036.023, 31.250), vec3(0, 0, 0), {model = "i45pt_hornys_kitchen_tool_grill_01"})
            CreateGriddle(vec3(-374.007, 6035.931, 31.137), vec3(0.000, 0.000, -44.509), {tableHidden = false})
            CreateBurgerTable(vec3(-375.719, 6039.979, 30.956), vec3(0.000, 0.000, 135.195), {tableHidden = true})
            CreateEntityHider(vec3(-374.311, 6041.075, 31.627), vec3(0, 0, 0), {model = "i45pt_hornys_food_box_01b"})
            CreateEntityHider(vec3(-374.677, 6041.231, 31.568), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(-374.677, 6041.231, 31.521), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01a"})
            CreateEntityHider(vec3(-374.286, 6041.526, 31.519), vec3(0, 0, 0), {model = "i45pt_hornys_bag_stack_01b"})
            CreateEntityHider(vec3(-375.057, 6040.535, 31.530), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreateDropTable(vec3(-374.503, 6041.166, 30.962), vec3(0.000, 0.000, 135.570), {tableHidden = true})
            CreateEntityHider(vec3(-373.733, 6042.017, 31.271), vec3(0, 0, 0), {model = "i45pt_hornys_prop_tools_fryer"})
            CreateFryer(vec3(-373.628, 6041.964, 31.358), vec3(0.000, 0.000, -44.530), {tableHidden = false})
            CreateEntityHider(vec3(-374.770, 6034.836, 31.555), vec3(0, 0, 0), {model = "v_ind_cftrayfillets"})
            CreateMeatContainer(vec3(-374.673, 6035.100, 31.577), vec3(0.000, 0.000, -45.616), {tableHidden = false})
            CreateMeatContainer(vec3(-374.916, 6034.908, 31.586), vec3(0.000, 0.000, -45.616), {tableHidden = false})
            CreateSpatula(vec3(-374.584, 6035.386, 31.523), vec3(0.000, 0.000, 44.948), {tableHidden = false})
            CreateSpatula(vec3(-372.912, 6036.261, 31.528), vec3(0.000, 0.000, -36.239), {tableHidden = false})
            CreateEntityHider(vec3(-375.888, 6034.824, 31.519), vec3(0, 0, 0), {model = "i45pt_hornys_tray_01"})
            CreatePattyWarmer(vec3(-375.906, 6034.795, 31.615), vec3(0.000, 0.000, -133.146), {tableHidden = false})

        end
    },
```

</details>

{% hint style="info" %}
Tested on **QBCore + ox\_inventory** with `utility_kitchen` **1.0.13**. Other frameworks the script supports should work the same — the entry only places props and uses the script's own functions.
{% endhint %}
{% endtab %}

{% tab title="Doorlock SQL" %}


```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES

	-- Sandy Shores Horny
	(DEFAULT, 'Sandy Shores Horny E-1', '{"coords":{"x":1845.299560546875,"y":3779.7646484375,"z":33.48891067504883},"doors":[{"coords":{"x":1845.9287109375,"y":3778.628173828125,"z":33.48891067504883},"model":-285040094,"heading":120},{"coords":{"x":1844.6702880859376,"y":3780.9013671875,"z":33.48891067504883},"model":-951201095,"heading":300}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Shores Horny E-2', '{"coords":{"x":1848.681884765625,"y":3792.423583984375,"z":33.48908996582031},"doors":[{"coords":{"x":1849.8184814453126,"y":3793.052734375,"z":33.48908996582031},"model":-951201095,"heading":210},{"coords":{"x":1847.54541015625,"y":3791.79443359375,"z":33.48908996582031},"model":-285040094,"heading":30}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Shores Horny E-3', '{"coords":{"x":1859.7623291015626,"y":3787.63134765625,"z":33.32556915283203},"heading":303,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(DEFAULT, 'Sandy Shores Horny 1-1', '{"coords":{"x":1855.5821533203126,"y":3779.783935546875,"z":33.32556915283203},"heading":30,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(DEFAULT, 'Sandy Shores Horny 1-2', '{"coords":{"x":1857.3046875,"y":3787.066162109375,"z":33.32556915283203},"heading":30,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),

	-- Mirror Park Horny
	(DEFAULT, 'Mirror Park Horny E-1', '{"coords":{"x":1241.724853515625,"y":-366.34051513671877,"z":69.46353912353516},"doors":[{"coords":{"x":1240.476318359375,"y":-365.9818115234375,"z":69.46353912353516},"model":-951201095,"heading":345},{"coords":{"x":1242.973388671875,"y":-366.6992492675781,"z":69.46353912353516},"model":-285040094,"heading":165}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Mirror Park Horny E-2', '{"coords":{"x":1235.16552734375,"y":-354.9976806640625,"z":69.46371459960938},"doors":[{"coords":{"x":1234.8067626953126,"y":-356.2462158203125,"z":69.46371459960938},"model":-285040094,"heading":75},{"coords":{"x":1235.5242919921876,"y":-353.7491760253906,"z":69.46371459960938},"model":-951201095,"heading":255}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Mirror Park Horny E-3', '{"coords":{"x":1246.3890380859376,"y":-350.5511169433594,"z":69.3001937866211},"heading":348,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(DEFAULT, 'Mirror Park Horny 1-1', '{"coords":{"x":1248.982421875,"y":-359.0560607910156,"z":69.3001937866211},"heading":75,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(DEFAULT, 'Mirror Park Horny 1-2', '{"coords":{"x":1245.0509033203126,"y":-352.6887512207031,"z":69.3001937866211},"heading":75,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),

	-- Ghetto Horny
	(DEFAULT, 'Ghetto Horny E-1', '{"coords":{"x":-182.5804443359375,"y":-1432.696044921875,"z":31.59699249267578},"doors":[{"coords":{"x":-181.72769165039063,"y":-1431.716064453125,"z":31.59699249267578},"model":-951201095,"heading":230},{"coords":{"x":-183.43321228027345,"y":-1433.676025390625,"z":31.59699249267578},"model":-285040094,"heading":50}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Ghetto Horny E-2', '{"coords":{"x":-181.42938232421876,"y":-1445.748291015625,"z":31.59681320190429},"doors":[{"coords":{"x":-182.40931701660157,"y":-1444.8955078125,"z":31.59681320190429},"model":-951201095,"heading":320},{"coords":{"x":-180.449462890625,"y":-1446.60107421875,"z":31.59681320190429},"model":-285040094,"heading":140}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Ghetto Horny E-3', '{"coords":{"x":-170.5293426513672,"y":-1433.409423828125,"z":31.43347358703613},"heading":323,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(DEFAULT, 'Ghetto Horny 1-1', '{"coords":{"x":-171.7733154296875,"y":-1442.21337890625,"z":31.43347358703613},"heading":50,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(DEFAULT, 'Ghetto Horny 1-2', '{"coords":{"x":-172.64537048339845,"y":-1434.78125,"z":31.43347358703613},"heading":50,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),

	-- Paleto Bay Horny
	(DEFAULT, 'Paleto Bay Horny E-1', '{"coords":{"x":-367.57537841796877,"y":6051.5703125,"z":31.87233734130859},"doors":[{"coords":{"x":-366.67352294921877,"y":6050.6357421875,"z":31.87233734130859},"model":-951201095,"heading":135},{"coords":{"x":-368.4772644042969,"y":6052.50537109375,"z":31.87233734130859},"model":-285040094,"heading":315}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Paleto Bay Horny E-2', '{"coords":{"x":-380.67828369140627,"y":6051.5615234375,"z":31.87215805053711},"doors":[{"coords":{"x":-381.61322021484377,"y":6050.65966796875,"z":31.87215805053711},"model":-285040094,"heading":45},{"coords":{"x":-379.74334716796877,"y":6052.46337890625,"z":31.87215805053711},"model":-951201095,"heading":225}],"maxDistance":2,"state":1}'),
	(DEFAULT, 'Paleto Bay Horny E-3', '{"coords":{"x":-369.3363342285156,"y":6039.62744140625,"z":31.70881843566894},"heading":228,"doors":false,"maxDistance":2,"state":1,"model":-1746981862}'),
	(DEFAULT, 'Paleto Bay Horny 1-1', '{"coords":{"x":-377.99847412109377,"y":6041.6337890625,"z":31.70881843566894},"heading":315,"doors":false,"maxDistance":2,"state":1,"model":1710114873}'),
	(DEFAULT, 'Paleto Bay Horny 1-2', '{"coords":{"x":-370.5185852050781,"y":6041.85498046875,"z":31.70881843566894},"heading":315,"doors":false,"maxDistance":2,"state":1,"model":1710114873}');
```
{% endtab %}

{% tab title="Custom Props" %}
## Props that you may want to use in your script



1. Seating & Furniture

* `i45pt_hornys_chair_01`
* `i45pt_hornys_seat_01`
* `i45pt_hornys_seat_02`
* `i45pt_hornys_chairbar_01`

2\. Food & Ingredients

* `i45pt_hornys_food_frites`
* `i45pt_hornys_food_burger_pack`
* `i45pt_hornys_food_burger_pack_02`
* `i45pt_hornys_food_burger_pack_03`
* `i45pt_hornys_food_sandwitch_pack_01`
* `i45pt_hornys_food_misc`
* `i45pt_hornys_food_burgermeet_01` (Meat)
* `i45pt_hornys_food_burgermeet_02` (Meat)
* `i45pt_hornys_food_burgermeet_03` (Meat)
* `i45pt_hornys_food_bag_b`
* `i45pt_hornys_food_bag_s`

3\. Script Props (Tills, Trays, Tools, Bins)

* `i45pt_hornys_till_01`
* `i45pt_hornys_tillpay`
* `i45pt_hornys_prop_bin_01`
* `i45pt_hornys_cutlery`
* `i45pt_hornys_tray_01`
* `i45pt_hornys_food_bs_tray_01`
* `i45pt_hornys_food_bs_tray_02`
* `i45pt_hornys_prop_tools_fryer`
* `i45pt_hornys_kitchen_tool_grill_01`
* `i45pt_hornys_prop_tools_frye_mesh`
{% endtab %}

{% tab title="Troubleshooting & Support" %}
**Common Issues**

* Have gta objects overlapping with the map? -> Usually this means you are using wrong map data or have a conflict with other maps around.

**Need Help?**

Open a ticket with:

* Resource name: **prompt\_hornys**
* Server artifact version
* Console error logs (if any)

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endtab %}
{% endtabs %}
