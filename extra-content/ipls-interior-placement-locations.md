---
description: >-
  Learn how to manage Interior Placement Locations (IPLs) to customize interiors
  and exteriors in your FiveM server
---

# 🪑 IPLs (Interior Placement Locations)

**🌍 Understanding IPLs in FiveM**

IPLs, or **Interior Placement Locations**, are essential for adding custom interiors and exteriors to your FiveM server. They define where and how structures, buildings, and environments appear in your game world. There are some maps that have variations of some parts of exterior. They are implemented by using IPLs. If a map includes IPLs, they must be properly loaded for the map to display correctly.

***

**🔧 What Do IPLs Need to Work?**

To ensure IPLs function as intended, follow these steps:

1. **📂 Enable IPL Loading in Your Server Configuration**\
   Ensure your `server.cfg` file includes the interior where IPLs are.&#x20;
2.  **🚀 Start the IPL Resource in Your Server**\
    Add the map resource to your `server.cfg` to ensure it loads when your server starts. For example:

    ```
    start prompt_resource
    ```
3. **🔍 Check for Additional Dependencies**\
   Some IPLs may require additional resources or dependencies to function properly. Always refer to the map’s documentation for specific instructions.

***

**📂 IPLs in Prompt's Studio Maps**

If a map from **Prompt's Studio** includes IPLs, the specific IPLs required will be listed in the map’s documentation. Be sure to check the related document for the map you’ve purchased to ensure all IPLs are loaded correctly. This guarantees that the map appears as intended in your FiveM server.

***

#### 🛠️ **IPL Quick Checklist**

✅ Ensure IPLs are enabled in `server.cfg`.\
✅ Start the map resource in your server.\
✅ Check the map’s documentation for IPL details.

***

#### 🛠️ **Loading IPLs Using a Lua Script**

If your map includes IPLs, you can load them dynamically using a Lua script. This method is useful if you want more control over when and how IPLs are loaded in your server. Below is a step-by-step guide to help you set this up.

***

**📜 Step 1: Create a Lua Script for IPL Loading**

1. Navigate to your `resources` folder and create a new folder for your IPL loader script. For example, name it `ipl_loader`.
2. Inside the folder, create a new file named `client.lua`. This will handle the IPL loading on the client side.

***

**📝 Step 2: Add the IPL Loading Code**

Open the `client.lua` file and add the following code:

```lua
-- ipl_loader/client.lua

-- List of IPLs to load (replace these with the IPLs from your map's documentation)
local iplList = {
    "example_ipl_1",
    "example_ipl_2",
    "example_ipl_3"
}

-- Function to load IPLs
local function loadIPLs()
    for _, ipl in ipairs(iplList) do
        if not IsIplActive(ipl) then
            RequestIpl(ipl)
            while not IsIplActive(ipl) do
                Wait(10) -- Wait until the IPL is fully loaded
            end
            print("[IPL Loader] Loaded IPL: " .. ipl)
        end
    end
end

-- Event to trigger IPL loading when the resource starts
CreateThread(function()
    if GetCurrentResourceName() == resourceName then
        loadIPLs()
        print("[IPL Loader] All IPLs have been loaded successfully!")
    end
end)
```

You can remove `print`lines if you want this script to work silently.

**⚙️ Step 3: Configure the Resource Manifest**

In the same `ipl_loader` folder, create a file named `fxmanifest.lua` and add the following code:

```lua
fx_version 'cerulean'
game 'gta5'

client_scripts {
    'client.lua' -- name of your script file
}
```

**🚀 Step 4: Add the Resource to Your Server**

1. Place the `ipl_loader` folder in your `resources` directory.
2. Add the following line to your `server.cfg` to ensure the resource starts with your server:

```
start ipl_loader
```

**✅ Step 5: Test the IPL Loader**

1. Restart your FiveM server.
2. Join the server and check the console for messages like `[IPL Loader] Loaded IPL: example_ipl_1`. This confirms that the IPLs are loading correctly. (if you removed all prints it will send nothing)

***

This Lua script method gives you full control over IPL loading and ensures your custom maps display correctly. If you encounter any issues, double-check the IPL names and ensure the script is properly configured. Let us know if you need further assistance! 🚀
