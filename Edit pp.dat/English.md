# PvZ2 Chinese: Modding Guide - How to modify your pp.dat?

The pp.dat file contains the player's progress serialized as binary data.

> Keep in mind that the Chinese version of PvZ2 has an anti-hacking system that detects changes in the data and nullifies them.
Modifying certain values in recent versions of the game risks getting your account permanently banned (only certain modifications are allowed; the guide was written for versions prior to banning).

---

In the guide, I detail the nodes responsible for the Integrity Check to validate that the data has not been altered.
This is still under investigation as I do not know how the hashes are generated, it may be MD5 with some Salt that varies per user.

Discovering how the validation hashes work would mean circumventing the banning system as it focuses mainly on data integrity.

**NOTE: I AM NOT RESPONSIBLE FOR ACCOUNT BLOCKING OR DATA LOSS. EDIT AT YOUR OWN RISK.**

That said, follow these steps to the letter.

## Step #1. Extract the file

Extract the pp.dat file from: **_/>data>data>com.popcap.pvz2cthdxx>no_backup_** and then move it to a folder where you can easily locate it.

`xx = 360, 4399, or cdbk, this varies depending on the game version`

**NOTE: To access this directory, your device must be rooted.
Also, don't forget to back up your data in case something goes wrong.**

## Step #2. Decode the file

RTONs from Chinese version are encrypted, so you will need to decrypt the file first and then decode it.

**NOTE: I recommend using Sen for this. Although there are other tools available, they come with limitations or are obsolete.**

Drag the file into the program and select **option 39 (PopCap RTON Encrypted to JSON).**

## Step #3. Download the editing software

Next, download one of the following programs:

- To edit on Windows

```
JSON Editor
Notepad++
```

- To edit on Android

```
MT Manager
JSON Validator
```

These are text editors for handling JSON files on different platforms.

## Step #4. Modify values

You can modify the values to whatever amount you want.

Just make sure not to exceed `2,147,483,647` or they will become negative due to an overflow.

