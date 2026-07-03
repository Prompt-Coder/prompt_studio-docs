# 🏋️ Gym (5 locations)

## Prompt’s Gym

{% embed url="https://portal.cfx.re/assets/granted-assets?page=1&sort=asset.updated_at&direction=asc&search=Prompt%27s+-+Gym+%28with+Animations%29" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**
{% endembed %}

{% embed url="https://www.youtube.com/watch?v=IWREV1zvP2E" %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Install the map

Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Gym+%28with+Animations%29).

After downloading, **you will get a zip with a folder named**:

<pre><code><strong>prompt_gym || prompt_gym_sandy_only (depends on your version)
</strong></code></pre>

Drag and drop the downloaded folder inside your `resources` directory.\
When done, the full path should look like this:

<pre><code><strong>resources/prompt_gym || resources/prompt_gym_sandy_only (depends on your version)
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Optional: Install the required dependencies

**If you want** custom animated props to work -> You’ll need the following resources before starting the gym: ([you can download them from here](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Animations+Core))<br>

<pre><code><strong>ensure ox_lib
</strong><strong>ensure ox_target        # Optional but recommended
</strong><strong>ensure prompt_anim_core  # Animation Core 
</strong><strong>ensure prompt_gym
</strong></code></pre>

> ⚠️ **Important:** Keep this order — `ox_lib` → `ox_target` → `prompt_anim_core` → `prompt_gym`
{% endstep %}

{% step %}
#### Step 4 — Restart your server



**/**<i class="fa-terminal">:terminal:</i> **USE  `/GYMSETS`  COMMAND TO CHANGE ENTITY SETS** \
\
Once done, restart your server and join it.\
If the gym loads correctly, installation was successful ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

{% hint style="info" %}
💡 **Tip:** Always restart your server after adding new resources — especially those using custom animations or dependencies like `ox_lib`.
{% endhint %}

***

### Additional Information

{% tabs %}
{% tab title="Compatibility & Locations" %}
**✅ Compatible Resources**

* [**prompt\_anim\_core**](https://prompt-studio.gitbook.io/prompt-studio/~/revisions/V9pwsH3i6vJM3NYwB5Tq/scripts/animations-core) — Required for gym animations and equipment logic
* [**ox\_lib**](https://github.com/overextended/ox_lib/releases/tag/v3.30.6) — Handles animations, UI, and interaction menus
* [**ox\_target**](https://github.com/overextended/ox_target/releases/tag/v1.17.2) — Optional for third-eye interaction targeting

***

**🏋️ Gym Locations**

{% hint style="info" %}
To remove a specific gym location:

1. Navigate to the `/stream` directory.
2. Delete the folder for the desired gym location.
{% endhint %}

| Area         | Coordinates                          |
| ------------ | ------------------------------------ |
| Vinewood     | -479.409943, 279.249756, 85.6466751  |
| Chumash      | -3150.26074, 1179.92725, 22.5626068  |
| Grove Street | -175.031143, -1733.55249, 35.0033875 |
| Paleto Bay   | -94.63109, 6402.26758, 30.5214844    |
| Sandy Shores | 1754.25232, 3696.35962, 36.0192032   |

> The Sandy Shores gym integrates seamlessly with other Sandy Shores maps using the shared map data system.
{% endtab %}

{% tab title="Configuration & Developer API" %}
#### 🧩 Configuration Overview

All configuration is located in `prompt_gym/config.lua`.

| Feature            | Purpose                                          | Customizable |
| ------------------ | ------------------------------------------------ | ------------ |
| Permissions System | Control `/gymsets` access                        | ✅ Yes        |
| Entity Set Labels  | Menu display names                               | ✅ Yes        |
| Location Enabled   | Enable/disable gym locations                     | ✅ Yes        |
| Default Props      | Always visible equipment                         | ✅ Yes        |
| Entity Set Props   | Toggleable layouts (e.g., weights, martial arts) | ✅ Yes        |

**Example Structure**

```lua
GymLocations = {
   vinewood = {
       enabled = true,
       coords = vector3(-479.41, 279.25, 85.65),
       entitySets = {
           martialarts = false,
           weights1 = false
       },
       defaultProps = {
           { baseConfig = "speedbag", coords = ..., heading = ..., instanceName = "..." }
       },
       entitySetProps = {
           martialarts = {
               { baseConfig = "vin_chu", coords = ..., heading = ..., instanceName = "..." }
           },
           weights1 = {
               { baseConfig = "leg_press", coords = ..., heading = ..., instanceName = "..." }
           }
       }
   }
}
```

> ⚙️ This configuration defines **where** equipment spawns.\
> The actual animation and model data come from `prompt_anim_core/config.lua`.

***

#### 💻 Developer API (This is part of the Animations Core resource, but I show it here for conveniency)

You can read full script documentation here: <br>

**Available Events**

* `gym:exerciseStarted` — Triggered when a player starts using equipment
* `gym:exerciseCompleted` — Triggered when a player finishes an exercise

**Quick Example**

```lua
AddEventHandler('gym:exerciseStarted', function(data)
    print(string.format("%s started using %s", data.playerName, data.machineType))
end)

AddEventHandler('gym:exerciseCompleted', function(data)
    print(string.format("%s completed %s in %d seconds",
        data.playerName, data.machineType, data.duration))
end)
```

> 📚 See `api/EXAMPLES.md` and `api/README.md` for full documentation.\
> To test API events, set `Config.Debug = true` and enable `gym_api_test.lua` in `fxmanifest.lua`.
{% endtab %}

{% tab title="Doorlock SQL" %}


```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES

	-- Grove Street Gym
	(1920, 'Grove Gym E-1', '{"state":1,"coords":{"x":-177.5177001953125,"y":-1750.030517578125,"z":32.80458831787109},"maxDistance":2,"doors":[{"model":851337539,"heading":320,"coords":{"x":-176.5602264404297,"y":-1750.833984375,"z":32.80458831787109}},{"model":-512770393,"heading":320,"coords":{"x":-178.4751739501953,"y":-1749.2271728515626,"z":32.80458831787109}}]}'),
	(1921, 'Grove Gym 1-1', '{"heading":50,"model":-220720898,"coords":{"x":-178.06008911132813,"y":-1745.9779052734376,"z":32.83189392089844},"maxDistance":2,"doors":false,"state":1}'),
	(1922, 'Grove Gym 1-2', '{"state":1,"coords":{"x":-173.62863159179688,"y":-1745.4027099609376,"z":32.80622863769531},"maxDistance":2,"doors":[{"model":2140150156,"heading":140,"coords":{"x":-174.58616638183595,"y":-1744.5992431640626,"z":32.80622863769531}},{"model":2140150156,"heading":320,"coords":{"x":-172.6710968017578,"y":-1746.2061767578126,"z":32.80622863769531}}]}'),
	(1923, 'Grove Gym 1-3', '{"heading":140,"model":1635118664,"coords":{"x":-179.65516662597657,"y":-1742.822509765625,"z":32.82985687255859},"maxDistance":2,"doors":false,"state":1}'),
	(1924, 'Grove Gym 1-4', '{"heading":320,"model":1635118664,"coords":{"x":-183.0167694091797,"y":-1739.984130859375,"z":32.83217620849609},"maxDistance":2,"doors":false,"state":1}'),
	(1925, 'Grove Gym 1-5', '{"heading":320,"model":1635118664,"coords":{"x":-187.81729125976563,"y":-1735.9676513671876,"z":32.83260345458984},"maxDistance":2,"doors":false,"state":1}'),
	(1926, 'Grove Gym 1-6', '{"heading":140,"model":1635118664,"coords":{"x":-176.1062469482422,"y":-1738.5927734375,"z":32.83394622802734},"maxDistance":2,"doors":false,"state":1}'),
	(1927, 'Grove Gym 1-7', '{"heading":320,"model":1635118664,"coords":{"x":-179.4811248779297,"y":-1735.7705078125,"z":32.83238220214844},"maxDistance":2,"doors":false,"state":1}'),
	(1928, 'Grove Gym 1-8', '{"heading":320,"model":1635118664,"coords":{"x":-184.27249145507813,"y":-1731.74755859375,"z":32.83311462402344},"maxDistance":2,"doors":false,"state":1}'),

	-- Vinewood Gym
	(1929, 'Vinewood Gym E-1', '{"state":1,"coords":{"x":-494.5778503417969,"y":272.3583068847656,"z":83.43801879882813},"maxDistance":2,"doors":[{"model":-512770393,"heading":263,"coords":{"x":-494.425537109375,"y":273.598876953125,"z":83.43801879882813}},{"model":851337539,"heading":263,"coords":{"x":-494.73016357421877,"y":271.11773681640627,"z":83.43801879882813}}]}'),
	(1930, 'Vinewood Gym 1-1', '{"heading":353,"model":-220720898,"coords":{"x":-491.47442626953127,"y":275.0204162597656,"z":83.46532440185547},"maxDistance":2,"doors":false,"state":1}'),
	(1931, 'Vinewood Gym 1-2', '{"state":1,"coords":{"x":-488.57843017578127,"y":271.6171875,"z":83.43965911865235},"maxDistance":2,"doors":[{"model":2140150156,"heading":83,"coords":{"x":-488.4261169433594,"y":272.8578186035156,"z":83.43965911865235}},{"model":2140150156,"heading":263,"coords":{"x":-488.73077392578127,"y":270.37652587890627,"z":83.43965911865235}}]}'),
	(1932, 'Vinewood Gym 1-3', '{"heading":83,"model":1635118664,"coords":{"x":-489.69671630859377,"y":278.0767822265625,"z":83.46328735351563},"maxDistance":2,"doors":false,"state":1}'),
	(1933, 'Vinewood Gym 1-4', '{"heading":263,"model":1635118664,"coords":{"x":-489.14715576171877,"y":282.4419250488281,"z":83.46560668945313},"maxDistance":2,"doors":false,"state":1}'),
	(1934, 'Vinewood Gym 1-5', '{"heading":263,"model":1635118664,"coords":{"x":-488.39324951171877,"y":288.6554870605469,"z":83.46603393554688},"maxDistance":2,"doors":false,"state":1}'),
	(1935, 'Vinewood Gym 1-6', '{"heading":83,"model":1635118664,"coords":{"x":-484.2165222167969,"y":277.404052734375,"z":83.46737670898438},"maxDistance":2,"doors":false,"state":1}'),
	(1936, 'Vinewood Gym 1-7', '{"heading":263,"model":1635118664,"coords":{"x":-483.68768310546877,"y":281.7715759277344,"z":83.46581268310547},"maxDistance":2,"doors":false,"state":1}'),
	(1937, 'Vinewood Gym 1-8', '{"heading":263,"model":1635118664,"coords":{"x":-482.92333984375,"y":287.9809875488281,"z":83.46654510498047},"maxDistance":2,"doors":false,"state":1}'),

	-- Chumash Gym
	(1938, 'Chumash Gym E-1', '{"state":1,"coords":{"x":-3157.889892578125,"y":1194.7003173828126,"z":20.84630584716797},"maxDistance":2,"doors":[{"model":851337539,"heading":176,"coords":{"x":-3159.136474609375,"y":1194.7916259765626,"z":20.84630584716797}},{"model":-512770393,"heading":176,"coords":{"x":-3156.643310546875,"y":1194.6090087890626,"z":20.84630584716797}}]}'),
	(1939, 'Chumash Gym 1-1', '{"heading":266,"model":-220720898,"coords":{"x":-3155.078857421875,"y":1191.731201171875,"z":20.87361145019531},"maxDistance":2,"doors":false,"state":1}'),
	(1940, 'Chumash Gym 1-2', '{"state":1,"coords":{"x":-3158.3359375,"y":1188.671875,"z":20.84794616699218},"maxDistance":2,"doors":[{"model":2140150156,"heading":356,"coords":{"x":-3157.08935546875,"y":1188.58056640625,"z":20.84794616699218}},{"model":2140150156,"heading":176,"coords":{"x":-3159.582763671875,"y":1188.76318359375,"z":20.84794616699218}}]}'),
	(1941, 'Chumash Gym 1-3', '{"heading":356,"model":1635118664,"coords":{"x":-3151.93896484375,"y":1190.1053466796876,"z":20.87157440185547},"maxDistance":2,"doors":false,"state":1}'),
	(1942, 'Chumash Gym 1-4', '{"heading":176,"model":1635118664,"coords":{"x":-3147.55224609375,"y":1189.7705078125,"z":20.87389373779297},"maxDistance":2,"doors":false,"state":1}'),
	(1943, 'Chumash Gym 1-5', '{"heading":176,"model":1635118664,"coords":{"x":-3141.309326171875,"y":1189.322021484375,"z":20.87432098388672},"maxDistance":2,"doors":false,"state":1}'),
	(1944, 'Chumash Gym 1-6', '{"heading":356,"model":1635118664,"coords":{"x":-3152.34228515625,"y":1184.5987548828126,"z":20.87566375732422},"maxDistance":2,"doors":false,"state":1}'),
	(1945, 'Chumash Gym 1-7', '{"heading":176,"model":1635118664,"coords":{"x":-3147.954345703125,"y":1184.28466796875,"z":20.87409973144531},"maxDistance":2,"doors":false,"state":1}'),
	(1946, 'Chumash Gym 1-8', '{"heading":176,"model":1635118664,"coords":{"x":-3141.714599609375,"y":1183.8255615234376,"z":20.87483215332031},"maxDistance":2,"doors":false,"state":1}'),

	-- Paleto Bay Gym
	(1947, 'Paleto Bay Gym E-1', '{"state":1,"coords":{"x":-80.21546173095703,"y":6404.89013671875,"z":31.75394439697265},"maxDistance":2,"doors":[{"model":-512770393,"heading":315,"coords":{"x":-81.09927368164063,"y":6405.77392578125,"z":31.75394439697265}},{"model":851337539,"heading":315,"coords":{"x":-79.33164978027344,"y":6404.00634765625,"z":31.75394439697265}}]}'),
	(1948, 'Paleto Bay Gym 1-1', '{"heading":45,"model":-220720898,"coords":{"x":-80.4025650024414,"y":6408.974609375,"z":31.78125},"maxDistance":2,"doors":false,"state":1}'),
	(1949, 'Paleto Bay Gym 1-2', '{"state":1,"coords":{"x":-75.93783569335938,"y":6409.1611328125,"z":31.75558471679687},"maxDistance":2,"doors":[{"model":2140150156,"heading":135,"coords":{"x":-76.82169342041016,"y":6410.04541015625,"z":31.75558471679687}},{"model":2140150156,"heading":315,"coords":{"x":-75.05397033691406,"y":6408.27734375,"z":31.75558471679687}}]}'),
	(1950, 'Paleto Bay Gym 1-3', '{"heading":135,"model":1635118664,"coords":{"x":-81.71654510498047,"y":6412.2568359375,"z":31.77921295166015},"maxDistance":2,"doors":false,"state":1}'),
	(1951, 'Paleto Bay Gym 1-4', '{"heading":315,"model":1635118664,"coords":{"x":-84.8179931640625,"y":6415.37744140625,"z":31.78153228759765},"maxDistance":2,"doors":false,"state":1}'),
	(1952, 'Paleto Bay Gym 1-5', '{"heading":315,"model":1635118664,"coords":{"x":-89.25018310546875,"y":6419.796875,"z":31.7819595336914},"maxDistance":2,"doors":false,"state":1}'),
	(1953, 'Paleto Bay Gym 1-6', '{"heading":135,"model":1635118664,"coords":{"x":-77.81248474121094,"y":6416.1611328125,"z":31.7833023071289},"maxDistance":2,"doors":false,"state":1}'),
	(1954, 'Paleto Bay Gym 1-7', '{"heading":315,"model":1635118664,"coords":{"x":-80.92855834960938,"y":6419.26708984375,"z":31.78173828125},"maxDistance":2,"doors":false,"state":1}'),
	(1955, 'Paleto Bay Gym 1-8', '{"heading":315,"model":1635118664,"coords":{"x":-85.35105895996094,"y":6423.69189453125,"z":31.782470703125},"maxDistance":2,"doors":false,"state":1}'),

	-- Sandy Shores Gym
	(1956, 'Sandy Shores Gym E-1', '{"state":1,"coords":{"x":1739.6400146484376,"y":3704.29248046875,"z":34.30290222167969},"maxDistance":2,"doors":[{"model":-512770393,"heading":210,"coords":{"x":1740.722412109375,"y":3704.917236328125,"z":34.30290222167969}},{"model":851337539,"heading":210,"coords":{"x":1738.5576171875,"y":3703.66748046875,"z":34.30290222167969}}]}'),
	(1957, 'Sandy Shores Gym 1-1', '{"heading":300,"model":-220720898,"coords":{"x":1743.6337890625,"y":3703.415771484375,"z":34.33020782470703},"maxDistance":2,"doors":false,"state":1}'),
	(1958, 'Sandy Shores Gym 1-2', '{"state":1,"coords":{"x":1742.6585693359376,"y":3699.054931640625,"z":34.3045425415039},"maxDistance":2,"doors":[{"model":2140150156,"heading":30,"coords":{"x":1743.7410888671876,"y":3699.679931640625,"z":34.3045425415039}},{"model":2140150156,"heading":210,"coords":{"x":1741.5760498046876,"y":3698.429931640625,"z":34.3045425415039}}]}'),
	(1959, 'Sandy Shores Gym 1-3', '{"heading":30,"model":1635118664,"coords":{"x":1747.1444091796876,"y":3703.835693359375,"z":34.32817077636719},"maxDistance":2,"doors":false,"state":1}'),
	(1960, 'Sandy Shores Gym 1-4', '{"heading":210,"model":1635118664,"coords":{"x":1750.9613037109376,"y":3706.023681640625,"z":34.33049011230469},"maxDistance":2,"doors":false,"state":1}'),
	(1961, 'Sandy Shores Gym 1-5', '{"heading":210,"model":1635118664,"coords":{"x":1756.37744140625,"y":3709.1611328125,"z":34.33091735839844},"maxDistance":2,"doors":false,"state":1}'),
	(1962, 'Sandy Shores Gym 1-6', '{"heading":30,"model":1635118664,"coords":{"x":1749.9052734375,"y":3699.053955078125,"z":34.33226013183594},"maxDistance":2,"doors":false,"state":1}'),
	(1963, 'Sandy Shores Gym 1-7', '{"heading":210,"model":1635118664,"coords":{"x":1753.7115478515626,"y":3701.260009765625,"z":34.33069610595703},"maxDistance":2,"doors":false,"state":1}'),
	(1964, 'Sandy Shores Gym 1-8', '{"heading":210,"model":1635118664,"coords":{"x":1759.130615234375,"y":3704.38671875,"z":34.33142852783203},"maxDistance":2,"doors":false,"state":1}');
```
{% endtab %}

{% tab title="Commands & Features" %}
#### 🧠 Commands

* `/gymsets` — Opens the entity set control menu (toggle weights/martial arts)

#### 💪 Key Features

* Dual Targeting System (ox\_target fallback)
* Synced equipment props across all players
* Multiple gym locations across San Andreas
* Customizable UI messages and labels
* Supports entity sets for dynamic layouts
* Fully compatible with `prompt_anim_core`
{% endtab %}

{% tab title="Troubleshooting & Support" %}
**Common Issues**

* **Gym not loading?** Check folder name `prompt_gym` and ensure correct order in `server.cfg`.
* **Animations not working?** Ensure `prompt_anim_core` and `ox_lib` are both started before this resource.
* **Entity sets missing?** Run `/gymsets` to toggle “weights1” or “martialarts” sets per location.

**Need Help?**

Open a ticket with:

* Resource name: **prompt\_gym**
* Server artifact version
* Console error logs (if any)

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endtab %}
{% endtabs %}
