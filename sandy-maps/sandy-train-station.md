# 🚉 Sandy Train Station

{% embed url="https://fivem.prompt-mods.com/package/6521797" %}

{% embed url="https://youtu.be/SigRjrf69Iw?si=RknjJfW6SR-IpPY_" %}

The **Sandy Train Station** is a custom map designed for FiveM servers, offering a functional and immersive train station environment for roleplay and transportation scenarios. This map includes a doorlock system information. Below is the available information about the map.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 **Map Position**

Sandy Train Station is located at the following coordinates: **`1873.2478, 3589.7039, 34.5833`**

***

### 🛠️ **Features**

#### 🚪 **Doorlock System**

The Sandy Train Station map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Chairs**

The following chair props are included in the map:

* **prop\_bench\_06**
* **v\_ret\_chair**
* **v\_ret\_chair\_white**
* **prompt\_sandy\_train\_circlar\_bench**
* **prompt\_sandy\_trainstation\_sitting\_chair**

**Doors**

Below is the doorlock configuration for Sandy Train Station. Add this to your doorlock system (e.g., `ox_doorlock` or similar, use it in database):

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(200, 'Sandy Train Station E-2', '{"doors":[{"coords":{"x":1909.319091796875,"y":3576.14794921875,"z":39.20650482177734},"model":-1894423230,"heading":210},{"coords":{"x":1907.347900390625,"y":3575.0322265625,"z":39.20650482177734},"model":297231150,"heading":210}],"coords":{"x":1908.33349609375,"y":3575.590087890625,"z":39.20650482177734},"state":1,"maxDistance":2}'),
(201, 'Sandy Train Station E-1', '{"doors":[{"coords":{"x":1901.7529296875,"y":3584.54248046875,"z":39.20650482177734},"model":-1894423230,"heading":30},{"coords":{"x":1903.703369140625,"y":3585.67431640625,"z":39.20650482177734},"model":297231150,"heading":30}],"coords":{"x":1902.7281494140626,"y":3585.1083984375,"z":39.20650482177734},"state":1,"maxDistance":2}'),
(202, 'Sandy Train Station E-3', '{"doors":[{"coords":{"x":1913.507568359375,"y":3578.54931640625,"z":39.20650482177734},"model":-1894423230,"heading":210},{"coords":{"x":1911.54248046875,"y":3577.43701171875,"z":39.20650482177734},"model":297231150,"heading":210}],"coords":{"x":1912.5250244140626,"y":3577.9931640625,"z":39.20650482177734},"state":1,"maxDistance":2}');


```

***

### 🚀 **Installation Guide**

1. **Download the Map Resource**
   * Ensure the Sandy Train Station map resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       plaintextCopy

       ```
       start cfx_prompt_sandy_train_station
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map location to ensure everything is working correctly.

***

For further assistance, contact support. Enjoy using Sandy City Hall on your FiveM server! 🚀
