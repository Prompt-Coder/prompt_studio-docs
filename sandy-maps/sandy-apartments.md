# 🏫 Sandy Apartments

## Sandy Apartments

{% embed url="https://portal.cfx.re/assets/granted-assets?page=1&sort=asset.updated_at&direction=asc&search=sandy+apartments&row=0" %}
**Official asset for FiveM — available on CFX Portal and Prompt’s Mods Store**
{% endembed %}

{% embed url="https://www.youtube.com/watch?v=JuNt5DSVGhU" fullWidth="false" %}

<details>

<summary><strong>Overview</strong></summary>

<br>

The **Sandy Shores Apartment Complex** is one of the largest projects we’ve created to date.

It features:

* **3 residential buildings**
* **33 fully walk-in apartments**
* **3 penthouses** with panoramic views of Sandy Shores and the Alamo Sea
* **Leasing office & lounge** with computers, TVs, and seating
* **Outdoor amenities** including a pool, basketball court, and dog park

Designed to support both **MLO-based housing** and **shell-based housing systems**.

</details>

***

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

### Installation Instructions

{% stepper %}
{% step %}
#### Download & Install

Download the resource from the [CFX Portal](https://portal.cfx.re/assets/granted-assets?page=1\&sort=asset.updated_at\&direction=asc\&search=sandy+apartments\&row=0).

Place the folder in your resources directory:

<pre><code><strong>resources/prompt_sandy_apts
</strong></code></pre>
{% endstep %}

{% step %}
#### Start the Resource

Add the following to your `server.cfg`:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_apts
</strong></code></pre>
{% endstep %}

{% step %}
#### Sandy MapData

This map **requires** [**Sandy Shores MapData**.](https://prompt-studio.gitbook.io/prompt-studio/~/revisions/BgF1SOhQTG7fLPorvSLl/sandy-maps/sandy-mapdata)\
Ensure it is installed and started before this resource.
{% endstep %}

{% step %}
#### Test In-Game

Restart your server and visit:

**1538.91, 3537.04, 36.91**

If everything loads correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

***

{% hint style="info" %}
💡 **Tip:** Always restart your server after installing or updating Sandy-area maps to avoid streaming conflicts.
{% endhint %}

***

### Additional Information

{% tabs %}
{% tab title="Interactive Props" %}
#### Available Props

| Category            | Prop Name                            |
| ------------------- | ------------------------------------ |
| 1 Bedroom Furniture | `prompt_sandy_apts_1bdr_wardrobe`    |
|                     | `prompt_sandy_apts_1bdr_sofa`        |
|                     | `prompt_sandy_apts_1bdr_chair`       |
| Penthouse Furniture | `prompt_sandy_apt_penth_sofa`        |
|                     | `prompt_sandy_apt_penth_chair`       |
| Penthouse Doors     | `prompt_sandy_apts_penth_door`       |
|                     | `prompt_sandy_apts_penth_door_white` |
|                     | `prompt_sandy_apts_penth_door_1bdr`  |

These props are suitable for targeting and housing system integration.
{% endtab %}

{% tab title="Shell Apartments (Optional)" %}
#### Shell Models

If you don’t want to use MLO interiors, shell apartments are included for housing systems.

| Shell Type | Model Name                    |
| ---------- | ----------------------------- |
| 1 Bedroom  | `prompt_sandy_apts_shell_1bd` |
| 2 Bedroom  | `prompt_sandy_apts_shell_2bd` |

* Shells can be spawned **anywhere**
* Compatible with most housing systems
* If you want the buildings to be **non-enterable** (recommended when using shells), follow: [**Disable MLO Interiors**](https://app.gitbook.com/o/vla1OiEqNwIHvUGOxnbv/s/OrhcX4VMOZXgAwql2wKN/~/edit/~/changes/92/sandy-maps/sandy-apartments#disable-mlo-interiors)
{% endtab %}

{% tab title="Disable MLO Interiors" %}
#### Non-Interior Version

If you want the buildings to be **non-enterable** and use only shells:

1. Copy files from the current folder
2.  Paste them into:

    ```
    prompt_sandy_apts/stream/replace_if_no_ints
    ```
3. Open `config.lua`
4.  Change:

    ```lua
    Config.ProximityEnabled = true
    ```

    to:

    ```lua
    Config.ProximityEnabled = false
    ```
5. Done ✅
{% endtab %}

{% tab title="Doorlock SQL" %}
####

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	-- Sandy Apartments 1
	(DEFAULT, 'Sandy Apartments 1 E-1', '{"doors":[{"heading":120,"model":-59888285,"coords":{"x":1593.9630126953126,"y":3589.519287109375,"z":35.8808708190918}},{"heading":300,"model":675794718,"coords":{"x":1595.2784423828126,"y":3587.239990234375,"z":35.8808708190918}}],"maxDistance":2,"coords":{"x":1594.6207275390626,"y":3588.379638671875,"z":35.8808708190918},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 E-2', '{"doors":[{"heading":210,"model":-59888285,"coords":{"x":1597.3043212890626,"y":3586.5859375,"z":35.8808708190918}},{"heading":30,"model":675794718,"coords":{"x":1599.5833740234376,"y":3587.9013671875,"z":35.8808708190918}}],"maxDistance":2,"coords":{"x":1598.44384765625,"y":3587.24365234375,"z":35.8808708190918},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 E-3', '{"doors":false,"maxDistance":2,"heading":30,"model":-59888285,"coords":{"x":1577.5062255859376,"y":3633.78369140625,"z":35.8808708190918},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 E-4', '{"doors":[{"heading":300,"model":675794718,"coords":{"x":1595.2369384765626,"y":3587.216064453125,"z":42.38113021850586}},{"heading":120,"model":-59888285,"coords":{"x":1593.9215087890626,"y":3589.495361328125,"z":42.38113021850586}}],"maxDistance":2,"coords":{"x":1594.5792236328126,"y":3588.355712890625,"z":42.38113021850586},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 E-5', '{"doors":[{"heading":30,"model":675794718,"coords":{"x":1599.76220703125,"y":3587.591552734375,"z":42.39113235473633}},{"heading":210,"model":-59888285,"coords":{"x":1597.483154296875,"y":3586.2763671875,"z":42.39113235473633}}],"maxDistance":2,"coords":{"x":1598.6226806640626,"y":3586.93408203125,"z":42.39113235473633},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 E-6', '{"doors":[{"heading":300,"model":1564423487,"coords":{"x":1597.68212890625,"y":3603.1796875,"z":50.69764709472656}},{"heading":120,"model":1564423487,"coords":{"x":1596.46337890625,"y":3605.290771484375,"z":50.69764709472656}}],"maxDistance":2,"coords":{"x":1597.07275390625,"y":3604.2353515625,"z":50.69764709472656},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1602.3369140625,"y":3594.429443359375,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-2', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1604.552734375,"y":3599.568603515625,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-3', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1609.19384765625,"y":3604.51123046875,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-4', '{"doors":false,"maxDistance":2,"heading":210,"coords":{"x":1609.674072265625,"y":3608.14111328125,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-5', '{"doors":false,"maxDistance":2,"heading":120,"coords":{"x":1611.90576171875,"y":3606.076904296875,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-6', '{"doors":[{"heading":300,"model":-751846545,"coords":{"x":1594.8172607421876,"y":3599.94091796875,"z":34.69391632080078}},{"heading":120,"model":-751846545,"coords":{"x":1594.0638427734376,"y":3601.245849609375,"z":34.69391632080078}}],"maxDistance":2,"coords":{"x":1594.4405517578126,"y":3600.59326171875,"z":34.69391632080078},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 1 1-7', '{"doors":[{"heading":300,"model":-751846545,"coords":{"x":1593.3690185546876,"y":3602.44921875,"z":34.69391632080078}},{"heading":120,"model":-751846545,"coords":{"x":1592.6156005859376,"y":3603.754150390625,"z":34.69391632080078}}],"maxDistance":2,"coords":{"x":1592.9923095703126,"y":3603.1015625,"z":34.69391632080078},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 1 1-8', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1591.8201904296876,"y":3612.64501953125,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-9', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1594.0360107421876,"y":3617.7841796875,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-10', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1598.6771240234376,"y":3622.726806640625,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-11', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1599.1573486328126,"y":3626.356689453125,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-12', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1601.3890380859376,"y":3624.29248046875,"z":35.8819694519043},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-13', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1585.40087890625,"y":3616.381103515625,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-14', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1578.356201171875,"y":3607.168212890625,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-15', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1573.803466796875,"y":3606.18994140625,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-16', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1583.583984375,"y":3626.94482421875,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-17', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1590.628662109375,"y":3636.15771484375,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-18', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1595.181396484375,"y":3637.135986328125,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-19', '{"doors":false,"maxDistance":2,"heading":120,"coords":{"x":1580.6297607421876,"y":3624.645263671875,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-20', '{"doors":false,"maxDistance":2,"heading":30,"coords":{"x":1568.467529296875,"y":3624.295654296875,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 1-21', '{"doors":false,"maxDistance":2,"heading":30,"coords":{"x":1565.338134765625,"y":3620.852294921875,"z":35.88267135620117},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1580.6297607421876,"y":3624.645263671875,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-2', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1568.467529296875,"y":3624.295654296875,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-3', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1565.338134765625,"y":3620.852294921875,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-4', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1583.583984375,"y":3626.94482421875,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-5', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1590.628662109375,"y":3636.15771484375,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-6', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1595.181396484375,"y":3637.135986328125,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-7', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1585.40087890625,"y":3616.381103515625,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-8', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1578.356201171875,"y":3607.168212890625,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-9', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1573.803466796875,"y":3606.18994140625,"z":42.38513565063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-10', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1591.8201904296876,"y":3612.64501953125,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-11', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1594.0360107421876,"y":3617.7841796875,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-12', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1598.6771240234376,"y":3622.726806640625,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-13', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1599.1573486328126,"y":3626.356689453125,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-14', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1601.3890380859376,"y":3624.29248046875,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-15', '{"doors":[{"heading":120,"model":-751846545,"coords":{"x":1592.6156005859376,"y":3603.754150390625,"z":41.19342803955078}},{"heading":300,"model":-751846545,"coords":{"x":1593.3690185546876,"y":3602.44921875,"z":41.19342803955078}}],"maxDistance":2,"coords":{"x":1592.9923095703126,"y":3603.1015625,"z":41.19342803955078},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 1 2-16', '{"doors":[{"heading":120,"model":-751846545,"coords":{"x":1594.0638427734376,"y":3601.245849609375,"z":41.19342803955078}},{"heading":300,"model":-751846545,"coords":{"x":1594.8172607421876,"y":3599.94091796875,"z":41.19342803955078}}],"maxDistance":2,"coords":{"x":1594.4405517578126,"y":3600.59326171875,"z":41.19342803955078},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 1 2-17', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1602.3369140625,"y":3594.429443359375,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-18', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1604.552734375,"y":3599.568603515625,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-19', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1609.19384765625,"y":3604.51123046875,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-20', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1609.674072265625,"y":3608.14111328125,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 2-21', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1611.90576171875,"y":3606.076904296875,"z":42.38226318359375},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 3-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-380256440,"coords":{"x":1600.59375,"y":3589.970947265625,"z":44.65471649169922},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 1 3-2', '{"doors":[{"heading":210,"model":-59888285,"coords":{"x":1602.1171875,"y":3588.7392578125,"z":45.83112716674805}},{"heading":30,"model":675794718,"coords":{"x":1604.3963623046876,"y":3590.0546875,"z":45.83112716674805}}],"maxDistance":2,"coords":{"x":1603.2568359375,"y":3589.39697265625,"z":45.83112716674805},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-380256440,"coords":{"x":1600.59375,"y":3589.970947265625,"z":49.53977584838867},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 1 4-2', '{"doors":false,"maxDistance":2,"heading":210,"model":181177192,"coords":{"x":1603.279052734375,"y":3598.02197265625,"z":50.70823669433594},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-3', '{"doors":false,"maxDistance":2,"heading":300,"model":-1826371819,"coords":{"x":1597.0133056640626,"y":3622.6650390625,"z":50.63784790039062},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-4', '{"doors":false,"maxDistance":2,"heading":210,"model":-1826371819,"coords":{"x":1595.5367431640626,"y":3623.2626953125,"z":50.63784790039062},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-5', '{"doors":false,"maxDistance":2,"heading":210,"model":-1826371819,"coords":{"x":1592.9840087890626,"y":3621.788818359375,"z":50.63784790039062},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-6', '{"doors":false,"maxDistance":2,"heading":210,"model":-1826371819,"coords":{"x":1584.66845703125,"y":3621.714599609375,"z":50.63784790039062},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-7', '{"doors":false,"maxDistance":2,"heading":210,"model":-1826371819,"coords":{"x":1581.351318359375,"y":3619.796875,"z":50.63784790039062},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-8', '{"doors":false,"maxDistance":2,"heading":300,"model":-1826371819,"coords":{"x":1575.858154296875,"y":3615.5361328125,"z":50.63784790039062},"state":1}'),
	(DEFAULT, 'Sandy Apartments 1 4-9', '{"doors":false,"maxDistance":2,"heading":300,"model":-1826371819,"coords":{"x":1577.3216552734376,"y":3613.001220703125,"z":50.63784790039062},"state":1}'),

	-- Sandy Apartments 2
	(DEFAULT, 'Sandy Apartments 2 E-1', '{"doors":[{"heading":210,"model":675794718,"coords":{"x":1615.8070068359376,"y":3553.990478515625,"z":35.8530387878418}},{"heading":30,"model":-59888285,"coords":{"x":1618.085693359375,"y":3555.30615234375,"z":35.8530387878418}}],"maxDistance":2,"coords":{"x":1616.9462890625,"y":3554.6484375,"z":35.8530387878418},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 E-2', '{"doors":[{"heading":300,"model":675794718,"coords":{"x":1616.677734375,"y":3549.62744140625,"z":35.8530387878418}},{"heading":120,"model":-59888285,"coords":{"x":1615.383544921875,"y":3551.9189453125,"z":35.8530387878418}}],"maxDistance":2,"coords":{"x":1616.0306396484376,"y":3550.773193359375,"z":35.8530387878418},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 E-3', '{"doors":false,"maxDistance":2,"heading":30,"model":-59888285,"coords":{"x":1647.352783203125,"y":3513.573974609375,"z":35.8530387878418},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 E-4', '{"doors":[{"heading":120,"model":-59888285,"coords":{"x":1615.32080078125,"y":3551.8828125,"z":42.35329818725586}},{"heading":300,"model":675794718,"coords":{"x":1616.63623046875,"y":3549.603515625,"z":42.35329818725586}}],"maxDistance":2,"coords":{"x":1615.978515625,"y":3550.7431640625,"z":42.35329818725586},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 E-5', '{"doors":[{"heading":30,"model":-59888285,"coords":{"x":1617.906982421875,"y":3555.6162109375,"z":42.36330032348633}},{"heading":210,"model":675794718,"coords":{"x":1615.628173828125,"y":3554.300048828125,"z":42.36330032348633}}],"maxDistance":2,"coords":{"x":1616.767578125,"y":3554.9580078125,"z":42.36330032348633},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 E-6', '{"doors":[{"heading":120,"model":1564423487,"coords":{"x":1630.3651123046876,"y":3546.06103515625,"z":50.67341232299805}},{"heading":300,"model":1564423487,"coords":{"x":1631.5838623046876,"y":3543.949951171875,"z":50.67341232299805}}],"maxDistance":2,"coords":{"x":1630.9744873046876,"y":3545.00537109375,"z":50.67341232299805},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-1', '{"doors":false,"heading":120,"coords":{"x":1641.10888671875,"y":3519.34033203125,"z":35.86264038085937},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-2', '{"doors":false,"heading":30,"coords":{"x":1634.064208984375,"y":3510.12744140625,"z":35.86264038085937},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-3', '{"doors":false,"heading":30,"coords":{"x":1629.511474609375,"y":3509.149169921875,"z":35.86264038085937},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-4', '{"doors":false,"heading":300,"coords":{"x":1643.2567138671876,"y":3523.089111328125,"z":35.86125946044922},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-5', '{"doors":false,"heading":210,"coords":{"x":1655.4189453125,"y":3523.438720703125,"z":35.86125946044922},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-6', '{"doors":false,"heading":210,"coords":{"x":1658.54833984375,"y":3526.882080078125,"z":35.86125946044922},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-7', '{"doors":false,"heading":120,"coords":{"x":1636.31494140625,"y":3527.64404296875,"z":35.86264038085937},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-8', '{"doors":false,"heading":30,"coords":{"x":1624.1527099609376,"y":3527.29443359375,"z":35.86264038085937},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-9', '{"doors":false,"heading":30,"coords":{"x":1621.0233154296876,"y":3523.85107421875,"z":35.86264038085937},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-10', '{"doors":false,"heading":300,"coords":{"x":1635.6519775390626,"y":3536.2275390625,"z":35.85602188110351},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-11', '{"doors":false,"heading":210,"coords":{"x":1641.2008056640626,"y":3535.572509765625,"z":35.85602188110351},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-12', '{"doors":false,"heading":300,"coords":{"x":1650.51025390625,"y":3538.68359375,"z":35.85602188110351},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-13', '{"doors":false,"heading":210,"coords":{"x":1651.1854248046876,"y":3535.72119140625,"z":35.85602188110351},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-14', '{"doors":false,"heading":300,"coords":{"x":1647.8016357421876,"y":3537.118408203125,"z":35.85602188110351},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-15', '{"doors":[{"coords":{"x":1628.3316650390626,"y":3541.34619140625,"z":34.66608428955078},"heading":300,"model":-751846545},{"coords":{"x":1627.5782470703126,"y":3542.651123046875,"z":34.66608428955078},"heading":120,"model":-751846545}],"coords":{"x":1627.9549560546876,"y":3541.99853515625,"z":34.66608428955078},"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-16', '{"doors":[{"coords":{"x":1626.1300048828126,"y":3545.159423828125,"z":34.66608428955078},"heading":120,"model":-751846545},{"coords":{"x":1626.8834228515626,"y":3543.8544921875,"z":34.66608428955078},"heading":300,"model":-751846545}],"coords":{"x":1626.5067138671876,"y":3544.5068359375,"z":34.66608428955078},"auto":true,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-17', '{"doors":false,"heading":300,"coords":{"x":1625.1348876953126,"y":3554.44384765625,"z":35.85869598388672},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-18', '{"doors":false,"heading":210,"coords":{"x":1630.6837158203126,"y":3553.788818359375,"z":35.85869598388672},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-19', '{"doors":false,"heading":300,"coords":{"x":1639.9931640625,"y":3556.89990234375,"z":35.85869598388672},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-20', '{"doors":false,"heading":210,"coords":{"x":1640.6683349609376,"y":3553.9375,"z":35.85869598388672},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 1-21', '{"doors":false,"heading":300,"coords":{"x":1637.2845458984376,"y":3555.334716796875,"z":35.85869598388672},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-1', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1643.2567138671876,"y":3523.089111328125,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-2', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1655.4189453125,"y":3523.438720703125,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-3', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1658.54833984375,"y":3526.882080078125,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-4', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1641.09130859375,"y":3519.37060546875,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-5', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1634.046630859375,"y":3510.15771484375,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-6', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1629.493896484375,"y":3509.179443359375,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-7', '{"doors":false,"maxDistance":2,"heading":120,"model":-1364787410,"coords":{"x":1636.3175048828126,"y":3527.639404296875,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-8', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1624.1552734375,"y":3527.289794921875,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-9', '{"doors":false,"maxDistance":2,"heading":30,"model":-1364787410,"coords":{"x":1621.02587890625,"y":3523.846435546875,"z":42.35756683349609},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-10', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1635.6519775390626,"y":3536.2275390625,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-11', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1641.2008056640626,"y":3535.572509765625,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-12', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1650.51025390625,"y":3538.68359375,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-13', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1651.1854248046876,"y":3535.72119140625,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-14', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1647.8016357421876,"y":3537.118408203125,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-15', '{"doors":[{"heading":120,"model":-751846545,"coords":{"x":1627.5782470703126,"y":3542.651123046875,"z":41.16559982299805}},{"heading":300,"model":-751846545,"coords":{"x":1628.3316650390626,"y":3541.34619140625,"z":41.16559982299805}}],"maxDistance":2,"coords":{"x":1627.9549560546876,"y":3541.99853515625,"z":41.16559982299805},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 2 2-16', '{"doors":[{"heading":120,"model":-751846545,"coords":{"x":1626.1300048828126,"y":3545.159423828125,"z":41.16559982299805}},{"heading":300,"model":-751846545,"coords":{"x":1626.8834228515626,"y":3543.8544921875,"z":41.16559982299805}}],"maxDistance":2,"coords":{"x":1626.5067138671876,"y":3544.5068359375,"z":41.16559982299805},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 2 2-17', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1625.1348876953126,"y":3554.44384765625,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-18', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1630.6837158203126,"y":3553.788818359375,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-19', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1639.9931640625,"y":3556.89990234375,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-20', '{"doors":false,"maxDistance":2,"heading":210,"model":-1364787410,"coords":{"x":1640.6683349609376,"y":3553.9375,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 2-21', '{"doors":false,"maxDistance":2,"heading":300,"model":-1364787410,"coords":{"x":1637.2845458984376,"y":3555.334716796875,"z":42.35584259033203},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 3-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-380256440,"coords":{"x":1619.6031494140626,"y":3556.436279296875,"z":44.62981414794922},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 2 3-2', '{"doors":[{"heading":30,"model":-59888285,"coords":{"x":1622.3570556640626,"y":3558.397705078125,"z":45.80329513549805}},{"heading":210,"model":675794718,"coords":{"x":1620.078369140625,"y":3557.081787109375,"z":45.80329513549805}}],"maxDistance":2,"coords":{"x":1621.2177734375,"y":3557.73974609375,"z":45.80329513549805},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-380256440,"coords":{"x":1619.6031494140626,"y":3556.436279296875,"z":49.51194381713867},"state":1,"auto":true}'),
	(DEFAULT, 'Sandy Apartments 2 4-2', '{"doors":false,"maxDistance":2,"heading":30,"model":181177192,"coords":{"x":1627.571533203125,"y":3552.838134765625,"z":50.69376754760742},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-3', '{"doors":false,"maxDistance":2,"heading":300,"model":-1826371819,"coords":{"x":1646.2467041015626,"y":3536.856689453125,"z":50.61560440063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-4', '{"doors":false,"maxDistance":2,"heading":30,"model":-1826371819,"coords":{"x":1645.558837890625,"y":3533.509521484375,"z":50.61560440063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-5', '{"doors":false,"maxDistance":2,"heading":30,"model":-1826371819,"coords":{"x":1643.0047607421876,"y":3532.034912109375,"z":50.61560440063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-6', '{"doors":false,"maxDistance":2,"heading":30,"model":-1826371819,"coords":{"x":1638.7823486328126,"y":3524.86767578125,"z":50.61560440063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-7', '{"doors":false,"maxDistance":2,"heading":30,"model":-1826371819,"coords":{"x":1635.4659423828126,"y":3522.953125,"z":50.61560440063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-8', '{"doors":false,"maxDistance":2,"heading":300,"model":-1826371819,"coords":{"x":1629.5029296875,"y":3522.105224609375,"z":50.61560440063476},"state":1}'),
	(DEFAULT, 'Sandy Apartments 2 4-9', '{"doors":false,"maxDistance":2,"heading":300,"model":-1826371819,"coords":{"x":1628.0384521484376,"y":3524.641845703125,"z":50.61560440063476},"state":1}'),

	-- Sandy Apartments 3
	(DEFAULT, 'Sandy Apartments 3 G-1', '{"doors":false,"heading":210,"coords":{"x":1585.2542724609376,"y":3514.168212890625,"z":34.72126770019531},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-2', '{"doors":false,"heading":210,"coords":{"x":1580.9488525390626,"y":3511.682373046875,"z":34.72126770019531},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-3', '{"doors":false,"heading":210,"coords":{"x":1576.6148681640626,"y":3509.18017578125,"z":34.72126770019531},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-4', '{"doors":false,"heading":210,"coords":{"x":1572.247802734375,"y":3506.65869140625,"z":34.72126770019531},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-5', '{"doors":false,"heading":120,"coords":{"x":1563.9014892578126,"y":3505.54833984375,"z":34.7580337524414},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-6', '{"doors":false,"heading":120,"coords":{"x":1561.4119873046876,"y":3509.8515625,"z":34.7580337524414},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-7', '{"doors":false,"heading":120,"coords":{"x":1558.906005859375,"y":3514.183349609375,"z":34.7580337524414},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-8', '{"doors":false,"heading":120,"coords":{"x":1556.380859375,"y":3518.54833984375,"z":34.7580337524414},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-9', '{"doors":false,"heading":30,"coords":{"x":1534.41455078125,"y":3568.63525390625,"z":34.77474975585937},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-10', '{"doors":false,"heading":30,"coords":{"x":1538.72216796875,"y":3571.117431640625,"z":34.77474975585937},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-11', '{"doors":false,"heading":30,"coords":{"x":1543.058349609375,"y":3573.61572265625,"z":34.77474975585937},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 G-12', '{"doors":false,"heading":30,"coords":{"x":1547.4276123046876,"y":3576.13330078125,"z":34.77474975585937},"auto":true,"model":331305963,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 E-1', '{"doors":false,"heading":30,"coords":{"x":1538.9222412109376,"y":3534.244873046875,"z":36.0062141418457},"model":-725970636,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 E-2', '{"doors":false,"heading":210,"coords":{"x":1537.6490478515626,"y":3538.8916015625,"z":36.00609970092773},"model":-725970636,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 3 1-1', '{"doors":false,"heading":120,"coords":{"x":1539.6064453125,"y":3547.05712890625,"z":35.9373664855957},"model":825720073,"maxDistance":2,"state":1}'),

	-- Sandy Apartments 4
	(DEFAULT, 'Sandy Apartments 4 E-1', '{"doors":false,"heading":11,"coords":{"x":1409.7884521484376,"y":3572.95458984375,"z":35.7137565612793},"model":-59888285,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 E-2', '{"doors":[{"coords":{"x":1410.661865234375,"y":3525.623046875,"z":35.7137565612793},"heading":101,"model":-59888285},{"coords":{"x":1411.1837158203126,"y":3523.0439453125,"z":35.7137565612793},"heading":281,"model":675794718}],"coords":{"x":1410.9228515625,"y":3524.33349609375,"z":35.7137565612793},"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 E-3', '{"doors":[{"coords":{"x":1412.896240234375,"y":3521.779052734375,"z":35.7137565612793},"heading":191,"model":-59888285},{"coords":{"x":1415.475341796875,"y":3522.30078125,"z":35.7137565612793},"heading":11,"model":675794718}],"coords":{"x":1414.185791015625,"y":3522.0400390625,"z":35.7137565612793},"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 E-4', '{"doors":[{"coords":{"x":1410.6148681640626,"y":3525.613525390625,"z":42.21401596069336},"heading":101,"model":-59888285},{"coords":{"x":1411.1368408203126,"y":3523.034423828125,"z":42.21401596069336},"heading":281,"model":675794718}],"coords":{"x":1410.8758544921876,"y":3524.323974609375,"z":42.21401596069336},"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 E-5', '{"doors":[{"coords":{"x":1412.96728515625,"y":3521.428466796875,"z":42.22401809692383},"heading":191,"model":-59888285},{"coords":{"x":1415.5462646484376,"y":3521.950439453125,"z":42.22401809692383},"heading":11,"model":675794718}],"coords":{"x":1414.2568359375,"y":3521.689453125,"z":42.22401809692383},"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 E-6', '{"doors":[{"coords":{"x":1420.7232666015626,"y":3522.81103515625,"z":45.66401290893555},"heading":11,"model":675794718},{"coords":{"x":1418.1441650390626,"y":3522.2890625,"z":45.66401290893555},"heading":191,"model":-59888285}],"coords":{"x":1419.4337158203126,"y":3522.550048828125,"z":45.66401290893555},"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 E-7', '{"doors":[{"coords":{"x":1418.0733642578126,"y":3539.75390625,"z":50.5522346496582},"heading":101,"model":1564423487},{"coords":{"x":1418.55712890625,"y":3537.36474609375,"z":50.5522346496582},"heading":281,"model":1564423487}],"coords":{"x":1418.315185546875,"y":3538.559326171875,"z":50.5522346496582},"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-1', '{"doors":false,"heading":101,"coords":{"x":1420.1627197265626,"y":3527.61376953125,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-2', '{"doors":false,"heading":191,"coords":{"x":1423.8985595703126,"y":3531.781005859375,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-3', '{"doors":false,"heading":101,"coords":{"x":1429.87109375,"y":3534.990234375,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-4', '{"doors":false,"heading":191,"coords":{"x":1431.4810791015626,"y":3538.2783203125,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-5', '{"doors":false,"heading":101,"coords":{"x":1432.940185546875,"y":3535.61181640625,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-6', '{"doors":[{"coords":{"x":1414.48828125,"y":3536.708251953125,"z":34.52680206298828},"heading":101,"model":-751846545},{"coords":{"x":1414.787353515625,"y":3535.2314453125,"z":34.52680206298828},"heading":281,"model":-751846545}],"coords":{"x":1414.6378173828126,"y":3535.9697265625,"z":34.52680206298828},"auto":true,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-7', '{"doors":[{"coords":{"x":1413.9134521484376,"y":3539.547119140625,"z":34.52680206298828},"heading":101,"model":-751846545},{"coords":{"x":1414.2125244140626,"y":3538.070068359375,"z":34.52680206298828},"heading":281,"model":-751846545}],"coords":{"x":1414.06298828125,"y":3538.80859375,"z":34.52680206298828},"auto":true,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-8', '{"doors":false,"heading":101,"coords":{"x":1415.98681640625,"y":3548.23486328125,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-9', '{"doors":false,"heading":191,"coords":{"x":1419.72265625,"y":3552.402099609375,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-10', '{"doors":false,"heading":101,"coords":{"x":1425.6951904296876,"y":3555.611328125,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-11', '{"doors":false,"heading":191,"coords":{"x":1427.30517578125,"y":3558.8994140625,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-12', '{"doors":false,"heading":101,"coords":{"x":1428.7642822265626,"y":3556.23291015625,"z":35.69096755981445},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-13', '{"doors":false,"heading":101,"coords":{"x":1411.0928955078126,"y":3553.80615234375,"z":35.71967315673828},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-14', '{"doors":false,"heading":11,"coords":{"x":1399.4515380859376,"y":3557.344482421875,"z":35.71967315673828},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-15', '{"doors":false,"heading":11,"coords":{"x":1395.38916015625,"y":3555.075439453125,"z":35.71967315673828},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-16', '{"doors":false,"heading":281,"coords":{"x":1412.729736328125,"y":3564.40576171875,"z":35.71781158447265},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-17', '{"doors":false,"heading":191,"coords":{"x":1422.3394775390626,"y":3570.89892578125,"z":35.71781158447265},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-18', '{"doors":false,"heading":191,"coords":{"x":1426.9669189453126,"y":3570.3779296875,"z":35.71781158447265},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-19', '{"doors":false,"heading":101,"coords":{"x":1409.1973876953126,"y":3563.166015625,"z":35.71967315673828},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-20', '{"doors":false,"heading":11,"coords":{"x":1393.49365234375,"y":3564.435302734375,"z":35.71967315673828},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 1-21', '{"doors":false,"heading":11,"coords":{"x":1397.5560302734376,"y":3566.704345703125,"z":35.71967315673828},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-1', '{"doors":false,"maxDistance":2,"heading":281,"coords":{"x":1412.7296142578126,"y":3564.406005859375,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-2', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1422.3394775390626,"y":3570.89892578125,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-3', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1426.9669189453126,"y":3570.377685546875,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-4', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1409.19677734375,"y":3563.168701171875,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-5', '{"doors":false,"maxDistance":2,"heading":11,"coords":{"x":1397.555419921875,"y":3566.70703125,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-6', '{"doors":false,"maxDistance":2,"heading":11,"coords":{"x":1393.4930419921876,"y":3564.43798828125,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-7', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1411.0926513671876,"y":3553.806640625,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-8', '{"doors":false,"maxDistance":2,"heading":11,"coords":{"x":1401.482666015625,"y":3547.313720703125,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-9', '{"doors":false,"maxDistance":2,"heading":11,"coords":{"x":1396.8553466796876,"y":3547.8349609375,"z":42.21802139282226},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-10', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1415.98828125,"y":3548.228515625,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-11', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1419.72412109375,"y":3552.395751953125,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-12', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1425.6964111328126,"y":3555.605224609375,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-13', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1427.3062744140626,"y":3558.8935546875,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-14', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1428.7655029296876,"y":3556.226806640625,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-15', '{"doors":[{"coords":{"x":1413.9134521484376,"y":3539.547119140625,"z":41.02631378173828},"heading":101,"model":-751846545},{"coords":{"x":1414.2125244140626,"y":3538.070068359375,"z":41.02631378173828},"heading":281,"model":-751846545}],"coords":{"x":1414.06298828125,"y":3538.80859375,"z":41.02631378173828},"auto":true,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-16', '{"doors":[{"coords":{"x":1414.48828125,"y":3536.708251953125,"z":41.02631378173828},"heading":101,"model":-751846545},{"coords":{"x":1414.787353515625,"y":3535.2314453125,"z":41.02631378173828},"heading":281,"model":-751846545}],"coords":{"x":1414.6378173828126,"y":3535.9697265625,"z":41.02631378173828},"auto":true,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-17', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1420.1627197265626,"y":3527.61376953125,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-18', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1423.8985595703126,"y":3531.781005859375,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-19', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1429.87109375,"y":3534.990234375,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-20', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1431.4810791015626,"y":3538.2783203125,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 2-21', '{"doors":false,"maxDistance":2,"heading":101,"coords":{"x":1432.940185546875,"y":3535.61181640625,"z":42.21514892578125},"model":-1364787410,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 3-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-380256440,"coords":{"x":1417.0916748046876,"y":3523.94140625,"z":44.48760223388672},"auto":true,"model":-380256440,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-1', '{"doors":false,"maxDistance":2,"heading":120,"model":-380256440,"coords":{"x":1417.0916748046876,"y":3523.94140625,"z":49.37266159057617},"auto":true,"model":-380256440,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-2', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1422.2222900390626,"y":3530.6943359375,"z":50.56282424926758},"model":181177192,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-3', '{"doors":false,"maxDistance":2,"heading":281,"coords":{"x":1424.1226806640626,"y":3556.05029296875,"z":50.49243545532226},"model":-1826371819,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-4', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1422.9129638671876,"y":3557.086669921875,"z":50.49243545532226},"model":-1826371819,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-5', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1420.0240478515626,"y":3556.501708984375,"z":50.49243545532226},"model":-1826371819,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-6', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1412.116943359375,"y":3559.0771484375,"z":50.49243545532226},"model":-1826371819,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-7', '{"doors":false,"maxDistance":2,"heading":191,"coords":{"x":1408.36181640625,"y":3558.314453125,"z":50.49243545532226},"model":-1826371819,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-8', '{"doors":false,"maxDistance":2,"heading":281,"coords":{"x":1401.798583984375,"y":3556.023193359375,"z":50.49243545532226},"model":-1826371819,"maxDistance":2,"state":1}'),
	(DEFAULT, 'Sandy Apartments 4 4-9', '{"doors":false,"maxDistance":2,"heading":281,"coords":{"x":1402.3795166015626,"y":3553.154296875,"z":50.49243545532226},"model":-1826371819,"maxDistance":2,"state":1}');
```
{% endtab %}
{% endtabs %}

***

### Notes

* Fully compatible with other **Sandy Shores** maps
* Supports both **MLO** and **shell-based** housing setups
* Optimized for large residential roleplay environments

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/rKbHHdfZFU)
