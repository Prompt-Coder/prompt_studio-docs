---
description: Playable arcade cabinets — screen games, physical machines, leaderboards & rewards
icon: gamepad
---

# Prompt Arcade

Turn the arcade cabinets in your map into **real, playable games**. Walk up to a cabinet, press
interact, and play — shooters, racers, a claw machine, a fortune teller, and a two-player love
tester. Every game is self-contained (no external assets to chase), keeps a **high-score
leaderboard**, and exposes clean **reward hooks** so you decide what a win is worth.

{% hint style="info" %}
The games render **on the cabinet screen** using the cabinet's own props — no full-screen NUI
takeover. Two-player games (Badlands + the racers) run split-screen on one cabinet, and the Love
Tester pairs two players on one machine.
{% endhint %}

***

### Requirements

* FiveM server (recent artifact recommended)
* [`ox_lib`](https://github.com/overextended/ox_lib) — started **before** this resource (hard dependency)
* A targeting resource — [`ox_target`](https://github.com/overextended/ox_target) **or** `qb-target` (auto-detected). One is required so players can interact with the cabinets.
* An **arcade map/MLO** where the cabinets are placed (see [Props & Placement](configuration.md#props-and-placement))

Optional:

* **Framework** (QBCore / ESX) — only used to grant rewards and show character names on leaderboards. Without one the games still play; rewards simply don't fire and names fall back to the Steam/license name.

***

### Installation

{% stepper %}
{% step %}
#### Copy the resource
Drop `prompt_arcade_games` into your `resources` folder.
{% endstep %}

{% step %}
#### Add to server.cfg — in this order
```
ensure ox_lib
ensure ox_target        # or: ensure qb-target
ensure prompt_arcade_games
```
`prompt_audio` / other resources are **not** required.
{% endstep %}

{% step %}
#### Place the cabinets
Place the stock arcade cabinet props in your arcade MLO (the game binds to them by model).
The custom "screen" props the games draw onto ship **inside this resource** — you don't install
them separately. See [Props & Placement](configuration.md#props-and-placement).
{% endstep %}

{% step %}
#### Configure & reward
Open `config.lua` to enable/disable games, rebind controls, or set the default volume. Hook the
reward events in your own resource to pay out wins — see [For Developers](developers.md).
{% endstep %}
{% endstepper %}

***

### First-boot checklist

| Check | What to look for |
| --- | --- |
| Targeting detected | Console prints `boot: N framework cabinet(s) wired (target=ox_target)` (or `qb-target`) |
| Framework detected | Console prints `[arc:framework] detected: qb` / `esx` / `standalone` |
| Interact prompt appears | Walk to a placed cabinet — you get a "Play …" target option |
| Screen lights up | On play, the game renders on the cabinet's screen |

{% hint style="warning" %}
If a cabinet has **no interact prompt**, you don't have `ox_target` or `qb-target` started. If the
**screen stays black**, the cabinet isn't a map-placed prop (the Love Tester in particular needs a
map-placed cabinet). See [Troubleshooting](troubleshooting.md).
{% endhint %}

***

### What's inside

<table data-view="cards"><thead><tr><th>Section</th><th></th><th data-card-target data-type="content-ref">Link</th></tr></thead><tbody><tr><td><strong>The Games</strong></td><td>The full roster and how each plays</td><td><a href="games.md">games.md</a></td></tr><tr><td><strong>Configuration</strong></td><td>config.lua reference — games, controls, volume, security</td><td><a href="configuration.md">configuration.md</a></td></tr><tr><td><strong>For Developers</strong></td><td>Reward hooks, exports, leaderboards, anti-cheat</td><td><a href="developers.md">developers.md</a></td></tr><tr><td><strong>Troubleshooting</strong></td><td>No prompt, black screen, no rewards…</td><td><a href="troubleshooting.md">troubleshooting.md</a></td></tr></tbody></table>
