[简体中文](README.zh_cn.md) | [English](README.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md)

# Dokumentacja Tłumaczeń

Witamy w projekcie tłumaczeń Ling Player! Ten przewodnik wyjaśnia strukturę plików internacjonalizacji oraz sposób wnoszenia wkładu w tłumaczenia.

---

## Struktura Katalogów

```
Languages/
├── Main/                          # Ciągi głównej aplikacji
│   ├── en_US.axaml                # Angielski (USA) — baza referencyjna
│   ├── zh_CN.axaml                # Chiński uproszczony
│   ├── zh_TW.axaml                # Chiński tradycyjny
│   ├── ja_JP.axaml                # Japoński
│   ├── ko_KR.axaml                # Koreański
│   ├── de_DE.axaml                # Niemiecki
│   ├── fr_FR.axaml                # Francuski
│   ├── es_ES.axaml                # Hiszpański
│   ├── pt_BR.axaml                # Portugalski (Brazylia)
│   ├── pl_PL.axaml                # Polski
│   ├── ru_RU.axaml                # Rosyjski
│   ├── tr_TR.axaml                # Turecki
│   └── en_GB.axaml                # Angielski (Wielka Brytania)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Wtyczka Steam
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (te same 13 języków)
├── README.md                      # Ten plik
└── CONTRIBUTORS.md                # Współtwórcy tłumaczeń
```

## Format Plików

Pliki językowe używają formatu XAML `ResourceDictionary` z [Avalonia UI](https://avaloniaui.net/):

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Komentarz kategorii  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — Unikalny identyfikator używany w kodzie do odwoływania się do tego ciągu. **NIE modyfikować.**
- **Value** — Treść tekstowa do przetłumaczenia
- **x:Class** — Kwalifikator przestrzeni nazw, format: `{Namespace}.Languages.{locale_code}`

## Obsługiwane Języki

| Kod | Język | Uwaga |
|-----|-------|-------|
| `en_US` | Angielski (USA) | **Baza referencyjna** |
| `zh_CN` | Chiński uproszczony | |
| `zh_TW` | Chiński tradycyjny | |
| `ja_JP` | Japoński | |
| `ko_KR` | Koreański | |
| `de_DE` | Niemiecki | |
| `fr_FR` | Francuski | |
| `es_ES` | Hiszpański | |
| `pt_BR` | Portugalski (Brazylia) | |
| `pl_PL` | Polski | |
| `ru_RU` | Rosyjski | |
| `tr_TR` | Turecki | |
| `en_GB` | Angielski (Wielka Brytania) | |

> **Uwaga:** `en_US` jest bazą referencyjną dla tłumaczeń. Wszystkie tłumaczenia na inne języki powinny opierać się na kluczach i semantyce z `en_US.axaml`.

---

## Wytyczne Tłumaczenia

### 1. Symbole Zastępcze

Ciągi tłumaczeń mogą zawierać symbole zastępcze, takie jak `{0}`, `{1}`, `{2}`, które są zastępowane rzeczywistymi wartościami w czasie wykonywania. **Należy zachować te symbole zastępcze i ich kolejność.**

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

### 2. Znaki Nowej Linii

Użyj encji XML `&#xA;` dla znaków nowej linii:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

Powyższy tekst będzie wyświetlany w interfejsie jako:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Komentarze Kategorii

Pliki są zorganizowane w sekcje za pomocą komentarzy XML `<!--  Category  -->` dla łatwiejszej nawigacji. Zachowaj te komentarze w oryginalnej kolejności:

- `General` — Tekst ogólny
- `Navigation` — Nawigacja / tytuły stron
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — Specyficzne dla modułów
- `Statistics` — Statystyki
- `Plugin` — Wtyczka
- `Setting` — Ustawienia
- `Dialog` — Okna dialogowe
- `MiniWindow` — Mini okno
- `Tray menu` — Menu w zasobniku
- `Options` — Opcje akcji
- `Lyric` — Teksty piosenek
- `Playing` — Teraz odtwarzane
- `Language` — Język
- `Toast` — Powiadomienia toast
- `Tips` — Wskazówki
- `Notice` — Powiadomienia
- `Misc` — Różne

---

## Jak Współtworzyć

### Ulepszanie Istniejących Tłumaczeń

1. Znajdź docelowy plik językowy w katalogu `Main/` (np. `de_DE.axaml`)
2. Porównaj go linia po linii z `en_US.axaml` (plik referencyjny)
3. Popraw niedokładne lub błędne tłumaczenia
4. Prześlij swoje zmiany przez Pull Request na GitHub

### Dodawanie Nowego Języka

1. Skopiuj `Main/en_US.axaml` do nowego pliku w formacie `{locale}_{region}.axaml` (np. `ar_SA.axaml`)
2. Zaktualizuj atrybut `x:Class`: `Ling.UI.Languages.{locale_region}`
3. Przetłumacz wszystkie Values, zachowując Keys i symbole zastępcze bez zmian
4. Dodaj nazwę wyświetlaną nowego języka w bloku `Language` (np. `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Zsynchronizuj katalogi wtyczek:** Skopiuj i przetłumacz również `en_US.axaml` w `Plugins/`
6. Prześlij PR

### Uwagi Dotyczące Tłumaczenia

- **NIE modyfikuj nazw Key** — Keys to unikalne identyfikatory używane w kodzie
- **Zachowaj symbole zastępcze** `{0}`, `{1}` itp. — nie usuwaj ich ani nie zmieniaj kolejności
- **Utrzymuj strukturę XML w nienaruszonym stanie** — nie uszkadzaj zamknięć tagów
- Dla Keys z ciągami formatującymi (np. `TrackBitRate` z `{0} Kbps`), przetłumacz tylko tekst jednostki, zachowując format

---

## Tłumaczenia Wtyczek

Każda wtyczka ma własny katalog tłumaczeń w `Plugins/`. Przykład dla wtyczki Steam:

- Katalog: `Plugins/Ling.Plugin.Steam/`
- Prefiks przestrzeni nazw: `Ling.Plugin.Steam.Languages.{locale}`
- Zawiera Keys specyficzne dla wtyczki, np. `SteamRichPresenceFormat`

Proces dodawania lub ulepszania tłumaczeń wtyczek jest taki sam jak dla głównej aplikacji.

---

## Powiązane Linki

- [Dokumentacja Avalonia UI](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [README Projektu](../../README.md)
