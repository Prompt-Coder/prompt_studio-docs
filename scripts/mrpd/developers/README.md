---
description: Extend MRPD without touching protected logic
icon: code
---

# For Developers

MRPD is built to plug into your server. There are three separate extension points — keep them straight and integration stays clean:

<table data-view="cards"><thead><tr><th></th><th></th><th data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Hooks</strong></td><td><strong>Who</strong> may use an interaction — allow / deny / react</td><td><a href="hooks.md">hooks.md</a></td></tr><tr><td><strong>Providers</strong></td><td><strong>How</strong> an action is performed in your stack — weapons, callbacks, bridges</td><td><a href="providers.md">providers.md</a></td></tr><tr><td><strong>Exports &#x26; Commands</strong></td><td>What your <strong>other resources</strong> can ask MRPD or tell it</td><td><a href="exports-and-commands.md">exports-and-commands.md</a></td></tr></tbody></table>

{% hint style="info" %}
**Hooks** decide *who*. **Providers** decide *how*. **Bridges** (framework / target / notify / textUI, in `bridge/*.lua`) decide *what your core is*. They never overlap.
{% endhint %}
