---
icon: transporter-1
---
# Animations Core 2.0

## Animations Core 2.0

### Prompt Anim Core

***

<details>

<summary><strong>Overview</strong></summary>

<br>

Prompt Anim Core 2.0 is a standalone gym equipment system for FiveM that provides:

* **Location-based gym management** (spawn equipment by location)
* Multiple **equipment types** with synchronized animations
* **In-game group editor** — create, edit, and manage gym setups without touching config files
* **Membership system** — optionally restrict gym usage to members, with admin commands and exports
* **Persistent prop despawn** — mark world props for removal (they stay deleted even after leaving/re-entering)
* **Clear Location** feature (hide vanilla objects inside a radius)
* Optional **boxing ring** support
* Admin placement tool: **`/gymcreator`**
* Developer exports for spawning/removing equipment, managing locations, and membership
* **Hooks** — per-machine custom logic (allow/deny, on start, on end) without touching core files
* **3D sound cues** per machine (entrance / rep / exit / loop), synced client-side to the animation
* Client-server synchronization + resource-based cleanup

</details>

***

<details>

<summary><strong>What's new in 1.3.1</strong></summary>

<br>

**Third-party stat providers.** anim_core can now feed **rtx\_gym** or **vms\_gym** instead of its own stat system — set `stats.provider` in `config_s.lua` and every completed rep is pushed into that resource's stat database through its public exports. The provider keeps owning decay, item boosters, and gameplay effects (anim_core's own modifiers and decay switch off automatically, so nothing double-applies), and `/gymstats` shows the provider's values — with vms\_gym it opens vms's own statistics menu. Ships with a ready mapping for vms\_gym; for rtx\_gym fill the stat names from their documentation into `stats.providerMap`.

* New **`onRep`** hook event — fires server-side for every completed rep; wire any other XP/stat/drug system there
* New **`statMultiplier`** editable function (`config/server.lua`) — scale pushed gains, e.g. to honor a provider's booster items
* Fixed: `stats.enable = false` now also stops per-rep stat gains (previously it only stopped decay), and the exhaustion recovery loop no longer depends on the stats system being enabled

</details>

***

<details>

<summary><strong>What's new in 1.3.0</strong></summary>

<br>

**Rebuilt synchronization engine.** The server no longer spawns networked props — every client renders its own local equipment, viewers pin the user's ped at the exact seat position (no floating or sliding on machines), and exercises replay in step on every screen. This fixes the long-standing issues where other players saw someone standing inside a machine, saw no equipment motion, or saw a "ghost rep" when someone sat down. Late joiners now see machines in use correctly, and cleanup is identical whether a player exits normally or crashes.

**New features:**

* **Hooks system** (`hooks/` folder) — gate machine use and react to start/end per spot, server- and client-side, crash-safe (fail-open)
* **3D sound cues** — optional `sounds` block per equipment type (start / rep / stop / loop), played per prop and per client
* **`restAnimation`** — dedicated rest loop per machine (the bench ships with one)
* **Per-call membership** — `CreateGymLocation(..., { requireMembership = true/false })` plus `GetDynamicLocation` / `SetLocationMembership` exports
* **Client exports** — `IsPlayerAnimated()` / `StopPlayerAnim(instant)` so death/cuff/admin scripts can release a player cleanly
* **ultraDebug** — live sync telemetry from every client into the server console for support

