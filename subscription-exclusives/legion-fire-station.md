# 🚒 Legion Fire Station

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/T5IuSVYl__I?si=2jVrWloENgounMW6" %}



Elevate your FiveM roleplay experience with the Legion Firehouse, a unique and expertly designed MLO that seamlessly blends functionality and style. Located in the heart of the city, this state-of-the-art facility serves as a home base for the modern firefighter. The Legion Firehouse includes the following:

* 🛋️ Two Hangout Rooms - Foster camaraderie among your team in these comfortable, welcoming spaces.
* 🚒 Large Apparatus Bay - House all your essential vehicles and gear in this spacious, well-organized area.
* 📋 Briefing Room - Facilitate seamless communication during crucial moments with a dedicated space for strategizing.
* 🖥️ Offices - Stay organized and efficient with designated workspaces for administrative tasks.
* 🗄️ Storage - Keep all your equipment and supplies easily accessible in ample storage areas.
* 🛏️ Sleeping Quarters - Provide a comfortable space for your firefighters to rest and recharge after a long day of heroics.
* 🏢 Custom Exterior - Make a bold statement with a striking, eye-catching facade that sets the Legion Firehouse apart.

***

### 🗺️ Map Location

The **Legion** **Fire Station** is located at the following coordinates:

* **Position**: `319.48, -1033.32, 30.91`

***

### 🚪 Doorlock System

The Vimap includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (1032, 'Legion Fire Station G-1', '{"maxDistance":2,"coords":{"x":320.9464,"y":-1027.1968,"z":30.2798},"doors":false,"heading":0,"state":1,"model":1221159160}'),
    (1033, 'Legion Fire Station G-2', '{"maxDistance":2,"coords":{"x":313.5936,"y":-1027.1912,"z":30.2681},"doors":false,"heading":0,"state":1,"model":1221159160}'),
    (1034, 'Legion Fire Station E-1', '{"maxDistance":2,"coords":{"x":317.8242,"y":-1027.4629,"z":29.2881},"doors":false,"heading":0,"state":1,"model":775638898}'),
    (1035, 'Legion Fire Station 1-1', '{"maxDistance":2,"coords":{"x":313.0444,"y":-1012.8805,"z":29.2773},"doors":false,"heading":180,"state":1,"model":2020131050}'),
    (1036, 'Legion Fire Station 1-2', '{"maxDistance":2,"coords":{"x":319.6942,"y":-1010.8317,"z":29.2773},"doors":false,"heading":180,"state":1,"model":2020131050}'),
    (1037, 'Legion Fire Station 1-3', '{"maxDistance":2,"coords":{"x":315.1183,"y":-1012.4478,"z":29.2773},"doors":false,"heading":90,"state":1,"model":2020131050}');

```

***

### :hole: Fire Pole Script&#x20;

This Map supports **FirePoll** script `prompt_j17_firepole.`You only need to start it in your server cfg and it will work as intended.

***

### :chair:Chairs

* prop\_off\_chair\_04b
* v\_club\_officechair
* gr\_prop\_bunker\_bed\_01

### :tv:TV

* xm\_prop\_x17\_tv\_ceiling\_01

***

🚀 Installation Guide

Follow these steps to install the **Legion Fire Station** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_j17_legionfire` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_j17_legionfire
    ```
3. **Set Up Doorlocks**\
   Once the doorlock configuration is available, execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `319.48, -1033.32, 30.91` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Legion Fire Station** on your FiveM server! 🚀
