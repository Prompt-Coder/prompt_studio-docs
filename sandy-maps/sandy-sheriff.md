# 👮 Sandy Sheriff

{% embed url="https://fivem.prompt-mods.com/package/6308272" %}

{% embed url="https://youtu.be/SxPlsYA9JEg?si=lsvzW45rIot2kHv8" %}

The **Sandy Sheriff Station** is a custom map designed for FiveM servers, offering a fully functional law enforcement environment for roleplay and policing scenarios. This map includes a variety of chairs, props, and a doorlock system for enhanced interactivity. Below is the available information about the map.

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

### 📍 **Map Position**

The Sandy Sheriff Station map is located at the following coordinates:\
&#xNAN;**`1832.67, 3660.27, 33.93`**

***

### 🛠️ **Features**

#### 🪑 **Chairs and Props**

The Sandy Sheriff Station map includes a variety of chairs and props to enhance the environment:

**Chairs**

* **prompt\_sandy\_sheriff\_chair\_01**
* **prop\_off\_chair\_01**
* **apa\_mp\_h\_din\_chair\_12**
* **prop\_bench\_06**
* **prop\_chair\_06**
* **v\_corp\_offchair**
* **v\_res\_trev\_framechair**
* **v\_ret\_gc\_chair03**
* **prop\_toilet\_01**
* **hei\_heist\_toilet03**
* **prop\_off\_chair\_05**

***

#### 🚪 **Doorlock System**

The Sandy Sheriff Station map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Doorlock Configuration**

