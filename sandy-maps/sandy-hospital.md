# 🏥 Sandy Hospital

{% embed url="https://fivem.prompt-mods.com/package/6381549" %}

{% embed url="https://youtu.be/MHvVSIeMXRU?si=aFjVtijxXEGbTchf" %}

The **Sandy Hospital** is a custom map designed for FiveM servers, offering a fully functional hospital environment for roleplay, medical scenarios, and emergency services. This map includes a variety of chairs, props, and a doorlock system for enhanced interactivity. Below is the available information about the map.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 **Map Position**

The Sandy Hospital map is located at the following coordinates:\
**1755.06, 3620.12, 34.87**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The Sandy Hospital map includes a variety of chairs and props to enhance the environment:

**Beds**

* **promt\_hospital\_sandy\_bed1**
* **promt\_hospital\_sandy\_bed2**





**Chairs**

* **prop\_air\_bench\_02**
* **prop\_air\_bench\_01\_new**
* **v\_club\_officechair**
* **prop\_table\_01\_chr\_a**
* **prop\_table\_01\_chr\_b**
* **v\_club\_officechair**
* **prop\_cs\_office\_chair**
* **prop\_sol\_chair**
* **v\_med\_cor\_medstool**
* **v\_med\_p\_easychair**
* **tr\_int1\_mod\_sofa\_009**
* **v\_res\_study\_chair**
* **prop\_wheelchair\_01**
* **v\_16\_study\_sofa\_new**
* **prop\_table\_03\_chr**

**TV Props**

* **prop\_tv\_flat\_01**
* **v\_med\_cor\_tvstand**

***

#### 🚪 **Doorlock System**

The Sandy Hospital map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Doorlock Configuration**

Add the following SQL lines to your database to configure the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Sandy Shores Hospital E-1', '{"doors":[{"model":-796515299,"heading":30,"coords":{"x":1749.4022216796876,"y":3629.635986328125,"z":35.29167938232422}},{"model":89809332,"heading":30,"coords":{"x":1747.15087890625,"y":3628.336181640625,"z":35.29167938232422}}],"state":1,"passcode":"1001","maxDistance":2,"coords":{"x":1748.276611328125,"y":3628.986083984375,"z":35.29167938232422}}'),
(DEFAULT, 'Sandy Shores Hospital E-2', '{"maxDistance":2,"doors":[{"heading":120,"model":-796515299,"coords":{"x":1769.570556640625,"y":3657.517822265625,"z":35.29065322875976}},{"heading":120,"model":89809332,"coords":{"x":1770.870361328125,"y":3655.266357421875,"z":35.29065322875976}}],"coords":{"x":1770.220458984375,"y":3656.39208984375,"z":35.29065322875976},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital  1-1', '{"maxDistance":2,"doors":[{"heading":120,"model":1858454504,"coords":{"x":1736.3389892578126,"y":3635.900390625,"z":35.29228210449219}},{"heading":300,"model":1858454504,"coords":{"x":1737.6402587890626,"y":3633.646484375,"z":35.29228210449219}}],"coords":{"x":1736.9896240234376,"y":3634.7734375,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-2', '{"maxDistance":2,"heading":120,"doors":false,"model":1858454504,"coords":{"x":1727.2381591796876,"y":3630.64599609375,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-3', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1736.96142578125,"y":3643.13330078125,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-4', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1742.1553955078126,"y":3646.132080078125,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-5', '{"maxDistance":2,"doors":[{"heading":210,"model":1858454504,"coords":{"x":1742.0296630859376,"y":3641.448974609375,"z":35.29228210449219}},{"heading":30,"model":1858454504,"coords":{"x":1744.2835693359376,"y":3642.750244140625,"z":35.29228210449219}}],"coords":{"x":1743.1566162109376,"y":3642.099609375,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-6', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1731.76513671875,"y":3640.133056640625,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-7', '{"maxDistance":2,"doors":[{"heading":120,"model":1858454504,"coords":{"x":1727.794677734375,"y":3637.033447265625,"z":35.29228210449219}},{"heading":300,"model":1858454504,"coords":{"x":1729.095947265625,"y":3634.779541015625,"z":35.29228210449219}}],"coords":{"x":1728.4453125,"y":3635.906494140625,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-8', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1726.67724609375,"y":3637.19580078125,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-9', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1748.2027587890626,"y":3645.01318359375,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-10', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1746.231201171875,"y":3648.485107421875,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-11', '{"maxDistance":2,"heading":300,"doors":false,"model":1858454504,"coords":{"x":1748.0799560546876,"y":3646.554443359375,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-12', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1750.6685791015626,"y":3646.436767578125,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-13', '{"maxDistance":2,"heading":120,"doors":false,"model":1858454504,"coords":{"x":1752.9859619140626,"y":3646.742431640625,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-14', '{"maxDistance":2,"doors":[{"heading":210,"model":1858454504,"coords":{"x":1755.5267333984376,"y":3641.314453125,"z":35.29228210449219}},{"heading":30,"model":1858454504,"coords":{"x":1757.780517578125,"y":3642.61572265625,"z":35.29228210449219}}],"coords":{"x":1756.653564453125,"y":3641.965087890625,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-15', '{"maxDistance":2,"heading":30,"doors":false,"model":1858454504,"coords":{"x":1752.322265625,"y":3639.46435546875,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-16', '{"maxDistance":2,"doors":[{"heading":210,"model":1858454504,"coords":{"x":1762.1534423828126,"y":3645.140380859375,"z":35.29228210449219}},{"heading":30,"model":1858454504,"coords":{"x":1764.4073486328126,"y":3646.441650390625,"z":35.29228210449219}}],"coords":{"x":1763.2803955078126,"y":3645.791015625,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-17', '{"maxDistance":2,"doors":[{"heading":210,"model":1858454504,"coords":{"x":1768.877197265625,"y":3649.0224609375,"z":35.29228210449219}},{"heading":30,"model":1858454504,"coords":{"x":1771.131103515625,"y":3650.32373046875,"z":35.29228210449219}}],"coords":{"x":1770.004150390625,"y":3649.673095703125,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital 1-18', '{"maxDistance":2,"doors":[{"heading":120,"model":1858454504,"coords":{"x":1763.3558349609376,"y":3660.07763671875,"z":35.29228210449219}},{"heading":300,"model":1858454504,"coords":{"x":1764.6571044921876,"y":3657.823974609375,"z":35.29228210449219}}],"coords":{"x":1764.0064697265626,"y":3658.95068359375,"z":35.29228210449219},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital E-3', '{"maxDistance":2,"heading":120,"doors":false,"model":1858454504,"coords":{"x":1763.4759521484376,"y":3639.375244140625,"z":44.99618911743164},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital E-4', '{"maxDistance":2,"heading":120,"doors":false,"model":1286535678,"coords":{"x":1782.408447265625,"y":3640.5810546875,"z":33.92490768432617},"state":0}'),
(DEFAULT, 'Sandy Shores Hospital E-5', '{"maxDistance":2,"heading":120,"doors":false,"model":1286535678,"coords":{"x":1786.941650390625,"y":3662.75244140625,"z":33.9372444152832},"state":0}');
```

***

### 🚀 **Installation Guide**

1. **Download the Map Resource**
   * Ensure the Sandy Hospital map resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       plaintextCopy

       ```
       start cfx_prompt_sandy_hospital
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map location at **1755.06, 3620.12, 34.87** to ensure everything is working correctly.

***

For further assistance, contact support. Enjoy using Sandy Hospital on your FiveM server! 🚀