**Updating from 1.2.x:** drop-in — configs and exports are backward compatible. The update adds new files, so do a **full server restart** and have players **reconnect** (a plain `restart` won't load new files).

</details>

***

### Installation Instructions

{% stepper %}
{% step %}

#### Step 1 — Install dependencies

Ensure these resources are installed:

* **ox\_lib** (required)
* **ox\_target** (optional, recommended)
  {% endstep %}

{% step %}

#### Step 2 — Install Prompt Anim Core

Place the resource folder in your `resources` directory:

<pre><code><strong>resources/prompt_anim_core_2_new
</strong></code></pre>

{% endstep %}

{% step %}

#### Step 3 — Start order (server.cfg)

Add this to your `server.cfg` (keep the order):

<pre class="language-cfg"><code class="lang-cfg"><strong>ensure ox_lib
</strong><strong>ensure ox_target   # Optional but recommended
</strong><strong>ensure prompt_anim_core_2_new
</strong></code></pre>

{% endstep %}

{% step %}

#### Step 4 — Restart & test

Restart your server and run:

* `/gymcreator`

If you can place equipment and interact with it (target or TextUI), installation was successful ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

{% hint style="info" %}
**Tip:** Keep `ox_lib` above this resource in your cfg. It provides menus, callbacks, notifications, and fallback zones used by the system.
{% endhint %}

***

<details>

<summary><strong>Configuration</strong></summary>

<br>

#### Server Config (`config/config_s.lua`)

```lua
{
    debug = false,            -- Debug logging: also relays every client's sync log into the SERVER console
    ultraDebug = false,       -- With debug: doer + viewers stream live anim/prop state 2x/sec (support tool)

    enableMinigame = false,   -- Enable skill check minigame when starting exercises

    gymCreator = {
        enable = true,
        restricted = 'group.admin',  -- ACE restriction for /gymcreator (false = unrestricted)
        canAccess = function(source) -- Extra custom permission logic on top of the ACE check
            return true
        end,
    },

    exhaustion = {
        enable = false,              -- Fatigue system (slows rep speed as muscles tire)
        recoveryRate = 0.01,         -- Recovery per minute
        enableMuscleGroups = true,   -- Track per muscle group
        muscleGroups = { ... },      -- Which equipment trains which muscle group
        rates = { ... },             -- Exhaustion added per exercise, per equipment type
    },

    groups = {
        enable = true,               -- Groups system (Manage Groups in /gymcreator)
        creatorCanEdit = true,       -- Original creator can edit without admin
        creatorCanDelete = false,    -- Original creator can delete without admin
        despawnCheckInterval = 10000, -- Re-check for respawned world props (ms)
    },

    membership = {
        enable = false,              -- When true, ALL gym locations require membership
        exemptLocations = {          -- Locations that never require membership
            -- 'prison',
        },
        commandRestricted = 'group.admin',  -- ACE restriction for membership commands
    },

    stats = {
        enable = true,               -- Stat progression (4 stats: speed, stamina, combat, strength)
        provider = 'internal',       -- 'internal' | 'rtx_gym' | 'vms_gym' — push gains into a third-party stat system instead
        providerMap = { ... },       -- anim_core stat -> provider stat/skill name (vms mapping ships ready)
        rates = { ... },             -- Stat gains per exercise, per equipment type
        decrease = {                 -- Stats decay over time when not training (internal provider only)
            enable = true,
            multiplier = 1.0,        -- Global decay speed (0.5 = half, 2.0 = double)
            -- per-stat decay per minute: speed / stamina / combat / strength
        },
    },
}
```

***

#### Client Config (`config/config_c.lua`)

Key sections:

```lua
{
    language = 'auto',           -- 'auto' or one of 12 shipped locales (en, es, fr, de, pt, ru, it, pl, zh, ko, sv, ar)
    renderDistance = 100.0,      -- Distance to render gym locations
    interaction = 'auto',        -- 'auto', 'ox_target', 'qb_target', 'textUI', 'custom'
    progressBar = 'built-in',    -- 'built-in' or 'custom' (see below)

    blip = {
        enable = true,           -- Master toggle for ALL gym blips
        sprite = 311,
        color = 21,
        scale = 0.9,
        label = 'Gym',
        showLocationBlips = false, -- Also create a blip per equipment location (off = static blips only)
        coords = {               -- Static map blips, optionally tied to resources
            { coords = vec3(x, y, z), label = 'Vinewood Gym' },
            -- only shows while one of these resources is running:
            -- { coords = vec3(x, y, z), label = 'Prison Gym', resources = { 'prompt_prison_study' } },
        },
    },

    boxingRing = {
        enable = true,
        model = "vision_gymboxingring",
        roundDuration = 60,      -- Round duration in seconds
        cancelDistance = 6.0,    -- Leave this radius mid-fight = you lose
        showBoundary = true,     -- Red sphere boundary shown during the fight
        coords = { ... },        -- Ring placements (vec4)
        conditionalCoords = {    -- Rings that only exist while a resource is running (MLO rings)
            { resources = { 'prompt_prison_study' }, coords = vec4(x, y, z, h), cancelDistance = 6.1 },
        },
    },

    locations = {
        ['my_gym'] = {
            coords = vec3(x, y, z),
            -- requireMembership = false,  -- Optional: exempt from membership
            props = { ... },
        },
    },

    props = { ... },  -- Equipment type definitions (models, animations, sounds, restAnimation)
}
```

**Custom progress bar** — set `progressBar = 'custom'` and implement the function in the same file:

```lua
customProgressBar = function(machine, duration)
    exports['your-progressbar']:Start(duration)
end
```

***

#### Editable Server Functions (`config/server.lua`)

This file contains functions you can customize:

* `server.canUseMachine(source, data)` — permission check before accessing equipment (membership check runs here automatically)
* `server.canDoExercise(source, data)` — permission check before starting an exercise
* `server.updateStats(source, data)` — stat progression storage (pre-configured for QBCore, QBX, ESX; JSON fallback for standalone)
* `server.getPlayerName(source)` — player name for boxing ring display
* `server.boxingRing.onFightStart / onFightEnd` — match hooks (pre-configured to revive both fighters)

#### Editable Client Functions (`config/client.lua`)

* `client.notify(title, message, type)` — swap in your own notification system
* `client.minigame(machine)` — the skill check used when `enableMinigame = true` (default: ox_lib skillCheck)
* `client.onExerciseStart / onExerciseEnd` — busy-state hooks (default: sets `invBusy`, disables targeting)
* `client.boxingRing.onFightStart / onFightEnd(result)` — client-side match hooks

</details>

***

<details>

<summary><strong>Groups System</strong></summary>

<br>

The groups system lets you create, edit, and manage gym equipment setups entirely in-game, without editing config files. Groups are saved to `groups/saved_groups.json` and persist across server restarts.

#### How to Use

1. Run `/gymcreator` and select **Manage Groups**
2. **Create New Group** — give it a name
3. **Add Props** — select equipment type, position it in the world with scroll to rotate, ENTER to place
4. **Mark Props for Despawn** — aim at world props you want removed, press E to mark, ENTER to apply
5. **Save Group** — saves to JSON and immediately loads the gym

#### Group Management Menu

From **Manage Groups** you can:

* **Load / Unload** groups (spawn/despawn all props)
* **Edit** a loaded group (add/move/delete props, mark/unmark despawns)
* **Toggle Auto-Load** — groups with auto-load enabled spawn automatically on server start
* **Toggle Membership Requirement** — require membership to use equipment in this group
* **Delete** a group permanently

#### Permissions

* **Admins** (matching `gymCreator.restricted` ACE) can edit/delete any group
* **Creators** can edit their own groups if `groups.creatorCanEdit = true` in config
* **Creators** can delete their own groups if `groups.creatorCanDelete = true` in config
* Creator identity is tracked by player license (framework-agnostic)

#### Persistent Prop Despawn

When you mark world props for despawn in a group:

* They are deleted when the group loads
* If a player leaves and re-enters the streaming area, the system re-deletes them automatically
* Late-joining players receive despawn data and see the correct state
* Despawn data persists in the group's JSON — survives server restarts

#### Files

* `groups/saved_groups.json` — persistent group storage
* `groups/server_manager.lua` — server-side group logic
* `groups/client_menu.lua` — in-game menu UI
* `groups/client_despawn.lua` — despawn monitoring and entity targeting mode

</details>

***

<details>

<summary><strong>Membership System</strong></summary>

<br>

Optionally restrict gym equipment usage to players with an active membership. Disabled by default.

#### Quick Start

1. Set `membership.enable = true` in `config/config_s.lua`
2. All config gym locations now require membership
3. Use `/gymmembership <playerId> [days]` to grant memberships

#### How It Works

When enabled:

* **All config gym locations** require membership by default
* **Individual locations** can opt out: set `requireMembership = false` in the location config
* **Exempt locations** listed in `membership.exemptLocations` never require membership (e.g., `'prison'`)
* **Groups** do NOT require membership by default — toggle per-group in the management menu
* **Custom equipment** (placed via `/gymcreator` save, not in a group) never requires membership

#### Admin Commands

* `/gymmembership <id> [days]` — Grant membership. No days = permanent.
* `/gymrevoke <id>` — Revoke membership from a player.

Both commands require the ACE permission set in `membership.commandRestricted` (default: `group.admin`).

#### Membership Storage

Members are stored in `membership/members.json`:

```json
[
    {
        "license": "license:abc123",
        "playerName": "PlayerOne",
        "grantedBy": "system",
        "grantedAt": 1707500000,
        "expiresAt": 1710092000
    }
]
```

Expired memberships are automatically pruned on server start.

#### Exports (Server-Side)

Other resources can integrate with the membership system:

```lua
-- Check if a player has an active membership
local isMember = exports['prompt_anim_core_2_new']:IsPlayerMember(source)

-- Grant membership (nil days = permanent)
exports['prompt_anim_core_2_new']:GrantMembership(source, 30)

-- Revoke membership
exports['prompt_anim_core_2_new']:RevokeMembership(source)

-- Override the entire membership check with custom logic (ESX/QBCore/etc)
-- Pass nil to restore the default JSON-based check
exports['prompt_anim_core_2_new']:SetMembershipCheckHandler(function(source)
    -- Your custom check here (e.g., check player metadata, inventory item, etc.)
    return true -- or false
end)
```

#### Files

* `membership/server_membership.lua` — all membership logic, exports, commands
* `membership/members.json` — persistent member storage

</details>

***

<details>

<summary><strong>Location System</strong></summary>

<br>

#### Defining Locations (`config/config_c.lua`)

Locations are defined in the `locations` table:

```lua
locations = {
    ['location_name'] = {
        coords = vec3(x, y, z),           -- Required: center point
        renderDistance = 100.0,            -- Optional override
        -- requireMembership = false,      -- Optional: exempt from membership when enabled

        clearLocation = {                  -- Optional: hide vanilla objects
            radius = 20.0,
            additionalObjects = {
                "prop_custom_model_1",
            }
        },

        props = {
            speedbag = {
                vec4(x, y, z, heading),
                vec4(x, y, z, heading),
            },
            bench = {
                -- Simple format: bar attaches to player
                vec4(x, y, z, heading),

                -- Extended format: bar spawns at fixed position
                { coords = vec4(x, y, z, h), bar = vec4(x, y, z, h) },
            },
        }
    }
}
```

#### Clear Location Feature

Hides default/vanilla objects when players enter your gym area:

1. When a player enters the location, the system scans objects within the radius
2. Matches against global `clearLocationModels` + per-location `additionalObjects`
3. Hides matching objects while inside
4. Restores objects when leaving (and on script restart)

#### Boxing Ring (Optional)

Target a placed ring to open the **fight lobby**: two players join, ready up, and fight for the round duration — leaving the boundary (`cancelDistance`, shown as a red sphere when `showBoundary = true`) counts as a loss. Both fighters are revived on start and end (customizable via the `boxingRing` hooks in `config/server.lua` / `config/client.lua`).

```lua
boxingRing = {
    enable = true,
    model = "vision_gymboxingring",
    roundDuration = 60,          -- Seconds per match
    cancelDistance = 6.0,        -- Leave this radius = you lose
    showBoundary = true,         -- Red sphere during the fight
    coords = {
        vec4(x, y, z, heading),
    },
    conditionalCoords = {        -- Rings inside MLOs from other resources:
        {                        -- only exist while one of these is running
            resources = { 'prompt_prison_study' },
            coords = vec4(x, y, z, heading),
            cancelDistance = 6.1,
        },
    },
}
```

</details>

***

<details>

<summary><strong>Equipment Types</strong></summary>

<br>

Available equipment types:

| Type | Model | Description |
| --- | --- | --- |
| `bench` | `vision_gymbench1_pepe` | Bench press (supports extended fixed-bar placement) |
| `vin_chu` | `vin_chu` | Sit-up / core station |
| `leg_press` | `vision_gymlegpress` | Leg press machine |
| `speedbag` | `vision_gymspeedbagwall` | Wall-mounted speed bag |
| `gymbike` | `vision_gymbike` | Exercise bike |
| `gymlatpull` | `vision_gymlatpull` | Lat pulldown machine |
| `gympullmachine1` | `vision_gympullmachine1` | Cable pull machine |
| `gympullmachine2` | `vision_gympullmachine2` | Cable pull machine (variant) |
| `gymrowpull` | `vision_gymrowpull` | Seated rowing machine |
| `gymspeedbag` | `vision_gymspeedbag` | Free-standing speed bag |

Safe to edit: labels, UI text, zone sizes.
Don't edit unless you know what you're doing: model names, animation dicts/names.

</details>

***

<details>

<summary><strong>Player Controls &amp; Stats</strong></summary>

<br>

#### Controls

* **Target / [E] prompt** — start using a machine
* **E** — perform a rep (keybind `gym:performExercise`)
* **X** — get off the machine (keybind `gym:exitMachine`)

Both keybinds are registered through ox_lib, so players can rebind them in **GTA Settings → Key Bindings → FiveM**.

#### Player Stats

Training progresses **4 stats**, each with real gameplay effects while the resource is running:

| Stat | Trained by | Effect |
| --- | --- | --- |
| Speed | Leg exercises (leg press, bike) | Faster sprint |
| Stamina | Cardio (bike, rowing) | Better endurance, faster stamina regen, faster swimming |
| Combat | Punching (speed bags, vin chu) | More melee damage |
| Strength | Pulls & bench | Less melee damage taken, faster health regen |

* Players check their progress with **`/gymstats`** (progress-bar menu, no permission needed)
* Stats **decay over time** when not training (`stats.decrease` in `config_s.lua`; disable or tune per stat)
* Storage is framework-aware: QBCore / QBX / ESX metadata, or a JSON file on standalone servers
* Gains per exercise are tuned in `stats.rates`, fatigue in the `exhaustion` block

**Already running rtx\_gym or vms\_gym for stats?** Set `stats.provider` in `config_s.lua` and anim_core pushes every rep's gains into **their** stat database through their public exports (names mapped in `stats.providerMap`) — the provider keeps owning decay, booster items, and gameplay effects, and anim_core's own modifiers switch off so nothing double-applies. `/gymstats` then shows the provider's values (vms\_gym opens its own statistics menu). Notes: the vms\_gym mapping ships ready (their skill is literally spelled `strenght` — keep it); for rtx\_gym fill in the stat names from their documentation; provider booster items only multiply the provider's *own* training loop — use the `statMultiplier` function in `config/server.lua` to make them scale anim_core reps too.

</details>

***

<details>

<summary><strong>Hooks — Custom Logic Per Machine</strong></summary>

<br>

The `hooks/` folder lets you gate machine use and react to sessions **without editing core files**. On first start the live files are created from the bundled templates — edit these (they survive updates):

* `hooks/hooks_server.lua` — authoritative checks + server reactions
* `hooks/hooks_client.lua` — hide/deny locally + client reactions
* `hooks/hooks_shared.lua` — written once, enforced on BOTH sides

Spot ids look like `'<location>:<equipmentType>:<n>'` (e.g. `'vinewood:speedbag:1'`). Events: `canUse(ctx)` (return `false` to block), `onStart(ctx)`, `onRep(ctx)` (every completed rep — wire XP or third-party stat systems here), `onEnd(ctx)`. Every handler is crash-safe — a broken hook never blocks play.

```lua
-- hooks/hooks_server.lua
return {
    anim = {
        global = {
            canUse = function(ctx)
                -- block all machines during a server event:
                -- if GlobalState.lockdown then return false end
                return true
            end,
        },
        entries = {
            ['vinewood:speedbag:1'] = {
                onStart = function(ctx) print(ctx.source, 'started', ctx.spotId) end,
            },
        },
    },
}
```

</details>

***

<details>

<summary><strong>Equipment Sounds & Rest Animations</strong></summary>

<br>

#### 3D Sound Cues

Every equipment type can define sound cues in `config_c.lua`. Sounds are attached to the machine prop and play **locally on each client, in sync with the animation that client sees** — no extra networking, no desync.

```lua
props = {
    gymlatpull = {
        ...,
        sounds = {
            set   = 'prompt_gym',       -- soundset (custom or native GTA)
            range = 40.0,               -- audible range in meters
            start = { name = '...' },   -- when the machine is taken
            rep   = { name = '...' },   -- every rep, in step with the prop motion
            stop  = { name = '...' },   -- when the machine is released
            loop  = { name = '...' },   -- continuous while occupied (seamless loop)
        },
    },
}
```

All cues are optional — add only what you need. Exact animation lengths for authoring audio are listed in `docs/anim_durations.md`.

#### Rest Animation

By default a player at rest holds the exercise clip's end frame. Machines can define a dedicated rest **loop** instead (smoothest result for big visible motions — the bench ships with one):

```lua
bench = {
    ...,
    restAnimation = {
        dict = 'amb@prop_human_seat_muscle_bench_press@base',
        name = 'base',
    },
}
```

</details>

***

<details>

<summary><strong>/gymcreator (Admin Placement Tool)</strong></summary>

<br>

Place gym equipment anywhere in the world using an in-game editor.

**Requirements**

Set via `gymCreator.restricted` in `config/config_s.lua` (default: `group.admin`). Set to `false` to allow everyone.

**How it works**

1. Run `/gymcreator` — opens a menu
2. Select equipment type to place
3. Move/rotate a transparent preview
4. Press **ENTER** to place, **BACKSPACE** to cancel
5. Use **Manage Groups** to create persistent gym setups

**Menu options:**

* **Add new machine point** — place equipment (saved to clipboard for config paste)
* **Manage Groups** — open the groups system (create/edit/load/unload gyms)

</details>

***

<details>

<summary><strong>Developer API (Exports)</strong></summary>

<br>

#### Location Management

```lua
-- Create a new gym location dynamically
exports['prompt_anim_core_2_new']:CreateGymLocation(locationName, {
    coords = vec3(x, y, z),
    requireMembership = false,  -- optional: force-exempt (or true to force-require)
    props = {
        speedbag = { vec4(x, y, z, h) },
        bench = { { coords = vec4(x, y, z, h), bar = vec4(x, y, z, h) } },
    }
})

-- Remove a gym location
exports['prompt_anim_core_2_new']:RemoveGymLocation(locationName)

-- Inspect / live-update a dynamic location
exports['prompt_anim_core_2_new']:GetDynamicLocation(locationName)
exports['prompt_anim_core_2_new']:SetLocationMembership(locationName, true)
```

#### Equipment Management

```lua
-- Add equipment to an existing location
exports['prompt_anim_core_2_new']:AddEquipmentToLocation(locationName, equipmentType, coords)

-- Remove equipment from a location
exports['prompt_anim_core_2_new']:RemoveEquipmentFromLocation(locationName, equipmentType, coords, tolerance)
```

#### Query Functions

```lua
exports['prompt_anim_core_2_new']:GetLocationEquipment(locationName)
exports['prompt_anim_core_2_new']:GetAllLocations()
exports['prompt_anim_core_2_new']:GetAvailableEquipmentTypes()
```

{% hint style="warning" %}
**Deprecated (still work, print a warning):** `SpawnGymEquipment`, `DespawnGymEquipment`, `GetEquipmentTypes`, `IsEquipmentBusy`, `GetSpawnedEquipment`. Kept for backward compatibility — use the location-based API above for new integrations. Full reference in the resource's `exports.md`.
{% endhint %}

#### Membership Exports

```lua
exports['prompt_anim_core_2_new']:IsPlayerMember(source)
exports['prompt_anim_core_2_new']:GrantMembership(source, durationDays)
exports['prompt_anim_core_2_new']:RevokeMembership(source)
exports['prompt_anim_core_2_new']:SetMembershipCheckHandler(handler)
```

#### Client Exports

```lua
-- Is the local player using a machine? (for death/cuff/admin scripts)
local animating, spotId = exports['prompt_anim_core_2_new']:IsPlayerAnimated()

-- Release the local player from a machine (true = instant, e.g. on death)
exports['prompt_anim_core_2_new']:StopPlayerAnim(true)
```

#### Exercise Tracking Events (Server-Side)

```lua
AddEventHandler('gym:exerciseStarted', function(data)
    print(("%s started using %s"):format(data.playerName, data.machineType))
end)

AddEventHandler('gym:exerciseCompleted', function(data)
    print(("%s completed %s in %d seconds"):format(data.playerName, data.machineType, data.duration))
end)
```

#### Interaction Systems

* **ox\_target** — Preferred. Target options with "Use Equipment" prompts.
* **qb\_target** — Fully supported (auto-detected, or set `interaction = 'qb_target'`).
* **TextUI** — Fallback. TextUI prompts when nearby (press E).
* **Custom** — Implement your own via `customInteraction` in config.

</details>

***

<details>

<summary><strong>Debug Mode & Troubleshooting</strong></summary>

<br>

#### Debug Mode

Set `debug = true` in `config/config_s.lua` to enable verbose logging. Every client's sync log is also relayed into the **server console** (prefixed `[client:<id>]`), so one console shows both sides of any sync issue:

* Machine usage attempts and results (reservations, frees, per-spot state)
* Membership checks (allowed/denied, which location, which player)
* Group loading/unloading, despawn monitoring, equipment state changes

For deep sync issues additionally set `ultraDebug = true`: while any machine is in use, the user **and every viewer** stream their live animation/prop/pin state to the server console twice a second (`[GYM:ULTRA-DOER]` / `[GYM:ULTRA-VIEW]` lines). Attach that console block to any support report.

Disable both in production for best performance.

#### Troubleshooting

* **Props not visible** — Ensure `ox_lib` is running and the resource is started
* **Can't use `/gymcreator`** — Check ACE permissions (`group.admin` by default)
* **Sync looks wrong for other players** — Enable `debug` + `ultraDebug` and read the server console; the doer's and viewers' phase lines should advance together
* **Just updated and things act strange** — The update added new files: full server restart + players must reconnect (a plain `restart` is not enough)
* **Vanilla objects clipping** — Configure `clearLocation` radius + additionalObjects
* **Membership not blocking** — Ensure `membership.enable = true` and restart the resource
* **Groups not loading on start** — Check `autoload` is enabled for the group

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)

</details>
