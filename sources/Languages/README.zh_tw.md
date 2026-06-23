[简体中文](README.zh_cn.md) | [English](README.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md)

# 語言翻譯參考

歡迎參與 Ling Player 的翻譯專案！本文件將幫助你了解專案的國際化文件結構以及如何貢獻翻譯。

---

## 目錄結構

```
Languages/
├── Main/                          # 主程式文本
│   ├── en_US.axaml                # 英語（美國）— 參考基準
│   ├── zh_CN.axaml                # 簡體中文
│   ├── zh_TW.axaml                # 繁體中文
│   ├── ja_JP.axaml                # 日語
│   ├── ko_KR.axaml                # 韓語
│   ├── de_DE.axaml                # 德語
│   ├── fr_FR.axaml                # 法語
│   ├── es_ES.axaml                # 西班牙語
│   ├── pt_BR.axaml                # 葡萄牙語（巴西）
│   ├── pl_PL.axaml                # 波蘭語
│   ├── ru_RU.axaml                # 俄語
│   ├── tr_TR.axaml                # 土耳其語
│   └── en_GB.axaml                # 英語（英國）
├── Plugins/
│   └── Ling.Plugin.Steam/         # Steam 插件
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ...（同上 13 種語言）
├── README.md                      # 本文件
└── CONTRIBUTORS.md                # 翻譯貢獻者名單
```

## 文件格式

語言文件使用 [Avalonia UI](https://avaloniaui.net/) 的 `ResourceDictionary` XAML 格式：

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  分類註釋  -->
    <x:String x:Key="AppName">輕靈音樂</x:String>
    <x:String x:Key="Welcome">歡迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — 在程式碼中引用該文本的唯一識別碼，**不可修改**
- **Value** — 需要翻譯的文本內容
- **x:Class** — 命名空間限定，格式為 `{Namespace}.Languages.{locale_code}`

## 當前支援的語言

| 語言代碼 | 語言 | Language |
|---------|------|----------|
| `en_US` | 英語（美國） | English (United States) — **基準語言** |
| `zh_CN` | 簡體中文 | Simplified Chinese |
| `zh_TW` | 繁體中文 | Traditional Chinese |
| `ja_JP` | 日語 | Japanese |
| `ko_KR` | 韓語 | Korean |
| `de_DE` | 德語 | German |
| `fr_FR` | 法語 | French |
| `es_ES` | 西班牙語 | Spanish |
| `pt_BR` | 葡萄牙語（巴西） | Portuguese (Brazil) |
| `pl_PL` | 波蘭語 | Polish |
| `ru_RU` | 俄語 | Russian |
| `tr_TR` | 土耳其語 | Turkish |
| `en_GB` | 英語（英國） | English (United Kingdom) |

> **注意：** `en_US` 是翻譯的參考基準。所有其他語言的翻譯均應以 `en_US.axaml` 的 Key 和語義為準。

---

## 翻譯規範

### 1. 佔位符

翻譯文本中可能包含 `{0}`, `{1}`, `{2}` 等佔位符，它們在執行時會替換為實際數值。**必須保留這些佔位符及其順序。**

```
en_US:  "{0} track(s)"
zh_CN:  "{0}首歌曲"
```

```
en_US:  "Scanning tracks {0}"
zh_CN:  "正在掃描歌曲 {0}"
```

```
en_US:  "Parsing tracks {0}/{1}"
zh_CN:  "正在解析歌曲 {0}/{1}"
```

### 2. 換行符

使用 XML 實體 `&#xA;` 表示換行：

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

以上文本在 UI 上將顯示為：
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. 分類註釋

文件透過 XML 註釋 `<!--  Category  -->` 進行分塊，便於定位。翻譯時請保持這些註釋與原始順序一致：

- `General` — 通用文本
- `Navigation` — 導航/頁面標題
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — 各模組
- `Statistics` — 統計
- `Plugin` — 插件
- `Setting` — 設定
- `Dialog` — 對話框
- `MiniWindow` — 迷你視窗
- `Tray menu` — 托盤選單
- `Options` — 操作選項
- `Lyric` — 歌詞
- `Playing` — 播放頁面
- `Language` — 語言
- `Toast` — 提示訊息
- `Tips` — 提示
- `Notice` — 公告
- `Misc` — 雜項

---

## 如何貢獻

### 改進現有翻譯

1. 在 `Main/` 目錄中找到對應的語言文件（如 `de_DE.axaml`）
2. 參考 `en_US.axaml`（基準文件），逐行對比翻譯
3. 修改不準確或錯誤的翻譯
4. 透過 GitHub Pull Request 提交修改

### 新增語言

1. 複製 `Main/en_US.axaml` 為新文件，按 `{locale}_{region}.axaml` 格式命名（如 `ar_SA.axaml`）
2. 修改 `x:Class` 屬性：`Ling.UI.Languages.{locale_region}`
3. 逐一翻譯所有 Value，保留 Key 和佔位符不變
4. 在 `Language` 分類塊中新增語言的顯示名稱（如 `<x:String x:Key="ar-SA">العربية</x:String>`）
5. **同步處理插件目錄：** 同樣複製並翻譯 `Plugins/` 下的 `en_US.axaml`
6. 提交 PR

### 翻譯注意事項

- **不要修改 Key 名稱**，Key 是程式碼中引用文本的唯一識別碼
- **保留佔位符** `{0}`, `{1}` 等，不要刪除或調換順序
- **保持 XML 結構完整**，不要破壞標籤閉合
- 對於包含格式化說明的 Key（如 `TrackBitRate` 的 `{0} Kbps`），只需翻譯單位文本，保留格式

---

## 插件翻譯

每個插件在 `Plugins/` 下有獨立的翻譯目錄。以 Steam 插件為例：

- 目錄：`Plugins/Ling.Plugin.Steam/`
- 命名空間前綴：`Ling.Plugin.Steam.Languages.{locale}`
- 包含插件特有的 Key，如 `SteamRichPresenceFormat`

新增或改進插件翻譯的流程與主程式相同。

---

## 相關連結

- [Avalonia UI 官方文件](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [專案 README](../../README.md)
