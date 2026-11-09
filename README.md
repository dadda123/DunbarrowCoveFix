# Dunbarrow Cove Crash Fix (Oblivion Remastered)

A tiny plugin that stops the crash at Dunbarrow Cove (Thieves Den DLC).

## The problem

For some players the game crashes every time they go near Dunbarrow Cove, fast travel there or open its door:

```
Unhandled Exception: EXCEPTION_ACCESS_VIOLATION reading address 0x0000000000000050
```

The cause is a leftover Mythic Dawn agent ("Ascended Immortal", reference `0005D392`) in the cave. Dunbarrow Cove
was built from an old Bethesda test cell, and the Thieves Den DLC deletes the agent that stood there.

If your save has picked that agent up, the game tries to load a character that no longer exists, and crashes. That is
why it only happens to some players, and why an older save often works. Finishing a questline does not fix it.

## Why some saves have the agent

Found by others while looking into a report on the Unofficial Patch bug tracker:

> xEdit versions newer than **4.1.5k** clean plugins wrongly. Deleted records that should be "undeleted and
> disabled" are "undeleted and enabled" instead.

If `DLCThievesDen.esp` was ever cleaned with one of those versions, the test agents appear in the cave (Ascended
Immortals where there should be none), and a save made then remembers them. Restore the original file later and the
agent is deleted again, but the save still has him: that is the crash. The xEdit developers have fixed this for their
next release.

**If you cleaned plugins with xEdit newer than 4.1.5k:** verify the game files in Steam (or reinstall the mods you
cleaned). Back up `Plugins.txt` first, verifying replaces it. Other cleaned plugins can have the same problem elsewhere,
this plugin only covers Dunbarrow Cove.

## What the plugin fixes

`DunbarrowCoveFix.esp` puts the agent back as **disabled** instead of deleted, the way xEdit is supposed to do it. The
game can load him again, so it no longer crashes, and because he is disabled he does not show up.

It works whether your DLC file is original or was cleaned. Nothing else in the DLC is changed, and the cave keeps its
normal name. No console needed, so achievements are not affected.

## How to install

1. Download [DunbarrowCoveFix.esp](https://github.com/dadda123/DunbarrowCoveFix/raw/main/DunbarrowCoveFix.esp).
2. Copy it to
   `...\steamapps\common\Oblivion Remastered\OblivionRemastered\Content\Dev\ObvData\Data\`
3. Open `Plugins.txt` in the same folder and add this line at the end:
   ```
   DunbarrowCoveFix.esp
   ```
4. Start the game, load your save and go to Dunbarrow Cove.

If the agent still appears in the cave, just kill him.

**Uninstall:** remove the line from `Plugins.txt` and delete the file.

## Other fix

[TES4R Civis Ascended Immortals Spawn Fix](https://www.nexusmods.com/oblivionremastered/mods/5232) on Nexus Mods
(December 2025) fixes the Ascended Immortals in Dunbarrow Cove too, and players report it stops the crash. Use one of
the two, not both.
