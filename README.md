# Titanfall-2-General-Text-Modding-Guide
A general guide to editing r1 localization files for text modding in Titanfall 2. With this you can edit all of Titanfall's text to your comedic liking.

## Base software and file management
Titanfall 2 stores their localization files in a package that needs to be unpacked using an unpacker, and we also need to repack that package after we're done with it. We also need a good tool to edit our text file migraine-free.
### Required and recommended software
- Download Notepad++ through their [website](https://notepad-plus-plus.org/downloads/) or the [repository](https://github.com/notepad-plus-plus/notepad-plus-plus/releases/tag/v8.5.7).

- Download Cra0kalo's VPK Tool through [this link](https://github.com/Wanty5883/Titanfall2/blob/master/tools/Titanfall_VPKTool3.4_Portable.zip). (required)
  - You can try [Harmony VPK Tool](https://github.com/harmonytf/HarmonyVPKTool) but I don't recommend it. While it has a patching feature, this feature for some reason does not work and unpacking/repacking VPKs leads to weird structure and missing files.
### Recommended file management structure
I recommend creating a folder structure to keep track of all files you'll be manipulating and for backups. This folder will take up 5-10GB of space when you're done modding your text. Below is the folder structure.

- VPK File Env
  - Text Modding
    - Edited Files
      - *Edited files you want to keep for future editing*
    - Packed Files
      - *Folder your repacked files will go to*
    - Packing Environment
      - *Folder to repack your package*
    - Unmodified Files
      - *Unmodified packed VPK's you copied from the game directory*
    - Unpacked Files
      - *Unpacked VPK contents that are not modified*
    - Working Packed Files Backup
      - *Backup of your working packed files here just in case your next revision doesn't work and you're too lazy to go back and see what you did wrong*
  - VPK Pack Tool
    - *Location of installed VPK tool*
   
It's worth keeping all of these folders and files if you plan to do more text editing down the line and if you want to save your edits.
## Text Editing Steps
### Find and retrieve game files
Navigate to the directory Titanfall 2 is installed:
- On STEAM
  - Right click Titanfall 2 > Manage > Browse Local Files, or
  - Navigate to `C:\Program Files (x86)\Steam\steamapps\common\Titanfall2`, or
  - If you've installed Titanfall 2 on a seperate drive, navigate to `[drive letter]:\Steam\steamapps\common\Titanfall2`
- On the EA app
  - Navigate to EA's install location (`C:\Program Files\EA Games\...` by default)

Navigate to the `vpk` folder (`Titanfall2\vpk`). Copy these two files:
- `client_frontend.bsp.pak000_000`
- `englishclient_frontend.bsp.pak000_dir`

and paste them to your `Unmodified Files` folder in your `VPK File Env` folder.

### Unpacking files
Launch up the Titanfall 2 VPK Tool.

Click Open or `CTRL + O`

Navigate to your `Unmodified Files` folder and open `englishclient_frontend.bsp.pak000_dir`. Do not open `client_frontend.bsp.pak000_000` or you will get an error.

Click Extract All and extract all files to your `Unpacked Files` folder.

### Picking the r1_english file and populating the packing environment
The `Unpacked Files` folder should now be populated with game files. Make a copy of these game files and paste them in `Packing Environment`.

In the `Unpacked Files` folder, navigate to `resource` and copy the `r1_english` text file. Paste this file to your `Edited Files`.

### Editing r1_english
Edit the `r1_english` file in your `Edited Files` folder using Notepad++ or your text editor of choice. The `r1_english` file contains almost all text in game from subtitles to menu text.

You can use `CTRL + F` to search for text you saw in game that you want to edit. For example, if you want to change the "RODEO ATTACK" text, simply search it using `CTRL + F` and change that text. Example on line 10391:
```
		"HUD_RODEO_ALERT"                               "Rodeo Attack"
```
to
```
		"HUD_RODEO_ALERT"                               "OH FUUUUUUUUUUUUUUUUUUUUUUUUUUUUUCK"
```
It is **important** you keep formatting proper while editing the text. If you accidentally delete quotation marks, you must put them back or else the formatting of the file will break and your game will start displaying debug text.

It is **important** you do not delete text formatted with `%%`. The game uses this to place values and binds. Examples are:
```
		"TRAINING_HINT_GRENADE"	 						"Press %offhand0% to throw a grenade."
		"AT_WAVE"										"WAVE %s1"
		"WILDS_HELMET_REBOOT_ORDNANCE"					"`1Ordnance%s1"
		"BURN_METER_REWARD_READY"									"%s1 Ready!"
```
You can still edit these fields, just take care you do not damage the `%%` formatting. For example on line 9397, you can change the amped weapon timer from:
```
		"AMPED_STATUS"											    "AMPED: `1%s1"
```
to
```
		"AMPED_STATUS"											    "BALLING: `1%s1"
```
and the text will work just fine.
### Patching and repacking the VPK
Save and close your edited text file. Copy your `r1_english` file and paste it to your `Packing Environment` folder. Replace the files in the destination.

Open up the Titanfall 2 VPK Tool and click Repack VPK.

For "Select a folder containing files you wish to pack into a VPK", select the `Packing Environment` folder.

For "Output Directory of the VPK", select the `Packed Files` folder.

Click Build VPK.
### Renaming packed files
The `Packed Files` folder should now be populated with two files named `pak000_000` and `pak000_dir`.
- Rename `pak000_000` to `client_frontend.bsp.pak000_000`
- Rename `pak000_dir` to `englishclient_frontend.bsp.pak000_dir`

Copy both these files and paste them to your `Working Packed Files backup` if you plan on doing further text modding in the future.

If you want to edit more text in the future, you can simply:
- Purge the `Packed Files` folder
- Re-edit `r1_english` in the `Edited Files` folder
- Copy said `r1_english` file to your `Packing Environment` folder and overwrite existing files
- Repack and rename packed files.

Now if this edit does not work, you can fall back with your original edited packed files if you decide to give up :)

### Patching the game
Copy `client_frontend.bsp.pak000_000` and `englishclient_frontend.bsp.pak000_dir` and paste it in your `\Titanfall2\vpk` folder. Replace the files in the destination.

Launch the game. It is normal for the game to stop responding momentarily while launching after a text edit for the first time.
### Troubleshooting
- If the game crashes on launch, crashes while loading into multiplayer, crashes when starting a match, displays an error, or stops responding indefenitely:
  - The VPK tool unpacked/packed the file incorrectly or an error was made when selecting files/folder to unpack/pack. I used to have this problem a lot but I don't have it anymore. Be sure you're unpacking the entire VPK and not just the `resources` folder where the `r1_english` file is.
- If the game displays debug text such as `NPC_TITAN_AUTO_STRYDER_SNIPER` or other debug text:
  - The formatting of the `r1_english` file is broken. You do not have to scrap the entire file and re-edit your file. You can use `CTRL + F` to search the debug text you see in game and look from that entry up to find where a missing quotation mark is breaking the formatting.
### Removing the modification
If you want to remove the modified text and return to defaults, you can:
- Copy the unmodified files from `Unmodified Files` to your `Titanfall2\vpk` folder and overwrite.
- Verify integrity of game files through EA or Steam.

This can also be used a troubleshooting step if you want to start on a clean slate.

## References
Below is a list of references that you may find useful in text modding.
- [NoSkill Community's guide to text modding](https://noskill.gitbook.io/titanfall2/Modding/user-interface/text-modding-r1_language)
  - Useful resource to understanding what some messages are
- [List of Titanfall 2 modding tools](https://noskill.gitbook.io/titanfall2/intro/duction/tools)
