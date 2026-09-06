# 🍔 Burger Shot (5 locations)

## Prompt's Burger Shot

{% embed url="https://store.prompt-mods.com/store/package/7658065" %}
**Official asset for FiveM — available on CFX Portal and Prompt's Mods Store**
{% endembed %}

{% embed url="https://youtu.be/sIeyUPhE6tE" %}

Five fully custom **Burger Shot** restaurants placed across San Andreas — each a new building with a walk-in interior, a drive-thru, animated billboards and custom lighting. Install all five or keep only the ones you want.

{% hint style="info" %}
Pure map resource — no framework, no scripts, no MapData required. Drop and play.
{% endhint %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Install the map

Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=Prompt%27s+-+Burgershot+%28FastFood+Chain%29).

After downloading, **you will get a folder named**:

<pre><code><strong>prompt_burger_shot
</strong></code></pre>

Drag and drop it inside your `resources` directory. When done, the full path should look like this:

<pre><code><strong>resources/prompt_burger_shot
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Add to your server.cfg

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_burger_shot
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 3 — Restart your server

Restart and visit any of the five locations below. If the building and interior load, installation was successful ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

### Additional Information

{% tabs %}
{% tab title="Locations" %}
| Location (folder name) | Coordinates |
| --- | --- |
| Vinewood | -245.9, 277.07, 94.37 |
| Beach | -1721.55, -722.81, 11.48 |
| Ghetto | 130.88, -1537.95, 31.57 |
| Chumash | -2971.62, 517.28, 17.55 |
| Highway | 2579.89, 421.07, 110.89 |

These are new custom buildings, not edits of the vanilla Burger Shots — the surrounding terrain in each folder is adjusted to fit them.

> Fully compatible with all other Prompt Studio maps — the locations sit on their own lots and don't touch any Sandy Shores, Paleto or Los Santos rework.
{% endtab %}

{% tab title="Removing a location" %}
Every location is its own folder inside `stream/`:

```
stream/
├── base(do not delete)/   ← shared props, keep this
├── beach/
├── chumash/
├── ghetto/
├── highway/
└── vinewood/
```

**To remove a location, delete its folder** and restart the resource. No config, no other changes.

{% hint style="danger" %}
Never delete `base(do not delete)` — it holds the models and textures every location uses. Without it none of them will load.
{% endhint %}
{% endtab %}

{% tab title="Compatibility" %}
Burger Shot edits vanilla-area files that several other Prompt Studio maps also edit — among them **Japanese Restaurant**, **Horny's Burgers**, **YouTool**, **SAHP**, **Rockford Dealership** and **Motorcycle Paradise**. Running Burger Shot alongside any of them can cause conflicts at a location: missing ground, floating props, broken collision or z-fighting.

#### The fix — Vertex Hub

