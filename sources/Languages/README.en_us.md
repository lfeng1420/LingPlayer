[简体中文](README.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# Language Translation Reference

Welcome to the Ling Player translation improvement effort! This guide explains the i18n file structure and how to contribute translations.

---

## Directory Structure

```
Languages/
├── Main/                          # Main application strings
│   ├── en_US.axaml                # English (United States) — reference base
│   ├── zh_CN.axaml                # Simplified Chinese
│   ├── zh_TW.axaml                # Traditional Chinese
│   ├── ja_JP.axaml                # Japanese
│   ├── ko_KR.axaml                # Korean
│   ├── de_DE.axaml                # German
│   ├── fr_FR.axaml                # French
│   ├── es_ES.axaml                # Spanish
│   ├── pt_BR.axaml                # Portuguese (Brazil)
│   ├── pl_PL.axaml                # Polish
│   ├── ru_RU.axaml                # Russian
│   ├── tr_TR.axaml                # Turkish
│   └── en_GB.axaml                # English (United Kingdom)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Steam plugin
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (same 13 languages as above)
├── README.md                      # This file
└── CONTRIBUTORS.md                # Translation contributors
```

## File Format

Language files use the [Avalonia UI](https://avaloniaui.net/) `ResourceDictionary` XAML format:

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Category comment  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — The unique identifier used in code to reference this string. **Do NOT modify.**
- **Value** — The text content to be translated
- **x:Class** — Namespace qualifier, format: `{Namespace}.Languages.{locale_code}`

## Supported Languages

| Code | Language | Note |
|------|----------|------|
| `en_US` | English (United States) | **Reference base** |
| `zh_CN` | Simplified Chinese | |
| `zh_TW` | Traditional Chinese | |
| `ja_JP` | Japanese | |
| `ko_KR` | Korean | |
| `de_DE` | German | |
| `fr_FR` | French | |
| `es_ES` | Spanish | |
| `pt_BR` | Portuguese (Brazil) | |
| `pl_PL` | Polish | |
| `ru_RU` | Russian | |
| `tr_TR` | Turkish | |
| `en_GB` | English (United Kingdom) | |

> **Note:** `en_US` is the reference base for translations. All other language translations should be based on the keys and semantics in `en_US.axaml`.

---

## Translation Guidelines

### 1. Placeholders

Translation strings may contain placeholders like `{0}`, `{1}`, `{2}`, which are replaced with actual values at runtime. **You must preserve these placeholders and their order.**

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

### 2. Line Breaks

Use the XML entity `&#xA;` for line breaks:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

The above text will render in the UI as:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Category Comments

Files are organized into sections using XML comments `<!--  Category  -->` for easy navigation. Please keep these comments consistent with the original order:

- `General` — General text
- `Navigation` — Navigation / page titles
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — Module-specific
- `Statistics` — Statistics
- `Plugin` — Plugin
- `Setting` — Settings
- `Dialog` — Dialogs
- `MiniWindow` — Mini window
- `Tray menu` — Tray menu
- `Options` — Action options
- `Lyric` — Lyrics
- `Playing` — Playing
- `Language` — Language
- `Toast` — Toast messages
- `Tips` — Tips
- `Notice` — Notices
- `Misc` — Miscellaneous

---

## How to Contribute

### Improve Existing Translations

1. Locate the target language file in the `Main/` directory (e.g., `de_DE.axaml`)
2. Compare against `en_US.axaml` (the reference file) line by line
3. Correct inaccurate or erroneous translations
4. Submit your changes via GitHub Pull Request

### Add a New Language

1. Copy `Main/en_US.axaml` to a new file named in the format `{locale}_{region}.axaml` (e.g., `ar_SA.axaml`)
2. Update the `x:Class` attribute: `Ling.UI.Languages.{locale_region}`
3. Translate all Values one by one, keeping Keys and placeholders unchanged
4. Add the new language's display name in the `Language` category block (e.g., `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Sync plugin directories:** Also copy and translate `en_US.axaml` under `Plugins/`
6. Submit a PR

### Translation Notes

- **Do NOT modify Key names** — Keys are the unique identifiers used in code
- **Preserve placeholders** `{0}`, `{1}`, etc. — do not delete or reorder them
- **Keep XML structure intact** — do not break tag closures
- For Keys with formatting strings (e.g., `TrackBitRate` with `{0} Kbps`), only translate the unit text, preserving the format

---

## Plugin Translations

Each plugin has its own translation directory under `Plugins/`. Example for the Steam plugin:

- Directory: `Plugins/Ling.Plugin.Steam/`
- Namespace prefix: `Ling.Plugin.Steam.Languages.{locale}`
- Contains plugin-specific Keys, e.g., `SteamRichPresenceFormat`

The process for adding or improving plugin translations is the same as for the main application.

---

## Related Links

- [Avalonia UI Documentation](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [Project README](../../README.md)
