# Changelog

All notable changes to the **fro** theme are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

Nothing scheduled. Everything below was developed and checked on macOS — Windows and Linux have not been re-tested since the rewrite, so reports there are what I need next.

## [0.1.0] - 2026-09-25

The first release since the 2024 beta, and the first whose version describes the stylesheet rather than the intent. The file is a near-complete rewrite of the original (302 → 1569 lines), reorganised into 22 numbered sections and rebuilt around CSS custom properties: every rule reads from a token, so a colour scheme is a token block rather than a second copy of every selector.

### Added

- **Dark mode.** Follows the system appearance through `prefers-color-scheme` — nothing to click, nothing to keep in sync by hand. Only tokens are re-declared for the dark scheme, and `color-scheme` is set so native controls (scrollbars, form fields, tooltips) flip with the page instead of staying light.
- **Code highlight palette from [lig.nvim](https://github.com/0froq/lig.nvim).** Colour is given to four roles only — structure (green), action (orange), reference (blue) and a neutral ramp for everything else — so keywords, identifiers and properties stay out of the way of the code itself. Separate light, dark and print ramps, each derived from lig's own triad model.
- **Print and export styles.** Paper is pinned to a light, high-contrast ramp no matter what the system appearance is, so a dark editor cannot put white text on white paper. Decorative heading and blockquote marks are dropped, images keep their outline and lose their shadow, checkboxes print as outlined boxes with a dark tick, and fences, tables and callouts stay off page breaks. Exported HTML/PDF sheds the editor-only chrome the same way.
- **Task-list checkboxes.** Accent-filled box with an inline SVG tick, plus done/not-done text states — replacing Typora's default control, which read as a foreign widget on both schemes.
- **Callout text colours.** The five alert types (`note` / `tip` / `important` / `warning` / `caution`) keep their tinted background and gain a matching foreground token per scheme, so a `warning` on a dark page is no longer dark-on-dark.
- **Image treatment.** Every image gets an outline and a soft drop shadow, because screenshots are mostly white and otherwise vanish into a dark page. `<figure>` / `<figcaption>` are styled and centred — Typora has no caption syntax for images, so inline HTML is the only route.
- **Source code mode** (`#typora-source`) now matches the theme: headings, raw blocks, strings, comments and the active line all read from the same tokens.
- **Coverage for the parts the old theme skipped**: blockquote markers, footnote definitions and back-references, `kbd`, `mark`, `del`, superscript/subscript, tables and the column-resize popover, math blocks, mermaid panels, raw HTML blocks and `<details>`, search hits, focus and typewriter modes, the sidebar / outline / window chrome, and the code-fence language tooltip.
- `style-test.md`, a fixture that exercises every element the theme paints — the quickest way to check a change end to end.

### Changed

- Typographic constants (content width, base size, line height) are tokens, unchanged at `800px` / `14px` / `1.6` so documents do not reflow when you update.
- Colour literals in `:root` replaced by a named token set — surfaces, text ramp, borders, chrome hooks, syntax marks.
- Inline code and fences now sit on a translucent surface (`rgba(0, 0, 0, .05)` where the old theme hardcoded `#f7f7f7`), so the same block reads correctly on either scheme without a second rule.

### Fixed

- Five hardcoded colours in Typora's own stylesheets that ignored the theme and glared on a dark page: the footnote `[^` opener (`#C7C5C5`, no `var()` twin), the empty-footnote placeholder (`#ddd`), the footnotes wrapper (`#888`), block metadata rendered bold italic `#CCC`, and HTML comments shipped as 60%-opacity amber.
- Footnote definition markers floated apart because Typora parks the generated brackets at the box edges with `2ch`/`2.5ch` padding; they now flow, so `[^1] :` reads as one marker.

### Removed

- `@import url("https://fonts.googleapis.com/icon?family=Material+Icons")`, the first line of the old file. Nothing in the rewritten theme needs an icon font — the checkbox tick is an inline SVG and the remaining marks are plain characters — so the render-blocking request, and the offline blind spot that came with it, are gone.

## [0.1.0-beta] - 2024-02-07

The `v0.1.0-beta` tag points at a commit that holds nothing but the README — `docs.css` (renamed `fro.css` the same day) landed just after it. A light-only stylesheet of 302 lines: headings, blockquotes, inline code, YAML front matter, callout backgrounds, TOC and scrollbars, with its glyphs pulled from a remote Material Icons font.

[unreleased]: https://github.com/0froq/typora-fro/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/0froq/typora-fro/releases/tag/v0.1.0
[0.1.0-beta]: https://github.com/0froq/typora-fro/releases/tag/v0.1.0-beta
