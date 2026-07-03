---
icon: handcuffs
---

# Prison Escape

## Prompt Prison Escape

***

<details>

<summary><strong>Overview</strong></summary>

<br>

This resource adds an **immersive toilet-based escape minigame** for prison cells.

Players must **unscrew 4 screws** from a toilet tank cover to reveal an escape route. The system includes:

* Custom **enter / work / exit** animation sequences
* Cursor-based **screw removal minigame** (hold LMB to progress)
* **Persistent progress** (unscrewed screws stay unscrewed if player leaves)
* Multiple interaction systems (**ox\_target**, **qb-target**, or **TextUI**)
* Optional inventory requirements (**ox\_inventory**, **qb-inventory**)

</details>

***

{% hint style="danger" %}
Prison Escape only works for the "left side" of the prison (only 3 blocks)
{% endhint %}

### Installation Instructions

{% stepper %}
{% step %}
#### Step 1 — Install dependencies

This resource requires:

* **ox\_lib** (required)

Optional (recommended depending on your server):

* **ox\_target** or **qb-target**
* **ox\_inventory** or **qb-inventory** (only if you want required items)
{% endstep %}

{% step %}
#### Step 2 — Add the resource

Place the folder inside your `resources` directory:

<pre><code><strong>resources/prompt_prison_escape
</strong></code></pre>
{% endstep %}

{% step %}
#### Step 3 — Start order (server.cfg)

Add to your `server.cfg`:

<pre class="language-cfg"><code class="lang-cfg"><strong>ensure ox_lib
</strong><strong>ensure prompt_prison_escape
</strong></code></pre>

If you use a target system, ensure it is started before this resource.
{% endstep %}

{% step %}
#### Step 4 — Integrate with your jail system (required)

Open:

<pre><code><strong>config/config_s.lua
</strong></code></pre>

Replace the function:

```lua
-- ⚠️ CRITICAL INTEGRATION POINT ⚠️
-- Return TRUE to allow, FALSE to deny
isPlayerInPrion = function(source)
    return true
end
```

with your jail/prison check (examples in the Additional Information section).
{% endstep %}

{% step %}
#### Step 5 — Restart & test

Restart your server. Go to a prison cell area that uses the supported toilet models and confirm the interaction appears.

If the player can start the minigame and screw progress saves correctly, installation was successful ✅

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
{% endstep %}
{% endstepper %}

***

{% hint style="warning" %}
If you skip the **`isPlayerInPrion(source)`** integration, the script will either allow everyone or deny everyone (depending on your config). This is the main control point for your prison system.
{% endhint %}

***

<details>

<summary><strong>Additional Information</strong></summary>

<br>

#### Dependencies

Required:

* `ox_lib`

Optional (pick what your server uses):

* Interaction: `ox_target` or `qb-target`
* Item checks: `ox_inventory` or `qb-inventory` (only if you enable `requiredItem`)

***

#### Configuration

**Client:** `config/config_c.lua`

```lua
return {
    -- Interaction system: 'auto' | 'ox_target' | 'qb-target' | 'textUI' | 'custom'
    interaction = 'auto',

    -- Item required to start (empty string = no requirement)
    -- Works with ox_inventory or qb-inventory
    requiredItem = '',

    -- UI location for screw selection:
    -- 'top-left' | 'top-right' | 'bottom-left' | 'bottom-right'
    -- 'middle-left' | 'middle-right' | 'center'
    uiLocation = 'middle-left',

    -- TextUI functions (customize for your framework)
    textUI = {
        hide = function()
            lib.hideTextUI()
        end,
        show = function(text)
            lib.showTextUI(text)
        end,
    },

    toilet = {
        -- Screw positions (do not modify unless you know what you're doing)
        screwOffsets = { ... },

        screwModel = joaat('prompt_prison_screw'),
        screwDriverModel = joaat('v_ind_cs_screwdrivr3'),

        -- Set true if you are NOT using entity lockdown / need networked objects
        useNetworkedObjects = false
    }
}
```

<mark style="color:red;">**THIS I WHERE YOU WOULD WANT TO START YOUR INTEGRATION INTO OTHER SCRIPTS OR FRAMEWORKS**</mark> <i class="fa-down">:down:</i>

**Server:** `config/config_s.lua`

```lua
return {
    debug = true,  -- enable server logs

    -- CRITICAL INTEGRATION POINT
    -- Return true to allow, false to deny
    --
    -- NOTE: the function name is spelled "isPlayerInPrion" in this config.
    isPlayerInPrion = function(source)
        return true
    end
}
```

