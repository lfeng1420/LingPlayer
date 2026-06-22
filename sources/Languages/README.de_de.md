[简体中文](README.md) | [English](README.en_us.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# Sprachübersetzungsreferenz

Willkommen bei der Übersetzungsverbesserung von Ling Player! Dieser Leitfaden erklärt die i18n-Dateistruktur des Projekts und wie man Übersetzungen beitragen kann.

---

## Verzeichnisstruktur

```
Languages/
├── Main/                          # Hauptanwendungszeichenketten
│   ├── en_US.axaml                # Englisch (USA) — Referenzbasis
│   ├── zh_CN.axaml                # Vereinfachtes Chinesisch
│   ├── zh_TW.axaml                # Traditionelles Chinesisch
│   ├── ja_JP.axaml                # Japanisch
│   ├── ko_KR.axaml                # Koreanisch
│   ├── de_DE.axaml                # Deutsch
│   ├── fr_FR.axaml                # Französisch
│   ├── es_ES.axaml                # Spanisch
│   ├── pt_BR.axaml                # Portugiesisch (Brasilien)
│   ├── pl_PL.axaml                # Polnisch
│   ├── ru_RU.axaml                # Russisch
│   ├── tr_TR.axaml                # Türkisch
│   └── en_GB.axaml                # Englisch (UK)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Steam-Plugin
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (gleiche 13 Sprachen wie oben)
├── README.md                      # Diese Datei
└── CONTRIBUTORS.md                # Übersetzungsmitwirkende
```

## Dateiformat

Sprachdateien verwenden das [Avalonia UI](https://avaloniaui.net/) `ResourceDictionary` XAML-Format:

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Kategorie-Kommentar  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — Die eindeutige Kennung, die im Code verwendet wird, um auf diese Zeichenkette zu verweisen. **NICHT ändern.**
- **Value** — Der zu übersetzende Textinhalt
- **x:Class** — Namespace-Qualifizierer, Format: `{Namespace}.Languages.{locale_code}`

## Unterstützte Sprachen

| Code | Sprache | Hinweis |
|------|---------|---------|
| `en_US` | Englisch (USA) | **Referenzbasis** |
| `zh_CN` | Vereinfachtes Chinesisch | |
| `zh_TW` | Traditionelles Chinesisch | |
| `ja_JP` | Japanisch | |
| `ko_KR` | Koreanisch | |
| `de_DE` | Deutsch | |
| `fr_FR` | Französisch | |
| `es_ES` | Spanisch | |
| `pt_BR` | Portugiesisch (Brasilien) | |
| `pl_PL` | Polnisch | |
| `ru_RU` | Russisch | |
| `tr_TR` | Türkisch | |
| `en_GB` | Englisch (UK) | |

> **Hinweis:** `en_US` ist die Referenzbasis für Übersetzungen. Alle Übersetzungen in andere Sprachen sollten auf den Schlüsseln und der Semantik in `en_US.axaml` basieren.

---

## Übersetzungsrichtlinien

### 1. Platzhalter

Übersetzungszeichenketten können Platzhalter wie `{0}`, `{1}`, `{2}` enthalten, die zur Laufzeit durch tatsächliche Werte ersetzt werden. **Diese Platzhalter und ihre Reihenfolge müssen beibehalten werden.**

```
en_US:  "{0} track(s)"
zh_CN:  "{0}首歌曲"
```

```
en_US:  "Scanning tracks {0}"
zh_CN:  "正在扫描歌曲 {0}"
```

```
en_US:  "Parsing tracks {0}/{1}"
zh_CN:  "正在解析歌曲 {0}/{1}"
```

### 2. Zeilenumbrüche

Verwenden Sie die XML-Entität `&#xA;` für Zeilenumbrüche:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

Der obige Text wird in der Benutzeroberfläche wie folgt angezeigt:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Kategorie-Kommentare

Dateien sind mit XML-Kommentaren `<!--  Category  -->` in Abschnitte unterteilt, um die Navigation zu erleichtern. Bitte halten Sie diese Kommentare in der ursprünglichen Reihenfolge:

- `General` — Allgemeiner Text
- `Navigation` — Navigation / Seitentitel
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — Modulspezifisch
- `Statistics` — Statistik
- `Plugin` — Plugin
- `Setting` — Einstellungen
- `Dialog` — Dialoge
- `MiniWindow` — Mini-Fenster
- `Tray menu` — Taskleistenmenü
- `Options` — Aktionsoptionen
- `Lyric` — Liedtexte
- `Playing` — Wiedergabeansicht
- `Language` — Sprache
- `Toast` — Toast-Nachrichten
- `Tips` — Tipps
- `Notice` — Hinweise
- `Misc` — Verschiedenes

---

## Wie man beiträgt

### Bestehende Übersetzungen verbessern

1. Suchen Sie die entsprechende Sprachdatei im Verzeichnis `Main/` (z. B. `de_DE.axaml`)
2. Vergleichen Sie sie zeilenweise mit `en_US.axaml` (der Referenzdatei)
3. Korrigieren Sie ungenaue oder fehlerhafte Übersetzungen
4. Reichen Sie Ihre Änderungen über einen GitHub Pull Request ein

### Eine neue Sprache hinzufügen

1. Kopieren Sie `Main/en_US.axaml` in eine neue Datei mit dem Namensformat `{locale}_{region}.axaml` (z. B. `ar_SA.axaml`)
2. Aktualisieren Sie das `x:Class`-Attribut: `Ling.UI.Languages.{locale_region}`
3. Übersetzen Sie alle Values, wobei Keys und Platzhalter unverändert bleiben
4. Fügen Sie den Anzeigenamen der neuen Sprache im `Language`-Kategorieblock hinzu (z. B. `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Plugin-Verzeichnisse synchronisieren:** Kopieren und übersetzen Sie auch `en_US.axaml` unter `Plugins/`
6. Reichen Sie einen PR ein

### Hinweise zur Übersetzung

- **Key-Namen NICHT ändern** — Keys sind die eindeutigen Kennungen, die im Code verwendet werden
- **Platzhalter beibehalten** `{0}`, `{1}` usw. — nicht löschen oder umsortieren
- **XML-Struktur intakt halten** — Tag-Schließungen nicht beschädigen
- Bei Keys mit Formatierungszeichenfolgen (z. B. `TrackBitRate` mit `{0} Kbps`) nur den Einheitentext übersetzen und das Format beibehalten

---

## Plugin-Übersetzungen

Jedes Plugin hat ein eigenes Übersetzungsverzeichnis unter `Plugins/`. Beispiel für das Steam-Plugin:

- Verzeichnis: `Plugins/Ling.Plugin.Steam/`
- Namespace-Präfix: `Ling.Plugin.Steam.Languages.{locale}`
- Enthält pluginspezifische Keys, z. B. `SteamRichPresenceFormat`

Der Prozess zum Hinzufügen oder Verbessern von Plugin-Übersetzungen ist derselbe wie für die Hauptanwendung.

---

## Verwandte Links

- [Avalonia UI Dokumentation](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [Projekt-README](../../README.md)
