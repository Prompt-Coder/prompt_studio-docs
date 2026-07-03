# 🏫 Exterior-Only Add-On

## Sandy Shores - Exterior-Only Add-On

A free drag-and-drop patch that strips interiors from the Prompt Studios Sandy Shores map collection. Exteriors stay 100% intact — only interior rooms, doors, and windows are removed.

{% hint style="info" %}
This is an **optional add-on**, not a standalone resource. You must own the original Sandy Shores maps for it to do anything — it only replaces files that already exist in those resources.
{% endhint %}

### Who is this for?

{% columns %}
{% column %}
#### <i class="fa-server">:server:</i> Server owners

Running a server that doesn't use interiors? This strips the unused interior streaming from every Sandy map you own - faster load, better fps, same exteriors.
{% endcolumn %}

{% column %}
#### <i class="fa-gauge-high">:gauge-high:</i> Lower-end players

If your players struggle with interior-heavy maps, the exterior-only variant keeps the full Sandy Shores look without the GPU/streaming cost of interiors they'll never enter.
{% endcolumn %}
{% endcolumns %}

### Download

<a href="https://github.com/Prompt-Coder/sandy_exterior_only/releases/latest/download/sandy-no-interior.zip" class="button primary" data-icon="download">Download latest version</a>

<a href="https://github.com/Prompt-Coder/sandy_exterior_only/releases/latest" class="button secondary" data-icon="github">View release notes</a>

The download link above always points to the latest version. Bookmark it — it will not change when the add-on is updated.

### Installation

{% stepper %}
{% step %}
**Download the archive**

Click the download button above to grab `sandy-no-interior.zip`.
{% endstep %}

{% step %}
**Extract it**

Unzip the archive anywhere — you'll see one folder per supported map (e.g. `prompt_sandy_apts/`, `prompt_sandy_bank/`, ...).

<figure><img src="../.gitbook/assets/2026-04-17 15-42-59.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Drop the folders into your `resources/` directory**

Drag all extracted folders into your server's `resources/` folder (where your existing Sandy Shores maps already live).

When Windows asks whether to replace files, choose **Replace the files in the destination**.

{% hint style="warning" %}
Only drop folders for maps you actually own and have installed. Extra folders are harmless (they just sit unused), but there's no reason to ship files you don't need.
{% endhint %}
{% endstep %}

{% step %}
**Restart the affected resources**

Either restart each replaced resource individually, or do a full server restart. That's it — no config changes, no extra `ensure` lines, no dependencies.
{% endstep %}
{% endstepper %}

### Supported maps

<details>

<summary>Full list — 20 maps supported (click to expand)</summary>

* `cfx_prompt_sandy_shores_fire_department`
* `prompt_gym`
* `prompt_hornys`
* `prompt_sandy_apts`
* `prompt_sandy_bank`
* `prompt_sandy_beaches`
* `prompt_sandy_church`
* `prompt_sandy_cityhall`
* `prompt_sandy_classic_car_dealership`
* `prompt_sandy_fire2`
* `prompt_sandy_hospital`
* `prompt_sandy_hospital2`
* `prompt_sandy_houses_part1`
* `prompt_sandy_illegal_garage`
* `prompt_sandy_market`
* `prompt_sandy_mechanic`
* `prompt_sandy_motel`
* `prompt_sandy_sheriff`
* `prompt_sandy_train_station`
* `prompt_sandy_university`

</details>

### How it works

The archive mirrors the resource folder structure of each supported map. When you drop it into your `resources/` folder, Windows overwrites the matching assets with **empty or interior-less variants**.

The maps still load normally — they just no longer stream interior geometry. Doors, windows, and interior rooms are gone; exteriors, collision, and props that live outside are untouched.

{% hint style="success" %}
Nothing is added to your server — only existing files are replaced with lighter versions. That means **no side effects** on other resources, frameworks, or scripts.
{% endhint %}

### How to revert

Reinstall the original map resources from Tebex or Keymaster. The replaced files will go back to the full interior-capable versions.

### Updates & support

This add-on is maintained in one place. Each new version is published as a GitHub release — the download link above always points to the latest.

{% hint style="info" %}
Hit a bug or want a map added to the list? Open an [issue on GitHub](https://github.com/Prompt-Coder/sandy_exterior_only/issues) or reach out on the Prompt Studios Discord.
{% endhint %}
