---
description: >-
  Trains running in 5 minutes: what goes where, the start order, and how to
  choose which trains run on each line.
icon: rocket
---

# Quick Setup

{% hint style="info" %}
For **version 2**. About 5 minutes.
{% endhint %}

### How it works

| Piece                        | What it is                                                     |
| ---------------------------- | -------------------------------------------------------------- |
| `prompt_train_script`        | The engine. It runs the trains                                 |
| `prompt_train_script-assets` | The data: every line and station                               |
| `prompt_sandy_traintunnel`   | The Sandy Shores tunnel map                                    |
| **Train packs**              | The trains: the Polar Express (`prompt_train_polar_express`) and the AERION bullet train (`prompt_train_bullet`). Separate resources: run one or both |

**Lines** are the routes: Los Santos, Sandy Shores, the metro… You choose **which trains** run on each line, and **how many**, in one place: `config/trains.lua` → `fleet`.

***

### Install

{% stepper %}
{% step %}
#### Copy the folders

Into your `resources` folder:

* `prompt_train_script`
* `prompt_train_script-assets`
* `prompt_sandy_traintunnel`
* your trains: `prompt_train_polar_express`, `prompt_train_bullet`, or both
{% endstep %}

{% step %}
#### Start them in this order

In `server.cfg`:

```
ensure ox_lib
ensure prompt_train_polar_express   # if you have it
ensure prompt_train_bullet          # if you have it
ensure prompt_sandy_traintunnel
ensure prompt_train_script-assets
ensure prompt_train_script
```

Trains always go **above** `prompt_train_script`.
{% endstep %}

{% step %}
#### Restart the server, read the console

Yellow `[prompt_train]` lines tell you what's missing and how to fix it. See [Console messages](#console-messages).
{% endstep %}

{% step %}
#### Join

Trains appear once the first player is online.
{% endstep %}
{% endstepper %}

***

### Choose your trains

Open `prompt_train_script/config/trains.lua` and find `fleet`. This is the preset:

{% code title="config/trains.lua" %}
```lua
fleet = {
    sandy     = { polar = 2 },             -- 2 Polar Express
    lossantos = { bullet = 5 },            -- 5 bullet trains
    roxwood   = { polar = 2, bullet = 1 }, -- 2 Polar Express + 1 bullet train
},
```
{% endcode %}

* **Left:** the line.
* **Inside:** train name `=` how many.
* Save, then **restart the server**.

{% hint style="success" %}
**Only one of the two trains?** Change nothing. A train you don't have is replaced by one you do, so every line runs.
{% endhint %}

The types take turns on the line, so the same train doesn't bunch up.

{% hint style="info" %}
Since 2.1.2. Older versions read these numbers as chances, not counts.
{% endhint %}

<details>

<summary>Which names can I use?</summary>

**Lines:** `lossantos`, `sandy`, `roxwood` (needs the Roxwood map), `monorail` (needs the monorail map). The metro runs by itself.

**Trains:** `polar` (Polar Express), `bullet` (AERION bullet train), or the name of a train pack you installed. Not sure of a name? The console tells you — see below.

</details>

***

### Add a new train

{% stepper %}
{% step %}
#### Install the pack

Copy it into `resources` and `ensure` it **above** `prompt_train_script`.
{% endstep %}

{% step %}
#### Restart and copy the line the console gives you

```
[prompt_train] My Train (my_train_pack) is installed but not running on any track. To run it, put it on a line in prompt_train_script/config/trains.lua -> fleet, for example:  lossantos = { bullet = 5, mytrain = 1 },  (1 = one My Train), then restart the server
```
{% endstep %}

{% step %}
#### Paste it into `fleet` and restart

Done. The train runs on that line.
{% endstep %}
{% endstepper %}

***

### Console messages

| Console says                                         | Do this                                                                     |
| ---------------------------------------------------- | --------------------------------------------------------------------------- |
| `... is installed but not running on any track`      | Put the train in `fleet` — copy the example from the message — and restart  |
| `none of its trains is installed (needs <resource>)` | Start that train pack **above** `prompt_train_script`                       |
| `started after prompt_train_script`                  | Move the train's `ensure` above the script, then restart the whole server   |
| `line "<id>" is dormant: <map> not running`          | That line needs a map you don't run. Start the map above the script, or ignore it |
| `fleet.<line> adds up to ... read as shares`         | Old config. Change the numbers to how many trains you want: `sandy = { polar = 2 }` |

***

### Good to know

* After any change, restart the **whole server**, not just the train script.
* A train that isn't installed is replaced by one that is. The line keeps its number of trains.
* Converted trains from GTA5-Mods work the same way — see [Train Packs](train-packs.md#trains-from-gta5-mods-kitsune-trains-7).

<table data-view="cards"><thead><tr><th>Next</th><th data-card-target data-type="content-ref">Page</th></tr></thead><tbody><tr><td><strong>Train Packs</strong> — what a train pack is, and how to make one</td><td><a href="train-packs.md">train-packs.md</a></td></tr><tr><td><strong>Lines &#x26; Stations</strong> — the routes and their stops</td><td><a href="lines-and-stations.md">lines-and-stations.md</a></td></tr><tr><td><strong>Configuration</strong> — every setting</td><td><a href="configuration.md">configuration.md</a></td></tr><tr><td><strong>Driving</strong> — let players drive the trains</td><td><a href="driving.md">driving.md</a></td></tr></tbody></table>
