# 🚒 Pillbox Fire Department

{% embed url="https://fivem.prompt-mods.com/package/5235239" %}

{% embed url="https://youtu.be/nRPpYy4qHpk" %}

The **Pillbox Fire Department** is a custom map designed for FiveM servers, offering a fully immersive fire station environment for roleplay, emergency response, and firefighting scenarios. This map features a detailed interior and exterior, complete with interactive props, seating arrangements, and a robust doorlock system for enhanced gameplay. Below, you’ll find all the necessary details to install and configure this map on your server.

***

### 📍 **Map Location**

The Pillbox Fire Department is located at the following coordinates:\
**324.31, -686.13, 29.31**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The map includes a variety of chairs and props to create a realistic fire station environment. Below is a list of the chairs included:

* `ex_mp_h_stn_chairstrip_010`
* `prop_chair_04a`
* `prop_stool_01`
* `prop_off_chair_04_s`

***

#### 🚪 **Doorlock System**

The Pillbox Fire Department map includes a customizable doorlock system to restrict access to specific areas. Below is the SQL configuration for the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Pillbox Fire Department G-1', '{"doors":false,"state":1,"maxDistance":2,"heading":70,"coords":{"x":320.0604553222656,"y":-677.0083618164063,"z":30.38467788696289},"model":-616841257}'),
(DEFAULT, 'Pillbox Fire Department G-2', '{"doors":false,"state":1,"maxDistance":2,"heading":70,"coords":{"x":318.3260498046875,"y":-681.796630859375,"z":30.3775405883789},"model":-616841257}'),
(DEFAULT, 'Pillbox Fire Department E-1', '{"doors":false,"state":1,"maxDistance":2,"heading":70,"coords":{"x":314.7314758300781,"y":-685.0941772460938,"z":30.14613342285156},"model":-35610440}'),
(DEFAULT, 'Pillbox Fire Department 2-1', '{"doors":false,"state":1,"maxDistance":2,"heading":340,"coords":{"x":304.6263427734375,"y":-677.6810302734375,"z":34.46896362304687},"model":964838196}'),
(DEFAULT, 'Pillbox Fire Department 2-3', '{"doors":false,"state":1,"maxDistance":2,"heading":70,"coords":{"x":302.55902099609377,"y":-669.5408935546875,"z":34.47222518920898},"model":-1726818330}'),
(DEFAULT, 'Pillbox Fire Department 2-2', '{"doors":[{"model":933053701,"heading":250,"coords":{"x":294.9454345703125,"y":-666.2735595703125,"z":34.46779251098633}},{"model":933053701,"heading":70,"coords":{"x":295.834716796875,"y":-663.8301391601563,"z":34.46779251098633}}],"state":1,"maxDistance":2,"coords":{"x":295.39007568359377,"y":-665.0518798828125,"z":34.46779251098633}}');
```

***

### 🚀 **Installation Guide**

Follow these steps to install the Pillbox Fire Department map on your FiveM server:

1. **Download the Map Resource**
   * Ensure the `cfx_prompt_pillbox_fd` resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start cfx_prompt_pillbox_fd
       ```
3. **Set Up Doorlocks**
   * Execute the provided SQL configuration in your database to enable the doorlock system.
4. **Test the Map**
   * Restart your server and visit the map location at **324.31, -686.13, 29.31** to ensure everything is functioning correctly.

***

For further assistance, contact support. Enjoy using the **Pillbox Fire Department** on your FiveM server! 🚀
