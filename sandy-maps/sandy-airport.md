# 🛫 Sandy Airport

{% embed url="https://fivem.prompt-mods.com/package/6254445" %}

{% embed url="https://youtu.be/d2cpWGlogmI?si=NlM-MKwd8pSSU7C-" %}

The **Sandy Airport** is a custom map designed for FiveM servers, offering a fully functional airport environment for roleplay, aviation activities, and transportation scenarios. This map includes a variety of chairs, props, and a doorlock system for enhanced interactivity. Below is the available information about the map.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 **Map Position**

The Sandy Airport map is located at the following coordinates:\
**1690.88, 3295.83, 41.40**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The Sandy Airport map includes a variety of chairs and props to enhance the environment:

**Chairs**

* **prop\_bench\_01a**
* **prop\_skid\_chair\_01**
* **tr\_int1\_mod\_sofa\_009**
* **prompt\_sdair\_seating\_hall**
* **h4\_prop\_battle\_club\_chair\_01**
* **v\_res\_tre\_officechair**
* **ch\_chint02\_toilet\_beam**
* **v\_ind\_meatbench**
* **prop\_off\_chair\_04b**
* **v\_ret\_gc\_chair01**
* **prop\_cs\_office\_chair**
* **prop\_ld\_farm\_couch02**
* **prop\_clown\_chair**
* **prop\_off\_chair\_03**
* **v\_club\_vuarmchair**

**TV Props**

* **prop\_cs\_tv\_stand**
* **prop\_tv\_06**

***

#### 🚪 **Doorlock System**

The Sandy Airport map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Doorlock Configuration**

