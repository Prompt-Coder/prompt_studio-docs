---
hidden: true
icon: transporter-1
---

# Animations Core

## Prompt Anim Core

{% embed url="https://fivem.prompt-mods.com/package/XXXXXXXX" %}
**Standalone animation system for gym equipment — used across all Prompt’s Mods gym maps.**
{% endembed %}

{% embed url="https://www.youtube.com/watch?v=tLU2zzmF-Oc" %}

***

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Download and install

Download the **Prompt Anim Core** resource and place it in your `resources` directory.

<pre><code><strong>resources/prompt_anim_core
</strong></code></pre>

Then add it to your `server.cfg`:

<pre class="language-cfg"><code class="lang-cfg"><strong>ensure ox_lib
</strong><strong>ensure ox_target   # Optional but recommended
</strong><strong>ensure prompt_anim_core
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 2 — Configure permissions

Edit your `server.cfg` to assign ACE permissions:

```cfg
# Give admin group all gym permissions
add_ace group.admin gym.admin allow

# Add player to admin group
add_principal identifier.steam:YOUR_STEAM_ID group.admin
```

To disable all permissions and allow everyone to use admin tools:

```lua
Config.Permissions.usePermissions = false
```
{% endstep %}

{% step %}
#### Step 3 — Start your server

Restart your server and use `/placeequipment` to begin placing gym props interactively.\
If animations and interaction zones appear correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

***

{% hint style="info" %}
💡 **Tip:** Keep `ox_lib` above this resource in your cfg. It provides the required callbacks, menus, and zones for proper animation handling.
{% endhint %}

***

### Configuration

{% tabs %}
{% tab title="System Settings" %}
#### ⚙️ Performance Settings

```lua
Config = {
    SpawnDistance = 50.0,  -- Distance props spawn (meters)
    SyncRadius = 20.0,     -- Animation sync radius
    Debug = true,          -- Enable debug logs
}
```

> 💡 Lower `SyncRadius` = better performance on high-pop servers.
{% endtab %}

{% tab title="Permissions" %}
#### 🔐 Permissions System

```lua
Config.Permissions = {
    usePermissions = true,        -- Set false to disable ACE checks
    placeEquipment = "gym.place", -- Permission for /placeequipment
    deleteEquipment = "gym.delete",
    admin = "gym.admin"           -- Grants all permissions
}
```

| Command           | Permission                  | Can Disable? |
| ----------------- | --------------------------- | ------------ |
| `/placeequipment` | `gym.place` or `gym.admin`  | ✅ Yes        |
| Remove Equipment  | `gym.delete` or `gym.admin` | ✅ Yes        |

> To disable all permissions, set `Config.Permissions.usePermissions = false`
{% endtab %}

{% tab title="Messages & Labels" %}
#### 🗨️ UI Text Configuration

```lua
Config.Messages = {
    open = "Start Exercise",
    close = "Stop Exercise",
    menuTitle = "Gym Equipment Menu"
}
```

Change these to customize menu and interaction text.
{% endtab %}

{% tab title="Equipment Types" %}
#### 🏋️ Equipment Definitions

Each equipment type includes:

* **model** — 3D prop name
* **label** — Display name in menu
* **animations** — Animation dictionary & clip
* **interactionZone** — Area size for usage

**Available Equipment:**

```
vin_chu — Wooden dummy  
leg_press — Leg press machine  
speedbag — Punching bag  
gymbike — Exercise bike  
gymlatpull — Lat pull machine  
gympullmachine1 — Cable machine 1  
gympullmachine2 — Cable machine 2  
gymrowpull — Row machine  
gymspeedbag — Speed bag  
```

✅ **Safe to edit:** `label`, interaction radius\
🚫 **Do not edit:** model names, animation dicts/names
{% endtab %}
{% endtabs %}

***

### <i class="fa-square-caret-down">:square-caret-down:</i> Unified Animation Menu

Manage all gym equipment and prop groups from **one unified, interactive menu** with real-time editing, placement, and group management.

#### Command: `/anim_menu`

Opens the unified interface where you can place props, manage groups, and edit existing setups — all in one place.

***

#### 🎯 Place Single Prop

Quickly place individual gym equipment **outside of any group** for testing or simple setups.

***

#### 🆕 Create New Group

Start a new prop group collection directly from the menu:

1. Click **"Create New Group"** and enter a name
2. Use the placement tool to add multiple props
3. Save your group to file for **persistence across restarts**

***

#### ✏️ Select & Edit Group

Manage existing groups effortlessly:

* View all saved prop groups
* Load any group for editing
* Add or remove props live in the world
* Save changes to update the group file
* Visual status indicators for each group:\
  ✅ **Loaded** / ⭕ **Unloaded**

***

#### 💾 Active Group Session

When a group is active:

* **Add Props** — Place new equipment linked to this group
* **Remove Props** — Delete button appears on props in the active group
* **Save Changes** — Automatically detects and saves modifications
* **Cancel** — Discards all unsaved changes and closes the session

***

#### Example Workflow

```
1. /anim_menu → Click "Create New Group"
2. Enter name: "my_custom_gym" → Confirm
3. Use placement tool → Place speedbag
4. Use placement tool → Place leg press
5. Use placement tool → Place bike
6. /anim_menu → Click "Save Group"
7. Server restart → Group auto-loads automatically!
```

***

#### Commands

| Command      | Description                                                  |
| ------------ | ------------------------------------------------------------ |
| `/anim_menu` | Opens unified animation management menu (groups + placement) |

