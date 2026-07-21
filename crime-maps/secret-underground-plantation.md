# 🌿 Secret Underground Plantation

{% embed url="https://fivem.prompt-mods.com/package/4551252" %}

{% embed url="https://youtu.be/5nrEncXWk5k" %}

The **Secret Underground Marijuana Plantation** is a hidden and immersive map designed for FiveM servers. Located beneath the streets of Los Santos, this map provides a realistic environment for roleplay gang scenarios, complete with a customizable doorlock system. Below is a comprehensive guide to help you set up and use this map on your server.

***

### 🗺️ Map Location

The **Secret Underground Marijuana Plantation** is located at the following coordinates:

* **Position**: `-184.76, -1699.13, 32.82`

***

### 🚪 Doorlock System

The **Secret Underground Marijuana Plantation** map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Secret Marijuana Plantation E-1', '{"maxDistance":2,"model":-1207991715,"coords":{"x":-186.4388427734375,"y":-1702.2708740234376,"z":33.15013122558594},"heading":131,"state":1,"doors":false}'),
(DEFAULT, 'Secret Marijuana Plantation 1-1', '{"maxDistance":2,"coords":{"x":-188.7267303466797,"y":-1706.1214599609376,"z":33.14407730102539},"state":1,"doors":[{"model":-340230128,"coords":{"x":-189.56077575683595,"y":-1705.12451171875,"z":33.14407730102539},"heading":310},{"model":-340230128,"coords":{"x":-187.89268493652345,"y":-1707.118408203125,"z":33.14407730102539},"heading":130}]}'),
(DEFAULT, 'Secret Marijuana Plantation 0-1', '{"maxDistance":2,"model":452874391,"coords":{"x":-187.68603515625,"y":-1713.491455078125,"z":28.42519950866699},"heading":310,"state":1,"doors":false}'),
(DEFAULT, 'Secret Marijuana Plantation 0-2', '{"maxDistance":2,"model":199886144,"coords":{"x":-173.4237060546875,"y":-1699.874755859375,"z":28.41531181335449},"heading":40,"state":1,"doors":false}'),
(DEFAULT, 'Secret Marijuana Plantation 0-3', '{"maxDistance":2,"model":199886144,"coords":{"x":-174.86668395996095,"y":-1692.38037109375,"z":26.18354797363281},"heading":310,"state":1,"doors":false}'),
(DEFAULT, 'Secret Marijuana Plantation 0-4', '{"maxDistance":2,"model":452874391,"coords":{"x":-180.088134765625,"y":-1692.2677001953126,"z":26.14149284362793},"heading":130,"state":1,"doors":false}'),
(DEFAULT, 'Secret Marijuana Plantation 0-5', '{"maxDistance":2,"coords":{"x":-189.20480346679688,"y":-1694.05712890625,"z":26.18293952941894},"state":1,"doors":[{"model":964838196,"coords":{"x":-190.2012481689453,"y":-1694.893310546875,"z":26.18293952941894},"heading":220},{"model":964838196,"coords":{"x":-188.20835876464845,"y":-1693.220947265625,"z":26.18293952941894},"heading":40}]}');
```

***

### 🚀 Installation Guide

Follow these steps to install the **Secret Underground Marijuana Plantation** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `cfx_prompt_marijuana_plantation` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    plaintextCopy

    ```
    start cfx_prompt_marijuana_plantation
    ```
3. **Set Up Doorlocks**\
   Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `-184.76, -1699.13, 32.82` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Secret Underground Marijuana Plantation** on your FiveM server! 🚀
