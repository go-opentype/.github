<p align="center"><img src="https://raw.githubusercontent.com/go-opentype/brand/main/social/go-opentype.png" alt="go-opentype" width="640"></p>

<h1 align="center">go-opentype</h1>
<p align="center"><strong>Pure-Go, zero-dependency TrueType/OpenType text stack.</strong></p>

<p align="center">
  🌐 <a href="https://go-opentype.github.io">Website</a> ·
  📚 <a href="https://go-opentype.github.io/docs/">Documentation</a>
</p>

<p align="center">
  <a href="https://go-opentype.github.io/docs/"><img alt="Docs" src="https://img.shields.io/badge/docs-mkdocs--material-B45309?style=flat-square"></a>
  <a href="https://github.com/go-opentype/opentype/blob/main/LICENSE"><img alt="License: BSD-3-Clause" src="https://img.shields.io/badge/license-BSD--3--Clause-blue?style=flat-square"></a>
  <img alt="Go 1.26.4+" src="https://img.shields.io/badge/go-1.26.4%2B-00ADD8?style=flat-square&logo=go&logoColor=white">
  <img alt="Coverage 100%" src="https://img.shields.io/badge/coverage-100%25-1a7f37?style=flat-square">
</p>

---

go-opentype is a family of **pure-Go, `CGO_ENABLED=0`, standard-library-only**
packages that together read a font file, resolve Unicode bidirectional and
complex-script text, and rasterise the result — with **no
`golang.org/x/*`** anywhere in the stack. It exists to functionally replace,
for a Go program that blits glyphs into a pixel buffer, the narrow slice of
`golang.org/x/image/font` a glyph-blitting UI needs, and
`golang.org/x/text/unicode/bidi` for mixed-direction text. The long-term aim
on the paths it covers is functional parity with the HarfBuzz + FreeType
pair.

## Repositories

| Repo | What it is |
|------|------------|
| [**opentype**](https://github.com/go-opentype/opentype) | the engine — sfnt parsing (`cmap`, `glyf` TrueType outlines) + anti-aliased rasterisation via 4×4 supersampling |
| [**bidi**](https://github.com/go-opentype/bidi) | the Unicode Bidirectional Algorithm (UAX #9), stdlib-only, no `x/text` |
| [**shape**](https://github.com/go-opentype/shape) | a HarfBuzz-lite complex-text shaper: Arabic cursive joining, ligatures, mark attachment, kerning, visual order |
| [**fonts**](https://github.com/go-opentype/fonts) | six bundled, legible, `go:embed`ded font families (Atkinson Hyperlegible default) |
| [**docs**](https://github.com/go-opentype/docs) | this documentation site (MkDocs Material, versioned with mike) |
| [**brand**](https://github.com/go-opentype/brand) | logo and brand assets |

## Principles

- **Pure Go, zero cgo, zero third-party dependencies.** Cross-compiles and
  embeds anywhere Go runs, including `GOOS=js GOARCH=wasm` — no C toolchain,
  no vendored assets, no runtime fetch.
- **Honest about scope.** Each repo's support matrix says plainly what's
  implemented and what's roadmap — CFF/CFF2 outlines, full GSUB/GPOS,
  hinting, vertical metrics and OpenType Variations (variable fonts) are
  tracked as future work, not claimed as done.
- **Conformance-tested.** `bidi` validates against the entire Unicode
  `BidiCharacterTest.txt`; `opentype` and `shape` synthesise fonts in
  memory so their test suites never depend on an external `.ttf`.
- **100% test coverage** is the target, enforced as a CI gate, green across
  6 arches plus `js/wasm`, `darwin/arm64` and `windows/amd64`.

## Status

`opentype` parses and rasterises TrueType `glyf` outlines (phase 1); `bidi`
implements UAX #9 through rule L2 with full conformance-test coverage;
`shape` composes both into Arabic and Latin/default complex-text shaping;
`fonts` bundles six OFL/BSD-licensed families. 100% coverage, CI green
across 6 arches.

BSD-3-Clause.