It should also be noted that some values are obfuscated. You can check [my repository](https://github.com/CyberKnightFran45/SexyCalculator/blob/main/Source/IntGuard.cs) to see how they are decrypted.

Here is the description of the nodes documented in the file:

### ▶ Change username

Look for an `n` in the editor; this string is your username.

The advantage of modifying it is that it will allow you to use more characters because the game has a limit.

**NOTE: It is not recommended to change it to an excessively long name, as UI may not display it correctly.**

### ▶ Edit amount of Coins

Look for a `c` in the editor.

This integer is obfuscated with bit rotations. Use **SexyCalculator** to calculate the original.

*__INTEGRITY CHECK: The hash used to validate the value is `csign` (deprecated)__*

### ▶ Edit amount of Days completed

Search for `dc` in the editor. This integer is the amount of Days completed in Adventure mode.

### ▶ Edit unlocked Cumulative Recharge Prizes

Search for `urn` in the editor.

You will see a list of numbers. These are the IDs assigned to the rewards you have unlocked by reloading real money.

Before `v1.8.0`, it was possible to obtain the rewards in the Gems Shop as the objectives were completed.

The shop UI was changed in recent versions, which means that most rewards are not claimable. However, some node values still work. I will underline the IDs that have no effect in italics.

List of rewards:

* 2 = Coin Multiplier
* *__6 = Daily Lottery Tickets__*
* *__10 = Random Plant__*
* 20 = Turbo Button
* *__30 = Cherry Bomb__*

### ▶ Modify amount of Recharged yuan

Search for `newrcc` in the editor.

This integer is obfuscated with bit rotations. Use **SexyCalculator** to calculate the original.

### ▶ Edit unlocked Prizes for new Top-ups

Search for `ntrrs` in the editor.

You will see a list of numbers. These are the IDs assigned to the prizes you have unlocked by topping up real money (in the new interface).

**NOTE: each prize has its own ID, which matches the milestone to be reached to unlock the prize.

### ▶ Edit amount of Gems

Look for a `g` in the editor.

This integer is obfuscated with bit rotations. Use **SexyCalculator** to calculate the original.

This is followed by another value: `gg`.

It has not been obfuscated and seems to be some kind of validation to know how many Gems you have purchased.

**NOTE: try not to exceed `100,000` or your Gems will be reset to 0 and your plants will be downgraded to Level 1.
This was done in some versions of the game as a measure to prevent the use of hacks.**

*__INTEGRITY CHECK: the hash used to validate the value is `gs`__*

### ▶ Edit amount of Stars

Look for an `s` in the editor.

This integer is obfuscated with bit rotations, use **SexyCalculator** to calculate the original.

*__INTEGRITY CHECK: the hash used to validate the value is `ssign`__*

### ▶ Edit last level played

Search for an `l` in the editor. This string is the name of the last level you played.

**NOTE: each level has its own ID**

*__INTEGRITY CHECK: the hash used to validate the value is `lsign`__*

### ▶ Edit Completed Worlds

Search for `wmed` in the editor.

You will see a list of objects. These are the Worlds you have completed.

The structure of each object is as follows:

◼ `w`: World ID

◼ `e`: object with world data, divided into:

- `i`: Level or event ID
- `h`: determines whether the level/event has been activated or completed `(1 = completed, 0 = incomplete)`

**NOTE: each world and event has its own ID**

### ▶ Edit which Plants you have

Search for a `p` in the editor.

You will see a list of numbers. These are the IDs assigned to the plants you have unlocked.

**NOTE: each plant has its own ID**

*__INTEGRITY CHECK: the hash used to validate the data is `ups`__*

### ▶ Edit amount of Red envelopes

Look for `rp` in the editor.

This integer is obfuscated with bit rotations. Use **SexyCalculator** to calculate the original.

*__INTEGRITY CHECK: the hash used to validate the value is `rpsign`__*

### ▶ Edit which Upgrades you have

Search for `gf` in the editor.

You will see a list of numbers. These are the IDs assigned to the upgrades you have unlocked.

**NOTE: each upgrade has its own ID**

*__INTEGRITY CHECK: the hash used to validate the data is `ugfs` (deprecated)__*

### ▶ Edit which Narratives you have seen

Search for `ne` in the editor.

You will see a list of numbers. These are the IDs assigned to the narratives you have seen in the WorldMap.

**NOTE: each narrative has its own ID**

### ▶ Edit which Zombies you have spotted

Search for `kz` in the editor.

You will see a list of numbers. These are the IDs assigned to the Zombies you have defeated.

**NOTE: each zombie has its own ID**

### ▶ Edit Power-up uses

Search for `pr` in the editor.

You will see a list of objects. These are the Power-ups you have unlocked.

The structure of each item is as follows:

- `n`: type of Power-up.
- `i`: number of uses.

*__INTEGRITY CHECK: the hash used to validate the data is `prs`__*

### ▶ Edit Plant Pieces

Search for `ppr` in the editor.

You will see a list of objects. These are the plants and their respective number of Pieces. 

The structure of each object is as follows:

- `pi`: plant ID
- `pc`: number of Pieces

*__INTEGRITY CHECK: the hash used to validate the data is `pprs`__*

### ▶ Edit Pendant Pieces

Search for `asp` in the editor.

You will see a list of objects. These are the pendants and their respective number of pieces.

The structure of each object is as follows:

- `acpt`: pendant name
- `acpc`: piece count

*__INTEGRITY CHECK: the hash used to validate the data is `asps`__*

### ▶ Edit Cannons and Shields from Sky City

Search for `rcstl` in the editor.

You will see a list of objects. These are the cannons and shields of Sky City.

The structure of each object is as follows:

- `rslwn`: world name (it will always be `"skycity"` by default, editing it has no effect).

- `rslcl`: cannon type `(1 = Basic, 2 = Laser, 3 = Rocket Launcher)`

- `rslbl`: shield type `(1 = Basic, 2 = Metal, 3 = Gold)`

**NOTE: this list has a single element, adding more is unnecessary, since the only world where upgrades work is in that one.**

### ▶ Edit Plant Leveling

Look for `psla` in the editor.

You will see a list of objects. These are the unlocked plants and their respective leveling.

The structure of each object is as follows:

- `icpi`: Plant ID
- `icl`: Current level

#### 🔶 **INTERESTING FACTS:**

1. Some plants do not have stats for certain levels, so their attributes will be reverted to Level 1 (e.g., Peashooter at Level 5 in older versions)*

2. In versions prior to `2.0.0`, attempting to place a Level 5 plant in a game caused the game to crash unexpectedly (due to certain properties being missing, even though graphics did exist).

3. In recent versions, there are graphics for Levels 6 to 10, but trying to view a plant in the Upgrades section crashes because there are no properties.

---

**NOTE: Edit with caution.**

### ▶ Edit Leveling of Defeated Zombies

Search for `zsla` in the editor.

You will see a list of objects. These are the defeated zombies and their respective levels.

The structure of each object is as follows:

- `icpi`: Zombie ID
- `icl`: Current level

#### 🔶 **INTERESTING FACTS:**

1. Current level indicators only have icons from 1 to 5. If the value differs, both the zombie background and the card will not display the leveling correctly in the Almanac.

2. If the value is set to 5, the card will display 4 instead.

---

**NOTE: Edit with caution.**

### ▶ Edit Daily Challenge data

Search for `ainfo` in the editor. You will see an object with the following structure:

- `rAt`: last date the event was accessed `(type: UnixTimestamp)`
- `ytl`: number of tickets for the Yeti Madness event
- `tcylc`: number of tickets for the God of Wealth event
- `tgclc`: number of tickets for the Gargantuar Crisis event
- `tdilc`: number of tickets for the Devil Invasion event
- `yetiCountPerDayVersion`: object version (always 0, uses rotation bits)
- `yetiCountPerDay`: number of yetis to spawn in the event
- `acl`: best time (not sure)
- `tyeti`: determines whether Yeti Madness is active or not
- `sptlc`: highest score (not sure)

### ▶ Edit which Costumes you have

Search for `ulokpa` in the editor.

You will see a list of objects. These are the costumes you have unlocked.

The structure of each object is as follows:

- `paipid`: costume ID
- `avt`: outfit type (`"normal"` by default)
- `vaulok`: array of booleans. The value determines whether the costume has been unlocked or not `(1 for true, 0 for false)`

*__INTEGRITY CHECK: the hash used to validate the data is `uas`__*

### ▶ Edit Costume Pieces

Search for `lpapi` in the editor.

You will see a list of objects. These are the Costumes and their respective Number of Pieces. 

The structure of each object is as follows:

- `papidid`: costume ID
- `vapc`: Number of Pieces

*__INTEGRITY CHECK: the hash used to validate the data is `ais`__*

### ▶ Edit Plant indexes in Daily Challenges

Search for `lfprii` in the editor.

You will see a list of objects. These are the Daily Challenge records.

The structure of each object is as follows:

- `gm`: game mode
- `gl`: difficulty
- `npri`: random prize index (common plant)
- `fpri`: random prize index (special plant)
- `rpri`: random prize index (rare plant)

**NOTE: random indexes appear to be the probabilities of obtaining Pieces in the level.
They are obfuscated with bit rotation; decrypt the original value with SexyCalculator**

### ▶ Edit which secondary Costumes you have

Search for `lpnai` in the editor.

You will see a list of objects. These are the secondary costumes you have unlocked. 

The structure of each object is as follows:

- `pnai`: Plant ID
- `vnaid`: List of unlocked costumes

### ▶ Edit secondary Costume Pieces

Search for `pnapi` in the editor.

You will see a list of items. These are the secondary outfits and their respective number of pieces. 

The structure of each item is as follows:

- `pnapid`: outfit ID
- `pnapc`: number of pieces

### ▶ Edit equipped Pendants

Search for `pasi` in the editor.

You will see a list of objects. These are the Pendants you have equipped on your plants. 

The structure of each object is as follows:

- `paci`: ID of the plant using the Pendant
- `pact`: name of the equipped pendant
- `pacid`: link ID, defaults to 0
- `l`: level (only applies to Super Pendants)

### ▶ Edit Plant Family Properties

**NOTE: the following node has subnodes with names identical to the root object. I will put a ´*´ to differentiate the child nodes from the parent. They do NOT appear this way in the JSON.**

Search for `pfi` in the editor.

You will see a list of objects. These are the plant families and their respective percentage effects. 

The structure of each object is as follows:

◼ `pfi*`: Plant family ID

◼ `pfbv`: Object with percentage values, divided into:

- `pfbvt`: boost type
- `pfbv*`: current value
- `pfbvrt`: boost type (slot 2)
- `pfvrb`: future value (slot 2)
- `pfbm` : TO-DO
- `pfbl`: determines whether the second slot is unlocked (not sure)

**NOTE: each plant family has its own ID**

### ▶ Edit World Trophies

Search for `wcif` in the editor.

You will see a list of objects. These are the worlds and their progress trophies. 

The structure of each object is as follows:

- `wcwn`: world name
- `wcscu`: star trophy `(true to unlock it, false to lock it)`
- `wcbcu`: boss trophy `(true to unlock it, false to lock it)`
- `wcpcu`: plant trophy `(true to unlock it, false to lock it)`

### ▶ Edit user avatar

Search for `hsid` in the editor. This integer is the ID of the avatar you're using.

**NOTE: each user avatar has its own ID

### ▶ Edit which avatars you have

Search for `unlockhs` in the editor.

You will see a list of numbers. These are the IDs assigned to the avatars you have unlocked.

**NOTE: each user avatar has its own ID

### ▶ Edit amount of Materials and event Coins

Search for `mtrl` in the editor.

You will see a list of objects. These are the event materials or coins you have accumulated.

The structure of each object is as follows:

- `id`: ID of the material or coin
- `count`: quantity (obfuscated with bit rotation)

### ▶ Edit equipped Artifact

Search for `catfc` in the editor. This integer is the ID of the artifact you have equipped.

**NOTE: each artifact has its own ID

### ▶ Edit Artifact Leveling

Search for `atfcla` in the editor.

You will see a list of objects. These are the artifacts and their respective levels.

The structure of each object is as follows:

- `id`: ID of the artifact
- `rank`: effectiveness rank
- `level`: level
- `boostinfos`: boost info (always empty)
- `uboostinfos`: unlocked boost info (always empty)

### ▶ Edit user banner

Search for `cravr` in the editor. This integer is the ID of the banner you're using.

**NOTE: each banner has its own ID

### ▶ Edit which banners you have

Search for `unlockrai` in the editor.

You will see a list of numbers. These are the IDs assigned to the banners you have unlocked.

**NOTE: each banner has its own ID

### ▶ Edit unlocked Plant Genes

Search for `mpgl` in the editor.

You will see a list of objects. These are the plant genes and their levels.

The structure of each object is as follows:

- `id`: gene ID
- `level`: level
- `lockState`: whether it is locked or not `(0 = locked, 1 = unlocked)`

### ▶ Edit amount of Genetic material

Search for `mpgel` in the editor.

You will see a list of objects. These are the different materials used in the Gene Refiner.

The structure of each object is as follows:

- `id`: ID of the material
- `num`: amount

---

The following values are exclusive to older versions `(v1.0.1 - v1.7.7)`

### ▶ Edit Stamina amount

Search for `staminaData` in the editor.

You will see an object with the following properties:

- `lastLocalTime`: last local date when Stamina ran out `(type: UnixTimestamp)`

- `startLocalTime`: local date when Stamina began to recharge `(type: UnixTimestamp)`

- `lastServerTime`: last server date when Stamina ran out `(type: UnixTimestamp)`

- `leftSeconds`: seconds remaining to receive more Stamina `(type: int)`

- `totalStamina`: current amount of Stamina, defaults to 5 `(type: int)`

- `isTrust`: whether to trust local data or use server data `(type: boolean)`

### ▶ Edit amount of World Keys

Search for `wks` in the editor.

This integer is obfuscated with bit rotations, use **SexyCalculator** to calculate the original.

*__INTEGRITY CHECK: the hash used to validate the value is `wkssign`__*

### ▶ Modify the amount of Recharged yuan (old)

Node for older versions of the game.

Search for `rcc` in the editor.

Then, search for `ttrc` and modify it with the same value you assigned to the previous node.

The second value is obfuscated with bit rotations, use **SexyCalculator** to calculate the original.

### ▶ Edit amount of Gold Beans

Search for `ptss` in the editor. This integer is the Gold Beans you have.

It is obfuscated with bit rotations, use **SexyCalculator** to calculate the original.

### ▶ Edit Completed Worlds (Old Map)

Search for `wm` in the editor.

You will see a list of objects. These are the Worlds you have completed.

The structure of each object is as follows:

- `W`: World ID
- `E`: Level or event ID
- `S`: Number of stars collected (max. 3)
- `C`: Challenge ID (if applicable)
- `N`: Narrative ID (if applicable)
- `P`: Level progress (not sure)

### ▶ Edit amount of Star Coins

Search for `sc` in the editor. This integer is the Star Coins you have in Garden Wars (former PvP Mode).

It is obfuscated with bit rotations, use **SexyCalculator** to calculate the original.

### ▶ Edit Yeti Event data

Used in early versions of the game.

Search for `tyi` in the editor. You will see an object with the following structure:

- `wml`: level where the event was triggered `(type: string)`
- `lst`: last date the yeti was sighted `(type: UnixTimestamp)`
- `nst`: next date of the event `(type: UnixTimestamp)`

### ▶ Edit Endless Zones

Search for `dri` in the editor.

You will see a list of objects. These are the Infinity Zones, with the following structure:

- `wn`: name of the World or event
- `cl`: current level
- `hl`: highest score.
- `pfco`: PlantFood left (max: 5)
- `l`: remaining lawnmowers, each configuration has its own ID.
- `sb`: list of plants, each with its respective ID
- `hr`: determines whether this level will draw a card or not

### ▶ Edit amount of Star Keys

Search for `wsk` in the editor.

You will see a list of objects. These are the worlds and their respective Star Keys.

The structure of each object is as follows:

- `wn`: world name
- `kc`: keys count

*__INTEGRITY CHECK: the hash used to validate the data is `ws`__*

### ▶ Edit Endless Zone records (Festival) 

Search for `mlescs` in the editor.

You will see a list of objects. These are the Endless Zones of the festival event and their records.

The structure of each object is as follows:

- `mark`: mark
- `level_name`: event name

### ▶ Edit amount of Space-Time Relics

Search for `mlgic` in the editor. This integer represents amount of Space-Time Relics you obtained.

### ▶ Edit amount of Magic Stones

Search for `mlgicstone` in the editor. This integer represents amount of Magic Stones you obtained.

### ▶ Edit amount of Leaves

Search for `lfgt` in the editor. This integer represents the Leaves you obtained.

---

> Made with ❤️ by FranZ, enjoy!