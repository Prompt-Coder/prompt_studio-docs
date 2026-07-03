---
icon: transporter-1
---

# Animations Core 2.0

## Animations Core 2.0

### Animations Core 2.0

#### Prompt Anim Core

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
* Client-server synchronization + resource-based cleanup

</details>

***

#### Installation Instructions

{% stepper %}
{% step %}
### Install dependencies

Ensure these resources are installed:

* **ox\_lib** (required)
* **ox\_target** (optional, recommended)
{% endstep %}

{% step %}
### Install Prompt Anim Core

Place the resource folder in your `resources` directory:

<pre><code><strong>resources/prompt_anim_core_2_new
</strong></code></pre>
{% endstep %}

{% step %}
### Start order (server.cfg)

Add this to your `server.cfg` (keep the order):

<pre class="language-cfg"><code class="lang-cfg"><strong>ensure ox_lib
</strong><strong>ensure ox_target   # Optional but recommended
</strong><strong>ensure prompt_anim_core_2_new
</strong></code></pre>
{% endstep %}

{% step %}
### Restart & test

Restart your server and run:

* `/gymcreator`

If you can place equipment and interact with it (target or TextUI), installation was successful ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

{% hint style="info" %}
**Tip:** Keep `ox_lib` above this resource in your cfg. It provides menus, callbacks, notifications, and fallback zones used by the system.
{% endhint %}

***

<details>

<summary><strong>Configuration</strong></summary>

<br>

**Server Config (`config/config_s.lua`)**

```lua
{
    debug = false,            -- Enable debug logging (prints membership checks, machine usage, etc.)
    syncDistance = 50.0,      -- Distance (in meters) for synchronizing equipment between players

    enableMinigame = false,   -- Enable skill check minigame when starting exercises

    gymCreator = {
        enable = true,
        restricted = 'group.admin',  -- ACE restriction for /gymcreator (false = unrestricted)
    },

    exhaustion = {
        enable = false,              -- Fatigue system
        recoveryRate = 0.01,         -- Recovery per minute
        enableMuscleGroups = true,   -- Track per muscle group
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
        enable = true,               -- Stat progression (condition + strength)
    },
}
```

***

**Client Config (`config/config_c.lua`)**

Key sections:

```lua
{
    renderDistance = 100.0,       -- Distance to render gym locations
    interaction = 'auto',        -- 'auto', 'ox_target', 'textUI', 'custom'
    progressBar = 'built-in',    -- 'built-in' or 'custom'

    blip = {
        enable = true,
        sprite = 311,
        color = 21,
        scale = 0.9,
        label = 'Gym',
    },

    boxingRing = {
        enable = true,
        model = "vision_gymboxingring",
        roundDuration = 60,
        coords = { ... },
    },

    locations = {
        ['my_gym'] = {
            coords = vec3(x, y, z),
            -- requireMembership = false,  -- Optional: exempt from membership
            props = { ... },
        },
    },

    props = { ... },  -- Equipment type definitions (models, animations)
}
```

***

**Editable Server Functions (`config/server.lua`)**

This file contains functions you can customize:

* `server.canUseMachine(source, data)` — permission check before accessing equipment (membership check runs here automatically)
* `server.canDoExercise(source, data)` — permission check before starting an exercise
* `server.updateStats(source, data)` — stat progression (pre-configured for QBCore, QBX, ESX)
* `server.getPlayerName(source)` — player name for boxing ring display

</details>

***

<details>

<summary><strong>Groups System</strong></summary>

<br>

The groups system lets you create, edit, and manage gym equipment setups entirely in-game, without editing config files. Groups are saved to `groups/saved_groups.json` and persist across server restarts.

**How to Use**

1. Run `/gymcreator` and select **Manage Groups**
2. **Create New Group** — give it a name
3. **Add Props** — select equipment type, position it in the world with scroll to rotate, ENTER to place
4. **Mark Props for Despawn** — aim at world props you want removed, press E to mark, ENTER to apply
5. **Save Group** — saves to JSON and immediately loads the gym

**Group Management Menu**

From **Manage Groups** you can:

* **Load / Unload** groups (spawn/despawn all props)
* **Edit** a loaded group (add/move/delete props, mark/unmark despawns)
* **Toggle Auto-Load** — groups with auto-load enabled spawn automatically on server start
* **Toggle Membership Requirement** — require membership to use equipment in this group
* **Delete** a group permanently

**Permissions**

* **Admins** (matching `gymCreator.restricted` ACE) can edit/delete any group
* **Creators** can edit their own groups if `groups.creatorCanEdit = true` in config
* **Creators** can delete their own groups if `groups.creatorCanDelete = true` in config
* Creator identity is tracked by player license (framework-agnostic)

**Persistent Prop Despawn**

When you mark world props for despawn in a group:

* They are deleted when the group loads
* If a player leaves and re-enters the streaming area, the system re-deletes them automatically
* Late-joining players receive despawn data and see the correct state
* Despawn data persists in the group's JSON — survives server restarts

**Files**

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

**Quick Start**

1. Set `membership.enable = true` in `config/config_s.lua`
2. All config gym locations now require membership
3. Use `/gymmembership <playerId> [days]` to grant memberships

