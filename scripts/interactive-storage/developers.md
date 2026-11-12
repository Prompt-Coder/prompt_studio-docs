---
description: Hooks (gate and react), server and client exports, commands, drawer stash names and the custom bridges
icon: code
---

# For Developers

Everything here works without touching the protected files. Rules and reactions go into the open hook files, other resources read and drive the cabinets through exports, and your own framework, target, notify or text UI plugs in through the open `bridge/` files.

***

### Hooks

Hook files live in `hooks/`. They are created from the `.example.lua` templates on the first start and are never overwritten by updates. Each file returns a Lua table. Restart the resource after editing.

| File | Role |
| --- | --- |
| `hooks_server.lua` | Decides. The server checks every gate here, even when the client already refused |
| `hooks_client.lua` | Only controls what this player is offered. Handlers must not wait (no `Wait`) |
| `hooks_shared.lua` | Runs on both sides: the client for visibility, the server as authority. Write a check once here. Only use data both sides can see (statebags, the `ctx` fields) |

* Gates (`can*`) return `false` to block; `nil` or `true` allows.
* Handlers go under `global` (every cabinet) or `entries['<id>']` (one id). The `global` handler, the `entries` handler, and the shared file must all allow an action.
* Every handler runs in `pcall` and fails open: a broken hook never blocks and never stops the resource.

| Feature | id | Gates | Reactions |
| --- | --- | --- | --- |
| `storage` | The cabinet's animated model, a `Config.Storage.models` key such as `prompt_filecab01`. A GTA cabinet goes by the model it opens as (`v_corp_filecablow` → `prompt_v_corp_filecablow`) | `canOpen` | `onOpen`, `onClose` |
| `creator` | The model being placed | `canPlace` | `onPlace`, `onMove`, `onRemove` |

#### When they fire

| Event | Side | Fires | ctx |
| --- | --- | --- | --- |
| `storage.canOpen` | server | When the player walks up (`drawer = nil`), and again before a drawer's stash opens (`drawer` = 1..n) | `source, id, model, coords, drawer` |
| `storage.canOpen` | client | Before the player walks up. `false` = nothing happens | `id, entity, coords` |
| `storage.onOpen` | both | The drawer is fully open, just before its stash opens | server: `source, id, model, coords, drawer` · client: `id, entity, drawer, label, coords` |
| `storage.onClose` | server | The player left the cabinet: after the drawer shut, or when the list was closed without a choice (`drawer = nil` then) | `source, id, model, coords, drawer` |
| `storage.onClose` | client | The drawer is shut and the player released (only after a drawer was opened) | `id, entity, drawer, label, coords` |
| `creator.canPlace` | server | Before `/storcreator` places a cabinet, and before it moves one (then `ctx.id` is the placement id) | `source, model, coords, heading` (+ `id` on a move) |
| `creator.onPlace` / `onMove` / `onRemove` | server | After a cabinet was placed, moved or removed with `/storcreator` | `source, id, model, coords, heading` |

* In `storage` hooks on the server, `model` and `coords` are the cabinet as it stands in the world: the GTA model name for GTA's own cabinets, the `prompt_` model for placed ones. `id` is always the animated model.
* `label` is the drawer's name in the server language, for example "Upper drawer".
* The `AddPlacement` and `RemovePlacement` exports do not run the `creator` hooks.

#### Examples

{% tabs %}
{% tab title="Placed cabinets only" %}
GTA's own cabinets have no fixed list of positions, so the server cannot tell a real one from a made-up one: a modified client could invent GTA cabinets (and their empty stashes) where none stand. To rule that out, allow placed cabinets only:

```lua
-- hooks/hooks_server.lua
return {
    storage = {
        global = {
            canOpen = function(ctx)
                -- GTA cabinets go by their GTA model name, placed ones by their prompt_ model
                return ctx.model == ctx.id
            end,
        },
        entries = {},
    },
}
```
{% endtab %}

{% tab title="Log opened drawers" %}
```lua
-- hooks/hooks_server.lua
return {
    storage = {
        global = {},
        entries = {
            ['prompt_tallcabdark01'] = {
                onOpen = function(ctx)
                    print(('%s opened drawer %d at %s'):format(GetPlayerName(ctx.source), ctx.drawer, ctx.coords))
                end,
            },
        },
    },
}
```
{% endtab %}

{% tab title="On duty only (shared)" %}
The cabinet does not open on the client, and the server refuses it too:

```lua
-- hooks/hooks_shared.lua
return {
    storage = {
        global = {
            canOpen = function(ctx)
                local st = IsDuplicityVersion() and Player(ctx.source).state or LocalPlayer.state
                return st.onDuty == true
            end,
        },
    },
}
```
{% endtab %}
{% endtabs %}

***

### Exports

Server, `exports.prompt_interactive_storage`:

| Export | Returns / does |
| --- | --- |
| `HasAccess(src)` | `true` when the player passes `Config.access` (jobs, grade, duty, ACE, showcase). Answers by the rule even when `Config.Storage.access` is off |
| `GetActive()` | Every cabinet in use: `{ { source, key, model, coords, twin, pos, heading, drawer, phase }, ... }` |
| `CloseDrawer(src)` | Shuts the drawer that player has open, with the closing animation, like pressing X. `false` when they are not at a cabinet |
| `GetPlacements()` | Every placed cabinet, in the order they were placed: `{ { id, model, coords, heading }, ... }` |
| `AddPlacement(model, coords, heading)` | Places a cabinet and returns its id, or `nil`. `model` is a `Config.Storage.models` key, `coords` a `vector3` (or `{ x, y, z }`), `heading` defaults to `0.0`. No ACE check, no hook |
| `RemovePlacement(id)` | Removes a placed cabinet; `true` when it existed. Its drawer stashes stay in the inventory. No hook |

