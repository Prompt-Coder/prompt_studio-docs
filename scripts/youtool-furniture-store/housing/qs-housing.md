---
description: Connect YouTool Furniture Store to qs-housing (Quasar Store). No files to copy; purchases land in the house's decoration stash.
icon: house-chimney
---

# qs-housing

YouTool delivers every purchase into the house's decoration stash in qs-housing (Quasar Store), and the player places it with the qs-housing decorator. There is nothing to copy into qs-housing; YouTool also registers its catalog with qs-housing by itself when it starts.

**Tested with:** qs-housing 5.2.16. **Minimum:** 5.2.16. **Recommended:** 5.3.19 or newer.

{% hint style="info" %}
qs-housing 5.2.16 to 5.3.18 work. From 5.3.19 qs-housing takes catalog registrations on the server side, which is how YouTool registers its catalog, so the setup check asks you to update to 5.3.19 when you run an older build.
{% endhint %}

***

### Install

{% stepper %}
{% step %}
#### Update qs-housing

You need qs-housing **5.2.16 or newer** (it ships the `addDecorationToHouse` export YouTool uses), ideally **5.3.19 or newer**. Download updates from Quasar's keymaster.
{% endstep %}

{% step %}
#### Start qs-housing before YouTool

{% code title="server.cfg" %}
```
ensure oxmysql
ensure ox_lib
ensure qs-housing
ensure prompt_youtool
ensure prompt_youtool_store_system
```
{% endcode %}
{% endstep %}

{% step %}
#### Copy the item pictures (optional)

The qs-housing decorator can show YouTool's item pictures. This is switched on by default, so copy the pictures, or switch it off (see [Settings](#settings)).

1. Create the folder `qs-housing/web/images/youtool/`.
2. Copy every `.webp` file from `prompt_youtool_store_system/images/` into it.

From the folder that contains both resources:

{% tabs %}
{% tab title="Windows" %}
```
xcopy "prompt_youtool_store_system\images\*.webp" "qs-housing\web\images\youtool\" /Y
```
{% endtab %}

{% tab title="Linux" %}
```
cp prompt_youtool_store_system/images/*.webp qs-housing/web/images/youtool/
```
{% endtab %}
{% endtabs %}

Without the pictures, items still work, they just show no picture in the decorator.
{% endstep %}

{% step %}
#### Restart

```
restart qs-housing
restart prompt_youtool_store_system
```

About 5 seconds after YouTool starts, the console shows the catalog registration (the numbers depend on your catalog):

```
[YouTool QS-Housing] Syncing 2112 items to qs-housing (server-side)...
[YouTool QS-Housing] Sync complete: 2112 items registered, 0 failed
```

YouTool registers its catalog only when **it** starts. Whenever you restart qs-housing on its own, restart `prompt_youtool_store_system` afterwards.
{% endstep %}
{% endstepper %}

***

### How players get the furniture

1. The player buys furniture at the YouTool store or in the phone app, and picks the house if they own several.
2. The items go straight into that house's **decoration stash** in qs-housing. No restart is needed; the buyer's decorations refresh right after the purchase.
3. Inside the house, the player opens the qs-housing **decorator** and places the items from the stash.

YouTool items also appear in qs-housing's own furniture categories. YouTool matches each item's category by name (chairs, sofas, tables, beds, lamps, plants, paintings and so on); items that match nothing go into the `defaultCategory` from the settings below.

***

### Settings

`integrations/qs-housing/client/config.lua` (open file, not encrypted):

| Option | Default | Meaning |
| --- | --- | --- |
| `syncDelay` | `5000` | Milliseconds YouTool waits after it starts before registering its catalog with qs-housing. Raise it if qs-housing loads slowly. |
| `defaultCategory` | `'decals'` | qs-housing category for YouTool items whose category matches no qs-housing category. |
| `imagesEnabled` | `true` | Show YouTool's item pictures in the decorator. Needs the pictures copied (install step 3). Set `false` to register items without pictures. |
| `imagePath` | `'nui://qs-housing/web/images/youtool/'` | Where the pictures load from. Can also be your own web host, for example `'https://your-server.com/youtool-images/'` (keep the trailing `/`). |

Restart `prompt_youtool_store_system` after changing them.

***

### Setup check

qs-housing needs no install file, so the setup check only checks the version. On qs-housing 5.3.19 or newer you see the `Housing:` line only (`[ OK ]` on the tested version, `[INFO]` on a newer one). On 5.2.16 to 5.3.18:

```
  [ OK ] Housing: qs-housing 5.2.16
  [INFO] qs-housing 5.2.16 works, but prints a warning for every catalog item at boot
         -> Update qs-housing to 5.3.19 or newer.
```

On a build older than 5.2.16, purchases can't be delivered:

```
  [FAIL] qs-housing 5.1.0 is too old for YouTool
         -> Update qs-housing to 5.2.16 or newer.
```

To test one real delivery, run `youtool_setup <playerId>` with a player who owns a house online. See [What the setup check verifies](README.md#what-the-setup-check-verifies).

***

### Troubleshooting

<details>

<summary><code>SCRIPT ERROR: No such export addDecorationToHouse in resource qs-housing</code></summary>

Your qs-housing is older than 5.2.16. Update it through Quasar's keymaster.

</details>

<details>

<summary>Items don't appear in the house stash</summary>

1. Check that the purchase went through (money taken, "Purchase complete!" notice).
2. Check which house the player picked at checkout; the items are in that house's stash.
3. Run `youtool_setup <playerId>` and fix any `[FAIL]` line.
4. Make sure qs-housing starts before YouTool in `server.cfg`.

</details>

<details>

<summary>YouTool items are missing from qs-housing's furniture categories</summary>

qs-housing was restarted after YouTool, so it lost the catalog YouTool registered. Run `restart prompt_youtool_store_system`. Check the console for `Sync complete: ... items registered`.

</details>

<details>

<summary>Items show no picture in the decorator</summary>

Copy the pictures (install step 3) and check that `imagePath` points to that folder. If you don't want pictures, set `imagesEnabled = false`.

</details>
