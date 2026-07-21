# 🚒 Sandy Fire Department

{% embed url="https://fivem.prompt-mods.com/package/5203353" %}

{% embed url="https://youtu.be/QpJ3QYu3I_U?si=kXNymGRI14oW3lNe" %}

The **Sandy Fire Department** is a custom map designed for FiveM servers, offering a fully functional fire station environment for roleplay, emergency response, and firefighting scenarios. This map includes a variety of chairs, props, and a doorlock system for enhanced interactivity. Below is the available information about the map.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 **Map Position**

The Sandy Fire Department map is located at the following coordinates:\
**1686.55, 3571.87, 35.56**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The Sandy Fire Department map includes a variety of chairs to enhance the environment:

**Chairs**

* **v\_club\_officechair**
* **prompt\_sofa\_office\_ssfd**
* **prop\_chair\_07**
* **v\_ret\_gc\_chair03**
* **mp\_b\_din\_chair\_05**
* **v\_res\_j\_dinechair**

***

#### 🚪 **Doorlock System**

The Sandy Fire Department map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Doorlock Configuration**

Add the following SQL lines to your database to configure the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Sandy Shores Fire Department G-1', '{"doors":false,"model":273713517,"coords":{"x":1707.2415771484376,"y":3587.66357421875,"z":36.97651290893555},"heading":30,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department G-2', '{"doors":false,"model":273713517,"coords":{"x":1702.439453125,"y":3584.89111328125,"z":36.97651290893555},"heading":30,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department G-3', '{"doors":false,"model":273713517,"coords":{"x":1697.6854248046876,"y":3582.146484375,"z":36.97651290893555},"heading":30,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department G-4', '{"doors":false,"model":273713517,"coords":{"x":1692.8687744140626,"y":3579.36572265625,"z":36.97651290893555},"heading":30,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department E-1', '{"doors":[{"coords":{"x":1685.133544921875,"y":3576.4892578125,"z":35.78355407714844},"model":1770281453,"heading":30},{"coords":{"x":1682.8966064453126,"y":3575.170654296875,"z":35.78355407714844},"model":1770281453,"heading":210}],"coords":{"x":1684.01513671875,"y":3575.830078125,"z":35.78355407714844},"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department E-2', '{"doors":false,"model":1770281453,"coords":{"x":1677.90771484375,"y":3589.48681640625,"z":35.78657913208008},"heading":30,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department E-3', '{"doors":false,"model":1770281453,"coords":{"x":1685.20068359375,"y":3590.613037109375,"z":35.7896499633789},"heading":30,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department E-4', '{"doors":false,"model":1770281453,"coords":{"x":1666.6214599609376,"y":3585.237548828125,"z":38.58706283569336},"heading":210,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department E-5', '{"doors":false,"model":1083279016,"coords":{"x":1685.4002685546876,"y":3614.33203125,"z":35.42639541625976},"heading":29,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-1', '{"doors":false,"model":-1289274673,"coords":{"x":1673.5196533203126,"y":3579.39892578125,"z":35.84309387207031},"heading":120,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-2', '{"doors":false,"model":-1289274673,"coords":{"x":1674.632568359375,"y":3581.06005859375,"z":35.83901596069336},"heading":30,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-3', '{"doors":false,"model":-1289274673,"coords":{"x":1678.83349609375,"y":3584.441162109375,"z":35.83913040161133},"heading":300,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-4', '{"doors":false,"model":-1289274673,"coords":{"x":1679.358642578125,"y":3588.471923828125,"z":35.84062957763672},"heading":300,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-5', '{"doors":false,"model":-1289274673,"coords":{"x":1680.611572265625,"y":3586.2939453125,"z":35.83715438842773},"heading":300,"state":0,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-6', '{"doors":false,"model":-1289274673,"coords":{"x":1682.591552734375,"y":3582.889892578125,"z":35.8482551574707},"heading":210,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-7', '{"doors":false,"model":-1289274673,"coords":{"x":1685.0535888671876,"y":3586.844482421875,"z":35.84097671508789},"heading":120,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 1-8', '{"doors":false,"model":-1289274673,"coords":{"x":1689.234130859375,"y":3579.695068359375,"z":35.83857345581055},"heading":300,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 2-2', '{"doors":false,"model":-952356348,"coords":{"x":1671.97509765625,"y":3582.00244140625,"z":38.64494323730469},"heading":300,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Shores Fire Department 2-1', '{"doors":false,"model":-1289274673,"coords":{"x":1679.4293212890626,"y":3588.331298828125,"z":38.74076461791992},"heading":300,"state":1,"maxDistance":2}');
```

***

### 🚀 **Installation Guide**

To install the Sandy Fire Department map on your FiveM server, follow these steps:

1. **Download the Map Resource**
   * Ensure the Sandy Fire Department map resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start cfx_prompt_sandy_shores_fire_department
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map location at **1686.55, 3571.87, 35.56** to ensure everything is working correctly.

***

For further assistance, contact support. Enjoy using Sandy Fire Department on your FiveM server! 🚀
