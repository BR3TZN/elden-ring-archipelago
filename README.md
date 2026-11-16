# Elden Ring Archipelago – Spawn-Fix

Inoffizielle Anpassung von [Peliarch Elden Ring Archipelago](https://peliarch.ca/elden-ring/) für Windows. Das Paket enthält die APWorld 1.0.2 und den darauf abgestimmten Peliarch-Client 1.0.2.1 mit einem Spawn-Fix für Elden Ring 2.7.2.0 (Worldwide). Die Änderungen am Client stehen in [Spawn-Fix.patch](me3/Spawn-Fix.patch).

## Spielen

1. [Mod Engine 3 installieren](https://github.com/garyttierney/me3/releases) und das [ZIP dieses Repos](https://github.com/BR3TZN/elden-ring-archipelago/archive/refs/heads/main.zip) in einen neuen Ordner entpacken.
2. `me3/START_ME_ap.me3` öffnen. In der [Peliarch-Anleitung](SETUP.md) heißt dieses Startprofil `ap.me3`.
3. Im Spiel **Connection** öffnen und die Raumadresse, den eigenen Slotnamen und bei Bedarf das Raumpasswort eingeben. Der Client legt die Einstellungen lokal in `me3/apconfig.json` ab, sobald du dich verbindest.
4. Für einen neuen Seed einen neuen Charakter im AP-Profil anlegen.

Wer den Seed generiert, installiert die mitgelieferte [eldenring.apworld](eldenring.apworld) in [Archipelago 0.6.7](https://github.com/ArchipelagoMW/Archipelago/releases/tag/0.6.7) und legt die Spieler-YAML in den `Players`-Ordner. Für einen regulären Run gibt es die [Quickstart-YAML](EldenRing-Quickstart.yaml).

## Charity Royale

Die [Charity-Royale-YAML](EldenRing-CharityRoyale.yaml) ist eine Vorlage für einen neuen Slot. Für eine bestehende Spieler-YAML reichen die fünf Optionen am Ende der Vorlage. Die APWorld kennt die unten stehenden Itemnamen bereits. Mit `trap_count: 0` bleiben sie gezielt zustellbar, ohne zufällig im Seed verteilt zu werden.

| Betrag | Aktion | AP-Item oder Funktion |
| --- | --- | --- |
| 5,00 € | Halbe Runen verlieren | `Trap: Rune Thief` |
| 6,66 € | 20 Sekunden keine Heilung durch die Flasche | `Trap: No Flask` |
| 7,77 € | 2 Sekunden schwarzer Bildschirm | `Trap: Blackout` |
| 10,00 € | DeathLink | `death_link: true` |
| Optional | Wächterlöwe | `Trap: c4270 x1 (4270/42700014)` |
| Optional | Bluthundritter | `Trap: c4290 x1 (4290/42900020)` |

Für eine gezielte Regel in AP Chaos Bridge den vollständigen AP-Itemnamen und den Zielslot verwenden. Der Host kann die Zustellung in der Archipelago-Serverkonsole mit `/send Slotname Trap: Blackout` testen. Bei aktiviertem DeathLink tauscht der Slot auch reguläre Tode mit den anderen DeathLink-Slots aus.

## Credits

- [Alaric (4laric) und Peliarch](https://git.peliarch.ca/alaric/er-archipelago-public) für die APWorld, den Elden-Ring-Client und die ursprüngliche Integration. [Client-Quellcode](https://git.peliarch.ca/alaric/from-software-archipelago-clients-public)
- [nex3](https://github.com/nex3) für `archipelago_rs` und [vswarte](https://github.com/vswarte/fromsoftware-rs) für `fromsoftware-rs`, einschließlich der Grundlage für die Spawn-Korrektur.
- [4laric](https://github.com/4laric/ERR-MapForGoblins-DLL), [VirusAlex](https://github.com/VirusAlex/ERR-MapForGoblins-DLL) und Gacsam für MapForGoblins und dessen Vorgänger.
- [ArialSenki](https://github.com/ArialSenki/NpcSpawner) für den NPC-Spawner als Referenz zur Spawn-Korrektur.

Die ursprünglichen Lizenztexte und weiteren Credits stehen in [LICENSE](LICENSE), [ATTRIBUTION.md](ATTRIBUTION.md) und [me3/licenses](me3/licenses).
