# French Telex for Keyman

French Telex is a custom Keyman keyboard for typing French with Telex-like postfix rules on macOS, Windows, and Linux.

It is designed for people who already type with Vietnamese Telex muscle memory and want French accents without switching to a positional French layout such as Canadian CSA.

## Install

1. Install Keyman.
2. Open [build/french_telex.kmp](/Users/kylepham/Code/keyman-french-telex/build/french_telex.kmp).
3. Add `Keyman` as an input source in macOS.
4. Select `French Telex` from the Keyman keyboard menu.

## Typing Rules

- Acute: `as es is os us` -> `á é í ó ú`
- Grave: `af ef uf` -> `à è ù`
- Circumflex: `aa ee ii oo uu` -> `â ê î ô û`
- Diaeresis: `aw ew iw ow uw yw` -> `ä ë ï ö ü ÿ`
- Cedilla: `cw` -> `ç`
- Ligatures: `o/` -> `œ`, `a/` -> `æ`

## Literal Text

Two ways to keep trigger sequences literal:

- Explicit escape with backslash: `a\s` -> `as`, `e\s` -> `es`, `c\w` -> `cw`

The backslash escape is the only literal-text rule. This avoids ambiguous cases in real French words.

## Word Boundaries

Typing a space inserts an invisible word-boundary marker. If you type `space`, then `backspace`, accent rules no longer modify the previous word.

Example:

- `a` then `space` then `backspace` then `s` -> `as`

## Examples

- `eslesves` -> `élévé`
- `francwais` -> `français`
- `maiitre` -> `maître`
- `Noewel` -> `Noël`
- `hootel` -> `hôtel`

## Source

- Main Keyman source: `source/french_telex.kmn`
- Build command: `kmc build /Users/kylepham/Code/keyman-french-telex`
