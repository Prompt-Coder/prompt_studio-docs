# 🔧 Sandy Mechanic

## Sandy Mechanic

{% embed url="https://fivem.prompt-mods.com/package/6254445" %}

The **Sandy Shores Mechanic**—better known as **“The Compound”**—turns a slice of Sandy Shores into an all-in-one automotive playground. Tune cars, run a business, or brew up criminal plots in a gated yard packed with interactives.

{% embed url="https://www.youtube.com/watch?v=rL9EzhSOs1o" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

#### 📍 Map Position

**1736.58, 3693.19, 35.22**

***

<details>

<summary>🔧 Main Features</summary>

* **Mechanic Bays** – Fully kitted for repairs & tuning
* **Performance Test Pad** – Drift / 0-100 trials
* **Detailing Zone** – Wash, wax, flex
* **Mini Barbershop** – Haircuts while you wait
* **Lounge-Café** – Hookahs, drinks, sofas
* **Gaming Corner** – Chill between jobs
* **Boss Office** – Oversee the compound

</details>

<details>

<summary>🏋️ Exterior &#x26; Future GYM</summary>

* Full compound fencing + security gates
* Back-lot access for haulers
* **GYM shell** next-door (interior coming soon)

</details>

<details>

<summary>🎛️ EntitySets</summary>

Toggle with your script / Codewalker: `default`

</details>

<details>

<summary>🪑 Custom Props</summary>

**Seating**\
`ex_prop_offchair_exec_01`, `car_service_barsofa`, `car_service_barstool`,\
`car_service_reception_sofa`, `v_corp_facebeanbagc`, `v_corp_facebeanbagd`,\
`sm_prop_offchair_smug_02`

**Screens**\
`car_service_chiilzone_det`

</details>

<details>

<summary>🎯 Prop Animations (requires <code>ox_lib</code>)</summary>



This project includes **custom prop animations** that enhance immersion and interactivity. These animations only function if [`ox_lib`](https://github.com/overextended/ox_lib) is properly **ensured** in your server.

> ⚠️ Make sure `ox_lib` is started before this resource.\
> Add this to your `server.cfg` if you haven’t already:

```cfg
ensure ox_lib
```

### 🪄 Activation Spots

Below are the locations where players can trigger animations on custom props:

<mark style="color:green;">**Press "E"**</mark>

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>PRESS "E" to activate animation</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>PRESS "E" to activate animation</p></figcaption></figure>

</details>

<details>

<summary><i class="fa-podcast" style="color:$primary;">:podcast:</i> Exports</summary>

#### Prop Names

| Prop                 | Name                     |
| -------------------- | ------------------------ |
| Car Lift 1           | `prompt_sandy_is_lift_2` |
| Car Lift 2           | `prompt_sandy_is_lift_3` |
| Car Lift 3           | `prompt_sandy_is_lift_4` |
| Garage Rollup Door 1 | `garage_rollup_1`        |
| Garage Rollup Door 2 | `garage_rollup_2`        |
| Garage Rollup Door 3 | `garage_rollup_3`        |
| Garage Rollup Door 4 | `garage_rollup_4`        |
| Garage Rollup Door 5 | `garage_rollup_5`        |

#### Exports



`getLiftState`

```lua
-- Returns: true (open/up), false (closed/down), or nil (unknown)
local isUp = exports['prompt_sandy_mechanic']:getLiftState('prompt_sandy_is_lift_2')
```



`isLiftBusy`

```lua
-- Returns: true if animating, false otherwise
local busy = exports['prompt_sandy_mechanic']:isLiftBusy('prompt_sandy_is_lift_2')
```



`setLiftState`

````lua
-- state: true = open/up, false = close/down
exports['prompt_sandy_mechanic']:setLiftState('prompt_sandy_is_lift_2', true)
```<div data-gb-custom-block data-tag="hint" data-style='warning'>`setLiftState` does not check if the prop is busy. You should check `isLiftBusy` first to avoid overlapping animations.</div></div><div data-gb-custom-block data-tag="tab" data-title='Server'>#### getLiftState

```lua
-- Returns: true (open/up), false (closed/down), or nil (unknown)
local isUp = exports['prompt_sandy_mechanic']:getLiftState('prompt_sandy_is_lift_2')
````



`isLiftBusy`

````lua
-- Returns: true if animating, false otherwise
local busy = exports['prompt_sandy_mechanic']:isLiftBusy('prompt_sandy_is_lift_2')
```</div></div>### Events<div data-gb-custom-block data-tag="tabs"><div data-gb-custom-block data-tag="tab" data-title='Client'>#### liftStateChanged

Fires when a prop animation **starts**.

```lua
AddEventHandler('prompt_sandy_mechanic:liftStateChanged', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift_2")
    -- state: true = opening/going up, false = closing/going down
end)
````



`liftAnimationComplete`

Fires when a prop animation **finishes**.

````lua
AddEventHandler('prompt_sandy_mechanic:liftAnimationComplete', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift_2")
    -- state: true = now open/up, false = now closed/down
end)
```</div><div data-gb-custom-block data-tag="tab" data-title='Server'>#### liftStateChanged

Fires when a prop's state is updated in GlobalState.

```lua
AddEventHandler('prompt_sandy_mechanic:liftStateChanged', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift_2")
    -- state: true = open/up, false = closed/down
end)
```</div></div>

### Full Example

```lua
-- Client-side: listen for any lift in the mechanic shop

AddEventHandler('prompt_sandy_mechanic:liftStateChanged', function(propName, state)
    print(propName .. ' is now ' .. (state and 'GOING UP' or 'GOING DOWN'))
end)

-- Raise lift 2 programmatically
local busy = exports['prompt_sandy_mechanic']:isLiftBusy('prompt_sandy_is_lift_2')
local isUp = exports['prompt_sandy_mechanic']:getLiftState('prompt_sandy_is_lift_2')

if not busy and not isUp then
    exports['prompt_sandy_mechanic']:setLiftState('prompt_sandy_is_lift_2', true)
end
````

***

</details>

***

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f6aa">🚪</span>Doorlock System</summary>

This map includes a doorlock system to control access to specific areas. Below are the details for implementing the doorlock feature:

**Doorlock Configuration**

Add the following SQL lines to your database to configure the doorlock system:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (DEFAULT, 'Sandy Shores Mechanic E-1', '{"coords":{"x":1745.6676025390626,"y":3672.833251953125,"z":35.52954483032226},"doors":[{"coords":{"x":1749.8431396484376,"y":3675.245361328125,"z":35.52766418457031},"heading":210,"model":200497552},{"coords":{"x":1741.4920654296876,"y":3670.421142578125,"z":35.53142547607422},"heading":30,"model":200497552}],"maxDistance":2,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic E-2', '{"coords":{"x":1715.160400390625,"y":3725.484375,"z":34.72872924804687},"doors":[{"coords":{"x":1710.98486328125,"y":3723.072265625,"z":34.73060989379883},"heading":30,"model":200497552},{"coords":{"x":1719.3359375,"y":3727.896484375,"z":34.72684860229492},"heading":210,"model":200497552}],"maxDistance":2,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic G-1', '{"heading":0,"coords":{"x":1714.885009765625,"y":3689.18994140625,"z":35.7239990234375},"doors":false,"maxDistance":2,"model":106631274,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic G-2', '{"heading":0,"coords":{"x":1711.9449462890626,"y":3694.260009765625,"z":35.28200149536133},"doors":false,"maxDistance":2,"model":106631274,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic G-3', '{"heading":0,"coords":{"x":1709.06494140625,"y":3699.260009765625,"z":35.28200149536133},"doors":false,"maxDistance":2,"model":106631274,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic G-4', '{"heading":0,"coords":{"x":1706.06494140625,"y":3704.449951171875,"z":35.28200149536133},"doors":false,"maxDistance":2,"model":106631274,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic G-5', '{"heading":0,"coords":{"x":1703.0350341796876,"y":3709.68994140625,"z":35.28200149536133},"doors":false,"maxDistance":2,"model":106631274,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic E-3', '{"heading":30,"coords":{"x":1719.623291015625,"y":3681.386474609375,"z":35.08953475952148},"doors":false,"maxDistance":2,"model":1858620080,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 2-1', '{"heading":120,"coords":{"x":1708.0487060546876,"y":3686.794189453125,"z":39.16519546508789},"doors":false,"maxDistance":2,"model":1686047085,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 2-2', '{"heading":120,"coords":{"x":1704.79296875,"y":3687.734375,"z":39.15148162841797},"doors":false,"maxDistance":2,"model":493737836,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 2-3', '{"heading":300,"coords":{"x":1702.81005859375,"y":3695.86767578125,"z":39.16519546508789},"doors":false,"maxDistance":2,"model":1686047085,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 2-4', '{"heading":120,"coords":{"x":1700.659423828125,"y":3694.897216796875,"z":39.15148162841797},"doors":false,"maxDistance":2,"model":-1538617716,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 2-5', '{"heading":120,"coords":{"x":1698.4752197265626,"y":3698.68017578125,"z":39.15148162841797},"doors":false,"maxDistance":2,"model":-1538617716,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 2-6', '{"heading":30,"coords":{"x":1698.35986328125,"y":3703.46240234375,"z":39.15148162841797},"doors":false,"maxDistance":2,"model":-495377267,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 1-1', '{"heading":30,"coords":{"x":1708.5318603515626,"y":3682.343505859375,"z":35.12274932861328},"doors":false,"maxDistance":2,"model":2094319813,"state":1}'),
    (DEFAULT, 'Sandy Shores Mechanic 1-2', '{"heading":30,"coords":{"x":1695.6029052734376,"y":3701.872314453125,"z":34.68849563598633},"doors":false,"maxDistance":2,"model":144666715,"state":1}');
```

</details>

***

<details>

<summary>🚀 Installation Guide</summary>

To install the Sandy Mechanic map on your FiveM server, follow these steps:

1. **Download the Map Resource**
   * Ensure the **prompt\_sandy\_mechanic** resource is downloaded and placed in your `resources` folder.
2. **Add the Resource to `server.cfg`**
   *   Add the following line to your `server.cfg` to ensure the map loads when your server starts:

       ```
       start prompt_sandy_mechanic
       ```
3. **Set Up Doorlocks**
   * Add the provided SQL lines to your database to configure the doorlock system.
4. **Install MapData**
   * For Sandy Area maps, ensure you have the correct MapData installed. Refer to the [MapData Documentation](sandy-mapdata.md) for detailed instructions.
5. **Test the Map**
   * Restart your server and visit the map at it's location to ensure everything is working correctly.

</details>

***

For further assistance, contact support. Enjoy using Sandy Mechanic on your FiveM server! 🚀