Run the [**Vertex Hub Merger**](https://app.vertex-hub.com/merger) on your server. It finds every file shared between your resources and merges them for the exact combination you run — two maps, three, all of them — and re-runs in seconds whenever you add or update one.

{% hint style="success" %}
**Merging our maps between each other with Vertex Hub is completely FREE of charge.** Any Prompt Studio map with any other Prompt Studio map — no cost, no limit.
{% endhint %}

We don't ship pre-merged files: with this many possible combinations they'd go stale the moment any map updated. Vertex Hub always merges what you actually have installed.

Need help with the tool? [Vertex Hub Discord](https://discord.gg/8pmQM5q7yP).
{% endtab %}

{% tab title="Doorlock SQL" %}
All five locations are compatible with [`ox_doorlock`](https://github.com/overextended/ox_doorlock). Import the SQL below into your database and restart `ox_doorlock` — 6 doors per location, 30 in total.

{% hint style="info" %}
The SQL uses `DEFAULT` for the `id` column, so your database assigns free IDs automatically on import — it won't conflict with doorlocks you already have.
{% endhint %}

<details>

<summary><strong>Burger Shot Doorlock SQL (30 doors)</strong></summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(DEFAULT, 'Burger Shot - Vinewood E-1', '{"state":1,"heading":270,"model":-166679493,"maxDistance":2,"coords":{"x":-252.45054626464845,"y":292.35821533203127,"z":92.14047241210938},"doors":false}'),
	(DEFAULT, 'Burger Shot - Vinewood 1-1', '{"state":1,"heading":0,"model":406914727,"maxDistance":2,"coords":{"x":-251.83363342285157,"y":293.62030029296877,"z":92.16523742675781},"doors":false}'),
	(DEFAULT, 'Burger Shot - Vinewood 1-2', '{"state":1,"heading":270,"model":-302342834,"maxDistance":2,"coords":{"x":-250.21510314941407,"y":292.34539794921877,"z":92.15997314453125},"doors":false}'),
	(DEFAULT, 'Burger Shot - Vinewood 1-3', '{"state":1,"heading":270,"model":-302342834,"maxDistance":1,"coords":{"x":-243.38845825195313,"y":293.5516662597656,"z":92.16226959228516},"doors":false}'),
	(DEFAULT, 'Burger Shot - Vinewood 1-4', '{"state":1,"auto":true,"heading":90,"model":-1325780274,"maxDistance":1,"coords":{"x":-241.06695556640626,"y":293.1061096191406,"z":91.9663314819336},"doors":false}'),
	(DEFAULT, 'Burger Shot - Vinewood 1-5', '{"state":1,"heading":0,"model":315614968,"maxDistance":1,"coords":{"x":-242.4630126953125,"y":294.052001953125,"z":92.15399932861328},"doors":false}'),
	(DEFAULT, 'Burger Shot - Beach E-1', '{"state":1,"heading":50,"model":-166679493,"maxDistance":2,"coords":{"x":-1722.6900634765626,"y":-732.3626098632813,"z":10.37658405303955},"doors":false}'),
	(DEFAULT, 'Burger Shot - Beach 1-1', '{"state":1,"heading":140,"model":406914727,"maxDistance":2,"coords":{"x":-1723.973876953125,"y":-732.932861328125,"z":10.40134906768798},"doors":false}'),
	(DEFAULT, 'Burger Shot - Beach 1-2', '{"state":1,"heading":50,"model":-302342834,"maxDistance":2,"coords":{"x":-1724.394287109375,"y":-730.9158935546875,"z":10.39608573913574},"doors":false}'),
	(DEFAULT, 'Burger Shot - Beach 1-3', '{"state":1,"heading":50,"model":-302342834,"maxDistance":1,"coords":{"x":-1730.399169921875,"y":-727.4518432617188,"z":10.39838123321533},"doors":false}'),
	(DEFAULT, 'Burger Shot - Beach 1-4', '{"state":1,"auto":true,"heading":230,"model":-1325780274,"maxDistance":1,"coords":{"x":-1731.8912353515626,"y":-725.6183471679688,"z":10.20244312286377},"doors":false}'),
	(DEFAULT, 'Burger Shot - Beach 1-5', '{"state":1,"heading":140,"model":315614968,"maxDistance":1,"coords":{"x":-1731.4296875,"y":-727.240234375,"z":10.39011192321777},"doors":false}'),
	(DEFAULT, 'Burger Shot - Ghetto E-1', '{"state":1,"heading":230,"model":-166679493,"maxDistance":2,"coords":{"x":135.6190948486328,"y":-1523.7344970703126,"z":29.37143325805664},"doors":false}'),
	(DEFAULT, 'Burger Shot - Ghetto 1-1', '{"state":1,"heading":320,"model":406914727,"maxDistance":2,"coords":{"x":136.90292358398438,"y":-1523.1640625,"z":29.39619827270507},"doors":false}'),
	(DEFAULT, 'Burger Shot - Ghetto 1-2', '{"state":1,"heading":230,"model":-302342834,"maxDistance":2,"coords":{"x":137.32330322265626,"y":-1525.18115234375,"z":29.39093399047851},"doors":false}'),
	(DEFAULT, 'Burger Shot - Ghetto 1-3', '{"state":1,"heading":230,"model":-302342834,"maxDistance":1,"coords":{"x":143.32818603515626,"y":-1528.6451416015626,"z":29.39323043823242},"doors":false}'),
	(DEFAULT, 'Burger Shot - Ghetto 1-4', '{"state":1,"auto":true,"heading":50,"model":-1325780274,"maxDistance":1,"coords":{"x":144.82015991210938,"y":-1530.478759765625,"z":29.19729232788086},"doors":false}'),
	(DEFAULT, 'Burger Shot - Ghetto 1-5', '{"state":1,"heading":320,"model":315614968,"maxDistance":1,"coords":{"x":144.3587188720703,"y":-1528.856689453125,"z":29.38496208190918},"doors":false}'),
	(DEFAULT, 'Burger Shot - Chumash E-1', '{"state":1,"heading":180,"model":-166679493,"maxDistance":2,"coords":{"x":-2958.4482421875,"y":523.0703125,"z":16.28047180175781},"doors":false}'),
	(DEFAULT, 'Burger Shot - Chumash 1-1', '{"state":1,"heading":270,"model":406914727,"maxDistance":2,"coords":{"x":-2957.184814453125,"y":522.456298828125,"z":16.30523681640625},"doors":false}'),
	(DEFAULT, 'Burger Shot - Chumash 1-2', '{"state":1,"heading":180,"model":-302342834,"maxDistance":2,"coords":{"x":-2958.4560546875,"y":520.8348388671875,"z":16.29997253417968},"doors":false}'),
	(DEFAULT, 'Burger Shot - Chumash 1-3', '{"state":1,"heading":180,"model":-302342834,"maxDistance":1,"coords":{"x":-2957.234130859375,"y":514.0109252929688,"z":16.30226898193359},"doors":false}'),
	(DEFAULT, 'Burger Shot - Chumash 1-4', '{"state":1,"auto":true,"heading":0,"model":-1325780274,"maxDistance":1,"coords":{"x":-2957.674560546875,"y":511.6884460449219,"z":16.10633087158203},"doors":false}'),
	(DEFAULT, 'Burger Shot - Chumash 1-5', '{"state":1,"heading":270,"model":315614968,"maxDistance":1,"coords":{"x":-2956.73193359375,"y":513.086669921875,"z":16.29400062561035},"doors":false}'),
	(DEFAULT, 'Burger Shot - Highway E-1', '{"state":1,"heading":270,"model":-166679493,"maxDistance":2,"coords":{"x":2574.303466796875,"y":434.5932312011719,"z":108.71746826171875},"doors":false}'),
	(DEFAULT, 'Burger Shot - Highway 1-1', '{"state":1,"heading":0,"model":406914727,"maxDistance":2,"coords":{"x":2574.92041015625,"y":435.8553161621094,"z":108.74223327636719},"doors":false}'),
	(DEFAULT, 'Burger Shot - Highway 1-2', '{"state":1,"heading":270,"model":-302342834,"maxDistance":2,"coords":{"x":2576.538818359375,"y":434.5804138183594,"z":108.73696899414063},"doors":false}'),
	(DEFAULT, 'Burger Shot - Highway 1-3', '{"state":1,"heading":270,"model":-302342834,"maxDistance":1,"coords":{"x":2583.365478515625,"y":435.78668212890627,"z":108.73926544189453},"doors":false}'),
	(DEFAULT, 'Burger Shot - Highway 1-4', '{"state":1,"auto":true,"heading":90,"model":-1325780274,"maxDistance":1,"coords":{"x":2585.68701171875,"y":435.34112548828127,"z":108.54332733154297},"doors":false}'),
	(DEFAULT, 'Burger Shot - Highway 1-5', '{"state":1,"heading":0,"model":315614968,"maxDistance":1,"coords":{"x":2584.291015625,"y":436.2870178222656,"z":108.73099517822266},"doors":false}');
```

</details>
{% endtab %}

{% tab title="Custom Props" %}
## Props that you may want to use in your script

1\. Seating & Furniture

* `marlon_bs_furn21` (seat)
* `marlon_bs_furn22` (seat)
* `marlon_bs_masalar` (table)

2\. Script Props

* `prompt_fastfood_register` — cashier register, targetable
* `marlon_bs_counter` — service counter, targetable
{% endtab %}

{% tab title="Editing" %}
The resource is left open for customisation:

* **Textures** — every `.ytd` is editable, so you can re-skin the branding
* **Placements** — every `.ymap` is editable, so you can move or remove props per location
* **Lighting** — `marlon_bs_main.xml` is the interior timecycle; tweak it to change the mood
* `stream/base(do not delete)/unlocked/` holds the editable shared models

Only the core shared models are escrow-locked.
{% endtab %}

{% tab title="Troubleshooting & Support" %}
<details>

<summary>A location doesn't appear</summary>

1. Check `stream/<location>/` still exists — a deleted folder is a removed location by design.
2. Confirm `base(do not delete)` is intact.
3. Clear your client cache: `%localappdata%\FiveM\FiveM Application Data\data\cache`, then rejoin.

</details>

<details>

<summary>Interior looks too dark or too bright</summary>

That's the custom timecycle. Adjust the values in `marlon_bs_main.xml` — `light_artificial_int_up_intensity` and `postfx_intensity_bloom` make the biggest difference.

</details>

Still stuck? Join the [Prompt Studio Discord](https://discord.gg/rKbHHdfZFU) with the location name, console errors and a screenshot.
{% endtab %}
{% endtabs %}

***

For further assistance, contact support. Enjoy using Burger Shot on your FiveM server! 🚀
