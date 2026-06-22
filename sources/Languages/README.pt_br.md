[简体中文](README.md) | [English](README.en_us.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# Referência de Tradução

Bem-vindo ao esforço de melhoria de tradução do Ling Player! Este guia explica a estrutura de arquivos de internacionalização do projeto e como contribuir com traduções.

---

## Estrutura de Diretórios

```
Languages/
├── Main/                          # Strings da aplicação principal
│   ├── en_US.axaml                # Inglês (EUA) — base de referência
│   ├── zh_CN.axaml                # Chinês simplificado
│   ├── zh_TW.axaml                # Chinês tradicional
│   ├── ja_JP.axaml                # Japonês
│   ├── ko_KR.axaml                # Coreano
│   ├── de_DE.axaml                # Alemão
│   ├── fr_FR.axaml                # Francês
│   ├── es_ES.axaml                # Espanhol
│   ├── pt_BR.axaml                # Português (Brasil)
│   ├── pl_PL.axaml                # Polonês
│   ├── ru_RU.axaml                # Russo
│   ├── tr_TR.axaml                # Turco
│   └── en_GB.axaml                # Inglês (Reino Unido)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Plugin Steam
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (mesmos 13 idiomas acima)
├── README.md                      # Este arquivo
└── CONTRIBUTORS.md                # Colaboradores da tradução
```

## Formato de Arquivo

Os arquivos de idioma usam o formato XAML `ResourceDictionary` do [Avalonia UI](https://avaloniaui.net/):

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Comentário de categoria  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — O identificador único usado no código para referenciar esta string. **NÃO modificar.**
- **Value** — O conteúdo de texto a ser traduzido
- **x:Class** — Qualificador de namespace, formato: `{Namespace}.Languages.{locale_code}`

## Idiomas Suportados

| Código | Idioma | Observação |
|--------|--------|------------|
| `en_US` | Inglês (EUA) | **Base de referência** |
| `zh_CN` | Chinês simplificado | |
| `zh_TW` | Chinês tradicional | |
| `ja_JP` | Japonês | |
| `ko_KR` | Coreano | |
| `de_DE` | Alemão | |
| `fr_FR` | Francês | |
| `es_ES` | Espanhol | |
| `pt_BR` | Português (Brasil) | |
| `pl_PL` | Polonês | |
| `ru_RU` | Russo | |
| `tr_TR` | Turco | |
| `en_GB` | Inglês (Reino Unido) | |

> **Observação:** `en_US` é a base de referência para as traduções. Todas as traduções para outros idiomas devem ser baseadas nas chaves e na semântica de `en_US.axaml`.

---

## Diretrizes de Tradução

### 1. Marcadores de Posição

As strings de tradução podem conter marcadores como `{0}`, `{1}`, `{2}`, que são substituídos por valores reais em tempo de execução. **Você deve preservar esses marcadores e sua ordem.**

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

### 2. Quebras de Linha

Use a entidade XML `&#xA;` para quebras de linha:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

O texto acima será exibido na interface como:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Comentários de Categoria

Os arquivos são organizados em seções usando comentários XML `<!--  Category  -->` para facilitar a navegação. Mantenha esses comentários na ordem original:

- `General` — Texto geral
- `Navigation` — Navegação / títulos de página
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — Específico do módulo
- `Statistics` — Estatísticas
- `Plugin` — Plugin
- `Setting` — Configurações
- `Dialog` — Diálogos
- `MiniWindow` — Mini janela
- `Tray menu` — Menu da bandeja
- `Options` — Opções de ação
- `Lyric` — Letras
- `Playing` — Reproduzindo
- `Language` — Idioma
- `Toast` — Mensagens toast
- `Tips` — Dicas
- `Notice` — Avisos
- `Misc` — Diversos

---

## Como Contribuir

### Melhorar Traduções Existentes

1. Localize o arquivo de idioma alvo no diretório `Main/` (ex. `de_DE.axaml`)
2. Compare linha por linha com `en_US.axaml` (o arquivo de referência)
3. Corrija traduções imprecisas ou incorretas
4. Envie suas alterações via Pull Request do GitHub

### Adicionar um Novo Idioma

1. Copie `Main/en_US.axaml` para um novo arquivo no formato `{locale}_{region}.axaml` (ex. `ar_SA.axaml`)
2. Atualize o atributo `x:Class`: `Ling.UI.Languages.{locale_region}`
3. Traduza todos os Values um por um, mantendo Keys e marcadores inalterados
4. Adicione o nome de exibição do novo idioma no bloco `Language` (ex. `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Sincronize os diretórios de plugins:** Copie e traduza também `en_US.axaml` em `Plugins/`
6. Envie um PR

### Notas de Tradução

- **NÃO modificar nomes de Key** — Keys são os identificadores únicos usados no código
- **Preserve os marcadores** `{0}`, `{1}`, etc. — não os exclua nem reordene
- **Mantenha a estrutura XML intacta** — não quebre os fechamentos de tags
- **As traduções do programa principal e dos plugins devem estar sincronizadas** — se você modificar a tradução de uma Key no Main, verifique se a mesma alteração é necessária nos Plugins
- Para Keys com strings de formatação (ex. `TrackBitRate` com `{0} Kbps`), traduza apenas o texto da unidade preservando o formato

---

## Traduções de Plugins

Cada plugin tem seu próprio diretório de tradução em `Plugins/`. Exemplo para o plugin Steam:

- Diretório: `Plugins/Ling.Plugin.Steam/`
- Prefixo de namespace: `Ling.Plugin.Steam.Languages.{locale}`
- Contém Keys específicas do plugin, ex. `SteamRichPresenceFormat`

O processo para adicionar ou melhorar traduções de plugins é o mesmo da aplicação principal.

---

## Links Relacionados

- [Documentação do Avalonia UI](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [README do Projeto](../../README.md)
