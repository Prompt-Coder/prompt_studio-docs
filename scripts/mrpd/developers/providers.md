---
description: Tell MRPD how your framework performs an action
icon: plug
---

# Providers

Providers are **not** gates — they define *how* something is done in your stack (framework, inventory). Distinct from [Hooks](hooks.md) (who may) and bridges (framework / notify / target).

***

### `Config.Weapons` — giving & removing training weapons

Used by both the range stalls and the CQB team match. Since **v1.1.0** delivery is picked by `Config.Weapons.provider` (`config/training.lua`):

| provider | behaviour |
| --- | --- |
| `'auto'` _(default)_ | your `custom` callbacks if `custom = true` → the built-in **ox\_inventory adapter** if ox\_inventory is running → native loadout |
| `'ox_inventory'` | force the built-in adapter |
| `'custom'` | your `give` / `remove` callbacks below |
| `'loadout'` | native weapons on the ped (pre-1.1.0 default behaviour) |

{% hint style="success" %}
**ox\_inventory servers need no custom code.** The built-in adapter (`bridge/weapons.lua`, open file) gives weapons as items flagged `mrpd_training = true`, removes exactly those flagged copies when the player leaves the stall / killhouse / match, **blocks moving them** into stashes, trunks, ground drops or other players (no dupes), and sweeps leftovers on disconnect and before every give. Map extra weapons in `Config.Weapons.items` (weapon hash → item name).
{% endhint %}

For any **other inventory**, set `custom = true` and write `give` / `remove` **once**:

{% code title="config/training.lua" %}
```lua
Config.Weapons = {
    provider = 'auto',
    custom   = true,

    give = function(src, weaponHash, ammo, context)
        local item = TRAINING_WEAPON_ITEMS[weaponHash]
        if not item then return end
        -- flag the copy so remove() never strips a real duty weapon of the same type
        exports.ox_inventory:AddItem(src, item, 1, { ammo = ammo, mrpd_training = true })
    end,

    remove = function(src, context)
        for _, item in pairs(TRAINING_WEAPON_ITEMS) do
            local slots = exports.ox_inventory:Search(src, 'slots', item)
            if slots then
                for _, slotData in pairs(slots) do
                    local meta = slotData.metadata
                    if meta and meta.mrpd_training == true then
                        exports.ox_inventory:RemoveItem(src, item, 1, nil, slotData.slot)
                    end
                end
            end
        end
    end,
}
```
{% endcode %}

{% hint style="warning" %}
With ox\_inventory, never pass the flag as `RemoveItem`'s **metadata argument** — ox matches metadata **exactly**, and every weapon carries auto-added `serial` / `durability` / `components`, so `{ mrpd_training = true }` matches nothing and the weapon silently stays. Check the flag per slot and remove **by slot number**, as above. Thanks to **HenryHapert** for contributing this pattern.
{% endhint %}

Configs from before 1.1.0 (no `provider` key) keep working unchanged — the `custom` flag decides.

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
