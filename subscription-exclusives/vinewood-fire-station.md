# 🚒 Vinewood Fire Station

{% embed url="https://fivem.prompt-mods.com/package/5231636" %}

{% embed url="https://youtu.be/T5IuSVYl__I?si=2jVrWloENgounMW6" %}



Elevate your FiveM roleplay experience with the Vinewood Firehouse, a unique and expertly designed MLO that seamlessly blends functionality and style. Located in the heart of the city, this state-of-the-art facility serves as a home base for the modern firefighter. The Vinewood Firehouse includes the following:

* 🛋️ Hangout Rooms - Foster camaraderie among your team in these comfortable, welcoming spaces.
* 🚒 Large Apparatus Bay - House all your essential vehicles and gear in this spacious, well-organized area.
* 📋 Briefing Room - Facilitate seamless communication during crucial moments with a dedicated space for strategizing.
* 🖥️ Offices - Stay organized and efficient with designated workspaces for administrative tasks.
* 🗄️ Storage - Keep all your equipment and supplies easily accessible in ample storage areas.
* 🛏️ Sleeping Quarters - Provide a comfortable space for your firefighters to rest and recharge after a long day of heroics.
* 🏢 Custom Exterior - Make a bold statement with a striking, eye-catching facade that sets the Vinewood Firehouse apart.

***

### 🗺️ Map Location

The **Vinewood Fire Station** is located at the following coordinates:

* **Position**: `398.44, 273.3, 104.06`

***

### 🚪 Doorlock System

The Vimap includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (1026, 'Vinewood Fire Station G-1', '{"maxDistance":2,"coords":{"x":391.6808,"y":284.3284,"z":101.989},"doors":false,"heading":70,"state":1,"model":-365339889}'),
    (1027, 'Vinewood Fire Station G-2', '{"maxDistance":2,"coords":{"x":389.0305,"y":277.0467,"z":101.989},"doors":false,"heading":70,"state":1,"model":-365339889}'),
    (1028, 'Vinewood Fire Station G-3', '{"maxDistance":2,"coords":{"x":386.38,"y":269.7645,"z":101.989},"doors":false,"heading":70,"state":1,"model":-365339889}'),
    (1029, 'Vinewood Fire Station E-1', '{"maxDistance":2,"coords":{"x":390.3964,"y":280.0641,"z":103.0652},"doors":false,"heading":70,"state":1,"model":945380231}'),
    (1030, 'Vinewood Fire Station E-2', '{"maxDistance":2,"coords":{"x":387.7531,"y":272.7846,"z":103.0733},"doors":false,"heading":70,"state":1,"model":1244856122}'),
    (1031, 'Vinewood Fire Station 1-1', '{"maxDistance":2,"coords":{"x":369.9583,"y":274.757,"z":103.0741},"doors":[{"coords":{"x":370.2972,"y":275.6884,"z":103.0741},"model":1345458177,"heading":250},{"coords":{"x":369.6193,"y":273.8257,"z":103.0741},"model":1345458177,"heading":70}],"state":1}');

```

***

### :hole: Fire Pole Script&#x20;

This Map supports **FirePoll** script `prompt_j17_firepole.`You only need to start it in your server cfg and it will work as intended.

***



### 🪑 Chairs

The map includes chairs for added realism. Below are the chair models used in the map:

* prop\_off\_chair\_04\_s
* prop\_off\_chair\_05
* v\_club\_officechair
* v\_ilev\_leath\_chr
* v\_med\_p\_sofa
* v\_61\_bth\_mesh\_toilet\_clean
* v\_res\_tre\_stool\_leather
* j17\_sm\_charlie\_bed



:8ball: **Pool: (COMPATIBLE)**

* prop\_pool\_rack\_01 coords: vec3(3.322793, -7.419705, 1.786812)
* prop\_pooltable\_02 coords: vec3(-1.465114, -9.121764, 0.9939881)

:tv: **TV:**

* prop\_tv\_flat\_michael

***



🚀 Installation Guide

Follow these steps to install the **Vinewood Fire Station** map on your FiveM server:

1. **Download the Map Resource**\
   Ensure the `prompt_j17_vinewoodfire` resource is downloaded and placed in your `resources` folder.
2.  **Add the Resource to `server.cfg`**\
    Add the following line to your `server.cfg` to ensure the map loads when your server starts:

    ```
    start prompt_j17_vinewoodfire
    ```
3. **Set Up Doorlocks**\
   Once the doorlock configuration is available, execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**\
   Restart your server and visit the map location at `398.44, 273.3, 104.06` to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Vinewood Fire Station** on your FiveM server! 🚀
