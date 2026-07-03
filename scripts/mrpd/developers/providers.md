---
description: Tell MRPD how your framework performs an action
icon: plug
---

# Providers

Providers are **not** gates — they define *how* something is done in your stack (framework, inventory). Distinct from [Hooks](hooks.md) (who may) and bridges (framework / notify / target).

***

### `Config.Weapons` — giving & removing training weapons

Used by both the range stalls and the CQB team match. The default hands weapons out natively. **Inventory servers** set `custom = true` and write `give` / `remove` **once** (`config/training.lua`):

```lua
Config.Weapons = {
    custom = true,
    give   = function(src, weaponHash, ammo, context)
        exports.ox_inventory:AddItem(src, item, 1, { ammo = ammo, mrpd_training = true })
    end,
    remove = function(src, context)
        -- strip the flagged training weapon
    end,
}
```

***

### `Config.Training.Callbacks.onDowned`

Override what happens to a **downed CQB player's body** — e.g. tell your ambulance/EMS script it isn't a real death (`config/training.lua`). Leave `nil` for the built-in behaviour.

```lua
Config.Training.Callbacks = {
    onDowned = function(src)
        -- your ambulance/death handling
    end,
}
```

***

### `Custom*` bridge functions

When a bridge in `config.lua` is set to `'custom'`, fill the matching `Custom*` functions in `bridge/*.lua` — `framework.lua`, `target.lua`, `notify.lua`, `textui.lua`. This is how you wire a job system, HUD, notify, or target we don't auto-detect.

{% hint style="info" %}
"Hooks" means **only** the gate service. These provider callbacks are named `Weapons` / `Callbacks` on purpose, so the two never get confused.
{% endhint %}