***

### `/placeequipment` (Single Prop)

Use `/placeequipment` to manually place a single prop outside of any group.

#### Controls

| Key             | Action                        |
| --------------- | ----------------------------- |
| **WASD**        | Move horizontally             |
| **PgUp / PgDn** | Adjust height                 |
| **Q / E**       | Rotate                        |
| **G**           | Snap to ground (align bottom) |
| **ENTER**       | Save and broadcast placement  |
| **BACKSPACE**   | Cancel placement              |

#### Requirements

`gym.place` or `gym.admin` permission\
(or set `usePermissions = false` to disable restrictions)

#### How It Works

1. Opens a menu to select equipment type
2. Spawns a transparent preview (visible only to you)
3. Move and rotate freely to position
4. Press **ENTER** to confirm placement — instantly syncs for all players

***

### <i class="fa-gear-code">:gear-code:</i> Developer API

{% tabs %}
{% tab title="Spawn Equipment" %}
```lua
exports['prompt_anim_core']:SpawnGymEquipment(
    equipmentType,  -- "speedbag", "leg_press", etc.
    coords,         -- vector3(x, y, z)
    heading,        -- 0.0–360.0
    locationName,   -- optional (e.g. "custom_gym")
    instanceName    -- optional unique ID
)
```

**Example:**

```lua
exports['prompt_anim_core']:SpawnGymEquipment(
    "speedbag",
    vector3(100.0, 200.0, 30.0),
    90.0,
    "custom_location",
    "my_speedbag_1"
)
```
{% endtab %}

{% tab title="Despawn Equipment" %}
```lua
exports['prompt_anim_core']:DespawnGymEquipment("my_speedbag_1")
```

Removes a specific piece of equipment by its instance name.
{% endtab %}

{% tab title="Utility Functions" %}
**Get Equipment Types**

```lua
local types = exports['prompt_anim_core']:GetEquipmentTypes()
-- returns: {"speedbag", "leg_press", ...}
```

**Check if Equipment Busy**

```lua
local isBusy = exports['prompt_anim_core']:IsEquipmentBusy("my_speedbag_1")
```

**Get All Spawned Equipment**

```lua
local equipment = exports['prompt_anim_core']:GetSpawnedEquipment()
-- returns table of all active props
```
{% endtab %}
{% endtabs %}

***

### <i class="fa-code-simple">:code-simple:</i> Exercise Tracking API

Hook into these events for progression or stats systems.

#### `gym:exerciseStarted`

```lua
AddEventHandler('gym:exerciseStarted', function(data)
    print(data.playerName .. " started using " .. data.machineType)
end)
```

#### `gym:exerciseCompleted`

```lua
AddEventHandler('gym:exerciseCompleted', function(data)
    print(data.playerName .. " completed " .. data.machineType)
    print("Duration: " .. data.duration .. " seconds")
end)
```

**Data Example:**

```lua
{
    playerId = 1,
    playerName = "John Doe",
    machineName = "vinewood_default_speedbag_1",
    machineType = "speedbag",
    animationDict = "prompt@speedbag",
    animationName = "speedbag@skel_clip_0",
    position = vector3(x, y, z),
    heading = 90.0,
    location = "vinewood",
    timestamp = 1699123456,
    duration = 15
}
```

***

### Interaction Systems

Two supported systems, auto-detected at runtime:

| System         | Description                                                         |
| -------------- | ------------------------------------------------------------------- |
| **ox\_target** | Preferred. Circular interaction zones with “Use Equipment” prompts. |
| **lib.zones**  | Fallback. TextUI prompts when nearby (press E).                     |

If `ox_target` is not installed, the script automatically switches to `lib.zones`.

***

### Debug Mode

```lua
Config.Debug = true
```

Displays:

* Spawn/despawn logs
* Animation triggers
* Player position/heading
* Permission checks
* Exercise data

> Disable in production for best performance.

***

### Dependencies

**Required:**

* `ox_lib`

**Optional:**

* `ox_target` (recommended for enhanced targeting)

***

### Quick Start

1. Install and ensure `ox_lib` (and optionally `ox_target`)
2. Add `ensure prompt_anim_core` to `server.cfg`
3. Configure permissions (or disable them)
4. Use `/placeequipment` to start placing gym props
5. Players interact via target zones or proximity prompts

***

### Example: Custom Gym Resource

```lua
RegisterCommand('spawngym', function()
    exports['prompt_anim_core']:SpawnGymEquipment("speedbag", vector3(100,200,30), 0.0, "custom", "bag1")
    exports['prompt_anim_core']:SpawnGymEquipment("leg_press", vector3(105,200,30), 90.0, "custom", "press1")
    exports['prompt_anim_core']:SpawnGymEquipment("gymbike", vector3(110,200,30), 180.0, "custom", "bike1")
end)

AddEventHandler('gym:exerciseCompleted', function(data)
    print(data.playerName .. " earned XP for " .. data.machineType)
end)
```

***

### Troubleshooting & Support

| Problem                       | Solution                                                 |
| ----------------------------- | -------------------------------------------------------- |
| **Props not visible**         | Ensure `ox_lib` is running and resource is started       |
| **Can't use /placeequipment** | Check ACE permissions or disable them in config          |
| **Animations not syncing**    | Increase `SyncRadius` or ensure players are within range |
| **Props floating/clipping**   | Use **G** to snap to ground, adjust with PgUp/PgDn       |

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