***

#### Jail Integration Examples

**Generic framework (ESX/QBCore/Custom job check)**

```lua
return {
    debug = false,

    isPlayerInPrion = function(source)
        local Player = YourFramework.GetPlayer(source)
        if not Player then return false end

        local job = Player.job.name
        return job == 'prisoner' or job == 'inmate'
    end
}
```

**qb-prison style (metadata injail)**

```lua
return {
    debug = false,

    isPlayerInPrion = function(source)
        local Player = QBCore.Functions.GetPlayer(source)
        if not Player then return false end

        local jailTime = Player.PlayerData.metadata['injail']
        return jailTime and jailTime > 0
    end
}
```

**ESX jail style (jailTime value)**

```lua
return {
    debug = false,

    isPlayerInPrion = function(source)
        local xPlayer = ESX.GetPlayerFromId(source)
        if not xPlayer then return false end

        local jailTime = xPlayer.get('jailTime') or 0
        return jailTime > 0
    end
}
```

**ND\_Jail style (export check)**

```lua
return {
    debug = false,

    isPlayerInPrion = function(source)
        return exports['ND_Jail']:isPlayerJailed(source)
    end
}
```

**Custom DB check (example concept)**

```lua
return {
    debug = false,

    isPlayerInPrion = function(source)
        local identifier = GetPlayerIdentifier(source, 0)
        local result = MySQL.Sync.fetchScalar(
            'SELECT jail_time FROM players WHERE identifier = ?',
            { identifier }
        )
        return result and result > 0
    end
}
```

***

#### Callbacks & Events (Reference)

Server callbacks (`lib.callback`) used by the resource:

* `prompt_prison_escape:createToiletObject`
* `prompt_prison_escape:unscrewProgress`
* `prompt_prison_escape:getUnscrewedState`
* `prompt_prison_escape:completeEscape`
* `prompt_prison_escape:stopSitting`

Client event used by the resource:

* `prompt_prison_escape:toggleToiletVisibility`

***

#### Customization

**Require an item (optional)**

```lua
-- config/config_c.lua
requiredItem = 'screwdriver'
```

**Force a specific interaction system (optional)**

```lua
-- config/config_c.lua
interaction = 'ox_target'   -- or 'qb-target' or 'textUI'
```

**Custom TextUI (optional)**

```lua
-- config/config_c.lua
textUI = {
    hide = function()
        exports['your_ui']:HideTextUI()
    end,
    show = function(text)
        exports['your_ui']:ShowTextUI(text)
    end,
},
```

**Custom interaction mode (optional)**\
Implement inside `client/editable/interaction.lua` (custom mode must call `onUse(entity)` when interacted).

```lua
-- example concept
exports['your_interact_system']:AddInteraction({
    model = toiletHash,
    label = locale('interaction_label'),
    action = function(entity)
        onUse(entity)
    end
})
```

***

#### Troubleshooting

**Interaction not showing**

* Set `interaction` explicitly instead of `auto`
* Confirm the prison uses supported toilet models in the cell area
* Confirm your `isPlayerInPrion(source)` returns `true` for jailed players

**Minigame starts but progress doesn’t save**

* Ensure `ox_lib` is running
* Check server console for callback errors
* Confirm the resource isn’t restarting/crashing

**Players can use it when they shouldn’t**

* Your `isPlayerInPrion(source)` check is returning `true` incorrectly
* Add real jail-time / jailed-state validation from your prison script

***

#### File Structure (Reference)

```
prompt_prison_escape/
├── client/
│   ├── main.lua
│   ├── events.lua
│   ├── utils.lua
│   ├── editable/
│   │   └── interaction.lua
│   └── minigame/
│       ├── screw_game.lua
│       ├── camera_manager.lua
│       └── animation_controller.lua
├── config/
│   ├── config_c.lua
│   └── config_s.lua
├── server/
│   └── server.lua
├── locales/
│   ├── en.json
│   ├── de.json
│   ├── es.json
│   ├── fr.json
│   └── pl.json
├── stream/
│   └── *.ycd
├── web/
│   └── (NUI)
└── fxmanifest.lua
```

Note: This resource handles **cell escape only**. Anything after escape (alerts, recapture, jail time changes, routes) should be handled by your prison system or additional scripts.

</details>
