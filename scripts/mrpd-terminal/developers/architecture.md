---
description: The three axes, the request flow, and where the terminal is going
icon: sitemap
---

# Architecture

How the terminal is built, why it's structured this way, and what's planned.

***

### The three axes

The design separates three concerns that most MDT scripts fuse together:

```
┌─────────────────────────────────────────────────────────────────┐
│  PHYSICAL AXIS — Config.targets                                 │
│  which prop models are screens, their calibration, which KIND   │
│  of screen each one opens ('terminal' MDT / 'fleet' kiosk)      │
├─────────────────────────────────────────────────────────────────┤
│  DATA AXIS — adapters/*.lua  (RegisterPoliceAdapter)            │
│  where police data lives: wasabi / lb-tablet / p_mdt /          │
│  qb-policejob / your own — one active, capability-declared      │
├─────────────────────────────────────────────────────────────────┤
│  IDENTITY AXIS — framework/*.lua  (RegisterFramework)           │
│  who a player is: QBCore / Qbox / ESX — identifier, job,        │
│  grade, duty                                                    │
└─────────────────────────────────────────────────────────────────┘
```

Each axis is a plug-in registry with a small contract. Any combination works — LB Tablet on ESX, wasabi on Qbox, a community adapter on QBCore. No code in one axis references a concrete member of another.

### Request flow

```
player walks to a monitor
  → target interaction (attached per prop MODEL — every instance works)
  → camera glides to the calibrated screen pose;
    the static prop swaps for the DUI-carrying variant
  → the UI renders on the monitor's glass (DUI texture); mouse is forwarded
  → UI action → server callback
  → access gate → grade gate (Config.features)
  → ActiveAdapter.<method>(...)      ← the only line that touches a backend
  → result → UI; writes also audit + live-push to other open terminals
```

The UI is capability-driven end to end — nav pages, sections, and action buttons each check the adapter's declarations, so the same UI produces a genuinely different terminal per backend with no dead surfaces.

***

### Open vs escrowed

Our position: **transparent about our layer, protective of other people's layers.**

| Component | Ships as | Why |
| ----------------------------------------------- | -------- | ---------------------------------------------------------------- |
| `config.lua`, docs | open | yours to read and edit |
| `shared/adapter_interface.lua` — the contract | open | you can't target an API you can't read |
| `framework/_registry.lua` — framework contract | open | same reason |
| `adapters/qb_policejob.lua` | open | the complete reference adapter |
| `adapters/showcase.lua`, `adapters/null.lua` | open | teaching examples — mock data / empty state |
| `server/`, `client/`, `html/` | escrowed | our core product |
| `adapters/wasabi_mdt.lua`, `lb_tablet.lua`, `p_mdt.lua` | escrowed | they embed export surfaces of other developers' paid scripts, shared with us for these integrations |

Custom adapters work against the escrowed build — your adapter file, `fxmanifest.lua`, and `config.lua` stay plaintext.

***

### Roadmap

Where this is going. The structure below is already in place today; timing isn't promised.

#### Placeable screens

Today, any instance of a *known* monitor model is already interactive (interactions attach per-model), and a new model is one config entry + one `/termcam` calibration. Planned: an **in-game placement tool** — spawn a monitor prop anywhere (any interior, any desk), calibrate it visually, persist it, and choose what it opens. Same resource, no per-map builds.

#### Beyond police — departments

Nothing in the adapter contract is inherently police-only — it's identity + registry reads + gated writes + a dispatch feed. Planned: **department-scoped terminals** — EMS/hospital records, sheriff, DOJ — where a placement declares its department, each department resolves its own adapter, and access/features are configured per department.

What that means for you:

* **Server owners** — nothing to prepare; future versions default to current behavior (police).
* **Adapter authors** — the contract in [Writing Adapters](writing-adapters.md) is the stable target. Department support arrives as *additive* context; `RegisterPoliceAdapter` remains valid permanently.

### Versioning promise

* Adapter and framework contracts change **additively only** — new optional methods and capability keys may appear; existing names and return shapes don't break.
* Capability keys the UI learns are always optional — adapters that don't declare them get the legacy default.
* If a breaking change is ever unavoidable, it ships behind a major version with migration notes on this page.
