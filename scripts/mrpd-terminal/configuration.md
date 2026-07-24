---
description: Every config.lua option — adapters, access, grades, screens, DUI
icon: sliders
---

# Configuration

All options live in `prompt_mrpd_terminal/config.lua` (plaintext, yours to edit). Section order follows the file.

***

### Top-level switches

| Option | Default | Meaning |
| ----------------- | ------- | ------------------------------------------------------------------------------------------------------ |
| `Config.debug` | `false` | Verbose logs, capability dump on boot, dev overlays, `/termcam` + `/termtest_*` commands. Keep `false` in production. |
| `Config.showcase` | `false` | **Demo mode** — bypasses ALL permission checks and serves scripted mock data. For videos/previews only. |

***

### Backend selection — `Config.adapterPriority`

{% code title="config.lua" %}
```lua
Config.adapterPriority = {
    'showcase',      -- only wins when Config.showcase = true
    'wasabi_mdt',
    'lb_tablet',
    'p_mdt',
    'qb_policejob',
    'null',          -- honest empty-state fallback
}
```
{% endcode %}

On boot the terminal walks this list and activates the **first adapter whose backend is actually running**. Reorder to prefer a different backend when several are installed.

### Framework — `Config.framework`

`'auto'` (default) picks Qbox → QBCore → ESX by detection. Force `'qbx'`, `'qb'`, or `'esx'` to override. This is the *identity* layer (who is this player, job/grade/duty) — independent of the MDT backend above.

### Backend tuning — `Config.pMdt` / `Config.lbTablet`

| Key | Default | Meaning |
| ----------------------- | ----------- | ---------------------------------------------------------------------------- |
| `pMdt.job` | `'police'` | Department job passed to p\_mdt exports |
| `pMdt.alertMaxAgeSec` | `3600` | Dispatch feed window |
| `lbTablet.mdt` | `'Police'` | Top-level key in lb-tablet's `config/mdts.json` — **case-sensitive** |
| `lbTablet.requireDuty` | `false` | Additionally require framework on-duty to open the terminal |

***

### Access — `Config.access`

| Key | Default | Meaning |
| --------------- | ---------------------------------- | ------------------------------------------ |
| `jobs` | `{ 'police', 'lspd', 'sasp', 'bcso' }` | Job names treated as police |
| `requireOnDuty` | `true` | Require `job.onduty == true` |
| `acePermission` | `'mrpd_terminal.use'` | ACE that bypasses the job check entirely |

### Feature grades — `Config.features`

A map of `feature = minimumGrade`. A feature renders/executes only if the officer's grade meets the threshold **and** the active backend supports it. Defaults:

| Tier | Features |
| --------------------- | ------------------------------------------------------------------------------------------------------------- |
| **0 — Officer** | `view_citizens`, `view_vehicles`, `view_officers`, `view_flagged_plates`, `view_impound`, `view_cameras`, `broadcast_911` |
| **2 — Sergeant** | `issue_fine`, `flag_plate`, `unflag_plate`, `anklet_location`, `band_add`, `band_remove`, `release_impound` |
| **3 — Lieutenant** | `remote_unjail`, `jail_citizen`, `clear_cuffs` |
| **4 — Chief** | `grant_license`, `revoke_license`, `view_financials`, `hire_officer`, `change_grade`, `fire_officer` |

Rewire freely — the keys are stable, the numbers are yours.

***

### The physical screens — `Config.targets`

{% hint style="info" %}
**One entry per prop model — not per location.** The terminal places no map markers: the interaction attaches to the prop *model*, so **every instance of that model in the world** (baked into an MLO, spawned by a script, placed by hand) becomes interactive with the same calibration. Same geometry → one calibration fits all instances.
{% endhint %}

Per entry:

| Field | Meaning |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| `kind` | `'terminal'` (full MDT) or `'fleet'` (garage kiosk) |
| `model` | prop model hash (backtick name) |
| `targetTxd` / `targetTex` | the texture (dict + name) the screen is rendered onto — the "glass" |
| `label`, `icon` | target option text / Font Awesome icon |
| `calibration` | `{ cam, tl, tr, bl }` — camera pose + screen corners in prop-local space. Capture in-game with `/termcam <idx>` (`Config.debug`) |
| `activeModel` | optional: on focus, the static prop is hidden and this DUI-carrying variant spawns in its place — other instances of the monitor stay dark while one is in use |
| `garageStrategy` | `'nearest'` — for `kind='fleet'`: how the spawn point is picked |
| `debugSpawn`, `debugHeading` | optional dev prop spawn for testing |

**Adding a monitor somewhere else:**

{% stepper %}
{% step %}
#### Same model?

Just place the prop (map editor, script, anything). It's already interactive — nothing to configure.
{% endstep %}

{% step %}
#### New model?

Add a `Config.targets` entry for it, set `Config.debug = true`, stand at the prop and run `/termcam <index>` to capture the camera + screen-corner calibration. Paste the printed values into the entry.
{% endstep %}
{% endstepper %}

***

### Rendering — `Config.dui`

| Key | Default | Meaning |
| ---------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------ |
| `canvasWidth` / `canvasHeight` | `3840×2160` | DUI render resolution. The UI is authored at 1920 wide and zoom-scaled, so raising this **sharpens** the screen without shrinking anything. Keep 16:9. Drop to `2560×1440` if VRAM-tight. |
| `kinds` | `terminal`, `fleet` | One DUI per kind; targets reference a kind. Texture binding is per-target, so many prop models can share one kind. |

### Control mode — `Config.controlMode`

Camera + cursor behavior while using a screen (enter/exit glide, mouse sensitivity, scroll). Defaults fit the shipped MRPD monitors.

### Station scope

`Config.stationCoords` / `Config.stationRadius` — the "at the station" zone used by the dashboard presence card.

### Manual fallbacks — `Config.cameras` / `Config.radars`

Fill these to back the cameras/radars pages when no backend provides them (see the qb-policejob bridge in [Adapters](adapters.md)). Empty by default.

### Live updates — `Config.live`

Throttle windows for live pushes (dispatch toasts, flag updates) and which events re-render open views. Defaults are sensible.
