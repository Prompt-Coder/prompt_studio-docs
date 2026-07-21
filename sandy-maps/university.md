# 🎒 University

{% embed url="https://store.prompt-mods.com/store/package/7304177" %}

The **Sandy Shores University** masterfully brings the true atmosphere of the American School. Check it out on our showcase server!

{% embed url="https://youtu.be/thj56sS0k00" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

#### Installation Instructions

{% stepper %}
{% step %}
### Step 1 - Add the resource

Place the `prompt_sandy_university` folder inside your `resources` directory.

<pre><code><strong>resources/prompt_sandy_university
</strong></code></pre>
{% endstep %}

{% step %}
### Step 2 - Add to your server.cfg

Insert the following line to ensure the map loads automatically:

<pre class="language-cfg"><code class="lang-cfg"><strong>start prompt_sandy_university
</strong></code></pre>
{% endstep %}

{% step %}
### Step 3 - Set up MapData

Make sure you have the correct **Sandy MapData** installed and started before this resource.
{% endstep %}

{% step %}
### Step 4 - Test the map

Restart your server and visit the **Sandy University** location.\
If the map and interiors load correctly, installation was successful ✅
{% endstep %}
{% endstepper %}

{% hint style="info" %}
🔔 Tip: Always restart your server after adding new resources — especially when adding multiple Sandy area maps.
{% endhint %}

***

:round\_pushpin:Location: `1536.65, 3659.73, 34.66`

***

<details>

<summary><strong>Interactive Props Names</strong></summary>

it\_ssi\_int\_studentchair

it\_ssi\_int\_conference\_chair

it\_ssi\_int\_lec\_chair

it\_ssi\_int\_caf\_table

it\_ssi\_int\_mesh\_4\_2

it\_ssi\_int\_awards

</details>

***

<details>

<summary><strong>Doorlock SQL</strong></summary>

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
	(DEFAULT, 'Sandy University E-1', '{"state":1,"coords":{"x":1518.2685546875,"y":3699.3740234375,"z":35.30481719970703},"doors":[{"model":971645943,"coords":{"x":1517.8197021484376,"y":3700.336669921875,"z":35.30481719970703},"heading":115},{"model":1945253201,"coords":{"x":1518.717529296875,"y":3698.41162109375,"z":35.30481719970703},"heading":295}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University E-2', '{"state":1,"coords":{"x":1534.96826171875,"y":3673.990234375,"z":35.30388259887695},"doors":[{"model":971645943,"coords":{"x":1534.0035400390626,"y":3673.540283203125,"z":35.30388259887695},"heading":205},{"model":1945253201,"coords":{"x":1535.9329833984376,"y":3674.43994140625,"z":35.30388259887695},"heading":25}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University E-3', '{"state":1,"coords":{"x":1531.4306640625,"y":3712.60009765625,"z":35.3204116821289},"doors":[{"model":971645943,"coords":{"x":1531.881103515625,"y":3711.63427734375,"z":35.3204116821289},"heading":295},{"model":1945253201,"coords":{"x":1530.9803466796876,"y":3713.56591796875,"z":35.3204116821289},"heading":115}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 1-1', '{"state":1,"coords":{"x":1528.69775390625,"y":3708.79150390625,"z":35.53086853027344},"doors":[{"model":-1203560041,"coords":{"x":1529.8759765625,"y":3709.341064453125,"z":35.53086853027344},"heading":205},{"model":-1203560041,"coords":{"x":1527.5196533203126,"y":3708.2421875,"z":35.53086853027344},"heading":25}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 1-2', '{"state":1,"coords":{"x":1520.845458984375,"y":3705.1298828125,"z":35.53086853027344},"doors":[{"model":-1203560041,"coords":{"x":1522.027099609375,"y":3705.680908203125,"z":35.53086853027344},"heading":205},{"model":-1203560041,"coords":{"x":1519.6636962890626,"y":3704.578857421875,"z":35.53086853027344},"heading":25}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 1-3', '{"state":1,"coords":{"x":1534.4810791015626,"y":3709.44482421875,"z":35.53057861328125},"doors":false,"maxDistance":2,"heading":295,"model":2102646650}'),
	(DEFAULT, 'Sandy University 1-4', '{"state":1,"coords":{"x":1529.90771484375,"y":3702.923583984375,"z":35.53610610961914},"doors":[{"model":-1203560041,"coords":{"x":1531.086181640625,"y":3703.47314453125,"z":35.53610610961914},"heading":205},{"model":-1203560041,"coords":{"x":1528.729248046875,"y":3702.3740234375,"z":35.53610610961914},"heading":25}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 1-5', '{"state":1,"coords":{"x":1533.5921630859376,"y":3702.732177734375,"z":35.52231979370117},"doors":false,"maxDistance":2,"heading":295,"model":2102646650}'),
	(DEFAULT, 'Sandy University 1-6', '{"state":1,"coords":{"x":1528.49462890625,"y":3694.111572265625,"z":35.54227066040039},"doors":false,"maxDistance":2,"heading":115,"model":-1203560041}'),
	(DEFAULT, 'Sandy University 1-7', '{"state":1,"coords":{"x":1529.8251953125,"y":3691.25830078125,"z":35.54227066040039},"doors":false,"maxDistance":2,"heading":115,"model":-1203560041}'),
	(DEFAULT, 'Sandy University 1-8', '{"state":1,"coords":{"x":1538.15234375,"y":3692.490966796875,"z":35.52783203125},"doors":[{"model":1099776443,"coords":{"x":1537.57177734375,"y":3693.736328125,"z":35.52783203125},"heading":295},{"model":1099776443,"coords":{"x":1538.7330322265626,"y":3691.24560546875,"z":35.52783203125},"heading":115}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 1-9', '{"state":1,"coords":{"x":1534.265625,"y":3680.404296875,"z":35.52493286132812},"doors":[{"model":1099776443,"coords":{"x":1534.8455810546876,"y":3679.160400390625,"z":35.52493286132812},"heading":115},{"model":1099776443,"coords":{"x":1533.685546875,"y":3681.648193359375,"z":35.52493286132812},"heading":295}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 1-10', '{"state":1,"coords":{"x":1543.6328125,"y":3680.75,"z":35.53333282470703},"doors":[{"model":1099776443,"coords":{"x":1544.2100830078126,"y":3679.511962890625,"z":35.53333282470703},"heading":115},{"model":1099776443,"coords":{"x":1543.0555419921876,"y":3681.988037109375,"z":35.53333282470703},"heading":295}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 2-1', '{"state":1,"coords":{"x":1544.1737060546876,"y":3681.7041015625,"z":39.6605339050293},"doors":false,"maxDistance":2,"heading":295,"model":2102646650}'),
	(DEFAULT, 'Sandy University 2-2', '{"state":1,"coords":{"x":1538.919677734375,"y":3692.8056640625,"z":39.65961074829101},"doors":[{"model":1099776443,"coords":{"x":1538.33984375,"y":3694.048828125,"z":39.65961074829101},"heading":295},{"model":1099776443,"coords":{"x":1539.4993896484376,"y":3691.562255859375,"z":39.65961074829101},"heading":115}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 2-3', '{"state":1,"coords":{"x":1534.86376953125,"y":3678.896484375,"z":39.66077423095703},"doors":false,"maxDistance":2,"heading":115,"model":2102646650}'),
	(DEFAULT, 'Sandy University 2-4', '{"state":1,"coords":{"x":1531.6260986328126,"y":3685.834716796875,"z":39.65943908691406},"doors":false,"maxDistance":2,"heading":115,"model":2102646650}'),
	(DEFAULT, 'Sandy University 2-5', '{"state":1,"coords":{"x":1528.5302734375,"y":3692.48681640625,"z":39.66086959838867},"doors":false,"maxDistance":2,"heading":115,"model":2102646650}'),
	(DEFAULT, 'Sandy University 2-6', '{"state":1,"coords":{"x":1532.1708984375,"y":3698.325439453125,"z":39.66520309448242},"doors":[{"model":-1203560041,"coords":{"x":1533.35009765625,"y":3698.875244140625,"z":39.66520309448242},"heading":205},{"model":-1203560041,"coords":{"x":1530.9915771484376,"y":3697.775634765625,"z":39.66520309448242},"heading":25}],"maxDistance":2}'),
	(DEFAULT, 'Sandy University 2-7', '{"state":1,"coords":{"x":1533.5806884765626,"y":3702.51611328125,"z":39.66360092163086},"doors":false,"maxDistance":2,"heading":295,"model":1099776443}'),
	(DEFAULT, 'Sandy University 2-8', '{"state":1,"coords":{"x":1534.5025634765626,"y":3709.481201171875,"z":39.66816711425781},"doors":false,"maxDistance":2,"heading":295,"model":1099776443}'),
	(DEFAULT, 'Sandy University 2-9', '{"state":1,"coords":{"x":1520.919921875,"y":3699.086181640625,"z":39.66449356079101},"doors":false,"maxDistance":2,"heading":205,"model":1099776443}');
```

</details>

***

#### Notes

* Fully compatible with other **Sandy Shores** maps and the MapData system.
* Optimized exterior and interior with minimal performance impact.

[![Join Discord](https://img.shields.io/badge/Join-Discord-5865F2?style=for-the-badge)](https://discord.gg/prompt)
