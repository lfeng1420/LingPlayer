[简体中文](README.md) | [English](README.en_us.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# Referencia de Traducción

¡Bienvenido al esfuerzo de mejora de traducción de Ling Player! Esta guía explica la estructura de archivos de internacionalización del proyecto y cómo contribuir con traducciones.

---

## Estructura de Directorios

```
Languages/
├── Main/                          # Cadenas de la aplicación principal
│   ├── en_US.axaml                # Inglés (EE. UU.) — base de referencia
│   ├── zh_CN.axaml                # Chino simplificado
│   ├── zh_TW.axaml                # Chino tradicional
│   ├── ja_JP.axaml                # Japonés
│   ├── ko_KR.axaml                # Coreano
│   ├── de_DE.axaml                # Alemán
│   ├── fr_FR.axaml                # Francés
│   ├── es_ES.axaml                # Español
│   ├── pt_BR.axaml                # Portugués (Brasil)
│   ├── pl_PL.axaml                # Polaco
│   ├── ru_RU.axaml                # Ruso
│   ├── tr_TR.axaml                # Turco
│   └── en_GB.axaml                # Inglés (Reino Unido)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Plugin Steam
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (mismos 13 idiomas que arriba)
├── README.md                      # Este archivo
└── CONTRIBUTORS.md                # Colaboradores de traducción
```

## Formato de Archivo

Los archivos de idioma utilizan el formato XAML `ResourceDictionary` de [Avalonia UI](https://avaloniaui.net/):

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Comentario de categoría  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — El identificador único utilizado en el código para referenciar esta cadena. **NO modificar.**
- **Value** — El contenido de texto a traducir
- **x:Class** — Calificador de espacio de nombres, formato: `{Namespace}.Languages.{locale_code}`

## Idiomas Soportados

| Código | Idioma | Nota |
|--------|--------|------|
| `en_US` | Inglés (EE. UU.) | **Base de referencia** |
| `zh_CN` | Chino simplificado | |
| `zh_TW` | Chino tradicional | |
| `ja_JP` | Japonés | |
| `ko_KR` | Coreano | |
| `de_DE` | Alemán | |
| `fr_FR` | Francés | |
| `es_ES` | Español | |
| `pt_BR` | Portugués (Brasil) | |
| `pl_PL` | Polaco | |
| `ru_RU` | Ruso | |
| `tr_TR` | Turco | |
| `en_GB` | Inglés (Reino Unido) | |

> **Nota:** `en_US` es la base de referencia para las traducciones. Todas las traducciones a otros idiomas deben basarse en las claves y la semántica de `en_US.axaml`.

---

## Directrices de Traducción

### 1. Marcadores de Posición

Las cadenas de traducción pueden contener marcadores como `{0}`, `{1}`, `{2}`, que se reemplazan con valores reales en tiempo de ejecución. **Debe conservar estos marcadores y su orden.**

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

### 2. Saltos de Línea

Use la entidad XML `&#xA;` para saltos de línea:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

El texto anterior se mostrará en la interfaz como:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Comentarios de Categoría

Los archivos están organizados en secciones usando comentarios XML `<!--  Category  -->` para facilitar la navegación. Mantenga estos comentarios en el orden original:

- `General` — Texto general
- `Navigation` — Navegación / títulos de página
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — Específico del módulo
- `Statistics` — Estadísticas
- `Plugin` — Plugin
- `Setting` — Configuración
- `Dialog` — Diálogos
- `MiniWindow` — Mini ventana
- `Tray menu` — Menú de bandeja
- `Options` — Opciones de acción
- `Lyric` — Letras
- `Playing` — Reproduciendo
- `Language` — Idioma
- `Toast` — Mensajes emergentes
- `Tips` — Consejos
- `Notice` — Avisos
- `Misc` — Misceláneo

---

## Cómo Contribuir

### Mejorar Traducciones Existentes

1. Localice el archivo de idioma objetivo en el directorio `Main/` (ej. `de_DE.axaml`)
2. Compárelo línea por línea con `en_US.axaml` (el archivo de referencia)
3. Corrija traducciones inexactas o erróneas
4. Envíe sus cambios mediante un Pull Request de GitHub

### Agregar un Nuevo Idioma

1. Copie `Main/en_US.axaml` a un nuevo archivo con el formato `{locale}_{region}.axaml` (ej. `ar_SA.axaml`)
2. Actualice el atributo `x:Class`: `Ling.UI.Languages.{locale_region}`
3. Traduzca todos los Values uno por uno, manteniendo Keys y marcadores sin cambios
4. Agregue el nombre de visualización del nuevo idioma en el bloque `Language` (ej. `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Sincronice los directorios de plugins:** Copie y traduzca también `en_US.axaml` bajo `Plugins/`
6. Envíe un PR

### Notas de Traducción

- **NO modificar los nombres de Key** — Las Keys son los identificadores únicos utilizados en el código
- **Conserve los marcadores** `{0}`, `{1}`, etc. — no los elimine ni reordene
- **Mantenga la estructura XML intacta** — no rompa los cierres de etiquetas
- **Las traducciones del programa principal y los plugins deben estar sincronizadas** — si modifica la traducción de una Key en Main, verifique si se necesita el mismo cambio en Plugins
- Para Keys con cadenas de formato (ej. `TrackBitRate` con `{0} Kbps`), traduzca solo el texto de la unidad conservando el formato

---

## Traducciones de Plugins

Cada plugin tiene su propio directorio de traducción bajo `Plugins/`. Ejemplo para el plugin Steam:

- Directorio: `Plugins/Ling.Plugin.Steam/`
- Prefijo de espacio de nombres: `Ling.Plugin.Steam.Languages.{locale}`
- Contiene Keys específicas del plugin, ej. `SteamRichPresenceFormat`

El proceso para agregar o mejorar traducciones de plugins es el mismo que para la aplicación principal.

---

## Enlaces Relacionados

- [Documentación de Avalonia UI](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [README del Proyecto](../../README.md)
