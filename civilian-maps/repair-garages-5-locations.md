# 🔧 Repair Garages (5 locations)

{% embed url="https://fivem.prompt-mods.com/package/6254445" %}

## Repair Garages :wrench:

Repair Garages Project is a beautiful addition to any roleplay server. 5 Unique locations and 2 interior styles makes each location experience unique. Actually working carlifts is a perfect touch to increase realism of your roleplay situations. Created with love and intent!

{% embed url="https://www.youtube.com/watch?v=V-uoP32h7O8" %}

***

### 📍 Map Positions

chumash = **-2969.34, 438.79, 17.16**,\
city = **990.01, -1393.61, 32.43**,\
highway = **2573.65, 481.06, 109.83**,\
paleto = **-292.54, 6042.77, 32.21**,\
beach = **-1645.78, -794.85, 11.17**,

***

### 🧱 Reworked Exterior

* 5 custom exteriors
* Integrated visuals and smooth layout for easy roleplay

### 🔁 Entity Sets

You can toggle the following themes using `EntitySets`:

* `1`&#x20;
* `2`

Use them in your scripts or prop editors like Codewalker.

### 🪑 Custom Props

This map includes custom, streamed furniture and ambiance items:

**Chairs:**

* v\_corp\_sidechair
* xs\_x18intvip\_bar\_stool
* xm\_lab\_sofa\_02
* prop\_off\_chair\_01

**TVs & Screens:**

* `car_service_chiilzone_det`

***

### 🎯 Custom Prop Animations (ox\_lib Required)

