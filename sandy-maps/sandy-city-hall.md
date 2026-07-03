# 🏢 Sandy City Hall

{% embed url="https://fivem.prompt-mods.com/package/6578222" %}

{% embed url="https://youtu.be/3F71qYcdP5M?si=YvsTxBwYWFAuI9Zu" %}

Sandy City Hall is a custom map designed for FiveM servers, offering a versatile location for roleplay, events, and administrative activities. This map includes a functional elevator script and various Entity Sets and IPLs to customize the environment. Below is a detailed guide to help you set up and configure the map on your server.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 **Map Position**

The Sandy City Hall map is located at the following coordinates:\
&#xNAN;**`1728.1, 3787.36, 35.18`**

***

### 🛠️ **Features**

{% tabs %}
{% tab title="🚪 Entity Sets" %}
Entity Sets allow you to control the visibility of specific objects within the map. Below are the Entity Sets included in Sandy City Hall:

* **`static_elevator`**
* **`conference_chairs`**
* **`conference_meeting_table`**
* **`eventroom_voting`**

To activate or deactivate these Entity Sets, refer to the [Entity Sets documentation](../extra-content/entity-sets.md) for guidance on using Lua scripts.
{% endtab %}

{% tab title="🌆 IPLs (Interior Placement Locations)" %}
IPLs are used to load specific objects and structures in the map. The following IPLs are included in Sandy City Hall:

* **`p_prompt_sandy_cityhall_backtables`**
* **`p_prompt_sandy_cityhall_coffin_closed`**
* **`p_prompt_sandy_cityhall_coffin_opened`**
* **`p_prompt_sandy_cityhall_fences_backclosed`**
* **`p_prompt_sandy_cityhall_fences_backopened`**
* **`p_prompt_sandy_cityhall_funeral_chairs`**
* **`p_prompt_sandy_cityhall_funeral_picture`**
* **`p_prompt_sandy_cityhall_leaves`**
* **`p_prompt_sandy_cityhall_tables`**
* **`p_prompt_sandy_cityhall_wedding_chairs`**
* **`p_prompt_sandy_cityhall_wedding_spotlight`**
* **`p_prompt_sandy_cityhall_wedding_venue`**

Ensure these IPLs are loaded correctly by following the [IPLs documentation](../extra-content/ipls-interior-placement-locations.md).
{% endtab %}

