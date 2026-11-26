# Warhammer 40,000: Darktide

[Deutsch](README.de.md)

The [game manifest](game.yml) records the 19 enabled entries from the local Steam installation's `mods/mod_load_order.txt`, last modified on 2 April 2025. All 19 mod folders were present. The installation reports Steam build `26101089`. The loader and framework files were present, but no console logs were available to confirm that the game loaded the mods on this build.

## Manual setup

1. Read [Fatshark's modding policy](https://forums.fatsharkgames.com/t/darktide-modding-policy/75407). Fatshark can warn or ban players for mod use that harms other players, degrades the service, bypasses progression or leads to harassment. Check each mod's requirements and current game compatibility.
2. Follow the [community installation guide](https://github.com/Darktide-Mod-Framework/Darktide-Mod-Framework/wiki/Installing-mods) to set up the Darktide Mod Loader and Darktide Mod Framework. Game updates can disable the loader or break individual mods.
3. Start with display and description changes such as Display Ping, Enhanced Descriptions and Merged Talent Stats. Use the source pages in [`game.yml`](game.yml) or the generated `dist/MODS.md`. Extract each selected mod into `mods/` and add its exact folder name to `mods/mod_load_order.txt` in the order required by the authors.
4. Check for errors in [Darktide's console log](https://support.fatshark.se/hc/en-us/articles/360017633918--PC-How-to-Provide-a-Crash-Report-Console-Log-Launcher-Log-or-user-settings-config) after launch. Leave Chat Block, Collectible Finder and Extended Weapon Customization disabled for the initial setup. Keep Scoreboard results and True Level data for personal use.

## Install prepared mod files

To install the mod files through Overdrive, prepare `payloads/<mod-id>/mods/<original-folder>/` for each of the 19 linked entries. Use the manifest ID and the original folder name shown in the mod notes. For example, Animation Events goes under `payloads/animation-events/mods/animation_events/`. Copy an existing installation's mod folders or obtain the files from the linked authors.

```powershell
.\gco-install.exe install --mod-payloads .\payloads --dry-run
.\gco-install.exe install --mod-payloads .\payloads
```

Use the Darktide Mod Loader and Framework setup above. The installer copies the staged files and backs up replacements. Use the loader's own file to choose which mods to enable.

## Saved load order

The manifest preserves the saved order for reference. The MasterItems Community Patch author recommends loading it at the top. Scoreboard requires Animation Events, and Ovenproof's plugin requires Scoreboard. The local Extended Weapon Customization is version `2.10`. The author also requires Visual Loadout Customization Community Patch for version `3.0` and later.

[Discord Rich Presence](https://www.nexusmods.com/warhammer40kdarktide/mods/168) was installed and commented out. `DPSMeter` was commented out and its folder was absent. Both entries were disabled in the file.

## Build the mod list

Run these commands with Node.js 24.

```sh
npm ci
npm run validate
npm test
npm run build
```

The build writes the linked inventory to `dist/MODS.md` and includes the manifest in `dist/fullrelease.zip`. Download mods from their original sources.
