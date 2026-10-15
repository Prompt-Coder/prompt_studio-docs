---
description: Connect YouTool Furniture Store to ps-housing (Project Sloth). Paste one code block; purchases appear in the ps-housing Furniture Menu.
icon: house-chimney
---

# ps-housing

YouTool adds every purchase to the property's furniture in ps-housing (Project Sloth), and the player places it from the ps-housing **Furniture Menu**. Stock ps-housing has no way for another script to add furniture, so you paste a short code block into ps-housing once.

**Tested with:** ps-housing 2.0.7.

{% hint style="warning" %}
**A ps-housing update overwrites `server/sv_property.lua`.** After every ps-housing update, paste the code block from step 1 again. The setup check shows `[FAIL] ps-housing: the YouTool furniture API is not added` until you do.
{% endhint %}

***

### Install

{% stepper %}
{% step %}
#### Add the furniture API to ps-housing

Open `ps-housing/server/sv_property.lua` and paste this block at the **very end** of the file:

{% code title="ps-housing/server/sv_property.lua (add at the end)" %}
```lua
-- ═══════════════════════════════════════════════════════════════════════════
-- EXTERNAL FURNITURE API (for YouTool and other external furniture systems)
-- ═══════════════════════════════════════════════════════════════════════════

local function AddExternalFurniture(propertyId, furnitureData)
    local property = Property.Get(tostring(propertyId))
    if not property then
        return false, "Property not found"
    end
    
    local id = tostring(math.random(100000, 999999) .. propertyId)
    
    local newItem = {
        id = id,
        object = furnitureData.object or furnitureData.model,
        label = furnitureData.label or furnitureData.name or furnitureData.object,
        price = furnitureData.price or 0,
        position = furnitureData.position or {x = 0, y = 0, z = 0},
        rotation = furnitureData.rotation or {x = 0, y = 0, z = 0},
        type = furnitureData.type or nil
    }
    
    local currentFurnitures = property.propertyData.furnitures or {}
    table.insert(currentFurnitures, newItem)
    property:UpdateFurnitures(currentFurnitures)
    
    return true, nil
end

exports('AddExternalFurniture', AddExternalFurniture)

local function AddExternalFurnitures(propertyId, items)
    local property = Property.Get(tostring(propertyId))
    if not property then
        return false, 0, "Property not found"
    end
    
    local currentFurnitures = property.propertyData.furnitures or {}
    local addedCount = 0
    
    for _, furnitureData in ipairs(items) do
        local id = tostring(math.random(100000, 999999) .. propertyId .. addedCount)
        
        local newItem = {
            id = id,
            object = furnitureData.object or furnitureData.model,
            label = furnitureData.label or furnitureData.name or furnitureData.object,
            price = furnitureData.price or 0,
            position = furnitureData.position or {x = 0, y = 0, z = 0},
            rotation = furnitureData.rotation or {x = 0, y = 0, z = 0},
            type = furnitureData.type or nil
        }
        
        table.insert(currentFurnitures, newItem)
        addedCount = addedCount + 1
    end
    
    property:UpdateFurnitures(currentFurnitures)
    
    return true, addedCount, nil
end

exports('AddExternalFurnitures', AddExternalFurnitures)

print('[ps-housing] External furniture API loaded')
```
{% endcode %}

ps-housing keeps each property's furniture in memory. These two exports add furniture through ps-housing itself, so its memory and the database stay in sync. Writing to the database directly would make the items disappear.

The same block is in `prompt_youtool_store_system/integrations/ps-housing/README.md` (Step 1).
{% endstep %}

{% step %}
#### Check the dependencies

These must run: `ox_lib`, `oxmysql` and `ps-housing` (with the code from step 1).
{% endstep %}

{% step %}
#### Restart ps-housing

```
restart ps-housing
```

The console shows the line from the end of the block:

```
[ps-housing] External furniture API loaded
```

About 8 seconds later the setup check runs and should show:

```
  [ OK ] Housing: ps-housing 2.0.7
  [ OK ] ps-housing: YouTool furniture API found
```
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the property if they own several.
2. The items are added to that property's furniture in ps-housing.
3. Inside the property, the player opens the **Radial Menu → Furniture Menu**. The purchased items are listed there, ready to place with the ps-housing decorator.

YouTool does not add its items to ps-housing's own furniture shop. They can only be bought in the YouTool store.

***

### Setup check

When the code block is in place:

```
  [ OK ] ps-housing: YouTool furniture API found
```

When it is missing (not pasted yet, or removed by a ps-housing update):

```
  [FAIL] ps-housing: the YouTool furniture API is not added
         -> Paste the code from integrations/ps-housing/README.md (Step 1) at the end of ps-housing/server/sv_property.lua and restart it. A ps-housing update overwrites that file.
```

To test one real delivery, run `youtool_setup <playerId>` with a player who owns a property online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary>Items don't appear in the Furniture Menu after a purchase</summary>

1. Leave the property and enter it again.
2. Check which property the player picked at checkout; the items are in that one.
3. Run `youtool_setup <playerId>` and fix any `[FAIL]` line.

</details>

<details>

<summary>The purchase fails with "You don't own this property" or "Property not found"</summary>

YouTool only delivers to properties where the player is the owner in ps-housing. Make sure the player owns the property (not only has access to it).

</details>

<details>

<summary><code>No such export AddExternalFurnitures in resource ps-housing</code></summary>

The code block from step 1 is missing or ps-housing wasn't restarted after you pasted it. Paste it at the end of `ps-housing/server/sv_property.lua` and run `restart ps-housing`.

</details>
