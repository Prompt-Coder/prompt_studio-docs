# 🏖️ Sandy Marina

{% embed url="https://fivem.prompt-mods.com/package/6443485" %}

{% embed url="https://youtu.be/KeOoVpzwvc0?si=xic_Jlvyxse1LosF" %}

The **Sandy Marina** is a custom map designed for FiveM servers, offering a vibrant and interactive marina environment for roleplay, boating activities, and lifeguard operations. This map includes a variety of props, chairs, and a doorlock system for enhanced interactivity. Below is the available information about the map.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 **Map Position**

Sandy Marina is located at these coordinates: **`1645.37, 3869.50, 34.49`**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The Sandy Marina map includes a variety of chairs and props to enhance the environment:

**Chairs**

* **v\_ret\_gc\_chair03**
* **apa\_mp\_h\_stn\_chairarm\_03**
* **v\_res\_m\_l\_chair1**
* **-115000005** (hash)

**Lifeguard Chairs**

* **v\_ind\_ss\_chair2**
* **v\_ret\_gc\_chair01**

**TV Props**

* **prop\_tv\_flat\_michael**
* **prompt\_prop2**

***

#### 🚪 **Doorlock System**

The Sandy Marina map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Boat Dealership Doors**

Add the following configuration to your doorlock system (e.g., `ox_doorlock` or similar, enter this into your database):

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Sandy Boat Dealership E-1', '{"doors":[{"coords":{"x":1416.5447998046876,"y":3821.980712890625,"z":32.90338897705078},"model":-1639843199,"heading":340},{"coords":{"x":1418.92333984375,"y":3821.13623046875,"z":32.90238952636719},"model":1820563205,"heading":160}],"coords":{"x":1417.734130859375,"y":3821.55859375,"z":32.90288925170898},"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Boat Dealership 1-1', '{"doors":false,"model":1665407005,"coords":{"x":1415.54736328125,"y":3815.278564453125,"z":32.21939086914062},"heading":340,"state":1,"maxDistance":2}'),
(DEFAULT, 'Sandy Boat Dealership 1-2', '{"doors":false,"model":1836838935,"coords":{"x":1415.642333984375,"y":3815.243896484375,"z":32.21939086914062},"heading":160,"state":1,"maxDistance":2}');
```

**Lifeguard Doors**

Add the following configuration for lifeguard doors:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(DEFAULT, 'Sandy Marina Lifeguard E-1', '{"coords":{"x":1692.553955078125,"y":3909.815673828125,"z":34.67904281616211},"maxDistance":2,"state":1,"doors":[{"heading":40,"model":1332681439,"coords":{"x":1693.4476318359376,"y":3910.5654296875,"z":34.67854309082031}},{"heading":40,"model":1983156904,"coords":{"x":1691.660400390625,"y":3909.06591796875,"z":34.6795425415039}}]}'),
(DEFAULT, 'Sandy Marina Lifeguard E-2', '{"coords":{"x":1687.19384765625,"y":3905.766845703125,"z":34.58753967285156},"heading":40,"model":-1874602384,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Sandy Marina Lifeguard E-3', '{"coords":{"x":1695.703857421875,"y":3912.29931640625,"z":38.79753875732422},"heading":40,"model":-1644531235,"maxDistance":2,"state":1,"doors":false}'),
(DEFAULT, 'Sandy Marina Lifeguard 1-1', '{"coords":{"x":1689.107177734375,"y":3911.09423828125,"z":34.6795425415039},"maxDistance":2,"state":1,"doors":[{"heading":40,"model":1334504662,"coords":{"x":1688.3487548828126,"y":3911.998046875,"z":34.6795425415039}},{"heading":40,"model":870503425,"coords":{"x":1689.86572265625,"y":3910.190185546875,"z":34.6795425415039}}]}'),
(DEFAULT, 'Sandy Marina Lifeguard 1-2', '{"coords":{"x":1695.910400390625,"y":3917.1748046875,"z":34.6795425415039},"maxDistance":2,"state":1,"doors":[{"heading":40,"model":870503425,"coords":{"x":1696.6688232421876,"y":3916.270751953125,"z":34.6795425415039}},{"heading":40,"model":1334504662,"coords":{"x":1695.15185546875,"y":3918.07861328125,"z":34.6795425415039}}]}');
```

***

### 🚀 **Installation Guide**

1. **Download the Map Resource**
   * Ensure the Sandy Marina map resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       plaintextCopy

       ```
       start cfx_prompt_sandy_marina
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map location to ensure everything is working correctly.

***

For further assistance, contact support. Enjoy using Sandy City Hall on your FiveM server! 🚀
