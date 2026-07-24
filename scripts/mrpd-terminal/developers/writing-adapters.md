---
description: Build a terminal adapter for any police script — contract, capabilities, skeleton
icon: puzzle-piece
---

# Writing Adapters

The terminal can sit on top of **any** police script. If there's no shipped adapter for yours, write one — it's a supported, intended extension point, not a hack.

An adapter answers one question: *"given this police script, how do I read its data and perform its actions?"* The terminal handles everything else — UI, permissions, DUI rendering, live updates.

***

### The two axes — don't mix them

| Axis | Registry | Owns |
| ------------------------------- | ------------------------------------------------ | ------------------------------------------------------------- |
| **Police data** *(this guide)* | `RegisterPoliceAdapter()` — `adapters/<id>.lua` | citizens, vehicles, warrants, dispatch, fines, fleet… |
| **Framework identity** | `RegisterFramework()` — `framework/<id>.lua` | who player X is: identifier, name, job, grade, duty |

Your adapter must **never** contain `if qb-core… elseif es_extended…` branches. For identity, call the `Framework` facade (already resolved for you):

```lua
Framework.resolveIdentifier(src)   -- -> citizenid/identifier or nil
Framework.getJob(src)              -- -> { name, label, grade, gradeLabel, onDuty } or nil
Framework.getName(src)             -- -> "First Last" or nil
Framework.identifierToSource(cid)  -- -> online server id or nil
Framework.onlinePlayers()          -- -> map identifier -> { source, job }
Framework.setDuty(src, on)         -- -> ok, err
Framework.db                       -- -> { players = '...', vehicles = '...' } table names
```

This is why one adapter works on QBCore, Qbox, and ESX unchanged. Adding a new *framework* is the same pattern one axis over — drop `framework/<id>.lua` calling `RegisterFramework{...}`; the full contract is documented in `framework/_registry.lua` (open).

***

### Setup

{% stepper %}
{% step %}
#### Create the file

`prompt_mrpd_terminal/adapters/my_mdt.lua` — server-side only.
{% endstep %}

{% step %}
#### Register it in the manifest

Add to `fxmanifest.lua` → `server_scripts`, **before** `adapters/_detection.lua`.
{% endstep %}

{% step %}
#### Add it to the priority list

Add `'my_mdt'` to `Config.adapterPriority` where you want it to rank. All three files are plaintext in the escrowed build.
{% endstep %}
{% endstepper %}

**Lifecycle:** boot → every adapter registers → `_detection.lua` walks `Config.adapterPriority`, first `detect() == true` wins → your capabilities go to the UI → the UI renders only what you declared → user acts → server gates (grade + feature) → your method runs.

{% hint style="danger" %}
**Gotcha — probing another resource's exports.** Indexing `exports['x'].SomeExport` **throws** (it does not return `nil`) when the resource exists but doesn't declare that export. Always probe under `pcall`:

```lua
local ok, fn = pcall(function() return exports['my_mdt_resource'].GetData end)
if not (ok and fn) then return false end
```
{% endhint %}

***

### Capabilities — how the UI shapes itself

Start from the default (everything off) and switch on what your backend truly has:

```lua
local capabilities = DefaultCapabilities()
capabilities.criminalRecords = true
capabilities.flagPlates      = true
capabilities.dispatch        = true
```

Three states matter:

| Value | Effect |
| ----------- | ----------------------------------------------------- |
| `true` | page / card / section renders |
| `false` | **explicitly hidden** — nav page removed, cards dropped |
| *(omitted)* | default behavior (legacy adapters keep working) |

Page-shaped keys the UI reads: `dispatch`, `warrants`, `bolos`, `incidents`, `evidence`, `charges`, `weapons`, `properties`, `announcements`, `cameras`, `impound`, `jail`, `anpr`, `anklet`, `globalSearch` — plus data-shape flags: `criminalRecords`, `mugshots`, `fingerprints`, `flagPlates`, `fines`, `licenses`, `dispatchFeed`.

**Write gating.** Optionally declare a `writes` map — then every action button renders **only** if its key is `true` there (omit the map entirely to keep all buttons, legacy-style):

```lua
capabilities.writes = {
    flag_plate    = true,
    unflag_plate  = true,
    broadcast_911 = true,
    -- everything not listed stays hidden — no dead "access denied" buttons
}
```

Known write keys: `flag_plate`, `unflag_plate`, `create_warrant`, `serve_warrant`, `cancel_warrant`, `create_bolo`, `resolve_bolo`, `create_incident`, `close_incident`, `create_citizen`, `create_vehicle`, `create_weapon`, `issue_fine`, `grant_license`, `revoke_license`, `broadcast_911`, `respond_dispatch`, `set_callsign`, `toggle_duty`, `jail`, `unjail`, `evidence_checkout`, `evidence_checkin`.

{% hint style="info" %}
**Philosophy: honesty over completeness.** If your backend can't do something, declare it off — an absent button is a feature; a button that errors is a bug.
{% endhint %}

***

### The contract

Authoritative, LuaLS-annotated source: `shared/adapter_interface.lua` (open). Summary:

**Required fields**

```lua
id           = 'my_mdt',            -- unique key, matches the Config.adapterPriority entry
label        = 'My MDT — Police',   -- UI header + boot banner
priority     = 50,
detect       = detect,              -- fun(): boolean — cheap and honest
capabilities = capabilities,
```

**Core reads** — the dashboard + registries expect these:

