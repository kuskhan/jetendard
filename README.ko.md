# Jetendard

[English](README.md)

이 프로젝트는 [Yeomil Mono](https://github.com/taevel02/yeomil-mono)에 큰
영향을 받았으며, 구현의 상당 부분을 최소한의 변경만 거쳐 재사용합니다.
[Yeomil Mono](https://github.com/taevel02/yeomil-mono)와 비교했을 때
Jetendard는 [Geist Mono](https://github.com/vercel/geist-font/tree/main/fonts/GeistMono)
대신 JetBrainsMono Nerd Font Mono를 사용하고,
[Pretendard](https://github.com/orioncactus/pretendard)에 `1.15` 배율을
적용합니다. Pretendard를 살짝 확대하면 한글 글리프 주변의 불필요한 여백을
줄일 수 있어, 한글 띄어쓰기가 시각적으로 더 안정적으로 느껴지고 한글 렌더링의
선명도와 정확성도 향상됩니다.

Jetendard는
[JetBrainsMono Nerd Font Mono](https://github.com/ryanoasis/nerd-fonts)와
[Pretendard](https://github.com/orioncactus/pretendard) 한글 글리프를 결합하여
폰트를 빌드하는 프로젝트입니다.

생성되는 폰트 패밀리의 이름은 `Jetendard`입니다. 라틴 글리프, 프로그래밍
리거처, Nerd Font 심볼은 리거처가 활성화된 `JetBrainsMonoNerdFontMono`
파일에서 가져옵니다. 한글 및 CJK 글리프는 Pretendard에서 가져오며, 라틴 문자
고정폭의 정확히 두 배 폭에 맞춰집니다.

**Zed 에디터 (폰트 사이즈 13.5)**

![예시 스크린샷](assets/screeshots/screenshot-2026-07-06-at-3.38.07-pm.png)

**유니코드 박스 드로잉 예시**
![예시 스크린샷](assets/screeshots/screenshot-2026-07-06-at-3.52.25-pm.png)

## 빌드

```bash
uv sync --all-groups
make download
make run
make test
```

`make run`은 전체 16개 변형 패밀리를 빌드합니다. 

생성된 파일은 다음 위치에 기록됩니다.

- `fonts/ttf/Jetendard-*.ttf`
- `fonts/otf/Jetendard-*.otf`
- `fonts/webfont/Jetendard-*.woff2`
- `fonts/webfont/jetendard.css`

생성 결과물과 업스트림 다운로드 파일은 의도적으로 git에서 무시됩니다.

## CLI

```bash
uv run jetendard --help
```

주요 옵션:

- `--latin-dir`: `JetBrainsMonoNerdFontMono-*.ttf`가 들어 있는 디렉터리
- `--cjk-dir`: `Pretendard-*.ttf`가 들어 있는 디렉터리
- `--all`: 전체 16개 변형 매트릭스 빌드
- `--variants`: `Regular`, `Italic`, `BoldItalic`처럼 출력 변형을 명시
- `--weights`: 빌드할 굵기. `--styles`가 없으면 upright 변형을 선택
- `--styles`: `normal`, `italic`, 또는 둘 다
- `--korean-italic-mode`: italic 변형에서 한글/CJK를 처리하는 정책. 현재는 `upright`
- `--korean-scale`: 한글/CJK 글리프 맞춤에 사용할 시각적 배율
- `--scale`: `--korean-scale`의 호환성 별칭

기본 한글 배율은 `1.15`입니다.

예시:

```bash
uv run jetendard --all
uv run jetendard --weights Regular Bold --styles normal italic
uv run jetendard --variants Regular Light Bold
```

## 변형 지원 범위

Jetendard는 고정된 Nerd Fonts 아카이브에 포함된, 리거처가 활성화된 모든
`JetBrainsMonoNerdFontMono` Mono TTF 변형을 빌드합니다.

| 굵기 | Upright | Italic | Pretendard 한글/CJK 소스 |
| --- | --- | --- | --- |
| Thin | `Jetendard-Thin` | `Jetendard-ThinItalic` | `Pretendard-Thin` |
| ExtraLight | `Jetendard-ExtraLight` | `Jetendard-ExtraLightItalic` | `Pretendard-ExtraLight` |
| Light | `Jetendard-Light` | `Jetendard-LightItalic` | `Pretendard-Light` |
| Regular | `Jetendard-Regular` | `Jetendard-Italic` | `Pretendard-Regular` |
| Medium | `Jetendard-Medium` | `Jetendard-MediumItalic` | `Pretendard-Medium` |
| SemiBold | `Jetendard-SemiBold` | `Jetendard-SemiBoldItalic` | `Pretendard-SemiBold` |
| Bold | `Jetendard-Bold` | `Jetendard-BoldItalic` | `Pretendard-Bold` |
| ExtraBold | `Jetendard-ExtraBold` | `Jetendard-ExtraBoldItalic` | `Pretendard-ExtraBold` |

Pretendard는 고정된 아카이브에서 true static italic 한글/CJK 폰트를 제공하지
않습니다. 따라서 italic Jetendard 변형은 italic JetBrainsMono 라틴 글리프와
upright Pretendard 한글/CJK 글리프를 함께 사용합니다. 생성된 폰트 메타데이터와
CSS에서는 해당 변형을 여전히 italic으로 식별합니다.

## 범위

Jetendard는 `JetBrainsMonoNerdFontMono`만 사용합니다.
`JetBrainsMonoNerdFont`, `JetBrainsMonoNerdFontPropo`, 또는 리거처가 없는
`JetBrainsMonoNL` 변형은 사용하지 않습니다. 기본 폰트가 이미 Nerd Font 패치가
적용된 상태이므로, 이 프로젝트는 두 번째 Nerd Fonts 패치 단계를 실행하지
않습니다.

`Pretendard-Black`은 기본으로 빌드되지 않습니다. 확인된
`JetBrainsMonoNerdFontMono` 아카이브에 대응되는 Black 소스가 없기 때문입니다.
다운로더는 향후 커스텀 굵기 작업을 위해 사용 가능한 경우 `PretendardVariable.ttf`도
추출합니다.

## 시각 확인 샘플

Jetendard를 yeomil-mono 또는 다른 고정폭 기준 폰트와 비교할 때는 동일한
렌더러, 포인트 크기, 줄 높이를 사용하세요.

```text
Jetendard 테스트 ABC abc 0123456789
가각간갇갈감갑값같꿇뷁힣
한글과 English가 섞인 source comment
if (상태 === "완료") return "성공";
ㄱㄴㄷㅏㅑㅓㅕㅗㅛㅜㅠㅡㅣ
（）［］｛｝，．：；！？
```

## 릴리스 패키징

빌드는 설치 가능한 파일을 `fonts/ttf`, `fonts/otf`, `fonts/webfont` 아래에
기록합니다. upright 및 italic 변형 전반에서 기본 한글 배율을 수동으로 시각
확인한 뒤, 해당 디렉터리에서 릴리스 아카이브를 준비할 수 있습니다. OTF 파일은
생성된 TTF와 동일한 TrueType outline을 사용하는 OTF 호환 출력물입니다.

## 라이선스

Jetendard는 [SIL Open Font License 1.1](LICENSE)에 따라 배포됩니다. 전체
저작권 및 reserved name 고지는 업스트림 JetBrains Mono, Nerd Fonts,
Pretendard, Yeomil Mono 프로젝트를 확인하세요.