`phase` is `enter` (opening), `idle` (open) or `exit` (closing); `nil` until the player picks a drawer. The placement exports exist only while `Config.Modules.creator` is on.

Client, `exports.prompt_interactive_storage`:

| Export | Returns / does |
| --- | --- |
| `Close()` | Shuts the open drawer with the closing animation. Its stash closes with it |
| `IsOpen()` | `true` from the moment the player picks a drawer until it is shut |
| `GetState()` | `{ id, entity, drawer, phase }` or `nil` |

```lua
-- server: shut every open drawer, for example before a restart
local storage = exports.prompt_interactive_storage
for _, cabinet in ipairs(storage:GetActive()) do
    storage:CloseDrawer(cabinet.source)
end
```

***

### Drawer stash names

| Cabinet | Stash name |
| --- | --- |
| GTA cabinet | `pstor_<model>_<x>_<y>_<z>_<drawer>`: the GTA model name, the position × 10 rounded to whole numbers (a 10 cm grid), the drawer number |
| Placed cabinet | `pstor_p<id>_<drawer>`: the placement id and the drawer number |

* A placed cabinet keeps its contents when it is moved: the name does not contain its position.
* A GTA cabinet that a map update moves to another spot gets new, empty stashes.
* The names are the same as in the 0.2.0 test build, so drawer contents from it carry over.
* With `ox_inventory`, the script blocks opening a `pstor_` stash by its name in any other way (an `openInventory` hook on `^pstor_`).

***

### Commands

| Command | Who | What |
| --- | --- | --- |
| `/storcreator` | ACE `stor.creator` | Place, move, remove and list cabinets (see [Placing Cabinets](placing-cabinets.md#commands)) |
| `/stor` | Everyone | Bridge, module and language report: the client side in F8, the server side (with inventory and access) in the server console |
| `stor_debugdump` | Server console, or ACE `command.stor_debugdump` | The support snapshot (see [Troubleshooting](troubleshooting.md#support-dump)) |
| `/stortest notify` \| `ui` \| `target` | `Config.debug = true` | Bridge self-tests: a notification, a text UI line, a target zone at your feet |

#### Debug commands

These exist only with `Config.debug = true`. They print English and have **no permission check**:

| Command | What |
| --- | --- |
| `/storagetest [model]` | Spawns every cabinet model in a row in front of you, or one model (a GTA model name spawns the GTA cabinet) |
| `/storageclear` | Removes the test cabinets |
| `/stordrawer <n>` | Opens drawer n of the nearest cabinet within 3 m straight away, without the list |
| `/stnudge x y z [h]` | Live-tunes where the character stands at the nearest test cabinet and prints the config line |
| `/stmenu x y z [h]` | Live-tunes the list's fallback spot on the cabinet front |
| `/stcam list` \| `browse` \| `action` `<values>` | Live-tunes the camera rules while a drawer list is up and prints the config line |
| `/stordiag` | Checks that the textures, cabinet models and replacement meshes load (F8) |
| `/storprobe` | Prints what your aim hits and every cabinet model within 15 m (F8) |

{% hint style="danger" %}
Keep `Config.debug = false` on a live server. Besides the commands above, with debug on the server also accepts a `prompt_` model cabinet at any spot the client names, not only placed ones (that is how the test spawns open).
{% endhint %}

***

### Custom bridges

Each `custom` value calls functions you define in the open `bridge/` files.

**Framework** (`Config.framework = 'custom'`), in `bridge/framework.lua`:

```lua
-- server: used for Config.access
function CustomGetJob(src) return { name = 'police', grade = 0, onDuty = true } end
-- client: shown by /stor
function CustomGetJobClient() return { name = 'police', grade = 0, onDuty = true } end
```

Without `CustomGetJob`, access uses the ACE as on a standalone server.

**Target** (`Config.target = 'custom'`), in `bridge/target.lua` (client). Options come in `ox_target` shape: `{ name, label, icon, distance, canInteract, onSelect }`.

```lua
function CustomTargetAddModel(models, options) end          -- GTA cabinets
function CustomTargetRemoveModel(models, names) end
function CustomTargetAddLocalEntity(entity, options) end    -- placed cabinets
function CustomTargetRemoveLocalEntity(entity, names) end
```

`CustomTargetAddSphereZone` and `CustomTargetRemoveZone` are only used by `/stortest target`.

**Notifications** (`Config.notify = 'custom'`), in `bridge/notify.lua` (client):

```lua
-- opts = { title?, description, type = 'inform' | 'success' | 'error', duration? }
function CustomNotify(opts) exports['my_hud']:Notify(opts.description, opts.type) end
```

**Text UI** (`Config.textUI = 'custom'`), in `bridge/textui.lua` (client). Used for the prompts only when `Config.prompt = 'textui'`:

```lua
function CustomShowUI(text, position) exports['my_ui']:Show(text) end
function CustomHideUI() exports['my_ui']:Hide() end
```

**Inventory**: see [Custom inventory](configuration.md#custom-inventory).