Add the following SQL lines to your database to configure the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
(159, 'Sandy Shores Sheriff Station E-1', '{"doors":[{"coords":{"x":1830.706298828125,"y":3666.197265625,"z":34.5544548034668},"model":-1980936835,"heading":210},{"coords":{"x":1828.701416015625,"y":3665.04296875,"z":34.55611801147461},"model":1581676092,"heading":30}],"coords":{"x":1829.703857421875,"y":3665.6201171875,"z":34.5552864074707},"state":1,"maxDistance":2}'),
	(160, 'Sandy Shores Sheriff Station E-2', '{"doors":[{"coords":{"x":1823.9677734375,"y":3662.896240234375,"z":38.88916397094726},"model":-1980936835,"heading":120},{"coords":{"x":1822.8138427734376,"y":3664.90087890625,"z":38.89082717895508},"model":1581676092,"heading":300}],"coords":{"x":1823.390869140625,"y":3663.8984375,"z":38.88999557495117},"state":1,"maxDistance":2}'),
	(161, 'Sandy Shores Sheriff Station E-3', '{"doors":[{"coords":{"x":1815.572998046875,"y":3679.877197265625,"z":34.55278778076172},"model":-1980936835,"heading":30},{"coords":{"x":1817.577880859375,"y":3681.031005859375,"z":34.55445098876953},"model":1581676092,"heading":210}],"coords":{"x":1816.575439453125,"y":3680.4541015625,"z":34.55361938476562},"state":1,"maxDistance":2}'),
	(162, 'Sandy Shores Sheriff Station E-4', '{"doors":[{"coords":{"x":1831.4598388671876,"y":3678.618896484375,"z":31.59107398986816},"model":-1980936835,"heading":300},{"coords":{"x":1832.61376953125,"y":3676.614013671875,"z":31.59273719787597},"model":1581676092,"heading":120}],"coords":{"x":1832.036865234375,"y":3677.616455078125,"z":31.59190559387207},"state":1,"maxDistance":2}'),
	(163, 'Sandy Shores Sheriff Station E-5', '{"doors":false,"model":-1980936835,"coords":{"x":1834.11279296875,"y":3675.2109375,"z":34.55445098876953},"heading":30,"state":1,"maxDistance":2}'),
	(164, 'Sandy Shores Sheriff Station E-6', '{"doors":false,"model":1286535678,"coords":{"x":1865.4468994140626,"y":3684.87548828125,"z":32.81907272338867},"heading":30,"state":1,"maxDistance":2}'),
	(165, 'Sandy Shores Sheriff Station E-7', '{"doors":false,"model":1286535678,"coords":{"x":1846.5853271484376,"y":3708.118896484375,"z":32.80280303955078},"heading":30,"state":1,"maxDistance":2}'),
	(166, 'Sandy Shores Sheriff Station E-8', '{"doors":false,"model":1286535678,"coords":{"x":1805.806884765625,"y":3675.81396484375,"z":33.27196502685547},"heading":300,"state":1,"maxDistance":2}'),
	(167, 'Sandy Shores Sheriff Station G-1', '{"doors":false,"model":-822900180,"coords":{"x":1838.95458984375,"y":3678.05224609375,"z":34.95901489257812},"heading":210,"state":1,"maxDistance":2}'),
	(168, 'Sandy Shores Sheriff Station 1-1', '{"doors":[{"coords":{"x":1824.369140625,"y":3669.497802734375,"z":34.55217742919922},"model":-1359993876,"heading":210},{"coords":{"x":1822.11572265625,"y":3668.19677734375,"z":34.55217742919922},"model":-1359993876,"heading":30}],"coords":{"x":1823.242431640625,"y":3668.84716796875,"z":34.55217742919922},"state":1,"maxDistance":2}'),
	(169, 'Sandy Shores Sheriff Station 1-2', '{"doors":false,"model":-1198567762,"coords":{"x":1831.8428955078126,"y":3667.123779296875,"z":34.55217742919922},"heading":30,"state":1,"maxDistance":2}'),
	(170, 'Sandy Shores Sheriff Station 1-3', '{"doors":false,"model":-1359993876,"coords":{"x":1834.154296875,"y":3668.947998046875,"z":34.55218124389648},"heading":120,"state":1,"maxDistance":2}'),
	(171, 'Sandy Shores Sheriff Station 1-4', '{"doors":false,"model":-1359993876,"coords":{"x":1829.177978515625,"y":3672.025146484375,"z":34.55218124389648},"heading":30,"state":1,"maxDistance":2}'),
	(172, 'Sandy Shores Sheriff Station 1-5', '{"doors":false,"model":-648906987,"coords":{"x":1819.3739013671876,"y":3666.528076171875,"z":34.5640983581543},"heading":210,"state":1,"maxDistance":2}'),
	(173, 'Sandy Shores Sheriff Station 1-6', '{"doors":[{"coords":{"x":1819.21875,"y":3672.133056640625,"z":34.55217742919922},"model":-443582481,"heading":255},{"coords":{"x":1818.6075439453126,"y":3669.85693359375,"z":34.55217742919922},"model":1090498258,"heading":75}],"coords":{"x":1818.9130859375,"y":3670.9951171875,"z":34.55217742919922},"state":0,"maxDistance":2}'),
	(174, 'Sandy Shores Sheriff Station 1-7', '{"doors":false,"model":-1359993876,"coords":{"x":1824.106201171875,"y":3672.313720703125,"z":34.55217742919922},"heading":30,"state":1,"maxDistance":2}'),
	(175, 'Sandy Shores Sheriff Station 1-8', '{"doors":false,"model":-1599297511,"coords":{"x":1821.6248779296876,"y":3675.105224609375,"z":34.55217742919922},"heading":300,"state":1,"maxDistance":2}'),
	(176, 'Sandy Shores Sheriff Station 1-9', '{"doors":[{"coords":{"x":1821.3836669921876,"y":3675.51953125,"z":34.55217742919922},"model":1220592199,"heading":120},{"coords":{"x":1820.0826416015626,"y":3677.77294921875,"z":34.55217742919922},"model":-1807296178,"heading":300}],"coords":{"x":1820.733154296875,"y":3676.646240234375,"z":34.55217742919922},"state":1,"maxDistance":2}'),
	(177, 'Sandy Shores Sheriff Station 1-10', '{"doors":false,"model":-902064185,"coords":{"x":1819.7030029296876,"y":3678.45849609375,"z":34.55217742919922},"heading":120,"state":1,"maxDistance":2}'),
	(178, 'Sandy Shores Sheriff Station 2-1', '{"doors":[{"coords":{"x":1823.3118896484376,"y":3668.576171875,"z":38.88373947143555},"model":1090498258,"heading":75},{"coords":{"x":1823.9229736328126,"y":3670.852294921875,"z":38.88373947143555},"model":-443582481,"heading":255}],"coords":{"x":1823.617431640625,"y":3669.71435546875,"z":38.88373947143555},"state":1,"maxDistance":2}'),
	(179, 'Sandy Shores Sheriff Station 2-2', '{"doors":false,"model":855469211,"coords":{"x":1830.811767578125,"y":3668.013671875,"z":38.88066864013672},"heading":120,"state":1,"maxDistance":2}'),
	(180, 'Sandy Shores Sheriff Station 2-3', '{"doors":false,"model":-1198567762,"coords":{"x":1832.43017578125,"y":3671.620849609375,"z":38.88855361938476},"heading":120,"state":1,"maxDistance":2}'),
	(181, 'Sandy Shores Sheriff Station 2-4', '{"doors":false,"model":-1198567762,"coords":{"x":1831.4564208984376,"y":3673.307373046875,"z":38.88855361938476},"heading":120,"state":1,"maxDistance":2}'),
	(182, 'Sandy Shores Sheriff Station 2-5', '{"doors":false,"model":-1198567762,"coords":{"x":1830.47900390625,"y":3675.000244140625,"z":38.88855361938476},"heading":120,"state":1,"maxDistance":2}'),
	(183, 'Sandy Shores Sheriff Station 2-6', '{"doors":false,"model":549536201,"coords":{"x":1825.579833984375,"y":3677.76806640625,"z":38.8885498046875},"heading":300,"state":1,"maxDistance":2}'),
	(184, 'Sandy Shores Sheriff Station 2-7', '{"doors":false,"model":1627904350,"coords":{"x":1823.675048828125,"y":3680.985107421875,"z":38.89082336425781},"heading":300,"state":1,"maxDistance":2}'),
	(185, 'Sandy Shores Sheriff Station E-9', '{"doors":false,"model":2076431776,"coords":{"x":1831.954833984375,"y":3670.895263671875,"z":42.83003234863281},"heading":210,"state":1,"maxDistance":2}'),
	(186, 'Sandy Shores Sheriff Station 1-11', '{"doors":false,"model":-1534276536,"coords":{"x":1836.4466552734376,"y":3670.271484375,"z":34.55218124389648},"heading":120,"state":1,"maxDistance":2}'),
	(187, 'Sandy Shores Sheriff Station 0-1', '{"doors":[{"coords":{"x":1830.08935546875,"y":3680.7158203125,"z":31.58880043029785},"model":-954071075,"heading":210},{"coords":{"x":1827.8359375,"y":3679.414794921875,"z":31.58880043029785},"model":-532039068,"heading":30}],"coords":{"x":1828.962646484375,"y":3680.0654296875,"z":31.58880043029785},"state":0,"maxDistance":2}'),
	(188, 'Sandy Shores Sheriff Station 0-2', '{"doors":[{"coords":{"x":1828.7684326171876,"y":3677.535888671875,"z":31.58880043029785},"model":-778772229,"heading":300},{"coords":{"x":1830.0701904296876,"y":3675.282958984375,"z":31.58880043029785},"model":1163413636,"heading":120}],"coords":{"x":1829.4193115234376,"y":3676.409423828125,"z":31.58880043029785},"state":0,"maxDistance":2}'),
	(189, 'Sandy Shores Sheriff Station 0-3', '{"doors":false,"model":1328379272,"coords":{"x":1827.4638671875,"y":3685.958984375,"z":30.80529975891113},"heading":120,"state":1,"maxDistance":2}'),
	(190, 'Sandy Shores Sheriff Station 0-4', '{"doors":false,"model":-954071075,"coords":{"x":1825.7886962890626,"y":3688.883544921875,"z":30.80529975891113},"heading":120,"state":1,"maxDistance":2}'),
	(191, 'Sandy Shores Sheriff Station 0-7', '{"doors":false,"model":1667632123,"coords":{"x":1821.9716796875,"y":3680.68310546875,"z":30.86857986450195},"heading":30,"state":1,"maxDistance":2}'),
	(192, 'Sandy Shores Sheriff Station 0-5', '{"doors":false,"model":-571098561,"coords":{"x":1823.087158203125,"y":3678.58935546875,"z":30.84140396118164},"heading":30,"state":1,"maxDistance":2}'),
	(193, 'Sandy Shores Sheriff Station 0-6', '{"doors":false,"model":961407919,"coords":{"x":1825.189697265625,"y":3673.342529296875,"z":30.84356307983398},"heading":300,"state":1,"maxDistance":2}'),
	(194, 'Sandy Shores Sheriff Station 0-8', '{"doors":false,"model":961407919,"coords":{"x":1822.91845703125,"y":3674.95556640625,"z":30.84356307983398},"heading":30,"state":1,"maxDistance":2}'),
	(195, 'Sandy Shores Sheriff Station 0-9', '{"doors":false,"model":961407919,"coords":{"x":1819.824462890625,"y":3673.28857421875,"z":30.84356307983398},"heading":30,"state":1,"maxDistance":2}'),
	(196, 'Sandy Shores Sheriff Station 0-10', '{"doors":false,"model":961407919,"coords":{"x":1825.03271484375,"y":3671.293701171875,"z":30.84356307983398},"heading":30,"state":1,"maxDistance":2}'),
	(197, 'Sandy Shores Sheriff Station 0-11', '{"doors":false,"model":961407919,"coords":{"x":1817.06787109375,"y":3678.063232421875,"z":30.84356307983398},"heading":30,"state":1,"maxDistance":2}'),
	(198, 'Sandy Shores Sheriff Station 0-12', '{"doors":false,"model":961407919,"coords":{"x":1820.0582275390626,"y":3679.90966796875,"z":30.84356307983398},"heading":30,"state":1,"maxDistance":2}'),
	(199, 'Sandy Shores Sheriff Station 0-13', '{"doors":false,"model":961407919,"coords":{"x":1827.0650634765626,"y":3667.7734375,"z":30.84356307983398},"heading":30,"state":1,"maxDistance":2}');
```

***

### 🚀 **Installation Guide**

To install the Sandy Sheriff Station map on your FiveM server, follow these steps:

1. **Download the Map Resource**
   * Ensure the Sandy Sheriff Station map resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start cfx_prompt_sandy_sheriff
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData (if required)**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map location to ensure everything is working correctly.

***

For further assistance, contact support. Enjoy using Sandy Hospital on your FiveM server! 🚀
