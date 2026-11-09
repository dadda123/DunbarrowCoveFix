# Dunbarrow Cove Crash Fix (Oblivion Remastered)

A tiny plugin that stops the crash at Dunbarrow Cove (Thieves Den DLC).

## The problem

For some players the game crashes every time they go near Dunbarrow Cove, fast travel there or open its door:

```
Unhandled Exception: EXCEPTION_ACCESS_VIOLATION reading address 0x0000000000000050
```

The cause is a Mythic Dawn agent ("Ascended Immortal", reference `0005D392`) that used to stand in the cave.
The Thieves Den DLC deletes him. If your main quest has already activated him, your save still remembers him, so the
game tries to load a character that no longer exists, and crashes.

That is why it only happens to some players, and why an older save often works.

## What the plugin fixes

`DunbarrowCoveFix.esp` puts the agent back as **disabled** instead of deleted. The game can load him again, so it
no longer crashes, and because he is disabled he does not show up.

Nothing else in the DLC is changed. No console needed, so achievements are not affected.

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
