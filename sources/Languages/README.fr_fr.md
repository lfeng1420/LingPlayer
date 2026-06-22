[简体中文](README.md) | [English](README.en_us.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# Référence de Traduction

Bienvenue dans l'effort d'amélioration des traductions de Ling Player ! Ce guide explique la structure des fichiers d'internationalisation du projet et comment contribuer aux traductions.

---

## Structure des Répertoires

```
Languages/
├── Main/                          # Chaînes de l'application principale
│   ├── en_US.axaml                # Anglais (États-Unis) — base de référence
│   ├── zh_CN.axaml                # Chinois simplifié
│   ├── zh_TW.axaml                # Chinois traditionnel
│   ├── ja_JP.axaml                # Japonais
│   ├── ko_KR.axaml                # Coréen
│   ├── de_DE.axaml                # Allemand
│   ├── fr_FR.axaml                # Français
│   ├── es_ES.axaml                # Espagnol
│   ├── pt_BR.axaml                # Portugais (Brésil)
│   ├── pl_PL.axaml                # Polonais
│   ├── ru_RU.axaml                # Russe
│   ├── tr_TR.axaml                # Turc
│   └── en_GB.axaml                # Anglais (Royaume-Uni)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Plugin Steam
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (mêmes 13 langues que ci-dessus)
├── README.md                      # Ce fichier
└── CONTRIBUTORS.md                # Contributeurs aux traductions
```

## Format de Fichier

Les fichiers de langue utilisent le format XAML `ResourceDictionary` d'[Avalonia UI](https://avaloniaui.net/) :

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Commentaire de catégorie  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — L'identifiant unique utilisé dans le code pour référencer cette chaîne. **NE PAS modifier.**
- **Value** — Le contenu textuel à traduire
- **x:Class** — Qualificatif d'espace de noms, format : `{Namespace}.Languages.{locale_code}`

## Langues Prises en Charge

| Code | Langue | Remarque |
|------|--------|----------|
| `en_US` | Anglais (États-Unis) | **Base de référence** |
| `zh_CN` | Chinois simplifié | |
| `zh_TW` | Chinois traditionnel | |
| `ja_JP` | Japonais | |
| `ko_KR` | Coréen | |
| `de_DE` | Allemand | |
| `fr_FR` | Français | |
| `es_ES` | Espagnol | |
| `pt_BR` | Portugais (Brésil) | |
| `pl_PL` | Polonais | |
| `ru_RU` | Russe | |
| `tr_TR` | Turc | |
| `en_GB` | Anglais (Royaume-Uni) | |

> **Remarque :** `en_US` est la base de référence pour les traductions. Toutes les traductions dans d'autres langues doivent être basées sur les clés et la sémantique de `en_US.axaml`.

---

## Règles de Traduction

### 1. Espaces Réservés

Les chaînes de traduction peuvent contenir des espaces réservés comme `{0}`, `{1}`, `{2}`, qui sont remplacés par des valeurs réelles à l'exécution. **Vous devez conserver ces espaces réservés et leur ordre.**

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

### 2. Sauts de Ligne

Utilisez l'entité XML `&#xA;` pour les sauts de ligne :

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

Le texte ci-dessus s'affichera dans l'interface comme suit :
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Commentaires de Catégorie

Les fichiers sont organisés en sections à l'aide de commentaires XML `<!--  Category  -->` pour faciliter la navigation. Veuillez conserver ces commentaires dans l'ordre d'origine :

- `General` — Texte général
- `Navigation` — Navigation / titres de page
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — Spécifique aux modules
- `Statistics` — Statistiques
- `Plugin` — Plugin
- `Setting` — Paramètres
- `Dialog` — Dialogues
- `MiniWindow` — Mini-fenêtre
- `Tray menu` — Menu de la barre d'état
- `Options` — Options d'action
- `Lyric` — Paroles
- `Playing` — Lecture en cours
- `Language` — Langue
- `Toast` — Messages toast
- `Tips` — Conseils
- `Notice` — Avis
- `Misc` — Divers

---

## Comment Contribuer

### Améliorer les Traductions Existantes

1. Localisez le fichier de langue cible dans le répertoire `Main/` (ex. `de_DE.axaml`)
2. Comparez-le ligne par ligne avec `en_US.axaml` (le fichier de référence)
3. Corrigez les traductions inexactes ou erronées
4. Soumettez vos modifications via une Pull Request GitHub

### Ajouter une Nouvelle Langue

1. Copiez `Main/en_US.axaml` dans un nouveau fichier nommé au format `{locale}_{region}.axaml` (ex. `ar_SA.axaml`)
2. Mettez à jour l'attribut `x:Class` : `Ling.UI.Languages.{locale_region}`
3. Traduisez toutes les Values une par une, en gardant les Keys et les espaces réservés inchangés
4. Ajoutez le nom d'affichage de la nouvelle langue dans le bloc de catégorie `Language` (ex. `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Synchronisez les répertoires de plugins :** Copiez et traduisez également `en_US.axaml` sous `Plugins/`
6. Soumettez une PR

### Notes de Traduction

- **NE PAS modifier les noms de Key** — Les Keys sont les identifiants uniques utilisés dans le code
- **Conservez les espaces réservés** `{0}`, `{1}`, etc. — ne les supprimez pas et ne les réorganisez pas
- **Gardez la structure XML intacte** — ne cassez pas les fermetures de balises
- Pour les Keys avec des chaînes de formatage (ex. `TrackBitRate` avec `{0} Kbps`), traduisez uniquement le texte de l'unité en conservant le format

---

## Traductions de Plugins

Chaque plugin possède son propre répertoire de traduction sous `Plugins/`. Exemple pour le plugin Steam :

- Répertoire : `Plugins/Ling.Plugin.Steam/`
- Préfixe d'espace de noms : `Ling.Plugin.Steam.Languages.{locale}`
- Contient des Keys spécifiques au plugin, ex. `SteamRichPresenceFormat`

Le processus d'ajout ou d'amélioration des traductions de plugins est le même que pour l'application principale.

---

## Liens Connexes

- [Documentation Avalonia UI](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [README du Projet](../../README.md)
