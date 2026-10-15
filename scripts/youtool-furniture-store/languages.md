---
description: Pick one of 12 languages or follow ox_lib's locale, edit any text in localization/, and add a language of your own.
icon: language
---

# Languages

Every text players see comes from one language file: the tablet shop, the Console, the phone app, on-screen notices and target labels. YouTool ships 12 languages, and the files are open, so you can change any text.

***

### Choose the language

Set `Config.language` in `config.lua`:

{% code title="config.lua" %}
```lua
Config.language = 'auto'
```
{% endcode %}

| Value | Result |
| --- | --- |
| `'auto'` (default) | Follows ox\_lib's `ox:locale` convar |
| A language code, for example `'de'` | That language, whatever ox\_lib uses |

With `'auto'`, set the convar in `server.cfg`. Use `setr`, not `set`: the convar has to reach the players' game as well as the server.

{% code title="server.cfg" %}
```
setr ox:locale "de"
```
{% endcode %}

Without the convar, `'auto'` means English. The language is read when the resource starts, so restart `prompt_youtool_store_system` after a change.

| Code | Language |
| --- | --- |
| `en` | English |
| `de` | German |
| `es` | Spanish |
| `fr` | French |
| `ru` | Russian |
| `pt` | Portuguese |
| `sv` | Swedish |
| `no` | Norwegian |
| `fi` | Finnish |
| `ar` | Arabic |
| `ko` | Korean |
| `zh` | Chinese (Simplified) |

{% hint style="warning" %}
ox\_lib also uses regional codes such as `zh-cn`, `zh-tw` and `pt-br`. YouTool has no file with those names, so with `'auto'` it falls back to English and the setup check warns `Language 'zh-cn' has no localization file, English is used`. Either set `Config.language = 'zh'` (or `'pt'`), or copy `localization/zh.lua` to `localization/zh-cn.lua`.
{% endhint %}

***

### What the language files don't cover

* **Product and category names** come from the catalog, not from the language files. Corporate admins can rename products in the Console. See [Catalog & Custom Furniture](catalog.md).
* **Store names** come from `name` in `Config.Stores` (`config.lua`).
* **Names your staff type in**, such as positions and furniture sets, stay as they were typed.
* **Server console output** (the setup check, `/youtool_diag` and other diagnostics) is always English, so support can read it.

***

### Edit a text

Open `localization/<code>.lua`, for example `localization/de.lua`. Every line is a key and its text:

{% code title="localization/en.lua" %}
```lua
    checkout_need_house = 'You need to own a house to purchase furniture',
    checkout_no_money = 'Not enough money. Need: $%d',
    checkout_done = 'Purchase complete! %d items added.',
    target_set_discount = '%s%% off',
```
{% endcode %}

Change the text, never the key on the left. Then restart `prompt_youtool_store_system`.

Rules for the text:

* **Keep every `%s` and `%d`**, in the same order as in English. YouTool fills them in order with the values (a name, a number, a price), so they can't swap places.
* **Write a percent sign as `%%`.** `'%s%% off'` shows as `25% off`. A single `%` can stop the values in that text from being filled in.
* **Mind the quotes.** The texts are in single quotes, so an apostrophe inside needs a backslash: `'You don\'t own any houses'`.
* **Save the file as UTF-8.**

{% hint style="info" %}
If the console prints `localization/de.lua missing — using English` while the file is there, the file has a Lua syntax error, most often an apostrophe without a backslash. YouTool then ignores the whole file and uses English. The message shows in the server console and in the F8 console.
{% endhint %}

***

### Missing texts fall back to English

YouTool loads `en.lua` first and lays your language over it, text by text. Any key your language file doesn't have shows in English. This also means:

* A partly translated file works. The untranslated texts show in English.
* After an update, texts added in the new version show in English until you add them to your file. Compare your file with the new `en.lua`.
* A key that is missing even from `en.lua` shows as the key name itself (for example `checkout_done`). Restore `en.lua` from the download.

***

### Add a new language

{% stepper %}
{% step %}
#### Copy the English file

Copy `localization/en.lua` and name the copy after your language code, for example `localization/it.lua`.
{% endstep %}

{% step %}
#### Translate the texts

Translate the text on the right of each line and follow the rules above. You don't have to translate everything at once.
{% endstep %}

{% step %}
#### Select it and restart

Set `Config.language = 'it'`, or `setr ox:locale "it"` with `Config.language = 'auto'`, then restart `prompt_youtool_store_system`.
{% endstep %}
{% endstepper %}

No code change is needed. YouTool picks the file by its name, and `fxmanifest.lua` already includes every file in `localization/`. When you update YouTool, copy your file into the new `localization/` folder.
