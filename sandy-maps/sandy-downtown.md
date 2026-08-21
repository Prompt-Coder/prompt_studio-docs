# 🏙️ Sandy Shores Downtown

## Sandy Shores Downtown

The downtown block of Sandy Shores, fully reworked — a row of shopfronts with **16 enterable interiors** behind them, from the bakery and coffee shop to the club, the pawn shop and the fire station. Built to slot into the wider Sandy Shores rework as the town's commercial centre.

***

{% hint style="info" %}
Pure map resource — no framework, no dependencies. It only needs the correct **Sandy MapData** installed.
{% endhint %}

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Add the resource

Place the `prompt_sandy_downtown` folder inside your `resources` directory.

<pre><code><strong>resources/prompt_sandy_downtown
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Add to your server.cfg

Insert the following line to ensure the map loads automatically:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_downtown
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 3 — Set up MapData

Make sure you have the correct [**Sandy MapData**](sandy-mapdata.md) installed.
{% endstep %}

{% step %}
#### Step 4 — Test the map

Restart your server and visit **Sandy Shores Downtown**.\
If the map and interiors load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

{% hint style="info" %}
💡 **Tip:** Always restart your server after adding new resources — especially when adding multiple Sandy area maps.
{% endhint %}

***

:round\_pushpin:Location: **1680.4, 3735.15, 35.58**

***

### Interiors

Sixteen interiors sit behind the downtown shopfronts.

{% tabs %}
{% tab title="Custom-built" %}
Purpose-built interiors with their own streamed models, props and textures:

| Interior | | Interior | |
| --- | --- | --- | --- |
| Clothing Store | Bakery | Bar | Club |
| Coffee Shop | Dream Cream | Fire Station Museum | Lawyers Office |
| Pawn Shop | Post Op | Apartment Tunnel | Pipedown |

{% hint style="info" %}
Folder names under `stream/Interiors/` don't always match the shop — the clothing store lives in `Aztec/`, and the museum in `Fire Station/`.
{% endhint %}
{% endtab %}

{% tab title="Placement-only" %}
Existing GTA interiors re-instanced into the downtown block, so the shopfronts open into a usable space out of the box:

* **Ammunation**
* **Fleeca**
* **Barber Shop**
* **Tattoo Shop**

The barber and tattoo slots are automatically upgraded when you own our custom versions — see [Custom interior swap](#custom-interior-swap) below.
{% endtab %}
{% endtabs %}

***

### Custom interior swap

The **Barber Shop** and **Tattoo Shop** slots ship with the standard GTA interior in place, and swap themselves out for our custom interiors the moment you install them:

<table data-view="cards"><thead><tr><th>Slot</th><th>Custom interior</th><th data-hidden data-card-target data-type="content-ref">Link</th></tr></thead><tbody><tr><td><strong>Barber Shop</strong></td><td><a href="https://store.prompt-mods.com/store/package/6897176">Sandy Barber Shop</a></td><td></td></tr><tr><td><strong>Tattoo Shop</strong></td><td><a href="https://store.prompt-mods.com/store/package/7226101">Sandy Tattoo Shop</a></td><td></td></tr></tbody></table>

**No configuration required.** When `prompt_barber` or `prompt_tattoo` is running, the map despawns the default GTA interior — visual *and* collision — and activates the custom placement in its place. Stop the resource and the default interior comes back.

{% hint style="success" %}
Start order doesn't matter. The custom interior resource can start before or after `prompt_sandy_downtown`, and the swap survives stopping and restarting it mid-session.
{% endhint %}

<details>

<summary>Forcing a slot manually</summary>

Auto-detection covers virtually every setup, but you can override a slot in `config.lua`:

{% code title="config.lua" %}
```lua
Config.Enabled = true   -- master switch for the whole auto-swap system
Config.Debug   = false  -- prints swap steps to F8; keep false for release

Config.Slots = {
    barber = {
        customResource = 'prompt_barber',
        forceUseCustom = nil,   -- nil = autodetect · true = always custom · false = always GTA
        -- ...
    },
}
```
{% endcode %}

Set `forceUseCustom = true` to pin the custom interior, or `false` to keep the GTA one even when the custom resource is running.

</details>

***

### Exterior-Only Mode

Don't need the interiors? Downtown is supported by the free [**Exterior-Only Add-On**](exterior-only-add-on.md), which strips 10 of its interiors while leaving the exterior fully intact — useful for servers that never send players inside.

***

### 🔒 Wanted: ox\_doorlock door data

{% hint style="success" %}
We're looking for someone to create the **`ox_doorlock` SQL** (door definitions) for Sandy Shores Downtown's interior doors. Do it well and we'll reward you with a **20% discount coupon** for the store.

Interested? Reach out in the [Prompt Studio Discord](https://discord.gg/rKbHHdfZFU).
{% endhint %}

***

### Notes

* Part of the **Sandy Shores rework** — designed to sit alongside the other Sandy maps.
* Exterior ships with **LODs, distant lights and LOD lights**, so the block reads correctly at range and at night.
* Textures, props and placements are left **open for editing** — the `unlocked` folders and the map's `.ymap` / `.ytyp` / `.ytd` files are not escrow-locked.
* A separate free [**Downtown Construction**](free-construction-zones.md) lot is available if you want a construction-in-progress variant of the area.

***

Need help? Join the [Prompt Studio Discord](https://discord.gg/rKbHHdfZFU) for support, bug reports, and feedback. Enjoy Sandy Shores Downtown on your FiveM server! 🚀
