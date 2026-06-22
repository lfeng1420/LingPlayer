[简体中文](README.md) | [English](README.en_us.md) | [繁體中文](README.zh_tw.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md) | [English (UK)](README.en_gb.md)

# 言語翻訳リファレンス

Ling Player の翻訳改善にご協力いただきありがとうございます！このガイドでは、プロジェクトの国際化ファイル構造と翻訳の貢献方法について説明します。

---

## ディレクトリ構造

```
Languages/
├── Main/                          # メインアプリケーションの文字列
│   ├── en_US.axaml                # 英語（米国）— リファレンスベース
│   ├── zh_CN.axaml                # 簡体字中国語
│   ├── zh_TW.axaml                # 繁体字中国語
│   ├── ja_JP.axaml                # 日本語
│   ├── ko_KR.axaml                # 韓国語
│   ├── de_DE.axaml                # ドイツ語
│   ├── fr_FR.axaml                # フランス語
│   ├── es_ES.axaml                # スペイン語
│   ├── pt_BR.axaml                # ポルトガル語（ブラジル）
│   ├── pl_PL.axaml                # ポーランド語
│   ├── ru_RU.axaml                # ロシア語
│   ├── tr_TR.axaml                # トルコ語
│   └── en_GB.axaml                # 英語（英国）
├── Plugins/
│   └── Ling.Plugin.Steam/         # Steam プラグイン
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ...（上記と同じ13言語）
├── README.md                      # このファイル
└── CONTRIBUTORS.md                # 翻訳貢献者リスト
```

## ファイル形式

言語ファイルは [Avalonia UI](https://avaloniaui.net/) の `ResourceDictionary` XAML 形式を使用します：

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  カテゴリコメント  -->
    <x:String x:Key="AppName">軽霊音楽</x:String>
    <x:String x:Key="Welcome">ようこそ</x:String>
    ...
</ResourceDictionary>
```

- **Key** — コード内でこの文字列を参照する一意の識別子。**変更しないでください。**
- **Value** — 翻訳対象のテキスト内容
- **x:Class** — 名前空間修飾子、形式：`{Namespace}.Languages.{locale_code}`

## サポートされている言語

| コード | 言語 | 備考 |
|--------|------|------|
| `en_US` | 英語（米国） | **リファレンスベース** |
| `zh_CN` | 簡体字中国語 | |
| `zh_TW` | 繁体字中国語 | |
| `ja_JP` | 日本語 | |
| `ko_KR` | 韓国語 | |
| `de_DE` | ドイツ語 | |
| `fr_FR` | フランス語 | |
| `es_ES` | スペイン語 | |
| `pt_BR` | ポルトガル語（ブラジル） | |
| `pl_PL` | ポーランド語 | |
| `ru_RU` | ロシア語 | |
| `tr_TR` | トルコ語 | |
| `en_GB` | 英語（英国） | |

> **注意：** `en_US` は翻訳のリファレンスベースです。他のすべての言語の翻訳は、`en_US.axaml` のキーと意味に基づいて行ってください。

---

## 翻訳ガイドライン

### 1. プレースホルダー

翻訳文字列には `{0}`, `{1}`, `{2}` などのプレースホルダーが含まれる場合があります。これらは実行時に実際の値に置き換えられます。**プレースホルダーとその順序を保持する必要があります。**

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

### 2. 改行

改行には XML エンティティ `&#xA;` を使用します：

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

上記のテキストは UI で次のように表示されます：
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. カテゴリコメント

ファイルは XML コメント `<!--  Category  -->` でセクション分けされており、ナビゲーションが容易です。翻訳時にはこれらのコメントを元の順序と一致させてください：

- `General` — 一般テキスト
- `Navigation` — ナビゲーション / ページタイトル
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — 各モジュール
- `Statistics` — 統計
- `Plugin` — プラグイン
- `Setting` — 設定
- `Dialog` — ダイアログ
- `MiniWindow` — ミニウィンドウ
- `Tray menu` — トレイメニュー
- `Options` — 操作オプション
- `Lyric` — 歌詞
- `Playing` — 再生画面
- `Language` — 言語
- `Toast` — トーストメッセージ
- `Tips` — ヒント
- `Notice` — 通知
- `Misc` — その他

---

## 貢献方法

### 既存の翻訳を改善する

1. `Main/` ディレクトリで対象の言語ファイルを探します（例：`de_DE.axaml`）
2. `en_US.axaml`（リファレンスファイル）と一行ずつ比較します
3. 不正確または誤った翻訳を修正します
4. GitHub Pull Request で変更を送信します

### 新しい言語を追加する

1. `Main/en_US.axaml` をコピーし、`{locale}_{region}.axaml` 形式で新しいファイル名を付けます（例：`ar_SA.axaml`）
2. `x:Class` 属性を更新します：`Ling.UI.Languages.{locale_region}`
3. すべての Value を翻訳し、Key とプレースホルダーは変更しません
4. `Language` カテゴリブロックに新しい言語の表示名を追加します（例：`<x:String x:Key="ar-SA">العربية</x:String>`）
5. **プラグインディレクトリも同期：** `Plugins/` 以下の `en_US.axaml` も同様にコピーして翻訳します
6. PR を送信します

### 翻訳時の注意事項

- **Key 名を変更しないでください** — Key はコード内で使用される一意の識別子です
- **プレースホルダーを保持してください** `{0}`, `{1}` など — 削除したり順序を変更したりしないでください
- **XML 構造を壊さないでください** — タグの閉じ忘れに注意
- フォーマット文字列を含む Key（例：`TrackBitRate` の `{0} Kbps`）は、単位テキストのみ翻訳し、フォーマットは保持してください

---

## プラグイン翻訳

各プラグインは `Plugins/` の下に独自の翻訳ディレクトリを持ちます。Steam プラグインの例：

- ディレクトリ：`Plugins/Ling.Plugin.Steam/`
- 名前空間プレフィックス：`Ling.Plugin.Steam.Languages.{locale}`
- プラグイン固有の Key を含みます（例：`SteamRichPresenceFormat`）

プラグイン翻訳の追加や改善の手順はメインプログラムと同じです。

---

## 関連リンク

- [Avalonia UI ドキュメント](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [プロジェクト README](../../README.md)