Add the following SQL lines to your database to configure the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(221, 'Sandy Shores Airport E-1', '{"doors":[{"coords":{"x":1695.1978759765626,"y":3300.292236328125,"z":41.68905258178711},"model":-1724308956,"heading":285},{"coords":{"x":1694.538818359375,"y":3302.752197265625,"z":41.68905258178711},"model":-1724308956,"heading":105}],"coords":{"x":1694.868408203125,"y":3301.522216796875,"z":41.68905258178711},"state":0,"maxDistance":2}'),
(222, 'Sandy Shores Airport 1-1', '{"doors":false,"model":1562995625,"coords":{"x":1703.8314208984376,"y":3307.389404296875,"z":41.71824645996094},"heading":285,"state":1,"maxDistance":2}'),
(223, 'Sandy Shores Airport 1-2', '{"doors":false,"model":1562995625,"coords":{"x":1703.1763916015626,"y":3309.833984375,"z":41.71824645996094},"heading":285,"state":1,"maxDistance":2}'),
(224, 'Sandy Shores Airport 1-3', '{"doors":false,"model":1562995625,"coords":{"x":1702.5233154296876,"y":3312.271728515625,"z":41.71824645996094},"heading":285,"state":1,"maxDistance":2}'),
(225, 'Sandy Shores Airport 1-4', '{"doors":false,"model":-1184592117,"coords":{"x":1699.7757568359376,"y":3293.64697265625,"z":41.81744384765625},"heading":285,"state":1,"maxDistance":2}'),
(226, 'Sandy Shores Airport 1-5', '{"doors":false,"model":-1259801187,"coords":{"x":1700.4830322265626,"y":3291.8671875,"z":41.63738250732422},"heading":285,"state":1,"maxDistance":2}'),
(227, 'Sandy Shores Airport 1-6', '{"doors":false,"model":-1184592117,"coords":{"x":1702.856689453125,"y":3290.73486328125,"z":41.82458877563476},"heading":195,"state":1,"maxDistance":2}'),
(228, 'Sandy Shores Airport 1-7', '{"doors":false,"model":1167251902,"coords":{"x":1706.36669921875,"y":3289.259033203125,"z":41.71150207519531},"heading":195,"state":1,"maxDistance":2}'),
(229, 'Sandy Shores Airport 1-8', '{"doors":false,"model":-1184592117,"coords":{"x":1703.14501953125,"y":3288.216552734375,"z":41.8117790222168},"heading":105,"state":1,"maxDistance":2}'),
(230, 'Sandy Shores Airport E-2', '{"doors":false,"model":-341973294,"coords":{"x":1704.1488037109376,"y":3285.532958984375,"z":41.69929885864258},"heading":15,"state":1,"maxDistance":2}'),
(231, 'Sandy Shores Airport 2-1', '{"doors":false,"model":-1230442770,"coords":{"x":1705.66162109375,"y":3294.537841796875,"z":44.85938262939453},"heading":15,"state":1,"maxDistance":2}'),
(232, 'Sandy Shores Airport 2-2', '{"doors":false,"model":-1821777087,"coords":{"x":1699.6700439453126,"y":3294.940673828125,"z":44.84265518188476},"heading":285,"state":1,"maxDistance":2}'),
(233, 'Sandy Shores Airport 2-3', '{"doors":false,"model":-1821777087,"coords":{"x":1698.82568359375,"y":3298.036376953125,"z":44.85874557495117},"heading":285,"state":1,"maxDistance":2}'),
(234, 'Sandy Shores Airport 2-4', '{"doors":false,"model":-522504255,"coords":{"x":1701.247314453125,"y":3300.3994140625,"z":44.85702514648437},"heading":285,"state":1,"maxDistance":2}'),
(235, 'Sandy Shores Airport 2-5', '{"doors":false,"model":-1821777087,"coords":{"x":1696.602783203125,"y":3306.3876953125,"z":44.84265518188476},"heading":105,"state":1,"maxDistance":2}'),
(236, 'Sandy Shores Airport 2-6', '{"doors":[{"coords":{"x":1699.327392578125,"y":3307.409423828125,"z":44.86448669433594},"model":-658747851,"heading":105},{"coords":{"x":1698.6534423828126,"y":3309.9189453125,"z":44.86448669433594},"model":1335311341,"heading":105}],"coords":{"x":1698.990478515625,"y":3308.6640625,"z":44.86448669433594},"state":1,"maxDistance":2}'),
(237, 'Sandy Shores Airport E-3', '{"doors":false,"model":-1775213343,"coords":{"x":1699.5006103515626,"y":3306.9296875,"z":47.6656608581543},"heading":285,"state":1,"maxDistance":2}'),
(238, 'Sandy Shores Airport E-4', '{"doors":false,"model":-1775213343,"coords":{"x":1702.2371826171876,"y":3293.650634765625,"z":47.73307418823242},"heading":285,"state":1,"maxDistance":2}'),
(239, 'Sandy Shores Airport 2-1-1', '{"doors":false,"model":270965283,"coords":{"x":1732.7806396484376,"y":3330.191162109375,"z":41.46370315551758},"heading":284,"state":1,"maxDistance":2}'),
(240, 'Sandy Shores Airport 2-E-1', '{"doors":false,"model":-517802710,"coords":{"x":1730.24609375,"y":3324.587158203125,"z":41.4677505493164},"heading":284,"state":1,"maxDistance":2}'),
(241, 'Sandy Shores Airport 3-G-1', '{"doors":false,"model":22664328,"coords":{"x":1656.3760986328126,"y":3339.6728515625,"z":43.13911819458008},"heading":15,"state":1,"maxDistance":2}'),
(242, 'Sandy Shores Airport 3-G-2', '{"doors":false,"model":22664328,"coords":{"x":1651.2008056640626,"y":3338.2861328125,"z":43.13911819458008},"heading":15,"state":1,"maxDistance":2}'),
(243, 'Sandy Shores Airport 3-G-3', '{"doors":false,"model":22664328,"coords":{"x":1646.0286865234376,"y":3336.900146484375,"z":43.13911819458008},"heading":15,"state":1,"maxDistance":2}'),
(244, 'Sandy Shores Airport 3-G-4', '{"doors":false,"model":22664328,"coords":{"x":1640.8265380859376,"y":3335.50634765625,"z":43.13911819458008},"heading":15,"state":1,"maxDistance":2}'),
(245, 'Sandy Shores Airport 3-E-1', '{"doors":false,"model":464151082,"coords":{"x":1631.7677001953126,"y":3329.55517578125,"z":42.50802230834961},"heading":105,"state":1,"maxDistance":2}'),
(246, 'Sandy Shores Airport 3-E-2', '{"doors":false,"model":452874391,"coords":{"x":1663.3388671875,"y":3350.65185546875,"z":44.48569869995117},"heading":105,"state":1,"maxDistance":2}'),
(247, 'Sandy Shores Airport 3-1-1', '{"doors":false,"model":452874391,"coords":{"x":1659.107666015625,"y":3350.12060546875,"z":44.48304748535156},"heading":105,"state":1,"maxDistance":2}'),
(249, 'Sandy Shores Airport 3-1-2', '{"doors":[{"coords":{"x":1634.9259033203126,"y":3341.044921875,"z":42.13880157470703},"model":452874391,"heading":105},{"coords":{"x":1635.5994873046876,"y":3338.53076171875,"z":42.13880157470703},"model":452874391,"heading":285}],"coords":{"x":1635.2626953125,"y":3339.787841796875,"z":42.13880157470703},"state":1,"maxDistance":2}'),
(250, 'Sandy Shores Airport 3-1-4', '{"doors":false,"model":452874391,"coords":{"x":1630.1126708984376,"y":3332.5048828125,"z":42.14106369018555},"heading":15,"state":1,"maxDistance":2}'),
(251, 'Sandy Shores Airport 3-1-5', '{"doors":[{"coords":{"x":1631.0718994140626,"y":3336.689697265625,"z":42.12973022460937},"model":-1421582160,"heading":195},{"coords":{"x":1633.5841064453126,"y":3337.3681640625,"z":42.12973022460937},"model":1248599813,"heading":15}],"coords":{"x":1632.3280029296876,"y":3337.02880859375,"z":42.12973022460937},"state":1,"maxDistance":2}'),
(252, 'Sandy Shores Airport 3-1-6', '{"doors":[{"coords":{"x":1632.5853271484376,"y":3341.070556640625,"z":42.13223266601562},"model":270965283,"heading":195},{"coords":{"x":1630.0806884765626,"y":3340.3994140625,"z":42.13223266601562},"model":270965283,"heading":15}],"coords":{"x":1631.3330078125,"y":3340.73486328125,"z":42.13223266601562},"state":1,"maxDistance":2}');
```

***

### 🚀 **Installation Guide**

To install the Sandy Airport map on your FiveM server, follow these steps:

1. **Download the Map Resource**
   * Ensure the Sandy Airport map resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start cfx_prompt_sandy_airfield
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map location at **1690.88, 3295.83, 41.40** to ensure everything is working correctly.

***

For further assistance, contact support. Enjoy using Sandy Airport on your FiveM server! 🚀
