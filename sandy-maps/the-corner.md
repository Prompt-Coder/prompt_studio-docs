# 🎳 Sandy Shores Bowling, Diner & Steak House

## Sandy Shores Bowling, Diner & Steak House

Known in-world as **The Corner**, this pack adds a full nightlife block to Sandy Shores. Go bowling, play the arcade cabinets, eat a steak, or hang out in the diner — three connected interiors built to give players somewhere to wind down with friends inside the Sandy Shores rework.

{% embed url="https://youtu.be/6ONcZWRJe7s" %}

***

{% hint style="info" %}
The Corner ships with the **Prompt Arcade** script, which makes the arcade cabinets playable. The arcade script requires [`ox_lib`](https://github.com/overextended/ox_lib); the map itself is a pure map resource.
{% endhint %}

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Add the resource

Place the `prompt_sandy_corner` folder inside your `resources` directory.

<pre><code><strong>resources/prompt_sandy_corner
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Add to your server.cfg

Insert the following line to ensure the map loads automatically:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_corner
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 3 — Set up MapData

Make sure you have the correct [**Sandy MapData**](sandy-mapdata.md) installed.
{% endstep %}

{% step %}
#### Step 4 — Test the map

Restart your server and visit **The Corner** in Sandy Shores.\
If the map and interiors load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

{% hint style="info" %}
💡 **Tip:** Always restart your server after adding new resources — especially when adding multiple Sandy area maps.
{% endhint %}

***

:round\_pushpin:Location: **1921.75, 3869.84, 33.34**

***

### What's Inside

| Area | Description |
| --- | --- |
| **Bowling Alley** | Full alley with lanes, seating, and a separate game room housing the arcade cabinets |
| **Steak Bar** | Sit-down steak restaurant and bar, with custom door audio |
| **Diner & Bar** | Classic roadside Sandy diner with bar and booth seating |
| **Surroundings** | Reworked ground and exterior detailing that blends into the Sandy Shores rework |

***

### Bowling Scripts

The bowling lanes are built to work with an external bowling script. Both of these are compatible:

1. [RTX Bowling](https://rtx.tebex.io/package/6861196)
2. [rCore Bowling](https://store.rcore.cz/package/5125529)

{% hint style="info" %}
The map ships the alley itself — lanes, pins, seating, and the surrounding interior. Install one of the scripts above to make the lanes playable.
{% endhint %}

***

### Arcade Games

The bowling alley's game room is filled with playable cabinets, run by the bundled **Prompt Arcade** script. Walk up to a cabinet and interact to play.

| Game | Players |
| --- | --- |
| Space Monkey | 1 |
| The Wizard's Ruin | 1 |
| Claw Machine | 1 |
| Nazar the Fortune Teller | 1 |
| Badlands Revenge | 2 (split screen) |
| Race and Chase: Crotch Rockets | 2 (split screen) |
| Race and Chase: Get Truckin' | 2 (split screen) |
| Race and Chase: Street Legal | 2 (split screen) |
| Love Tester | 2 |

{% hint style="info" %}
Interaction uses **ox\_target** or **qb-target**, auto-detected at runtime — whichever you already run. If neither is present, the script falls back to its own interaction handling.
{% endhint %}

<details>

<summary>Adjusting the arcade cabinets</summary>

Cabinet behaviour lives in `config.lua` inside the arcade resource. Each game entry controls its own settings:

* `enabled` — turn an individual game on or off
* `title` — the name shown to players
* `target` — the interaction label and icon

Global defaults at the top of the file control interaction distance (`targetDistance`), how far the script looks for a placed cabinet (`findRange`), and the cooldown between plays (`cooldown`).

</details>

***

### Notes

* The Corner is part of the **Sandy Shores rework** and is designed to sit alongside the other Sandy maps.
* The building is signed as **The Corner** in-world — that's the name players will see.
* The map itself is a pure map resource — no framework required. Only the arcade script needs `ox_lib`.
* Bowling alley interior loads at `1931.5, 3893.69, 33.61`.

***

Need help? Join the [Prompt Studio Discord](https://discord.gg/rKbHHdfZFU) for support, bug reports, and feedback. Enjoy The Corner on your FiveM server! 🚀
