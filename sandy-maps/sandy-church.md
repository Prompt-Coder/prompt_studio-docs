# ⛪ Sandy Church

{% embed url="https://fivem.prompt-mods.com/package/6254445" %}

The **Sandy Church** is a peaceful, ambient map for FiveM servers. Designed for versatility, it supports ceremonies, religious services, casual gatherings, and even hidden crime setups thanks to a secret root cellar and graveyard.

Preconfigured entity set script by `motrion`:\
[https://github.com/motrion/sandy-church-script](https://github.com/motrion/sandy-church-script)

{% embed url="https://www.youtube.com/watch?v=e65JFRwvC2Q" %}

{% hint style="info" icon="gear" %}
Supports **EXTERIOR ONLY** Mode: [exterior-only-add-on.md](exterior-only-add-on.md "mention")
{% endhint %}

***

#### 📍 Map Position

**1767.54, 3891.87, 36.64**

***

<details>

<summary>✨ Areas Included</summary>

* ⛪ Main Church Interior
* 🪦 Atmospheric Graveyard
* 🌿 Relaxing Backyard
* 🧱 Root Cellar (underground access)

</details>

<details>

<summary>🎛️ Entity Sets</summary>

Use in script or Codewalker:

* `church_funeral`
* `church_married`
* `church_service`

</details>

<details>

<summary>🪑 Custom Props</summary>

* `prop_church_bench_l`
* `prop_church_bench_s`

</details>

***

<details>

<summary><span data-gb-custom-inline data-tag="emoji" data-code="1f6aa">🚪</span>Doorlock System</summary>



Add this SQL to integrate with **ox\_doorlock**:

```sql
INSERT INTO `ox_doorlock` (`id`, `name`, `data`) VALUES
    (1051, 'Sandy Church E-1', '{"maxDistance":2,"doors":[{"model":1499410363,"heading":291,"coords":{"x":1786.1871337890626,"y":3897.19970703125,"z":35.19813919067383}},{"model":1732635280,"heading":110,"coords":{"x":1785.5010986328126,"y":3899.037353515625,"z":35.19813919067383}}],"state":1,"coords":{"x":1785.8441162109376,"y":3898.11865234375,"z":35.19813919067383}}'),
    (1052, 'Sandy Church E-2', '{"maxDistance":2,"doors":[{"model":1499410363,"heading":291,"coords":{"x":1785.1024169921876,"y":3900.172119140625,"z":35.19813919067383}},{"model":1732635280,"heading":110,"coords":{"x":1784.41650390625,"y":3902.009765625,"z":35.19813919067383}}],"state":1,"coords":{"x":1784.759521484375,"y":3901.0908203125,"z":35.19813919067383}}'),
    (1053, 'Sandy Church E-3', '{"maxDistance":2,"doors":[{"model":1499410363,"heading":291,"coords":{"x":1784.0037841796876,"y":3903.19384765625,"z":35.19813919067383}},{"model":1732635280,"heading":110,"coords":{"x":1783.3177490234376,"y":3905.03125,"z":35.19813919067383}}],"state":1,"coords":{"x":1783.6607666015626,"y":3904.112548828125,"z":35.19813919067383}}'),
    (1054, 'Sandy Church E-4', '{"maxDistance":2,"doors":[{"model":512557835,"heading":201,"coords":{"x":1802.9735107421876,"y":3918.51123046875,"z":34.9409294128418}},{"model":-29757852,"heading":21,"coords":{"x":1805.479736328125,"y":3919.447265625,"z":34.9409294128418}}],"state":1,"coords":{"x":1804.2265625,"y":3918.979248046875,"z":34.9409294128418}}'),
    (1055, 'Sandy Church E-5', '{"maxDistance":2,"doors":false,"heading":360,"state":1,"model":-251858016,"coords":{"x":1825.4625244140626,"y":3926.236328125,"z":33.89401245117187}}');
```

</details>

***

<details>

<summary>🚀 Installation Guide</summary>

1. Place `prompt_sandy_church` in your server's `resources`
2. In your `server.cfg`, add:

```cfg
start prompt_sandy_church
```

3. Import the SQL above to your database
4. Install MapData (see MapData Docs)
5. Restart your server and test in-game

</details>

***

Need help? Contact support and enjoy **Sandy Church** on your FiveM server! 🚀
