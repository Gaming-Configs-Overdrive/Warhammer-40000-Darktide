# Warhammer 40,000: Darktide

[English](README.md)

Das [Spielmanifest](game.yml) erfasst die 19 aktivierten Einträge aus `mods/mod_load_order.txt` der lokalen Steam-Installation. Die Datei wurde zuletzt am 2. April 2025 geändert. Alle 19 Mod-Ordner waren vorhanden. Die Installation meldet den Steam-Build `26101089`. Loader und Framework lagen im Spielordner. Konsolenlogs für einen Nachweis, dass dieser Build die Mods geladen hat, lagen nicht vor.

## Manuelle Einrichtung

1. Lies [Fatsharks Modding-Richtlinie](https://forums.fatsharkgames.com/t/darktide-modding-policy/75407). Fatshark kann Verwarnungen und Sperren aussprechen, wenn Mods anderen Spielern schaden, den Dienst beeinträchtigen, Fortschritt umgehen oder zu Belästigung führen. Prüfe die Voraussetzungen und die Kompatibilität der einzelnen Mods.
2. Richte den Darktide Mod Loader und das Darktide Mod Framework nach der [Anleitung des Projekts](https://github.com/Darktide-Mod-Framework/Darktide-Mod-Framework/wiki/Installing-mods) ein. Spielupdates können den Loader deaktivieren oder einzelne Mods unbrauchbar machen.
3. Beginne mit Anzeige- und Textänderungen wie Display Ping, Enhanced Descriptions und Merged Talent Stats. Die Originalquellen stehen in [`game.yml`](game.yml) und in der generierten `dist/MODS.md`. Entpacke jede ausgewählte Mod unter `mods/` und trage ihren exakten Ordnernamen in `mods/mod_load_order.txt` ein. Beachte dabei die Ladereihenfolge der Autoren.
4. Prüfe nach dem Start [Darktides Konsolenlog](https://support.fatshark.se/hc/en-us/articles/360017633918--PC-How-to-Provide-a-Crash-Report-Console-Log-Launcher-Log-or-user-settings-config) auf Fehler. Lass Chat Block, Collectible Finder und Extended Weapon Customization bei der ersten Einrichtung deaktiviert. Nutze Scoreboard-Ergebnisse und True-Level-Daten für dich selbst.

## Vorbereitete Mod-Dateien installieren

Für die Installation über Overdrive lege für alle 19 verlinkten Mods die Dateien unter `payloads/<mod-id>/mods/<Originalordner>/` ab. Nimm die ID aus dem Manifest und den Originalordner aus den Mod-Hinweisen. Animation Events liegt zum Beispiel unter `payloads/animation-events/mods/animation_events/`. Verwende die Dateien einer vorhandenen Installation oder die Downloads der verlinkten Autoren.

```powershell
.\gco-install.exe install --mod-payloads .\payloads --dry-run
.\gco-install.exe install --mod-payloads .\payloads
```

Richte Loader und Framework wie oben beschrieben ein. Der Installer kopiert die vorbereiteten Dateien und sichert ersetzte Dateien. Welche Mods aktiv sind, legst du weiterhin in der Ladeliste des Loaders fest.

## Gespeicherte Ladereihenfolge

Das Manifest enthält die gespeicherte Reihenfolge als Referenz. Der Autor von MasterItems Community Patch empfiehlt, den Patch an die erste Stelle zu setzen. Scoreboard benötigt Animation Events. Ovenproofs Plugin benötigt Scoreboard. Lokal liegt Extended Weapon Customization in Version `2.10` vor. Ab Version `3.0` verlangt der Autor zusätzlich Visual Loadout Customization Community Patch.

[Discord Rich Presence](https://www.nexusmods.com/warhammer40kdarktide/mods/168) war installiert und auskommentiert. `DPSMeter` war auskommentiert und der zugehörige Ordner fehlte. Beide Einträge waren laut Datei deaktiviert.

## Mod-Liste bauen

Führe diese Befehle mit Node.js 24 aus.

```sh
npm ci
npm run validate
npm test
npm run build
```

Der Build schreibt die verlinkte Mod-Liste nach `dist/MODS.md` und legt das Manifest in `dist/fullrelease.zip` ab. Lade die Mods aus ihren Originalquellen herunter.