| Method | Returns |
| ----------------------- | ------------------------------------------------------------------------------------------------------- |
| `getOfficerInfo(src)` | `{ cid, firstName, lastName, callsign, grade, gradeLabel, jobName, onDuty }` or `nil` |
| `getOnDutyOfficers()` | list of officer entries (above + `source`, `online`, `atStation`) |
| `getRoster()` | full roster, online + offline |
| `getCitizenByCid(cid)` | citizen profile (identity, licenses, vehicles, record…) or `nil` |
| `searchCitizens(query)` | list — name / CID / phone match |
| `lookupPlate(plate)` | `{ plate, model, ownerCid, owner, isFlagged, flagReason, … }` or `nil` |
| `getFlaggedPlates()` | list |
| `getVehicleStats()` | `{ registered, policeFleet }` |
| `getFleetData(src)` | `{ ok, fleet = {{model,label,gradeReq}…}, spawns = {{index,x,y,z,heading}…}, officerGrade }` |

**Writes** — return `ok:boolean, err:string?`; decline honestly:

`flagPlate(src, plate, reason)` · `unflagPlate(src, plate)` · `issueFine(src, cid, amount, reason)` · `grantLicense(src, cid, licenseId)` · `revokeLicense(src, cid, licenseId)` · `broadcastAlert(src, message)` · `unjailPlayer(src, cid)` · `requestAnkletLoc(src, cid)`

```lua
function Adapter.issueFine()
    return false, 'Not supported by My MDT'   -- honest decline → UI shows a toast
end
```

**Optional extended surface** — everything the richer pages use (`getWarrants`/`getWarrant(id)`, `getBolos`, `getIncidents`, `getEvidenceList`, `getCharges`, `getDispatches`, `getCameras`, `searchWeapons`/`getWeapon`, `getJailed`, `getImpoundedVehicles`, `setCallsign`, `setDuty`, `logJailed`, …) is **optional**: the server nil-guards every one, so an absent method equals "not supported". Implement what your capability flags promise; skip the rest.

**Access gating** — your side of security. `hasTerminalAccess(src)` and `hasFeature(src, featureKey)` run before every view/write, on top of the terminal's own grade gates. **Fail closed**: on any backend error return `false`, never `true`-by-default.

**Live pushes** *(optional)* — if your backend has an event feed, forward it and the UI toasts + refreshes:

```lua
TriggerEvent('mrpd_terminal:dispatchReceived', { title = '10-31 Robbery', location = 'Legion Sq' })
```

If you subscribe to another resource's hook system, **unsubscribe in `onResourceStop`** — a dead function reference left registered in their VM errors on every event after your resource restarts.

***

### Minimal skeleton

{% code title="adapters/my_mdt.lua" %}
```lua
if not IsDuplicityVersion() then return end

local function detect()
    return GetResourceState('my_mdt_resource') == 'started'
end

local capabilities = DefaultCapabilities()
capabilities.criminalRecords = true
capabilities.flagPlates      = true
capabilities.dispatch        = true
capabilities.writes = { flag_plate = true, unflag_plate = true, broadcast_911 = true }

local Adapter = { id = 'my_mdt', label = 'My MDT — Police', priority = 50,
                  detect = detect, capabilities = capabilities }

function Adapter.hasTerminalAccess(src)
    local j = Framework.getJob(src)
    return j ~= nil and j.onDuty
end

function Adapter.hasFeature(src, key)
    return Adapter.hasTerminalAccess(src)   -- + your own per-feature logic
end

function Adapter.getOfficerInfo(src)
    local id = Framework.resolveIdentifier(src); if not id then return nil end
    local j  = Framework.getJob(src)
    local first, last = (Framework.getName(src) or '? ?'):match('^(%S+)%s+(.*)$')
    return { cid = id, firstName = first, lastName = last, callsign = '—',
             grade = j and j.grade or 0, gradeLabel = j and j.gradeLabel or 'Officer',
             jobName = j and j.name or '?', onDuty = j and j.onDuty or false }
end

function Adapter.lookupPlate(plate)
    local ok, v = pcall(function() return exports['my_mdt_resource']:GetVehicle(plate) end)
    if not ok or not v then return nil end
    return { plate = plate, model = v.model, ownerCid = v.owner,
             isFlagged = v.flagged == true, flagReason = v.flagReason }
end

function Adapter.flagPlate(src, plate, reason)
    local ok = pcall(function() exports['my_mdt_resource']:FlagPlate(plate, reason) end)
    return ok, ok and nil or 'My MDT rejected the flag'
end

function Adapter.issueFine() return false, 'Not supported by My MDT' end

RegisterPoliceAdapter(Adapter)
```
{% endcode %}

Study `adapters/qb_policejob.lua` (real backend + SQL fallbacks + an export-bridge pattern) and `adapters/showcase.lua` (every method shaped correctly with mock data) for the full picture.

***

### Golden rules

1. **Fail closed** on gates; **decline honestly** on writes (`false, reason`).
2. **Never throw** because a backend is missing or stubbed — `GetResourceState` first, `pcall` around every export access.
3. **Don't touch other resources' internals** — public exports and documented DB tables only. If an export doesn't exist, hide the feature and ask that script's developer for it.
4. **Unsubscribe on `onResourceStop`** from any external hook system.
5. **No framework branches** in adapters — that's the `Framework` facade's job.
6. **Declare, don't pretend** — capabilities are a promise to the player.

### Testing checklist

* [ ] Boot banner shows **your** id/label; the `Config.debug` capability dump matches your intent
* [ ] Nav shows only your declared pages; no dead buttons anywhere
* [ ] Dashboard, citizen search + detail, plate lookup render real data
* [ ] Every declared write round-trips (do → visible change → undo)
* [ ] `stop <your backend>` mid-session → gates fail closed, zero script errors; `start` → recovers
* [ ] A grade-0 officer is view-only (writes denied cleanly)
* [ ] With a second backend installed, reordering `Config.adapterPriority` flips selection correctly
