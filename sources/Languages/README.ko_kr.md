[简体中文](README.zh_cn.md) | [English](README.md) | [繁體中文](README.zh_tw.md) | [日本語](README.ja_jp.md) | [Deutsch](README.de_de.md) | [Français](README.fr_fr.md) | [Español](README.es_es.md) | [Português](README.pt_br.md) | [Polski](README.pl_pl.md) | [Русский](README.ru_ru.md) | [Türkçe](README.tr_tr.md)

# 언어 번역 참조

Ling Player 번역 프로젝트에 참여해 주셔서 감사합니다! 이 가이드는 프로젝트의 국제화 파일 구조와 번역 기여 방법을 설명합니다.

---

## 디렉터리 구조

```
Languages/
├── Main/                          # 메인 애플리케이션 문자열
│   ├── en_US.axaml                # 영어(미국) — 참조 기준
│   ├── zh_CN.axaml                # 중국어 간체
│   ├── zh_TW.axaml                # 중국어 번체
│   ├── ja_JP.axaml                # 일본어
│   ├── ko_KR.axaml                # 한국어
│   ├── de_DE.axaml                # 독일어
│   ├── fr_FR.axaml                # 프랑스어
│   ├── es_ES.axaml                # 스페인어
│   ├── pt_BR.axaml                # 포르투갈어(브라질)
│   ├── pl_PL.axaml                # 폴란드어
│   ├── ru_RU.axaml                # 러시아어
│   ├── tr_TR.axaml                # 터키어
│   └── en_GB.axaml                # 영어(영국)
├── Plugins/
│   └── Ling.Plugin.Steam/         # Steam 플러그인
│       ├── en_US.axaml
│       ├── zh_CN.axaml
│       └── ... (위와 동일한 13개 언어)
├── README.md                      # 이 파일
└── CONTRIBUTORS.md                # 번역 기여자 목록
```

## 파일 형식

언어 파일은 [Avalonia UI](https://avaloniaui.net/)의 `ResourceDictionary` XAML 형식을 사용합니다:

```xml
<ResourceDictionary xmlns="https://github.com/avaloniaui"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                    x:Class="Ling.UI.Languages.zh_CN">
    <!--  카테고리 주석  -->
    <x:String x:Key="AppName">轻灵音乐</x:String>
    <x:String x:Key="Welcome">欢迎</x:String>
    ...
</ResourceDictionary>
```

- **Key** — 코드에서 이 문자열을 참조하는 고유 식별자입니다. **수정하지 마세요.**
- **Value** — 번역할 텍스트 내용
- **x:Class** — 네임스페이스 한정자, 형식: `{Namespace}.Languages.{locale_code}`

## 지원되는 언어

| 코드 | 언어 | 비고 |
|------|------|------|
| `en_US` | 영어(미국) | **참조 기준** |
| `zh_CN` | 중국어 간체 | |
| `zh_TW` | 중국어 번체 | |
| `ja_JP` | 일본어 | |
| `ko_KR` | 한국어 | |
| `de_DE` | 독일어 | |
| `fr_FR` | 프랑스어 | |
| `es_ES` | 스페인어 | |
| `pt_BR` | 포르투갈어(브라질) | |
| `pl_PL` | 폴란드어 | |
| `ru_RU` | 러시아어 | |
| `tr_TR` | 터키어 | |
| `en_GB` | 영어(영국) | |

> **참고:** `en_US`는 번역의 참조 기준입니다. 다른 모든 언어의 번역은 `en_US.axaml`의 키와 의미에 기반해야 합니다.

---

## 번역 가이드라인

### 1. 자리표시자

번역 문자열에는 `{0}`, `{1}`, `{2}`와 같은 자리표시자가 포함될 수 있습니다. 이들은 런타임에 실제 값으로 대체됩니다. **자리표시자와 그 순서를 반드시 유지해야 합니다.**

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

### 2. 줄바꿈

줄바꿈에는 XML 엔티티 `&#xA;`를 사용합니다:

```xml
<x:String x:Key="TransparencyEffectDesc">The effects will be applied to the main window and the mini window&#xA;Please note that some effects may not be supported on the current platform</x:String>
```

위 텍스트는 UI에서 다음과 같이 표시됩니다:
```
The effects will be applied to the main window and the mini window
Please note that some effects may not be supported on the current platform
```

### 3. 카테고리 주석

파일은 탐색을 쉽게 하기 위해 XML 주석 `<!--  Category  -->`로 섹션별로 구성되어 있습니다. 번역 시 이 주석을 원래 순서와 일치하게 유지하세요:

- `General` — 일반 텍스트
- `Navigation` — 내비게이션 / 페이지 제목
- `Track` / `Album` / `Artist` / `Playlist` / `Folder` — 모듈별
- `Statistics` — 통계
- `Plugin` — 플러그인
- `Setting` — 설정
- `Dialog` — 대화 상자
- `MiniWindow` — 미니 창
- `Tray menu` — 트레이 메뉴
- `Options` — 작업 옵션
- `Lyric` — 가사
- `Playing` — 재생 화면
- `Language` — 언어
- `Toast` — 토스트 메시지
- `Tips` — 팁
- `Notice` — 공지
- `Misc` — 기타

---

## 기여 방법

### 기존 번역 개선하기

1. `Main/` 디렉터리에서 대상 언어 파일을 찾습니다 (예: `de_DE.axaml`)
2. `en_US.axaml`(참조 파일)과 한 줄씩 비교합니다
3. 부정확하거나 잘못된 번역을 수정합니다
4. GitHub Pull Request로 변경 사항을 제출합니다

### 새로운 언어 추가하기

1. `Main/en_US.axaml`을 복사하여 `{locale}_{region}.axaml` 형식으로 이름을 지정합니다 (예: `ar_SA.axaml`)
2. `x:Class` 속성을 업데이트합니다: `Ling.UI.Languages.{locale_region}`
3. 모든 Value를 번역하고 Key와 자리표시자는 변경하지 않습니다
4. `Language` 카테고리 블록에 새 언어의 표시 이름을 추가합니다 (예: `<x:String x:Key="ar-SA">العربية</x:String>`)
5. **플러그인 디렉터리도 동기화:** `Plugins/` 아래의 `en_US.axaml`도 복사하여 번역합니다
6. PR을 제출합니다

### 번역 시 주의사항

- **Key 이름을 수정하지 마세요** — Key는 코드에서 사용되는 고유 식별자입니다
- **자리표시자를 유지하세요** `{0}`, `{1}` 등 — 삭제하거나 순서를 변경하지 마세요
- **XML 구조를 손상시키지 마세요** — 태그 닫힘을 확인하세요
- 형식 문자열이 포함된 Key(예: `TrackBitRate`의 `{0} Kbps`)는 단위 텍스트만 번역하고 형식은 유지하세요

---

## 플러그인 번역

각 플러그인은 `Plugins/` 아래에 자체 번역 디렉터리를 가집니다. Steam 플러그인 예시:

- 디렉터리: `Plugins/Ling.Plugin.Steam/`
- 네임스페이스 접두사: `Ling.Plugin.Steam.Languages.{locale}`
- 플러그인 고유 Key 포함 (예: `SteamRichPresenceFormat`)

플러그인 번역 추가 또는 개선 절차는 메인 프로그램과 동일합니다.

---

## 관련 링크

- [Avalonia UI 문서](https://docs.avaloniaui.net/)
- [GitHub Issues](https://github.com/lfeng1420/LingPlayer/issues)
- [프로젝트 README](../../README.md)
