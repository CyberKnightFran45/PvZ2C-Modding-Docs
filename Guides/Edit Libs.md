# PvZ2C Modding Guide: How to edit Libs?

Libs is the main game code source where the logic remains.

> This guide was written for simple modifications in Hex editors, you won't see nothing related to lib injection or function hooks over here

---

That said, follow these steps to the letter.

1️⃣   Extract the file

Extract the file named `LibSrc.so` (or `libGameSource.so` for older releases) from: **_/>data>data>com.popcap.pvz2cthdxx>Lib** and then move it to a folder where you can easily locate it.

`xx = 360, 4399, or cdbk, this varies depending on the game version`

**NOTE: To access this directory, your device must be rooted. Editing an APK and patching libs is also possible (note that some of them might have signature protection).**

**Also, don't forget to make a back up in case something goes wrong.**

2️⃣   Download the editing software

Next, download one of the following programs:

- Hex Editor (for Android)

- HxD (for Windows)

These are hex editors you will use for the fowlling modifications.

3️⃣   Patch libs


## ▶ 0 Plant Cost

Search for `PlantDamageType`. The next value should be named `Cost`. Rename it accordingly or nullify it by setting all its bytes to 0

**NOTE: these doesn't affect Tile Turnip cost, for no reason**

## ▶ No Plant Cooldown

Search for `MaxLevel`, Next values should be named `PacketCooldown` and `StartingCooldown`, rename or nullify them.

## ▶ Disable World Plant Restrictions

Search for `ValidStages`. Once found, rename or nullify it.

## ▶ Enable all Plant Costume Layers

Search for `custom_`; if the byte following it has `00`, change it to `01` (or vice versa)

## ▶ Change Powerup Type

Search for `TacticalCukePowerupUses` and replace it with `FlickPowerupUses`

## ▶ Reveal Hidden Plants

Search for `Enabled`. Once found, rename or nullify it.

*NOTE: you must have a modded pp.dat with those plants unlocked for using them* 

## ▶ Enable World Previews

Search for `ComingSoon`. Once found, rename or nullify it.

## ▶ Enable Hidden Worlds

Search for `Hidden`. Once found, rename or nullify it.

Hidden worlds such as Tutorial World should appear now (note that attempting to access them might cause game softlock)

## ▶ Get Early Access to Zomboss Fights

This works for some Worlds that are unfinished yet and don't have their Final Day (aka: Boss Fight)

Search for: `[ZOMBIE_` and then look the previous values (`steam`, `renai`, `heian` and `atlantis`)

Replace the desired World Name to another string or just nullify its bytes to get access to its beta level.

## ▶ Kill Bannying System

Bannying System is present in the following versions: `2.2.7 - 2.4.81`

If you want to get rid of it, search for the following values and replace them with `P125`

Target values: `V202`, `V220`, `V316`

**NOTE: this no longer work as for the 2.4.83 version. Bannying is now handled via servers and not locally**

## ▶ Bypass Device Binding Limit

• ARM-v7 lib:

TO-DO

• ARM-8 lib:

Search for the text `4AAC8e52` and replace with `0A005052`