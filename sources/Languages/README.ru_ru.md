[简体中文](README.md) | [English](README.en_us.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# Справочник по Переводу

Добро пожаловать в проект по улучшению перевода Ling Player! Это руководство объясняет структуру файлов интернационализации проекта и способы внесения вклада в переводы.

---

## Структура Каталогов

```
Languages/
├── Main/                          # Строки основного приложения
│   ├── en_US.axaml                # Английский (США) — эталонная база
│   ├── zh_CN.axaml                # Упрощённый китайский
│   ├── zh_TW.axaml                # Традиционный китайский
│   ├── ja_JP.axaml                # Японский
│   ├── ko_KR.axaml                # Корейский
│   ├── de_DE.axaml                # Немецкий
│   ├── fr_FR.axaml                # Французский
│   ├── es_ES.axaml                # Испанский
│   ├── pt_BR.axaml                # Португальский (Бразилия)
│   ├── pl_PL.axaml                # Польский
│   ├── ru_RU.axaml                # Русский
│   ├── tr_TR.axaml                # Турецкий
│   └── en_GB.axaml                # Английский (Великобритания)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Плагин Steam
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (те же 13 языков, что и выше)
├── README.md                      # Этот файл
└── CONTRIBUTORS.md                # Участники перевода
```

## Формат Файлов

Языковые файлы используют формат XAML `ResourceDictionary` из [Avalonia UI](https://avaloniaui.net/):

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Комментарий категории  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — Уникальный идентификатор, используемый в коде для ссылки на эту строку. **НЕ изменять.**
- **Value** — Текстовое содержимое для перевода
- **x:Class** — Квалификатор пространства имён, формат: `{Namespace}.Languages.{locale_code}`

## Поддерживаемые Языки

| Код | Язык | Примечание |
|-----|------|------------|
| `en_US` | Английский (США) | **Эталонная база** |
| `zh_CN` | Упрощённый китайский | |
| `zh_TW` | Традиционный китайский | |
| `ja_JP` | Японский | |
| `ko_KR` | Корейский | |
| `de_DE` | Немецкий | |
| `fr_FR` | Французский | |
| `es_ES` | Испанский | |
| `pt_BR` | Португальский (Бразилия) | |
| `pl_PL` | Польский | |
| `ru_RU` | Русский | |
| `tr_TR` | Турецкий | |
| `en_GB` | Английский (Великобритания) | |

> **Примечание:** `en_US` является эталонной базой для переводов. Все переводы на другие языки должны основываться на ключах и семантике из `en_US.axaml`.

---

## Рекомендации по Переводу

### 1. Заполнители

Строки перевода могут содержать заполнители, такие как `{0}`, `{1}`, `{2}`, которые заменяются фактическими значениями во время выполнения. **Необходимо сохранять эти заполнители и их порядок.**

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

### 2. Переносы Строк

Используйте XML-сущность `&#xA;` для переносов строк:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

Приведённый выше текст будет отображаться в интерфейсе как:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Комментарии Категорий

Файлы организованы в разделы с помощью XML-комментариев `<!--  Category  -->` для удобства навигации. Сохраняйте эти комментарии в исходном порядке:

- `General` — Общий текст
- `Navigation` — Навигация / заголовки страниц
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — По модулям
- `Statistics` — Статистика
- `Plugin` — Плагин
- `Setting` — Настройки
- `Dialog` — Диалоги
- `MiniWindow` — Мини-окно
- `Tray menu` — Меню в трее
- `Options` — Параметры действий
- `Lyric` — Тексты песен
- `Playing` — Сейчас играет
- `Language` — Язык
- `Toast` — Всплывающие сообщения
- `Tips` — Подсказки
- `Notice` — Уведомления
- `Misc` — Разное

---

## Как Внести Вклад

### Улучшение Существующих Переводов

1. Найдите целевой языковой файл в каталоге `Main/` (например, `de_DE.axaml`)
2. Сравните его построчно с `en_US.axaml` (эталонным файлом)
3. Исправьте неточные или ошибочные переводы
4. Отправьте свои изменения через Pull Request на GitHub

### Добавление Нового Языка

1. Скопируйте `Main/en_US.axaml` в новый файл с именем в формате `{locale}_{region}.axaml` (например, `ar_SA.axaml`)
2. Обновите атрибут `x:Class`: `Ling.UI.Languages.{locale_region}`
3. Переведите все Values одно за другим, сохраняя Keys и заполнители без изменений
4. Добавьте отображаемое имя нового языка в блоке `Language` (например, `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Синхронизируйте каталоги плагинов:** Также скопируйте и переведите `en_US.axaml` в `Plugins/`
6. Отправьте PR

### Примечания по Переводу

- **НЕ изменяйте имена Key** — Keys являются уникальными идентификаторами, используемыми в коде
- **Сохраняйте заполнители** `{0}`, `{1}` и т.д. — не удаляйте и не меняйте их порядок
- **Сохраняйте структуру XML нетронутой** — не нарушайте закрытие тегов
- Для Keys со строками форматирования (например, `TrackBitRate` с `{0} Kbps`), переводите только текст единицы измерения, сохраняя формат

---

## Переводы Плагинов

Каждый плагин имеет собственный каталог переводов в `Plugins/`. Пример для плагина Steam:

- Каталог: `Plugins/Ling.Plugin.Steam/`
- Префикс пространства имён: `Ling.Plugin.Steam.Languages.{locale}`
- Содержит специфичные для плагина Keys, например, `SteamRichPresenceFormat`

Процесс добавления или улучшения переводов плагинов такой же, как и для основного приложения.

---

## Связанные Ссылки

- [Документация Avalonia UI](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [README Проекта](../../README.md)