This project includes **custom prop animations** that enhance immersion and interactivity. These animations only function if [`ox_lib`](https://github.com/overextended/ox_lib) is properly **ensured** in your server.

> ⚠️ Make sure `ox_lib` is started before this resource.\
> Add this to your `server.cfg` if you haven’t already:

```cfg
ensure ox_lib
```

### 🪄 Activation Spots

Below are the locations where players can trigger animations on custom props:

<mark style="color:green;">**Press "E" when looking at the**</mark>**&#x20;**<mark style="color:red;">**RED button**</mark>

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

#### Prop Names

Prop names are defined in each location's config. The default lifts use this naming pattern:

| Prop    | Name                               |
| ------- | ---------------------------------- |
| Lift 1  | `prompt_sandy_is_lift_mechanic_1`  |
| Lift 2  | `prompt_sandy_is_lift_mechanic_2`  |
| Lift 3  | `prompt_sandy_is_lift_mechanic_3`  |
| Lift 4  | `prompt_sandy_is_lift_mechanic_4`  |
| Lift 5  | `prompt_sandy_is_lift_mechanic_5`  |
| Lift 6  | `prompt_sandy_is_lift_mechanic_6`  |
| Lift 7  | `prompt_sandy_is_lift_mechanic_7`  |
| Lift 8  | `prompt_sandy_is_lift_mechanic_8`  |
| Lift 9  | `prompt_sandy_is_lift_mechanic_9`  |
| Lift 10 | `prompt_sandy_is_lift_mechanic_10` |

{% hint style="info" %}
The exact prop names depend on your `config.lua`. Check the `name` field of each prop entry to find the correct identifier for your setup.
{% endhint %}

### <i class="fa-podcast" style="color:$primary;">:podcast:</i> Exports



`getLiftState`

```lua
-- Returns: true (open/up), false (closed/down), or nil (unknown)
local isUp = exports['prompt_repair_shops']:getLiftState('prompt_sandy_is_lift_mechanic_1')
```

`isLiftBusy`

```lua
-- Returns: true if animating, false otherwise
local busy = exports['prompt_repair_shops']:isLiftBusy('prompt_sandy_is_lift_mechanic_1')
```

`setLiftState`

````lua
-- state: true = open/up, false = close/down
exports['prompt_repair_shops']:setLiftState('prompt_sandy_is_lift_mechanic_1', true)
```<div data-gb-custom-block data-tag="hint" data-style='warning'>`setLiftState` does not check if the prop is busy. You should check `isLiftBusy` first to avoid overlapping animations.</div></div><div data-gb-custom-block data-tag="tab" data-title='Server'>#### getLiftState

```lua
-- Returns: true (open/up), false (closed/down), or nil (unknown)
local isUp = exports['prompt_repair_shops']:getLiftState('prompt_sandy_is_lift_mechanic_1')
````

`isLiftBusy`

````lua
-- Returns: true if animating, false otherwise
local busy = exports['prompt_repair_shops']:isLiftBusy('prompt_sandy_is_lift_mechanic_1')
```</div></div>### Events<div data-gb-custom-block data-tag="tabs"><div data-gb-custom-block data-tag="tab" data-title='Client'>#### liftStateChanged

Fires when a prop animation **starts**.

```lua
AddEventHandler('prompt_repair_shops:liftStateChanged', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift_mechanic_1")
    -- state: true = opening/going up, false = closing/going down
end)
````

`liftAnimationComplete`

Fires when a prop animation **finishes**.

````lua
AddEventHandler('prompt_repair_shops:liftAnimationComplete', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift_mechanic_1")
    -- state: true = now open/up, false = now closed/down
end)
```</div><div data-gb-custom-block data-tag="tab" data-title='Server'>#### liftStateChanged

Fires when a prop's state is updated in GlobalState.

```lua
AddEventHandler('prompt_repair_shops:liftStateChanged', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift_mechanic_1")
    -- state: true = open/up, false = closed/down
end)
```</div></div>

### Full Example

```lua
-- Client-side: listen for any lift across all repair shop locations

AddEventHandler('prompt_repair_shops:liftStateChanged', function(propName, state)
    print(propName .. ' is now ' .. (state and 'GOING UP' or 'GOING DOWN'))
end)

AddEventHandler('prompt_repair_shops:liftAnimationComplete', function(propName, state)
    print(propName .. ' finished animating, now ' .. (state and 'UP' or 'DOWN'))
end)

-- Raise a specific lift programmatically
local propName = 'prompt_sandy_is_lift_mechanic_1'
local busy = exports['prompt_repair_shops']:isLiftBusy(propName)
local isUp = exports['prompt_repair_shops']:getLiftState(propName)

if not busy and not isUp then
    exports['prompt_repair_shops']:setLiftState(propName, true)
end
````

***

### :door:Doorlock System

This map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Doorlock Configuration**

Add the following SQL lines to your database to configure the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (1082, 'Chumash Repair Garage E-1', '{"coords":{"x":-2966.07763671875,"y":424.1371154785156,"z":15.36836433410644},"doors":[{"model":-1625527568,"coords":{"x":-2966.15771484375,"y":422.8583679199219,"z":15.36836433410644},"heading":266},{"model":104937776,"coords":{"x":-2965.997802734375,"y":425.4158630371094,"z":15.36836433410644},"heading":86}],"maxDistance":2,"state":0}'),
    (1083, 'Chumash Repair Garage E-2', '{"coords":{"x":-2959.872802734375,"y":428.8106994628906,"z":15.37855148315429},"model":-1232417342,"doors":false,"maxDistance":2,"heading":86,"state":1}'),
    (1084, 'Chumash Repair Garage E-3', '{"coords":{"x":-2959.634521484375,"y":431.8291015625,"z":15.94517135620117},"model":1748710857,"doors":false,"maxDistance":2,"heading":266,"state":1}'),
    (1085, 'Chumash Repair Garage E-4', '{"coords":{"x":-2959.311279296875,"y":436.99658203125,"z":15.94517135620117},"model":1748710857,"doors":false,"maxDistance":2,"heading":266,"state":1}'),
    (1086, 'Chumash Repair Garage E-5', '{"coords":{"x":-2958.988037109375,"y":442.1640625,"z":15.94517135620117},"model":1748710857,"doors":false,"maxDistance":2,"heading":266,"state":1}'),
    (1087, 'Chumash Repair Garage 1-1', '{"coords":{"x":-2965.0537109375,"y":419.3752136230469,"z":15.37855148315429},"model":263193286,"doors":false,"maxDistance":2,"heading":266,"state":1}'),
    (1088, 'Chumash Repair Garage 1-2', '{"coords":{"x":-2957.90087890625,"y":426.35821533203127,"z":15.37855052947998},"model":263193286,"doors":false,"maxDistance":2,"heading":176,"state":1}'),
    (1089, 'City Repair Garage E-1', '{"coords":{"x":990.1591796875,"y":-1404.3338623046876,"z":31.50117492675781},"doors":[{"model":-1625527568,"coords":{"x":990.1569213867188,"y":-1405.6151123046876,"z":31.50117492675781},"heading":270},{"model":104937776,"coords":{"x":990.161376953125,"y":-1403.0526123046876,"z":31.50117492675781},"heading":90}],"maxDistance":2,"state":0}'),
    (1090, 'City Repair Garage E-2', '{"coords":{"x":996.0689697265625,"y":-1399.292236328125,"z":31.51136207580566},"model":-1232417342,"doors":false,"maxDistance":2,"heading":90,"state":1}'),
    (1091, 'City Repair Garage E-3', '{"coords":{"x":996.1236572265625,"y":-1396.2650146484376,"z":32.0779800415039},"model":1748710857,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1092, 'City Repair Garage E-4', '{"coords":{"x":996.1326904296875,"y":-1391.08740234375,"z":32.0779800415039},"model":1748710857,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1093, 'City Repair Garage E-5', '{"coords":{"x":996.1417236328125,"y":-1385.9097900390626,"z":32.0779800415039},"model":1748710857,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1094, 'City Repair Garage 1-1', '{"coords":{"x":991.470703125,"y":-1409.0247802734376,"z":31.51136207580566},"model":263193286,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1095, 'City Repair Garage 1-2', '{"coords":{"x":998.1863403320313,"y":-1401.62060546875,"z":31.51136207580566},"model":263193286,"doors":false,"maxDistance":2,"heading":180,"state":1}'),
    (1096, 'Highway Repair Garage E-1', '{"coords":{"x":2574.46533203125,"y":467.824951171875,"z":108.66834259033203},"doors":[{"model":-1625527568,"coords":{"x":2574.472412109375,"y":466.5437316894531,"z":108.66834259033203},"heading":270},{"model":104937776,"coords":{"x":2574.45849609375,"y":469.106201171875,"z":108.66834259033203},"heading":90}],"maxDistance":2,"state":0}'),
    (1097, 'Highway Repair Garage E-2', '{"coords":{"x":2580.3388671875,"y":472.9087219238281,"z":108.67852783203125},"model":-1232417342,"doors":false,"maxDistance":2,"heading":90,"state":1}'),
    (1098, 'Highway Repair Garage E-3', '{"coords":{"x":2580.3720703125,"y":475.9363708496094,"z":109.24514770507813},"model":1748710857,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1099, 'Highway Repair Garage E-4', '{"coords":{"x":2580.343994140625,"y":481.1138610839844,"z":109.24514770507813},"model":1748710857,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1100, 'Highway Repair Garage E-5', '{"coords":{"x":2580.316162109375,"y":486.2913818359375,"z":109.24514770507813},"model":1748710857,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1101, 'Highway Repair Garage 1-1', '{"coords":{"x":2575.810302734375,"y":463.1435546875,"z":108.67852783203125},"model":263193286,"doors":false,"maxDistance":2,"heading":270,"state":1}'),
    (1102, 'Highway Repair Garage 1-2', '{"coords":{"x":2582.472900390625,"y":470.5957336425781,"z":108.67852783203125},"model":263193286,"doors":false,"maxDistance":2,"heading":180,"state":1}'),
    (1103, 'Paleto Repair Garage E-1', '{"coords":{"x":-298.0663146972656,"y":6031.6259765625,"z":31.60483360290527},"doors":[{"model":-1625527568,"coords":{"x":-298.9722900390625,"y":6030.72021484375,"z":31.60483360290527},"heading":225},{"model":104937776,"coords":{"x":-297.16033935546877,"y":6032.5322265625,"z":31.60483360290527},"heading":45}],"maxDistance":2,"state":0}'),
    (1104, 'Paleto Repair Garage E-2', '{"coords":{"x":-290.3214416503906,"y":6031.02587890625,"z":31.61502075195312},"model":-1232417342,"doors":false,"maxDistance":2,"heading":45,"state":1}'),
    (1105, 'Paleto Repair Garage E-3', '{"coords":{"x":-288.1457824707031,"y":6033.13134765625,"z":32.181640625},"model":1748710857,"doors":false,"maxDistance":2,"heading":225,"state":1}'),
    (1106, 'Paleto Repair Garage E-4', '{"coords":{"x":-284.48468017578127,"y":6036.79248046875,"z":32.181640625},"model":1748710857,"doors":false,"maxDistance":2,"heading":225,"state":1}'),
    (1107, 'Paleto Repair Garage E-5', '{"coords":{"x":-280.8235778808594,"y":6040.45361328125,"z":32.181640625},"model":1748710857,"doors":false,"maxDistance":2,"heading":225,"state":1}'),
    (1108, 'Paleto Repair Garage 1-1', '{"coords":{"x":-300.4485168457031,"y":6027.37744140625,"z":31.61502075195312},"model":263193286,"doors":false,"maxDistance":2,"heading":225,"state":1}'),
    (1109, 'Paleto Repair Garage 1-2', '{"coords":{"x":-290.4650573730469,"y":6027.8818359375,"z":31.61502075195312},"model":263193286,"doors":false,"maxDistance":2,"heading":135,"state":1}'),
    (1110, 'Beach Repair Garage E-1', '{"coords":{"x":-1646.264404296875,"y":-785.3914184570313,"z":10.31435871124267},"doors":[{"model":-1625527568,"coords":{"x":-1645.44140625,"y":-784.4094848632813,"z":10.31435871124267},"heading":50},{"model":104937776,"coords":{"x":-1647.0875244140626,"y":-786.3733520507813,"z":10.31435871124267},"heading":230}],"maxDistance":2,"state":0}'),
    (1111, 'Beach Repair Garage E-2', '{"coords":{"x":-1654.0322265625,"y":-785.4723510742188,"z":10.32454586029052},"model":-1232417342,"doors":false,"maxDistance":2,"heading":230,"state":1}'),
    (1112, 'Beach Repair Garage E-3', '{"coords":{"x":-1656.014892578125,"y":-787.7607421875,"z":10.8911657333374},"model":1748710857,"doors":false,"maxDistance":2,"heading":50,"state":1}'),
    (1113, 'Beach Repair Garage E-4', '{"coords":{"x":-1659.3408203125,"y":-791.728759765625,"z":10.8911657333374},"model":1748710857,"doors":false,"maxDistance":2,"heading":50,"state":1}'),
    (1114, 'Beach Repair Garage E-5', '{"coords":{"x":-1662.6668701171876,"y":-795.69677734375,"z":10.8911657333374},"model":1748710857,"doors":false,"maxDistance":2,"heading":50,"state":1}'),
    (1115, 'Beach Repair Garage 1-1', '{"coords":{"x":-1644.263916015625,"y":-780.9503784179688,"z":10.32454586029052},"model":263193286,"doors":false,"maxDistance":2,"heading":50,"state":1}'),
    (1116, 'Beach Repair Garage 1-2', '{"coords":{"x":-1654.1646728515626,"y":-782.3281860351563,"z":10.32454490661621},"model":263193286,"doors":false,"maxDistance":2,"heading":320,"state":1}');
```

***

### 🚀 **Installation Guide**

To install the Repair Garage map on your FiveM server, follow these steps:

1. **Download the Map Resource**
   * Ensure the **prompt\_repair\_shops** resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start prompt_repair_shops
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](../sandy-maps/sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map at it's location to ensure everything is working correctly.

***

For further assistance, contact support. Enjoy using Repair Garage on your FiveM server! 🚀
