# ⛽ Sandy Illegal Garage & Gas Station with Carwash

## Sandy Illegal Garage & Gas Station with Carwash

{% embed url="https://fivem.prompt-mods.com/package/6254445" %}

The **Sandy Shores Illegal Garage** blends a car wash, gas station, and an underground hacker garage into a roleplay-ready crime front. Perfect for secret operations, casual stops, or police busts.

{% embed url="https://www.youtube.com/watch?v=rL9EzhSOs1o" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

#### 📍 Map Position

**2015.01, 3775.77, 32.72**

***

<details>

<summary>🚗 Features</summary>

* 🧼 Car Wash Interior
* ⛽ Gas Station Interior
* 🔧 Hidden Hacker Garage with underground vehicle storage
* 🏚️ Reworked Exterior seamlessly integrated

</details>

<details>

<summary>🎛️ Entity Sets</summary>

Use in Codewalker or script: `default`

</details>

<details>

<summary>🪑 Custom Props</summary>

`vw_prop_casino_chair_01a`, `prop_table_03_chr`, `v_res_tt_sofa`,\
`prop_bar_stool_01`, `prop_off_chair_04_s`, `v_ret_gc_chair03`,\
`ch_chint02_03_sofa`, `prop_tv_flat_michael`

</details>

<details>

<summary>🎯 Prop Animations (requires <code>ox_lib</code>)</summary>

```cfg
ensure ox_lib
```

Animations trigger by pressing **E** at custom interactable spots:

<figure><img src="https://2466319842-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FOrhcX4VMOZXgAwql2wKN%2Fuploads%2FAFDqGSN0CPSZuhrjrLtt%2Fimage.png?alt=media&#x26;token=f7250260-bfa6-4967-8cab-7372084eee7d" alt=""><figcaption><p>PRESS "E" looking at the garage door to activate animation</p></figcaption></figure>

<figure><img src="https://2466319842-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FOrhcX4VMOZXgAwql2wKN%2Fuploads%2F6BHxlZk3UYOXHrlBVGpj%2Fimage.png?alt=media&#x26;token=502f0c4d-1cbc-4108-9ce1-34d57b5ae1b9" alt=""><figcaption><p>PRESS "E" to use the carlift</p></figcaption></figure>

<figure><img src="https://2466319842-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FOrhcX4VMOZXgAwql2wKN%2Fuploads%2FerURNSCEWRGWz5ppfRdw%2Fimage.png?alt=media&#x26;token=3bbd09d4-efa9-48f8-80d1-5e111385aebf" alt=""><figcaption><p>PRESS "E" on the tire welding to open "SECRET UNDERGROUND GARAGE"</p></figcaption></figure>

<figure><img src="https://2466319842-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FOrhcX4VMOZXgAwql2wKN%2Fuploads%2FurI7OP0LUreejGjDMrk5%2Fimage.png?alt=media&#x26;token=a68eaae8-8363-45af-8e94-4d8e73e17f05" alt=""><figcaption><p>PRESS "E" to use the engine lift. (just for roleplay scenarios)</p></figcaption></figure>

<figure><img src="https://2466319842-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FOrhcX4VMOZXgAwql2wKN%2Fuploads%2FNrJjLFgTJdJkqTsKQaEa%2Fimage.png?alt=media&#x26;token=b5eeebb0-47e9-4142-bd16-2bfafe50e7fe" alt=""><figcaption><p>PRESS "E" to open secret door with weapons</p></figcaption></figure>

</details>

<details>

<summary><i class="fa-podcast" style="color:$primary;">:podcast:</i> Exports</summary>

#### Prop Names

Each prop has a unique `name` used as its identifier in all exports and events:

| Prop               | Name                            |
| ------------------ | ------------------------------- |
| Car Lift           | `prompt_sandy_is_lift`          |
| Garage Rollup Door | `prompt_sandy_is_garage_rollup` |
| Secret Floor Door  | `prompt_sandy_is_floorgate`     |
| Secret Wall Door   | `prompt_sandy_is_secret_door`   |
| Engine Hoist       | `prompt_sandy_is_engine_full`   |

#### Exports

`getLiftState`

Returns the current state of a prop.

```lua
-- Returns: true (open/up), false (closed/down), or nil (unknown)
local isUp = exports['prompt_sandy_illegal_garage']:getLiftState('prompt_sandy_is_lift')
```

`isLiftBusy`

Returns whether a prop is currently animating.

```lua
-- Returns: true if animating, false otherwise
local busy = exports['prompt_sandy_illegal_garage']:isLiftBusy('prompt_sandy_is_lift')
```

`setLiftState`

Programmatically control a prop's state. Triggers the animation and server sync.

````lua
-- state: true = open/up, false = close/down
exports['prompt_sandy_illegal_garage']:setLiftState('prompt_sandy_is_lift', true)
```<div data-gb-custom-block data-tag="hint" data-style='warning'>`setLiftState` does not check if the prop is busy. You should check `isLiftBusy` first to avoid overlapping animations.</div></div><div data-gb-custom-block data-tag="tab" data-title='Server'>#### getLiftState

Returns the current state of a prop from the server.

```lua
-- Returns: true (open/up), false (closed/down), or nil (unknown)
local isUp = exports['prompt_sandy_illegal_garage']:getLiftState('prompt_sandy_is_lift')
````

`isLiftBusy`

Returns whether a prop is currently animating.

````lua
-- Returns: true if animating, false otherwise
local busy = exports['prompt_sandy_illegal_garage']:isLiftBusy('prompt_sandy_is_lift')
```</div></div>### Events<div data-gb-custom-block data-tag="tabs"><div data-gb-custom-block data-tag="tab" data-title='Client'>#### liftStateChanged

Fires when a prop animation **starts**.

```lua
AddEventHandler('prompt_sandy_illegal_garage:liftStateChanged', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift")
    -- state: true = opening/going up, false = closing/going down
    print(propName .. ' is now ' .. (state and 'OPENING' or 'CLOSING'))
end)
````

`liftAnimationComplete`

Fires when a prop animation **finishes**.

````lua
AddEventHandler('prompt_sandy_illegal_garage:liftAnimationComplete', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift")
    -- state: true = now open/up, false = now closed/down
    print(propName .. ' animation complete, now ' .. (state and 'UP' or 'DOWN'))
end)
```</div><div data-gb-custom-block data-tag="tab" data-title='Server'>#### liftStateChanged

Fires when a prop's state is updated in GlobalState.

```lua
AddEventHandler('prompt_sandy_illegal_garage:liftStateChanged', function(propName, state)
    -- propName: string (e.g. "prompt_sandy_is_lift")
    -- state: true = open/up, false = closed/down
    print(propName .. ' state changed to ' .. (state and 'UP' or 'DOWN'))
end)
```</div></div>

### Full Example

```lua
-- Client-side: react to lift going up, then do something when animation finishes

AddEventHandler('prompt_sandy_illegal_garage:liftStateChanged', function(propName, state)
    if propName == 'prompt_sandy_is_lift' and state then
        print('Lift is going up!')
    end
end)

AddEventHandler('prompt_sandy_illegal_garage:liftAnimationComplete', function(propName, state)
    if propName == 'prompt_sandy_is_lift' and state then
        print('Lift is fully up, do something now')
    end
end)

-- Programmatically raise the lift (with busy check)
local busy = exports['prompt_sandy_illegal_garage']:isLiftBusy('prompt_sandy_is_lift')
local isUp = exports['prompt_sandy_illegal_garage']:getLiftState('prompt_sandy_is_lift')

if not busy and not isUp then
    exports['prompt_sandy_illegal_garage']:setLiftState('prompt_sandy_is_lift', true)
end
````

***

</details>

***



<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f6aa">🚪</span>Doorlock System</summary>

This map supports **ox\_doorlock**. Add the following SQL:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station E-1', '{"heading":32,"coords":{"x":2012.722900390625,"y":3791.4658203125,"z":32.87763214111328},"doors":false,"maxDistance":2,"model":-1793984540,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station E-2', '{"heading":0,"coords":{"x":2002.6920166015626,"y":3791.26904296875,"z":33.40999984741211},"doors":false,"maxDistance":2,"model":957340662,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station 2-1', '{"heading":300,"coords":{"x":1996.93115234375,"y":3783.171875,"z":35.30082321166992},"doors":false,"maxDistance":2,"model":747286790,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station 2-2', '{"heading":298,"coords":{"x":2000.0584716796876,"y":3782.98046875,"z":35.31220245361328},"doors":false,"maxDistance":2,"model":108110432,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station 0-1', '{"coords":{"x":1984.8240966796876,"y":3787.3486328125,"z":27.36436462402343},"doors":[{"coords":{"x":1984.34375,"y":3788.1806640625,"z":27.36436462402343},"heading":120,"model":1972289202},{"coords":{"x":1985.304443359375,"y":3786.516845703125,"z":27.36436462402343},"heading":300,"model":1972289202}],"maxDistance":2,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station 1-1', '{"heading":181,"coords":{"x":1988.239990234375,"y":3789.796630859375,"z":31.21485519409179},"doors":false,"maxDistance":2,"model":871083343,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station E-3', '{"heading":31,"coords":{"x":1982.0697021484376,"y":3767.3984375,"z":32.60374450683594},"doors":false,"maxDistance":2,"model":-1677161358,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station E-4', '{"heading":121,"coords":{"x":1983.0889892578126,"y":3774.855224609375,"z":32.62191772460937},"doors":false,"maxDistance":2,"model":-1677161358,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station E-5', '{"heading":31,"coords":{"x":1972.7923583984376,"y":3761.8232421875,"z":32.58348846435547},"doors":false,"maxDistance":2,"model":-1603870487,"state":1}'),
    (DEFAULT, 'Sandy Illegal Garage & Carwash & Gas Station E-6', '{"heading":211,"coords":{"x":1967.503173828125,"y":3766.66064453125,"z":32.58348846435547},"doors":false,"maxDistance":2,"model":-1603870487,"state":1}');
```

</details>

***

<details>

<summary>🚀 Installation Guide</summary>

1. Drop the folder: `prompt_sandy_illegal_garage` into your `resources`
2. `server.cfg`:

```cfg
start prompt_sandy_illegal_garage
```

3. Import the SQL
4. Install proper MapData – see MapData Docs
5. Restart and test in-game

</details>

***

Need help? Contact support and enjoy **Sandy Illegal Garage** on your FiveM server! 🚀
