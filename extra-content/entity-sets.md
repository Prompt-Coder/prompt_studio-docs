---
description: >-
  Discover how to control object visibility and states using Entity Sets for
  dynamic map customization in FiveM
---

# 📦 Entity Sets

Entity Sets, are a crucial part of customizing your FiveM server's environment. They allow you to control the visibility and state of specific objects or groups of objects within the game world. Entity Sets are particularly useful for creating dynamic environments where certain objects appear or disappear based on specific conditions or triggers.

🔧 What Are Entity Sets Used For?

Entity Sets are used to:

* Toggle the visibility of objects in the interior world.
* Create variations of maps by showing or hiding specific elements.
* Enhance performance by unloading unnecessary objects when they are not needed.
* Create interactive environments where objects change based on player actions or server events.



📂 Entity Sets in Prompt's Studio Maps\
If a map from Prompt's Studio includes Entity Sets, the specific Entity Sets required will be listed in the map’s documentation. Be sure to check the related document for the map you’ve purchased to ensure all Entity Sets are configured correctly. This guarantees that the map behaves as intended in your FiveM server.

🛠️ Entity Sets Quick Checklist\
✅ Ensure Entity Sets are properly configured in your server.\
✅ Use the correct Entity Set names as specified in the map’s documentation.\
✅ Test the Entity Sets to ensure they function as expected.

🛠️ Loading Entity Sets Using a Lua Script\
If your map includes Entity Sets, you can load and manage them dynamically using a Lua script. **We already provide the script to lod entity sets with each interior** that has them, but if you want more flexibility in loading those you can do following steps. This method gives you full control over when and how Entity Sets are activated or deactivated in your server. Below is a step-by-step guide to help you set this up.

📜 Step 1: Create a Lua Script for Entity Set Management\
Navigate to your resources folder and create a new folder for your Entity Set management script. For example, name it enset\_manager.\
Inside the folder, create a new file named client.lua. This will handle the Entity Set management on the client side.

📝 Step 2: Add the Entity Set Management Code\
Open the client.lua file and add the following code:

```lua
-- enset_manager/client.lua

-- List of Entity Sets to manage (replace these with the Entity Sets from your map's documentation)
local entitySets = {
    "example_enset_1",
    "example_enset_2",
    "example_enset_3"
}

-- Function to activate Entity Sets
local function activateEntitySets()
    for _, enset in ipairs(entitySets) do
        if not IsEntitySetActive(enset) then
            ActivateEntitySet(enset)
            while not IsEntitySetActive(enset) do
                Wait(10) -- Wait until the Entity Set is fully activated
            end
            print("[Entity Set Manager] Activated Entity Set: " .. enset)
        end
    end
end

-- Function to deactivate Entity Sets
local function deactivateEntitySets()
    for _, enset in ipairs(entitySets) do
        if IsEntitySetActive(enset) then
            DeactivateEntitySet(enset)
            while IsEntitySetActive(enset) do
                Wait(10) -- Wait until the Entity Set is fully deactivated
            end
            print("[Entity Set Manager] Deactivated Entity Set: " .. enset)
        end
    end
end

-- Event to trigger Entity Set management when the resource starts
CreateThread(function()
    if GetCurrentResourceName() == resourceName then
        activateEntitySets()
        print("[Entity Set Manager] All Entity Sets have been activated successfully!")
    end
end)

-- Example of how to deactivate Entity Sets when the resource stops
AddEventHandler('onResourceStop', function(resourceName)
    if resourceName == GetCurrentResourceName() then
        deactivateEntitySets()
        print("[Entity Set Manager] All Entity Sets have been deactivated successfully!")
    end
end)
```

You can remove printlines if you want this script to work silently.

⚙️ Step 3: Configure the Resource Manifest\
In the same enset\_manager folder, create a file named fxmanifest.lua and add the following code:

```lua
fx_version 'cerulean'
game 'gta5'

client_scripts {
    'client.lua' -- name of your script file
}
```

🚀 Step 4: Add the Resource to Your Server Place the enset\_manager folder in your resources directory. Add the following line to your server.cfg to ensure the resource starts with your server:

```
start enset_manager
```

✅ Step 5: Test the Entity Set Manager\
Restart your FiveM server.\
Join the server and check the console for messages like `[Entity Set Manager] Activated Entity Set: example_enset_1`. This confirms that the Entity Sets are loading correctly. (if you removed all prints it will send nothing)

This Lua script method gives you full control over Entity Set management and ensures your custom maps behave correctly. If you encounter any issues, double-check the Entity Set names and ensure the script is properly configured. Let us know if you need further assistance! 🚀
