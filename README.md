# Jetendard

This project is heavily inspired by
[Yeomil Mono](https://github.com/taevel02/yeomil-mono) and reuses much of its
implementation with minimal changes. Compared with
[Yeomil Mono](https://github.com/taevel02/yeomil-mono), Jetendard uses
JetBrainsMono Nerd Font Mono instead of
[Geist Mono](https://github.com/vercel/geist-font/tree/main/fonts/GeistMono)
and applies a `1.15` scale to
[Pretendard](https://github.com/orioncactus/pretendard). Slightly enlarging
Pretendard reduces unnecessary spacing around Korean glyphs, making Korean word
spacing feel more visually stable while improving the clarity and precision of
Hangul rendering.

Jetendard is a reproducible font build project that combines
[JetBrainsMono Nerd Font Mono](https://github.com/ryanoasis/nerd-fonts) with
[Pretendard](https://github.com/orioncactus/pretendard) Korean glyphs.

The generated family is named `Jetendard`. Latin glyphs, programming ligatures,
and Nerd Font symbols come from the ligature-enabled `JetBrainsMonoNerdFontMono`
files. Korean and CJK glyphs come from Pretendard and are fitted into exactly two
Latin monospace advances.

**Zed Editor (font size 13.5)**

![screenshot](assets/screeshots/screenshot-2026-07-06-at-3.38.07-pm.png)

**Unicode Box Drawing Example**
![screenshot](assets/screeshots/screenshot-2026-07-06-at-3.52.25-pm.png)

## Build

```bash
uv sync --all-groups
make download
make run
make test
```

`make run` builds the full 16-variant family. 

Generated files are written to:

- `fonts/ttf/Jetendard-*.ttf`
- `fonts/otf/Jetendard-*.otf`
- `fonts/webfont/Jetendard-*.woff2`
- `fonts/webfont/jetendard.css`

Generated outputs and upstream downloads are intentionally ignored by git.

## CLI

```bash
uv run jetendard --help
```

Important options:

- `--latin-dir`: directory containing `JetBrainsMonoNerdFontMono-*.ttf`
- `--cjk-dir`: directory containing `Pretendard-*.ttf`
- `--all`: build the full 16-variant matrix
- `--variants`: explicit output variants such as `Regular`, `Italic`, or `BoldItalic`
- `--weights`: weights to build; without `--styles`, this selects upright variants
- `--styles`: `normal`, `italic`, or both
- `--korean-italic-mode`: Korean/CJK policy for italic variants, currently `upright`
- `--korean-scale`: visual scale for Korean/CJK glyph fitting
- `--scale`: compatibility alias for `--korean-scale`

The default Korean scale is `1.15`.

Examples:

```bash
uv run jetendard --all
uv run jetendard --weights Regular Bold --styles normal italic
uv run jetendard --variants Regular Light Bold
```

## Variant Coverage

Jetendard builds every ligature-enabled `JetBrainsMonoNerdFontMono` Mono TTF
variant present in the pinned Nerd Fonts archive:

| Weight | Upright | Italic | Pretendard Korean/CJK source |
| --- | --- | --- | --- |
| Thin | `Jetendard-Thin` | `Jetendard-ThinItalic` | `Pretendard-Thin` |
| ExtraLight | `Jetendard-ExtraLight` | `Jetendard-ExtraLightItalic` | `Pretendard-ExtraLight` |
| Light | `Jetendard-Light` | `Jetendard-LightItalic` | `Pretendard-Light` |
| Regular | `Jetendard-Regular` | `Jetendard-Italic` | `Pretendard-Regular` |
| Medium | `Jetendard-Medium` | `Jetendard-MediumItalic` | `Pretendard-Medium` |
| SemiBold | `Jetendard-SemiBold` | `Jetendard-SemiBoldItalic` | `Pretendard-SemiBold` |
| Bold | `Jetendard-Bold` | `Jetendard-BoldItalic` | `Pretendard-Bold` |
| ExtraBold | `Jetendard-ExtraBold` | `Jetendard-ExtraBoldItalic` | `Pretendard-ExtraBold` |

Pretendard does not provide true static italic Korean/CJK fonts in the pinned
archive, so italic Jetendard variants use italic JetBrainsMono Latin glyphs and
upright Pretendard Korean/CJK glyphs. The generated font metadata and CSS still
identify those variants as italic.

## Scope

Jetendard only uses `JetBrainsMonoNerdFontMono`. It does not use
`JetBrainsMonoNerdFont`, `JetBrainsMonoNerdFontPropo`, or `JetBrainsMonoNL`
no-ligature variants. Because the base font is already Nerd Font patched, this
project does not run a second Nerd Fonts patching step.

`Pretendard-Black` is not built by default because the confirmed
`JetBrainsMonoNerdFontMono` archive does not contain a matching Black source.
The downloader also extracts `PretendardVariable.ttf` when available for future
custom-weight work.

## Visual Check Samples

Use the same renderer, point size, and line height when comparing Jetendard
against yeomil-mono or another monospace baseline:

```text
Jetendard 테스트 ABC abc 0123456789
가각간갇갈감갑값같꿇뷁힣
한글과 English가 섞인 source comment
if (상태 === "완료") return "성공";
ㄱㄴㄷㅏㅑㅓㅕㅗㅛㅜㅠㅡㅣ
（）［］｛｝，．：；！？
```

## Release Packaging

The build writes installable files under `fonts/ttf`, `fonts/otf`, and
`fonts/webfont`. Release archives can be prepared from those directories after a
manual visual pass confirms the default Korean scale across upright and italic
variants. The OTF files are OTF-compatible outputs using the same TrueType
outlines as the generated TTFs.

## License

Jetendard is distributed under the [SIL Open Font License 1.1](LICENSE). Review
the upstream JetBrains Mono, Nerd Fonts, Pretendard, and Yeomil Mono projects for
their full copyright and reserved-name notices.
