[简体中文](README.zh_cn.md) | [English](README.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [한국어](README.ko_kr.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md)

# Çeviri Referansı

Ling Player çeviri projesine hoş geldiniz! Bu kılavuz, projenin uluslararasılaştırma dosya yapısını ve çevirilere nasıl katkıda bulunabileceğinizi açıklar.

---

## Dizin Yapısı

```
Languages/
├── Main/                          # Ana uygulama metinleri
│   ├── en_US.axaml                # İngilizce (ABD) — referans temel
│   ├── zh_CN.axaml                # Basitleştirilmiş Çince
│   ├── zh_TW.axaml                # Geleneksel Çince
│   ├── ja_JP.axaml                # Japonca
│   ├── ko_KR.axaml                # Korece
│   ├── de_DE.axaml                # Almanca
│   ├── fr_FR.axaml                # Fransızca
│   ├── es_ES.axaml                # İspanyolca
│   ├── pt_BR.axaml                # Portekizce (Brezilya)
│   ├── pl_PL.axaml                # Lehçe
│   ├── ru_RU.axaml                # Rusça
│   ├── tr_TR.axaml                # Türkçe
│   └── en_GB.axaml                # İngilizce (Birleşik Krallık)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Steam eklentisi
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (yukarıdakiyle aynı 13 dil)
├── README.md                      # Bu dosya
└── CONTRIBUTORS.md                # Çeviri katkıda bulunanlar
```

## Dosya Formatı

Dil dosyaları [Avalonia UI](https://avaloniaui.net/) `ResourceDictionary` XAML formatını kullanır:

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  Kategori yorumu  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — Kodda bu metne başvurmak için kullanılan benzersiz tanımlayıcı. **Değiştirmeyin.**
- **Value** — Çevrilecek metin içeriği
- **x:Class** — Ad alanı niteleyicisi, format: `{Namespace}.Languages.{locale_code}`

## Desteklenen Diller

| Kod | Dil | Not |
|-----|-----|-----|
| `en_US` | İngilizce (ABD) | **Referans temel** |
| `zh_CN` | Basitleştirilmiş Çince | |
| `zh_TW` | Geleneksel Çince | |
| `ja_JP` | Japonca | |
| `ko_KR` | Korece | |
| `de_DE` | Almanca | |
| `fr_FR` | Fransızca | |
| `es_ES` | İspanyolca | |
| `pt_BR` | Portekizce (Brezilya) | |
| `pl_PL` | Lehçe | |
| `ru_RU` | Rusça | |
| `tr_TR` | Türkçe | |
| `en_GB` | İngilizce (BK) | |

> **Not:** `en_US` çeviriler için referans temeldir. Diğer tüm dillere yapılan çeviriler, `en_US.axaml` dosyasındaki anahtarlara ve anlama dayanmalıdır.

---

## Çeviri Yönergeleri

### 1. Yer Tutucular

Çeviri metinleri, çalışma zamanında gerçek değerlerle değiştirilen `{0}`, `{1}`, `{2}` gibi yer tutucular içerebilir. **Bu yer tutucuları ve sıralarını korumanız gerekir.**

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

### 2. Satır Sonları

Satır sonları için XML varlığı `&#xA;` kullanın:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

Yukarıdaki metin arayüzde şu şekilde görüntülenecektir:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. Kategori Yorumları

Dosyalar, kolay gezinme için `<!--  Category  -->` XML yorumları ile bölümlere ayrılmıştır. Bu yorumları orijinal sırayla tutun:

- `General` — Genel metin
- `Navigation` — Gezinme / sayfa başlıkları
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — Modüle özgü
- `Statistics` — İstatistikler
- `Plugin` — Eklenti
- `Setting` — Ayarlar
- `Dialog` — Diyaloglar
- `MiniWindow` — Mini pencere
- `Tray menu` — Tepsi menüsü
- `Options` — Eylem seçenekleri
- `Lyric` — Şarkı sözleri
- `Playing` — Şu an çalıyor
- `Language` — Dil
- `Toast` — Bildirim mesajları
- `Tips` — İpuçları
- `Notice` — Bildirimler
- `Misc` — Çeşitli

---

## Nasıl Katkıda Bulunulur

### Mevcut Çevirileri İyileştirme

1. `Main/` dizininde hedef dil dosyasını bulun (örn. `de_DE.axaml`)
2. `en_US.axaml` (referans dosya) ile satır satır karşılaştırın
3. Hatalı veya yanlış çevirileri düzeltin
4. Değişikliklerinizi GitHub Pull Request ile gönderin

### Yeni Bir Dil Ekleme

1. `Main/en_US.axaml` dosyasını `{locale}_{region}.axaml` formatında yeni bir dosyaya kopyalayın (örn. `ar_SA.axaml`)
2. `x:Class` özniteliğini güncelleyin: `Ling.UI.Languages.{locale_region}`
3. Tüm Value'ları tek tek çevirin, Key'leri ve yer tutucuları değiştirmeden bırakın
4. `Language` kategori bloğuna yeni dilin görünen adını ekleyin (örn. `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **Eklenti dizinlerini senkronize edin:** `Plugins/` altındaki `en_US.axaml` dosyasını da kopyalayıp çevirin
6. PR gönderin

### Çeviri Notları

- **Key adlarını değiştirmeyin** — Key'ler kodda kullanılan benzersiz tanımlayıcılardır
- **Yer tutucuları koruyun** `{0}`, `{1}` vb. — silmeyin veya sıralarını değiştirmeyin
- **XML yapısını bozmayın** — etiket kapanışlarını kırmayın
- Biçimlendirme dizeleri içeren Key'ler için (örn. `TrackBitRate` ile `{0} Kbps`), yalnızca birim metnini çevirin, formatı koruyun

---

## Eklenti Çevirileri

Her eklenti `Plugins/` altında kendi çeviri dizinine sahiptir. Steam eklentisi örneği:

- Dizin: `Plugins/Ling.Plugin.Steam/`
- Ad alanı öneki: `Ling.Plugin.Steam.Languages.{locale}`
- Eklentiye özgü Key'ler içerir, örn. `SteamRichPresenceFormat`

Eklenti çevirilerini ekleme veya iyileştirme süreci ana uygulama ile aynıdır.

---

## İlgili Bağlantılar

- [Avalonia UI Belgeleri](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [Proje README](../../README.md)
