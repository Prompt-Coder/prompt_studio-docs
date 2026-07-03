---
description: The one command to send support, and common fixes
icon: wrench
---

# Troubleshooting

### `/mrpd_debugdump` — the one command to send us

ACE-gated (`command.mrpd_debugdump`; the **server console always works**). It prints a full snapshot:

* Resource & tier state — `prompt_mrpd` vs `prompt_mrpd_scripts`, `ox_lib`, `screenshot-basic`, anim cores
* Resolved bridges (framework / target / notify / textUI)
* Module toggles and debug flags
* Live per-module state (briefing mode, banners, etc.)

{% hint style="success" %}
**Run it and paste the output** when you report an issue — it tells us almost everything we need in one go.
{% endhint %}

***

### Debug logging

Global **or** per-module — flip only what you're troubleshooting.

```lua
-- config.lua
Config.debug = false      -- master: verbose for EVERY module + enables dev/test commands
Config.Debug = {          -- per-module (each logs if this OR Config.debug is on)
    training = false, custody = false, gym = false, elevator = false,
    anims = false, audio = false, banners = false, interiors = false,
}
```

Lines look like `^5[MRPD TRAINING SV]^0 14:03:11 …` — greppable by module and side (`SV`/`CL`), timestamped. Genuine failures (missing exports, file writes) **always** print as `^1[MRPD … ERROR]^0`, whatever the flags say.

***

### Common issues

<details>

<summary>A feature does nothing / the target won't appear</summary>

* Confirm the module is `true` in `Config.Modules`.
* Confirm the player passes `Config.access` — job is in the list, grade ≥ `minGrade`, and on duty if `requireOnDuty = true`.
* Set `Config.Debug.<module> = true` and read the console as you interact.

</details>

<details>

<summary>"No access" on the briefing TV or instructor panel</summary>

That's the **instructor tier**, which is stricter than normal access. Grant the job + grade (see [Configuration → Instructor tier](configuration.md)) or the matching ACE (`mrpd.briefing.instructor` / `mrpd.training.instructor`).

</details>

<details>

<summary>Framework not detected / wrong framework</summary>

Set `Config.framework` explicitly (`qbox`, `qbcore`, `esx`, `standalone`) instead of `'auto'`. Confirm your core resource starts **before** `prompt_mrpd_scripts`.

</details>

<details>

<summary>I added a new file and it isn't loading</summary>

Adding a **new file** to the resource needs connected players to **rejoin** — `restart prompt_mrpd_scripts` streams edits to existing files, but not brand-new manifest entries. Editing an existing file only needs a restart.

</details>

***

Still stuck? Run `/mrpd_debugdump`, copy the output, and reach us on Discord.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
