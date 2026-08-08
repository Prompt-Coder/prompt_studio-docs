---
description: The cabinet roster — what plays, how it plays, and single vs two-player
icon: ghost
---

# The Games

Every cabinet shows a short **pre-game menu** on its screen (Start · Volume · Leave) and a
**Top-10 high-score panel** before you play. Games come in three kinds:

* **Screen games** — the game renders on the cabinet screen (single or split-screen two-player).
* **Physical machines** — the player and machine animate (claw, fortune) with no screen game.
* **Occupancy** — two players take opposite sides of one machine (love tester).

***

### Roster

| Cabinet | Kind | Players | How it plays |
| --- | --- | --- | --- |
| **Space Monkey** | Screen | 1 | Arcade shooter — dodge & blast, smart bombs, shields, boss waves. Move `A/D`, fire `[E]/Space`, bomb `[Shift]`. |
| **The Wizard's Ruin** | Screen | 1 | Side-scrolling hack-and-slash across 5 biomes, weapons, skills & bosses. Move `A/D`, jump `Up`, attack `[E]`, skill `Up+[E]`. Full HP each level. |
| **Badlands Revenge** | Screen (co-op) | 1–2 | Western gun gallery — shoot outlaws, spare friendlies. Aim with the cursor; fire / reload / special. Two players shoot the same scene as a team. |
| **Crotch Rockets** | Screen (split) | 1–2 | Pseudo-3D bike racer — wheelie for top speed, slipstream, dodge traffic. Accel / brake / steer / special. |
| **Get Truckin'** | Screen (split) | 1–2 | Delivery hauler racer — hit the checkpoints before the clock, ram / horn special. |
| **Street Legal** | Screen (split) | 1–2 | Street racer — drift, nitro, outrun the heat. |
| **Love Tester** | Occupancy | 2 | Two players grip opposite sides; the machine rates the couple. Server rolls one shared result. |
| **Claw Machine** | Physical | 1 | Drive the claw over the prizes and grab — arrows move, grab, carry to the chute. A win fires a reward hook. |
| **Nazar the Fortune Teller** | Physical | 1 | Drop a coin, the animatronic reads your fortune (rare readings included). |

{% hint style="info" %}
A **Strength Tester** ("Axe of Fury") cabinet ships **disabled** in `config.lua` (`enabled=false`).
It's kept in the code for a future update — flip it on only if you know its cabinet is placed.
{% endhint %}

***

### Two-player games

**Badlands + the three racers** are two-player on a **single cabinet**:

{% stepper %}
{% step %}
#### Player 1 interacts
The first player targets the cabinet and enters — the pre-game menu appears.
{% endstep %}
{% step %}
#### Player 2 joins, or P1 starts solo
A second player targeting the **same cabinet** pairs in for co-op / split-screen. Or Player 1
presses **`[E]`** to start solo. If a partner leaves mid-game, the session ends cleanly.
{% endstep %}
{% endstepper %}

The **Love Tester** is occupancy-based: two players simply take the left and right sides of the
machine and the test plays automatically — the server picks one shared rating so both see the same
result, lag-free.

***

### Leaving a game

Press **`[Backspace]`** at any time to leave a cabinet. Players are locked to the cabinet while
playing (no walking off mid-animation), and every exit path cleans up the camera, screen and props.

{% hint style="success" %}
Scores, claw wins and love results all flow to the **leaderboards** and **reward hooks** — see
[For Developers](developers.md).
{% endhint %}