{% tab title="🛗 Elevator Script" %}
The map includes a functional elevator script, allowing players to move between floors seamlessly. The elevator is pre-configured and ready to use. You will need [ox-lib](https://github.com/overextended/ox_lib) resource loaded on your server in order for an elevator to work. No additional setup is required unless you want to customize its behavior.
{% endtab %}

{% tab title="🔒 Doorlock Feature" %}
The Sandy City Hall map includes a doorlock system for enhanced security and roleplay. Below are the details for implementing the doorlock feature:

**Chairs**

The following chair props are included in the map and can be used with the doorlock system:

* **prop\_off\_chair\_03**
* **prop\_off\_chair\_04\_s**
* **apa\_mp\_h\_stn\_chairarm\_11**
* **prop\_table\_06\_chr**
* **v\_res\_fa\_chair01**
* **prompt\_sandy\_cityhall\_exterior\_seating**
* **prop\_table\_03\_chr**
* **prop\_bench\_06**
* **vw\_prop\_vw\_offchair\_02**
* **prop\_off\_chair\_01**

**Textures**

To edit the texture for **prompt\_sandy\_cityhall\_exterior\_infobooth**, modify the texture dictionary **prompt\_sandy\_cityhall\_ext\_txd**.

**Doors**

**Here is `ox_doorlock` configuration (use it in your database):**

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(97, 'Sandy City Hall E-1', '{"maxDistance":2,"doors":[{"heading":303,"model":-2023167872,"coords":{"x":1750.66748046875,"y":3801.838134765625,"z":35.55295944213867}},{"heading":303,"model":-1712058986,"coords":{"x":1749.7076416015626,"y":3803.30810546875,"z":35.55295944213867}}],"coords":{"x":1750.1875,"y":3802.5732421875,"z":35.55295944213867},"state":1}'),
	(98, 'Sandy City Hall E-2', '{"maxDistance":2,"doors":[{"heading":123,"model":-2023167872,"coords":{"x":1771.1002197265626,"y":3817.51025390625,"z":35.56166839599609}},{"heading":123,"model":-1712058986,"coords":{"x":1772.06005859375,"y":3816.040283203125,"z":35.56166839599609}}],"coords":{"x":1771.580078125,"y":3816.775390625,"z":35.56166839599609},"state":1}'),
	(99, 'Sandy City Hall E-3', '{"maxDistance":2,"doors":[{"heading":123,"model":1443374866,"coords":{"x":1769.597900390625,"y":3817.283447265625,"z":43.48043823242187}},{"heading":123,"model":834428539,"coords":{"x":1770.6138916015626,"y":3815.7275390625,"z":43.48043823242187}}],"coords":{"x":1770.10595703125,"y":3816.50537109375,"z":43.48043823242187},"state":1}'),
	(100, 'Sandy City Hall E-4', '{"maxDistance":2,"doors":[{"heading":123,"model":-2023167872,"coords":{"x":1757.1083984375,"y":3802.109375,"z":46.58335876464844}},{"heading":123,"model":-1712058986,"coords":{"x":1758.068359375,"y":3800.639404296875,"z":46.58335876464844}}],"coords":{"x":1757.58837890625,"y":3801.37451171875,"z":46.58335876464844},"state":1}'),
	(101, 'Sandy City Hall 1-1', '{"maxDistance":2,"heading":123,"doors":false,"model":1053379387,"coords":{"x":1757.737060546875,"y":3801.625,"z":35.72456741333008},"state":1}'),
	(102, 'Sandy City Hall 1-2', '{"maxDistance":2,"heading":33,"doors":false,"model":1053379387,"coords":{"x":1748.8878173828126,"y":3809.44384765625,"z":35.72349548339844},"state":1}'),
	(103, 'Sandy City Hall 1-3', '{"maxDistance":2,"heading":303,"doors":false,"model":1053379387,"coords":{"x":1751.8167724609376,"y":3810.19873046875,"z":35.7244644165039},"state":1}'),
	(104, 'Sandy City Hall 1-4', '{"maxDistance":2,"doors":[{"heading":213,"model":1053379387,"coords":{"x":1770.079345703125,"y":3811.75048828125,"z":35.72996520996094}},{"heading":33,"model":1053379387,"coords":{"x":1768.1585693359376,"y":3810.49609375,"z":35.72918701171875}}],"coords":{"x":1769.118896484375,"y":3811.123291015625,"z":35.72957611083984},"state":1}'),
	(105, 'Sandy City Hall 2-1', '{"maxDistance":2,"heading":303,"doors":false,"model":1053379387,"coords":{"x":1753.16748046875,"y":3803.31201171875,"z":40.22330856323242},"state":1}'),
	(106, 'Sandy City Hall 2-2', '{"maxDistance":2,"heading":123,"doors":false,"model":1053379387,"coords":{"x":1762.56201171875,"y":3808.486083984375,"z":40.2269401550293},"state":1}'),
	(107, 'Sandy City Hall 2-3', '{"maxDistance":2,"heading":123,"doors":false,"model":1053379387,"coords":{"x":1759.979736328125,"y":3812.4404296875,"z":40.22693634033203},"state":1}'),
	(108, 'Sandy City Hall 2-4', '{"maxDistance":2,"doors":[{"heading":213,"model":1053379387,"coords":{"x":1769.3228759765626,"y":3810.90380859375,"z":40.22930908203125}},{"heading":33,"model":1053379387,"coords":{"x":1767.402099609375,"y":3809.6494140625,"z":40.22853088378906}}],"coords":{"x":1768.362548828125,"y":3810.276611328125,"z":40.22891998291015},"state":1}'),
	(109, 'Sandy City Hall 3-1', '{"maxDistance":2,"heading":123,"doors":false,"model":1053379387,"coords":{"x":1753.39404296875,"y":3810.52734375,"z":43.47457885742187},"state":1}'),
	(110, 'Sandy City Hall 3-2', '{"maxDistance":2,"heading":123,"doors":false,"model":1053379387,"coords":{"x":1753.0794677734376,"y":3804.685546875,"z":43.47341156005859},"state":1}'),
	(111, 'Sandy City Hall 3-3', '{"maxDistance":2,"doors":[{"heading":123,"model":1053379387,"coords":{"x":1759.4586181640626,"y":3801.19580078125,"z":43.47457885742187}},{"heading":303,"model":1053379387,"coords":{"x":1758.204345703125,"y":3803.116455078125,"z":43.47457885742187}}],"coords":{"x":1758.83154296875,"y":3802.15625,"z":43.47457885742187},"state":1}'),
	(112, 'Sandy City Hall 3-4', '{"maxDistance":2,"heading":123,"doors":false,"model":1053379387,"coords":{"x":1764.017333984375,"y":3810.0908203125,"z":43.47751998901367},"state":1}'),
	(113, 'Sandy City Hall 3-5', '{"maxDistance":2,"heading":213,"doors":false,"model":1053379387,"coords":{"x":1762.7135009765626,"y":3816.012451171875,"z":43.4782485961914},"state":1}'),
	(114, 'Sandy City Hall 3-6', '{"maxDistance":2,"heading":33,"doors":false,"model":1053379387,"coords":{"x":1769.10888671875,"y":3810.7685546875,"z":43.47909545898437},"state":1}');
```
{% endtab %}
{% endtabs %}

***

### 🚀 **Installation Guide**

1. **Download the Map Resource**
   * Ensure the Sandy City Hall map resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       plaintextCopy

       ```
       start cfx_prompt_sandy_cityhall
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map location at **1728.1, 3787.36, 35.18** to ensure everything is working correctly.

For further assistance, contact support. Enjoy using Sandy City Hall on your FiveM server! 🚀
