# French Telex for Keyman

French Telex is a custom Keyman keyboard for typing French with Telex-like postfix rules on macOS, Windows, and Linux.

It is designed for people who already type with Vietnamese Telex muscle memory and want French accents without switching to a positional French layout such as Canadian CSA.

French version: [README.fr.md](/Users/kylepham/Code/keyman-french-telex/README.fr.md)

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

Typing a space inserts an invisible word-boundary marker. A custom backspace rule preserves that marker if you then delete the space again, so accent rules no longer modify the previous word.

Example:

- `a` then `space` then `backspace` then `s` -> `as`

## Double-Space Shortcuts

Some common shortcuts expand only when you press `space` twice after the shortcut. The first space keeps the shortcut literal; the second space commits the expansion, so it won't trigger inside a larger word.

- `c1` then `space` then `space` -> `c'est `
- `c2` then `space` then `space` -> `ce sont `
- `qcq` then `space` then `space` -> `qu'est-ce que `
- `ya` then `space` then `space` -> `il y a `
- `nya` then `space` then `space` -> `il n'y a `
- `qun` then `space` then `space` -> `quelqu'un `
- `qch` then `space` then `space` -> `quelque chose `

## Examples

- `eslesves` -> `élévé`
- `francwais` -> `français`
- `maiitre` -> `maître`
- `Noewl` -> `Noël`
- `hootel` -> `hôtel`

## Source

- Main Keyman source: `source/french_telex.kmn`
- Build command: `kmc build /Users/kylepham/Code/keyman-french-telex`
