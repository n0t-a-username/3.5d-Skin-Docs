# 3.5D Animation Skin Pack
---

## Overview

This repository documents the **3.5D animation method** for Minecraft Bedrock Skins. The method works by **explicitly binding existing mob animations to player animation channels** through `Skins.json`.

This approach does **not** modify the player geometry, but rather moves and resizes the players limbs.

The term *3.5D* is used to describe the method as a "middle man" between proper vanilla and 4D skins.

---

## Key Characteristics

* Uses **existing Mojang player animation assets**
* No Molang queries or conditionals
* No scripts, controllers, or state machines
* No custom animation files
* Compatible with standard player behavior
* Works entirely within a skin pack

---

## Installation/Getting Started

1. Download `Base.mcpack` from this repository.
2. Import the pack into Minecraft Bedrock Edition.
3. Open the pack contents and locate the `Skins.json` file.

---

## `Skins.json` Example

```json
{
    "format_version": "1.10.0",
    "serialize_name": "name",
    "localization_name": "name",
    "skins": [
        {
            "localization_name": "name",
            "geometry": "geometry.humanoid.custom",
            "texture": "skin.png",
            "cape": "cape.png",
            "animations": {
                "humanoid_base_pose": "animation.humanoid.base_pose",
                "look_at_target": "controller.animation.humanoid.look_at_target",
                "cape": "animation.player.cape",
                "move.arms": "animation.player.move.arms",
                "move.legs": "animation.player.move.legs",
                "holding": "animation.player.holding",
                "attack.positions": "animation.player.attack.positions",
                "attack.rotations": "animation.player.attack.rotations",
                "bob": "animation.player.bob"
            },
            "type": "free",
            "enable_attachables": true
        }
    ]
}
```

## Geometry Usage

```json
"geometry": "geometry.humanoid.custom"
```

In skin packs, geometry **does not define new models**. Its role is limited to:

* Selecting **classic (thick) or slim arm** variants
* Localizing player model variants

You cannot:

* Add or remove bones
* Change limb proportions
* Modify the humanoid hierarchy
* Introduce non-player geometry

All structural aspects remain the standard Bedrock player model.

---

## Animation Bindings - The good stuff

The `animations` object is the core of this method.

Each entry maps a **skin animation slot** to an **existing player animation asset** that already exists in Bedrock.

Example:

```json
"move.arms": "animation.react_idle"
```

This does **not** define a new animation. It simply instructs minecraft to bind that animation directly to the skin.

---

## Common Animation Channels

| Channel              | Description                                |
| -------------------- | ------------------------------------------ |
| `humanoid_base_pose` | Base bind pose used for animation layering |
| `move.arms`          | Arm motion while walking                   |
| `move.legs`          | Leg motion while walking                   |
| `holding`            | Item holding offsets                       |
| `attack.positions`   | Arm positioning during attacks             |
| `attack.rotations`   | Swing rotation motion                      |
| `bob`                | Breathing-styled animation                 |
| `cape`               | Cape physics                               |
| `look_at_target`     | Head rotation                              |

---

## How to Hide Armor

```json
"enable_attachables": false
"hide_armor": true
```
Please note, "enable attachables" also hides tridents or anything geometry based.
---

## Limitations

* Player animation behavior cannot be altered unless you use custom animations via a texture pack
* Bones/Limbs cannot be added, only removed
* Invalid animation IDs fail silently

---
