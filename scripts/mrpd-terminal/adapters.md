---
description: Supported backends, what each one lights up, and per-backend setup
icon: plug
---

# Adapters

The terminal reads and writes police data exclusively through an **adapter** — one per backend, one active at a time. The UI then builds itself from what that adapter *declares it can do*: pages, cards, and buttons for unsupported features simply don't render. Different backends genuinely produce different terminals — with **no dead buttons**.

{% hint style="success" %}
**Big thanks to [Wasabi](https://wasabiscripts.com), [pscripts](https://pscripts.tebex.io/), Kartik and Night** for working with us and providing the exports that make these integrations possible ❤️
{% endhint %}

| Adapter | Backend | Status | Ships as |
| -------------- | ---------------------------------------------------------------- | ------------- | ---------------------------------- |
| `wasabi_mdt` | [Wasabi Advanced MDT](https://wasabiscripts.com) | verified | escrowed |
| `p_mdt` | [pscripts](https://pscripts.tebex.io/) p\_mdt (+ p\_policejob) | verified | escrowed |
| `lb_tablet` | LB Tablet (MDT app) | verified | escrowed |
| `redutzu_mdt` | Redutzu MDT | verified | escrowed |
| `kartik_mdt` | Kartik MDT (`kartik-mdt` v2.1.1+) | verified | escrowed |
| `nightshifts` | Night Shifts MDT (`night_shifts_mdt` v1.4.7+) | verified | escrowed |
| `lonexcad` | LonexCAD (web CAD over HTTP) | 🧪 **beta** | escrowed |
| `sonoran` | Sonoran CAD (via `sonorancad`) | 🧪 **beta** | escrowed |
| `qb_policejob` | stock qb-policejob + framework DB | verified | **open — the reference adapter** |
| `showcase` | none — scripted demo data | — | open |
| `null` | none — honest empty state | — | open |

{% hint style="warning" %}
**What "beta" means here.** A beta adapter was written from the vendor's documentation and has **never been run against a real install** of the product it wraps. It shows an amber **BETA · UNVERIFIED** badge in the toolbar and prints a notice in your server console on startup.

If a page looks empty on a beta adapter, that may be **our integration rather than your data** — please report it and we'll fix it fast.
{% endhint %}

{% hint style="info" %}
**Why are some adapters escrowed?** They embed integration details of *other developers'* paid products — export surfaces and data shapes shared with us for these integrations. Closing them protects that work. The adapter **contract** itself is open, and `qb_policejob.lua` ships fully readable as a worked example — you can build an adapter for any backend: see [For Developers](developers/README.md).
{% endhint %}

***

### Capability matrix

What each backend lights up. ✓ = renders · — = hidden · `pj` = requires p\_policejob next to p\_mdt.

| Feature / page | wasabi\_mdt | p\_mdt | lb\_tablet | qb\_policejob |
| -------------------------------- | ----------- | -------------- | ------------------ | ------------------- |
| Citizens + criminal records | ✓ | ✓ | ✓ | ✓ |
| Mugshots / avatars | — | ✓ | ✓ | — |
| Fingerprints | ✓ | pj | ✓ | ✓ |
| Vehicles + flagged plates | ✓ (BOLO-backed) | ✓ | ✓ (warrant-backed) | ✓ |
| Warrants | ✓ | ✓ (read) | ✓ | — |
| BOLOs | ✓ | ✓ | — | — |
| Incidents | ✓ | — | — | — |
| Evidence | ✓ | pj | — | — |
| Charges catalog | ✓ | ✓ | ✓ | — |
| Weapons registry | ✓ | ✓ (read) | ✓ | — |
| Properties | ✓ | — | — | — |
| Announcements | ✓ | — | — | — |
| Global search | ✓ | — | — | — |
| Dispatch (911 + live feed) | ✓ | ✓ | ✓ | ✓ |
| Fines | — | ✓ (real money) | — | ✓ |
| Licenses (grant/revoke) | — | ✓ | ✓ | ✓ |
| Jail roster | — | pj | ✓ | — |
| Impound | — | pj | — | — |
| Anklet / tracking bands | — | pj | — | — |
| Cameras | ✓ (live view) | pj | — | ✓ (via bridge) |
| ANPR / radar hits | — | pj | — | — |

And the newer backends — 🧪 marks the two beta adapters:

| Feature / page | redutzu\_mdt | kartik\_mdt | nightshifts | 🧪 lonexcad | 🧪 sonoran |
| -------------------------------- | ------------ | ----------- | ----------- | ----------- | ---------- |
| Citizens + criminal records | ✓ | ✓ | ✓ | ✓ | ✓ |
| Mugshots / avatars | ✓ | — | — | ✓ | — |
| Fingerprints | ✓ | ✓ | — | — | — |
| Vehicles + flagged plates | ✓ | — | ✓ | ✓ | ✓ |
| Warrants | ✓ | ✓ | ✓ | ✓ | ✓ |
| BOLOs | ✓ | — | ✓ | ✓ | ✓ |
| Incidents | ✓ | — | — | — | — |
| Evidence | ✓ | — | — | — | — |
| Charges catalog | ✓ | ✓ | ✓ | — | ✓ |
| Weapons registry | ✓ | — | — | — | — |
| Properties | ✓ | — | — | — | — |
| Announcements | ✓ | — | — | — | — |
| Global search | — | — | — | ✓ | — |
| Dispatch (911 + live feed) | — | ✓ | ✓ | ✓ | ✓ |
| Fines | — | — | ✓ | — | — |
| Licenses (grant/revoke) | ✓ | ✓ | ✓ | ✓ | ✓ |
| Jail roster | — | — | — | ✓ | — |
| Impound | — | — | — | — | — |
| Anklet / tracking bands | — | — | — | — | — |
| Cameras | ✓ | — | — | — | — |
| ANPR / radar hits | — | — | ✓ | — | ✓ |

{% hint style="warning" %}
The matrix reflects what each **backend exposes** — not what we chose to build. When a backend ships more exports, its adapter (and this matrix) grows.

A few entries are blocked on the vendor rather than on us — for example Redutzu's Dispatch page is hidden because the terminal can *push* a call to their dispatch but there's no export to *read* the list back. Those stay hidden rather than half-working, and turn on by themselves once the export lands.
{% endhint %}

***

### The fleet kiosk

The garage screen (`kind='fleet'`) lists grade-authorized vehicles and spawns them. A vehicle fleet is a *police-job* concern, not MDT data, so resolution is automatic:

1. If the **active** adapter owns a fleet (p\_mdt, qb\_policejob) — it serves it.
2. Otherwise the terminal **falls back** to any other *installed* adapter that provides one — e.g. Wasabi or LB Tablet as the MDT + qb-policejob installed still gets a working kiosk.
3. Nothing provides a fleet → a calm *"Vehicle fleet isn't supported by the … adapter."* message. No error, no configuration needed.

***

### Per-backend setup

{% tabs %}
{% tab title="Wasabi MDT" %}
Works out of the box once `wasabi_mdt` is started before the terminal.

* **Duty is wasabi's own** (`Officers[].onDuty`) — it defaults **off**; officers toggle it in the MDT/terminal.
* Citizen identity stays in wasabi's citizen ID space.
* Plate flags are BOLO-backed.
* Serve/cancel-warrant style *write* exports are **auto-probed** — if wasabi ships them in a later version, the buttons appear by themselves.
{% endtab %}

{% tab title="pscripts p_mdt" %}
Backend by [pscripts](https://pscripts.tebex.io/). Set your department if it isn't `police`:

{% code title="config.lua" %}
```lua
Config.pMdt = { job = 'police', alertMaxAgeSec = 3600 }
```
{% endcode %}

* Write features are verified against **p\_mdt 2.1.8+** — older builds lack the required exports. Reads work either way.
* With **p\_policejob** also installed, the enforcement pages (jail, impound, anklet, cameras, ANPR, evidence) light up automatically; without it they stay hidden.
* Fines move **real money** (bank/invoice).
* The fleet kiosk lists vehicles the department has **purchased in p\_mdt's own garage** — a fresh install with none purchased shows an empty (but working) kiosk.
{% endtab %}

{% tab title="LB Tablet" %}
Set your MDT key if it isn't the default:

{% code title="config.lua" %}
```lua
Config.lbTablet = {
    mdt         = 'Police',   -- key from lb-tablet/config/mdts.json — CASE-SENSITIVE
    requireDuty = false,
}
```
{% endcode %}

* Plate flag = warrant-with-vehicle-target; soft-closing the warrant clears the flag and keeps the record.
* Jail roster shows **live framework sentences**.
* Fine *deduction* has no LB export yet — fines stay hidden rather than half-working.
{% endtab %}

{% tab title="Redutzu MDT" %}
Works out of the box once `redutzu-mdt` is started before the terminal.

{% code title="config.lua" %}
```lua
Config.redutzu = {
    requireDuty    = false,   -- true = also require Redutzu duty (IsDuty) to open the terminal
    boloExpiryDays = 30,      -- expiry written onto BOLOs the terminal creates
}
```
{% endcode %}

* Their MDT doesn't require duty, so `requireDuty` defaults **off**.
* Cameras are read-only, backed by their own `mdt_cameras` table.
* The Dispatch page is hidden: the terminal can push a 911 broadcast into their dispatch, but there's no export to read the call list back.
{% endtab %}

{% tab title="Kartik MDT" %}
Requires **kartik-mdt v2.1.1 or newer** — that's the version that added the export API.

{% code title="config.lua" %}
```lua
Config.kartik = {
    requireDuty         = false,  -- true = also require Kartik's onDuty
    penalCodeDepartment = nil,    -- e.g. 'police' to filter the charges list; nil = all
    dispatchTtlSec      = 3600,   -- how long a 911 call stays on the Dispatch page
}
```
{% endcode %}

* Includes a **live dispatch feed**.
* Kartik has no export to read its existing call list, so the Dispatch page accumulates live calls — calls created *before* the resource started aren't shown. `dispatchTtlSec` controls how long they linger.
{% endtab %}

{% tab title="Night Shifts MDT" %}
Requires **night\_shifts\_mdt v1.4.7 or newer**.

{% code title="config.lua" %}
```lua
Config.nightshifts = {
    requireOnShift = true,   -- Night Shifts owns duty ("on shift"); their MDT requires it
    departments    = nil,    -- department ids allowed to use the terminal; nil = any
    permissions    = nil,    -- override our feature -> permission mapping if needed
}
```
{% endcode %}

* Duty is **Night Shifts' own** "on shift" state, and their MDT requires it — so `requireOnShift` defaults **on**. Set it `false` to let any MDT user open the terminal.
* `permissions` maps our features onto their Admin → Ranks permission strings, e.g. `permissions = { flag_plate = 'pnc.anpr' }`.
{% endtab %}

{% tab title="LonexCAD (beta)" %}
{% hint style="warning" %}
**Beta — unverified.** Written from LonexCAD's documentation and never run against a real CAD. Enable it and tell us what breaks.
{% endhint %}

A web CAD reached over HTTP, so it only activates once **all three** of `enabled`, `baseUrl` and `apiKey` are set:

{% code title="config.lua" %}
```lua
Config.lonex = {
    enabled        = true,
    baseUrl        = 'https://cad.yourserver.com',   -- no trailing slash
    apiKey         = 'cad_...',                      -- CAD admin -> API Keys
    departments    = { 'LSPD', 'BCSO', 'SAHP' },     -- LEO short_names; empty = any
    dutyDepartment = 'LSPD',                         -- used when clocking in from the terminal
    timeoutMs      = 5000,                           -- a dead CAD degrades to empty pages
}
```
{% endcode %}
{% endtab %}

{% tab title="Sonoran CAD (beta)" %}
{% hint style="warning" %}
**Beta — unverified, and off by default on purpose.** Turning this on opts you in to testing an unverified integration against your **live** CAD. Reads degrade to empty pages; record writes stay hidden unless your CAD templates resolve.
{% endhint %}

{% code title="config.lua" %}
```lua
Config.sonoran = {
    enabled        = true,   -- opt-in
    requireCadUnit = true,   -- require being signed in to a unit in the CAD
}
```
{% endcode %}

**If you run it, please help us verify it.** Run this in your server console and post the output in our Discord — that one command answers everything we still need to check:

```
termsonoran_probe <lastname> <plate>
```

Sonoran sits **below** the other MDTs in the detection order on purpose: Sonoran ships its own in-world CAD display, so a server running both already has a screen and is more likely to want the other MDT on the terminal.
{% endtab %}

{% tab title="qb-policejob" %}
Works out of the box against the framework DB (`players`, `player_vehicles`).

**Optional 5-line bridge** — shares `/flagplate` state both ways and fills the cameras/radars pages. In `qb-policejob/server/vehicle.lua`, right below `local Plates = {}`:

{% code title="qb-policejob/server/vehicle.lua" %}
```lua
exports('GetFlaggedPlates',   function() return Plates end)
exports('AddFlaggedPlate',    function(plate, reason) Plates[plate:upper()] = { isflagged = true, reason = reason or 'no reason given' } end)
exports('RemoveFlaggedPlate', function(plate) if Plates[plate:upper()] then Plates[plate:upper()].isflagged = false end end)
exports('GetCameras',         function() return Config.SecurityCameras end)
exports('GetRadars',          function() return Config.Radars end)
```
{% endcode %}

Then `restart qb-policejob` + `restart prompt_mrpd_terminal` and look for the three green checkmarks in the console banner. The lines only **add** exports — nothing existing changes, and they're harmless if the terminal is removed.

Without the bridge: BOLOs stay terminal-scoped, and cameras/radars fall back to `Config.cameras` / `Config.radars` or hide.
{% endtab %}

{% tab title="showcase / null" %}
* **`showcase`** — activated by `Config.showcase = true`. Every page populated with scripted demo data, permissions bypassed. For previews/videos — and it's also a readable end-to-end example adapter.
* **`null`** — what you get with no backend at all: the terminal opens, states honestly that no data source is connected, and nothing errors.
{% endtab %}
{% endtabs %}

***

{% hint style="info" %}
**MDT developer?** Want your script in this list with an official, maintained adapter? See [Integrating Your MDT](developers/mdt-integration.md) — it's a short export checklist, and we do the rest.
{% endhint %}
