# Personal Knowledge Sync

Obsidian-Plugin, das einen Vault mit einem **selbst betriebenen** Knowledge
Service synchronisiert. Es enthält kein Git, keine SSH-Bibliothek und kein
GitHub-Token — das Gerät spricht ausschließlich mit dem eigenen Dienst.

Dieses Repository enthält nur die gebauten Artefakte für die Installation über
[BRAT](https://github.com/TfTHacker/obsidian42-brat). Der Quellcode liegt
woanders.

## Installation

1. In Obsidian das Community-Plugin **BRAT** installieren.
2. BRAT → *Add beta plugin* → `bassistrs/obsidian-personal-knowledge-sync`
3. Plugin unter *Community Plugins* aktivieren.

Funktioniert auch auf iOS und Android — `isDesktopOnly` ist `false`.

## Einrichten

In den Plugin-Einstellungen eintragen:

| Feld | Bedeutung |
|---|---|
| Server-URL | Basis-URL des eigenen Knowledge Service |
| Geräte-ID | muss der `deviceId` des Gerätecredentials entsprechen |
| Token | Gerätecredential mit `sync`-Scope |

Ohne diese drei Angaben tut das Plugin nichts — es gibt keinen voreingestellten
Server.

## Verhalten

- Pull kurz nach dem Start des Vaults (abschaltbar).
- Push nach 60 Sekunden Inaktivität, nur solange Obsidian im Vordergrund läuft.
- Löschungen werden per Dialog bestätigt.
- Bei einem Konflikt bleibt die Serverversion am Originalpfad, die eigene landet
  als Konfliktnotiz unter `00-inbox/conflicts/`. Nichts wird still überschrieben.

## Hinweis zum Token

Obsidian bietet keine stabile SecretStorage-API, daher liegt das Gerätetoken in
`data.json` des Plugins innerhalb des Vaults. Es hat nur den `sync`-Scope, ist
an eine Geräte-ID gebunden und serverseitig widerrufbar — der Vault sollte
deshalb nicht in einem fremden Cloud-Ordner liegen.
