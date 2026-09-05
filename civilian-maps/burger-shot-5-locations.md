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
{% hint style="success" %}
**🔒 Wanted: ox\_doorlock door data**

We don't have door definitions for Burger Shot yet. Submit the **`ox_doorlock` SQL** for the five locations and we'll reward you with a **10% discount coupon** for the store.

Interested? Reach out in the [Prompt Studio Discord](https://discord.gg/rKbHHdfZFU).
{% endhint %}
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
