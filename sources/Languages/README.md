[English](README.en_us.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# 语言翻译参考

欢迎参与 Ling Player 的翻译改进工作！本文档将帮助你了解项目的国际化文件结构以及如何贡献翻译。

---

## 目录结构

```
Languages/
├── Main/                          # 主程序文本
│   ├── en_US.axaml                # 英语（美国）— 参考基准
│   ├── zh_CN.axaml                # 简体中文
│   ├── zh_TW.axaml                # 繁体中文
│   ├── ja_JP.axaml                # 日语
│   ├── ko_KR.axaml                # 韩语
│   ├── de_DE.axaml                # 德语
│   ├── fr_FR.axaml                # 法语
│   ├── es_ES.axaml                # 西班牙语
│   ├── pt_BR.axaml                # 葡萄牙语（巴西）
│   ├── pl_PL.axaml                # 波兰语
│   ├── ru_RU.axaml                # 俄语
│   ├── tr_TR.axaml                # 土耳其语
│   └── en_GB.axaml                # 英语（英国）
├── Plugins/
│   └── Ling.Plugin.Steam/         # Steam 插件
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ...（同上 13 种语言）
├── README.md                      # 本文件
└── CONTRIBUTORS.md                # 翻译贡献者名单
```

## 文件格式

语言文件使用 [Avalonia UI](https://avaloniaui.net/) 的 `ResourceDictionary` XAML 格式：

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  分类注释  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — 在代码中引用该文本的唯一标识符，**不可修改**
- **Value** — 需要翻译的文本内容
- **x:Class** — 命名空间限定，格式为 `{Namespace}.Languages.{locale_code}`

## 当前支持的语言

| 语言代码 | 语言 | Language |
|---------|------|----------|
| `en_US` | 英语（美国） | English (United States) — **基准语言** |
| `zh_CN` | 简体中文 | Simplified Chinese |
| `zh_TW` | 繁体中文 | Traditional Chinese |
| `ja_JP` | 日语 | Japanese |
| `ko_KR` | 韩语 | Korean |
| `de_DE` | 德语 | German |
| `fr_FR` | 法语 | French |
| `es_ES` | 西班牙语 | Spanish |
| `pt_BR` | 葡萄牙语（巴西） | Portuguese (Brazil) |
| `pl_PL` | 波兰语 | Polish |
| `ru_RU` | 俄语 | Russian |
| `tr_TR` | 土耳其语 | Turkish |
| `en_GB` | 英语（英国） | English (United Kingdom) |

> **注意：** `en_US` 是翻译的参考基准。所有其他语言的翻译均应以 `en_US.axaml` 的 Key 和语义为准。

---

## 翻译规范

### 1. 占位符

翻译文本中可能包含 `{0}`, `{1}`, `{2}` 等占位符，它们在运行时会替换为实际数值。**必须保留这些占位符及其顺序。**

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

### 2. 换行符

使用 XML 实体 `&#xA;` 表示换行：

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

以上文本在UI上将显示为：
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. 分类注释

文件通过 XML 注释 `<!--  Category  -->` 进行分块，便于定位。翻译时请保持这些注释与原始顺序一致：

- `General` — 通用文本
- `Navigation` — 导航/页面标题
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — 各模块
- `Statistics` — 统计
- `Plugin` — 插件
- `Setting` — 设置
- `Dialog` — 对话框
- `MiniWindow` — 迷你窗口
- `Tray menu` — 托盘菜单
- `Options` — 操作选项
- `Lyric` — 歌词
- `Playing` — 播放页面
- `Language` — 语言
- `Toast` — 提示消息
- `Tips` — 提示
- `Notice` — 公告
- `Misc` — 杂项

---

## 如何贡献

### 改进现有翻译

1. 在 `Main/` 目录中找到对应的语言文件（如 `de_DE.axaml`）
2. 参考 `en_US.axaml`（基准文件），逐行对比翻译
3. 修改不准确或错误的翻译
4. 通过 GitHub Pull Request 提交修改

### 新增语言

1. 复制 `Main/en_US.axaml` 为新文件，按 `{locale}_{region}.axaml` 格式命名（如 `ar_SA.axaml`）
2. 修改 `x:Class` 属性：`Ling.UI.Languages.{locale_region}`
3. 逐一翻译所有 Value，保留 Key 和占位符不变
4. 在 `Language` 分类块中添加新语言的显示名称（如 `<x:String x:Key="ar-SA">العربية</x:String>`）
5. **同步处理插件目录：** 同样复制并翻译 `Plugins/` 下的 `en_US.axaml`
6. 提交 PR

### 翻译注意事项

- **不要修改 Key 名称**，Key 是代码中引用文本的唯一标识
- **保留占位符** `{0}`, `{1}` 等，不要删除或调换顺序
- **保持 XML 结构完整**，不要破坏标签闭合
- **主程序和插件的翻译需同步**，如果修改了某个 Key 在 Main 中的翻译，请检查 Plugins 中是否需要同样处理
- 对于包含格式化说明的 Key（如 `TrackBitRate` 的 `{0} Kbps`），只需翻译单位文本，保留格式

---

## 插件翻译

每个插件在 `Plugins/` 下有独立的翻译目录。以 Steam 插件为例：

- 目录：`Plugins/Ling.Plugin.Steam/`
- 命名空间前缀：`Ling.Plugin.Steam.Languages.{locale}`
- 包含插件特有的 Key，如 `SteamRichPresenceFormat`

新增或改进插件翻译的流程与主程序相同。

---

## 相关链接

- [Avalonia UI 官方文档](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [项目 README](../../README.md)
