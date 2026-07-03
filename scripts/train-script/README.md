---
description: by adaz
icon: train
---

# Train Script

### Requirements

* FiveM server (artifact 6683 or newer recommended)
* [`ox_lib`](https://github.com/overextended/ox_lib) started **before** this resource
* `prompt_train_polar_express` — the model pack that ships alongside the script

***

### Installation

1. Copy `prompt_train_script` and `prompt_train_polar_express` into your `resources` folder.
2. Add the following to your `server.cfg` **in this order**:

```
ensure ox_lib
ensure prompt_train_polar_express
ensure prompt_train_script
```

3. Open `config/config.lua` and adjust settings for your server (framework, inventory, routes, etc.). See Configuration for a full reference.
   1. If you want to use train tickets, register the `train_ticket` item in your inventory resource. See [tickets.md](tickets.md "mention") for the exact snippets.

***

### First Boot Checklist

| Check                      | What to look for                                                        |
| -------------------------- | ----------------------------------------------------------------------- |
| No `resource name` warning | Console should **not** say `Resource name is not "prompt_train_script"` |
| Framework detected         | Console prints the detected framework (`qbx`, `qb`, `esx`, or `none`)   |
| Trains spawn               | After the first player joins you should see trains appear on the map    |