**How It Works**

When enabled:

* **All config gym locations** require membership by default
* **Individual locations** can opt out: set `requireMembership = false` in the location config
* **Exempt locations** listed in `membership.exemptLocations` never require membership (e.g., `'prison'`)
* **Groups** do NOT require membership by default — toggle per-group in the management menu
* **Custom equipment** (placed via `/gymcreator` save, not in a group) never requires membership

**Admin Commands**

* `/gymmembership <id> [days]` — Grant membership. No days = permanent.
* `/gymrevoke <id>` — Revoke membership from a player.

Both commands require the ACE permission set in `membership.commandRestricted` (default: `group.admin`).

**Membership Storage**

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

**Exports (Server-Side)**

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

**Files**

* `membership/server_membership.lua` — all membership logic, exports, commands
* `membership/members.json` — persistent member storage

</details>

***

<details>

<summary><strong>Location System</strong></summary>

<br>

**Defining Locations (`config/config_c.lua`)**

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

**Clear Location Feature**

Hides default/vanilla objects when players enter your gym area:

1. When a player enters the location, the system scans objects within the radius
2. Matches against global `clearLocationModels` + per-location `additionalObjects`
3. Hides matching objects while inside
4. Restores objects when leaving (and on script restart)

**Boxing Ring (Optional)**

```lua
boxingRing = {
    enable = true,
    model = "vision_gymboxingring",
    roundDuration = 60,
    coords = {
        vec4(x, y, z, heading),
    }
}
```

</details>

***

<details>

<summary><strong>Equipment Types</strong></summary>

<br>

Available equipment types:

* `bench` (supports extended bar placement)
* `vin_chu`
* `leg_press`
* `speedbag`
* `gymbike`
* `gymlatpull`
* `gympullmachine1`
* `gympullmachine2`
* `gymrowpull`
* `gymspeedbag`

Safe to edit: labels, UI text, zone sizes. Don't edit unless you know what you're doing: model names, animation dicts/names.

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

**Location Management**

```lua
-- Create a new gym location dynamically
exports['prompt_anim_core_2_new']:CreateGymLocation(locationName, {
    coords = vec3(x, y, z),
    props = {
        speedbag = { vec4(x, y, z, h) },
        bench = { { coords = vec4(x, y, z, h), bar = vec4(x, y, z, h) } },
    }
})

-- Remove a gym location
exports['prompt_anim_core_2_new']:RemoveGymLocation(locationName)
```

**Equipment Management**

```lua
-- Add equipment to an existing location
exports['prompt_anim_core_2_new']:AddEquipmentToLocation(locationName, equipmentType, coords)

-- Remove equipment from a location
exports['prompt_anim_core_2_new']:RemoveEquipmentFromLocation(locationName, equipmentType, coords, tolerance)
```

**Query Functions**

```lua
exports['prompt_anim_core_2_new']:GetLocationEquipment(locationName)
exports['prompt_anim_core_2_new']:GetAllLocations()
exports['prompt_anim_core_2_new']:GetAvailableEquipmentTypes()
exports['prompt_anim_core_2_new']:GetSpawnedEquipment()
```

**Membership Exports**

```lua
exports['prompt_anim_core_2_new']:IsPlayerMember(source)
exports['prompt_anim_core_2_new']:GrantMembership(source, durationDays)
exports['prompt_anim_core_2_new']:RevokeMembership(source)
exports['prompt_anim_core_2_new']:SetMembershipCheckHandler(handler)
```

**Exercise Tracking Events (Server-Side)**

```lua
AddEventHandler('gym:exerciseStarted', function(data)
    print(("%s started using %s"):format(data.playerName, data.machineType))
end)

AddEventHandler('gym:exerciseCompleted', function(data)
    print(("%s completed %s in %d seconds"):format(data.playerName, data.machineType, data.duration))
end)
```

**Interaction Systems**

* **ox\_target** — Preferred. Target zones with "Use Equipment" prompts.
* **TextUI** — Fallback. TextUI prompts when nearby (press E).
* **Custom** — Implement your own via `customInteraction` in config.

</details>

***

<details>

<summary><strong>Debug Mode &#x26; Troubleshooting</strong></summary>

<br>

**Debug Mode**

Set `debug = true` in `config/config_s.lua` to enable verbose server console logging:

* Machine usage attempts and results
* Membership checks (allowed/denied, which location, which player)
* Group loading/unloading
* Despawn monitoring
* Equipment state changes

Disable in production for best performance.

**Troubleshooting**

* **Props not visible** — Ensure `ox_lib` is running and the resource is started
* **Can't use `/gymcreator`** — Check ACE permissions (`group.admin` by default)
* **Animations not syncing** — Increase `syncDistance` in config\_s.lua
* **Vanilla objects clipping** — Configure `clearLocation` radius + additionalObjects
* **Equipment stuck "in use"** — Fixed in 2.0 — denied access now properly releases the machine
* **Membership not blocking** — Ensure `membership.enable = true` and restart the resource
* **Wrong location in debug logs** — Fixed in 2.0 — location detection now uses coordinates
* **Groups not loading on start** — Check `autoload` is enabled for the group

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)

</details>
