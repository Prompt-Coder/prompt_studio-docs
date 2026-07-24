---
description: MDT developer? What to provide so we can ship a first-class adapter for your script
icon: handshake
---

# Integrating Your MDT

This page is for **MDT / police-script developers** who want their product supported by the MRPD Terminal as a shipped adapter — the way [Wasabi](https://wasabiscripts.com) and [pscripts](https://pscripts.tebex.io/) already are.

**The short version:** you expose server-side exports for the data you already have; we build and maintain the adapter, and your MDT becomes a supported backend with credits and a store link in these docs. Your script stays the **source of truth** — the terminal is an in-world screen for it, not a replacement, and the adapter we write for you ships **escrowed**, so the integration details of your product stay protected.

{% hint style="info" %}
**Contact:** reach us on Discord — [discord.gg/rKbHHdfZFU](https://discord.gg/rKbHHdfZFU) — with "MDT integration" and your script's name.
{% endhint %}

***

### How the integration works

{% stepper %}
{% step %}
#### You send us access + the export surface

A dev copy or Keymaster grant of your MDT (for our test server), plus your export documentation — or just the export **names**; we're happy to probe shapes ourselves (we've done 40–99 export probes per integration before).
{% endstep %}

{% step %}
#### We build the adapter

We write and maintain `adapters/<your_mdt>.lua` against our open adapter contract, plus an automated test battery that runs against a real install of your script on our QB test server.
{% endstep %}

{% step %}
#### Verification pass together

We confirm shapes, permissions, and edge cases with you (usually a handful of quick questions), run the in-world verification, and lock the integration.
{% endstep %}

{% step %}
#### Shipped + credited

Your MDT appears in [Adapters](../adapters.md) with your store link, the capability matrix row, and a thank-you credit. When you ship new exports later, features light up — several of our probes are automatic.
{% endstep %}
{% endstepper %}

***

### What we need — the export surface

Everything below is **server-side exports** returning plain Lua tables (JSON-serializable). You almost certainly have this data already — this is about exposing reads, not building features.

#### Tier 1 — minimum for a useful terminal

| # | Export (naming is yours) | Returns |
| - | ------------------------------------ | ------------------------------------------------------------------------------------------------ |
| 1 | Get officer by server id *(or documented permission model)* | name, callsign, rank/grade, department, on-duty — enough to identify who's at the keyboard |
| 2 | Get citizen by id | identity (names, DOB), licenses, mugshot/avatar URL if you have one, record summary |
| 3 | Search citizens | by name (ideally also id / phone), returning a list of matches |
| 4 | Lookup vehicle by plate | owner id + display name, model/label, flagged/BOLO state if you track it |
| 5 | Citizen's owned vehicles | list for the citizen profile |

With Tier 1 alone, your MDT gets a working terminal: dashboard, citizen registry, vehicle registry.

#### Tier 2 — records (each one lights up a page)

* Warrants — list + get-by-id, **including the subject** (citizen or vehicle), status, issuing officer, timestamps
* BOLOs — list + get + resolve state
* Incidents / reports — list + get
* Charges catalog — your offence list (title, category, fine, sentence, severity)
* Weapons registry — list/search + get (serial, owner, name)
* Evidence — list + get
* Jail — roster with remaining time

#### Tier 3 — actions (write exports)

* Flag / unflag plate (or BOLO create + resolve — either model works for us)
* Create warrant
* Create dispatch / broadcast
* **Issue fine — including the money movement** (the #1 gap we hit: a fine that only writes a record can't be offered as a real "Issue fine" button)
* Grant / revoke license
* Jail (log a sentence)
* Set callsign · set duty

For every write, tell us one thing: **is it permission-gated inside your script, or should we gate it?** Both are fine — we already pre-gate writes for some partners — we just need to know, so nothing is double-gated or wide open.

#### Tier 4 — live events (what makes it feel alive)

* **Dispatch created** — a hook/callback or event we can subscribe to for the live feed + toasts
* Duty changed — fires on duty toggles
* Optional: record created/updated notifications

{% hint style="warning" %}
If your hook system takes **function references**, please also provide an **unsubscribe** (`RemoveCheck`-style). Without one, our function reference dies inside your VM when our resource restarts, and your script then errors on every event. We hit this in production — a 2-line remove export prevents it.
{% endhint %}

***

### Technical ground rules

The lessons from our existing integrations, distilled:

1. **Server-side exports.** Client-only exports can't back a server-authoritative terminal.
2. **Callable when idle** — exports must work without your UI being open and without hidden init steps. If there's a boot-order requirement, document it.
3. **Stable identifiers** — tell us whether your citizen IDs are the framework's (citizenid/identifier) or your own ID space, and keep record IDs stable.
4. **Plain-table returns** — no functions/userdata in results; shapes documented *or* probe-able (we'll happily dump shapes ourselves on a dev license).
5. **Fail soft** — an export called with a valid-but-unknown id should return `nil`/empty, not error.
6. **Additive versioning** — add fields/exports freely (we auto-probe several and light features up automatically); ping us before renaming or changing shapes so we ship the adapter update alongside your release.
7. **DB reads as fallback** — where an export doesn't exist yet, we may (with your blessing) read your tables read-only until you ship one. Exports are always preferred — table schemas churn.

### What you never have to build

UI/UX, the DUI rendering and monitor calibration, framework identity (QBCore/Qbox/ESX), grade/permission configuration, capability gating, the fleet kiosk fallback, documentation, and support for the terminal itself — all ours. **You expose data; we do the rest.**

***

### What you get

* A shipped, maintained adapter — your customers get an in-world physical terminal for *your* MDT with zero work on your side
* Your product listed in [Adapters](../adapters.md) with your store link + credit (see the thank-you to Wasabi and pscripts — that's the treatment)
* Escrowed adapter — your export surface and data shapes aren't exposed in plaintext
* Features that auto-appear for your users when you ship new exports

{% hint style="success" %}
Sound good? Ping us — [discord.gg/rKbHHdfZFU](https://discord.gg/rKbHHdfZFU). Worst case it's a 20-minute conversation; best case your MDT gets a physical in-world terminal your competitors don't have.
{% endhint %}
