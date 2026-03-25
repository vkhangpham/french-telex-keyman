# French Telex for Keyman

French Telex is a custom Keyman keyboard for typing French with Telex-like postfix rules on macOS, Windows, and Linux.

It is designed for people who already type with Vietnamese Telex muscle memory and want French accents without switching to a positional French layout such as Canadian CSA.

French version: [README.fr.md](/Users/kylepham/Code/keyman-french-telex/README.fr.md)

## Install

1. Install Keyman.
2. Download the latest `french_telex.kmp` from [GitHub Releases](https://github.com/vkhangpham/french-telex-keyman/releases/latest).
3. Open the downloaded `.kmp` package.
4. Add `Keyman` as an input source in macOS.
5. Select `French Telex` from the Keyman keyboard menu.

## Typing Rules

- Acute: `a1 e1 i1 o1 u1` -> `á é í ó ú`
- Grave: `a2 e2 u2` -> `à è ù`
- Circumflex: `aa ee ii oo uu` -> `â ê î ô û`
- Diaeresis: `a3 e3 i3 o3 u3 y3` -> `ä ë ï ö ü ÿ`
- Cedilla: `c1` -> `ç`
- Ligatures: `o4` -> `œ`, `a4` -> `æ`
- Quotes: `"` opens with `« ` at the start of text or after a space, and otherwise inserts ` »`

## Literal Text

Use an explicit escape with backslash to keep trigger sequences literal:

- `a\1` -> `a1`, `e\2` -> `e2`, `u\3` -> `u3`, `o\4` -> `o4`, `c\1` -> `c1`, `\"` -> `"`

The backslash escape is the only literal-text rule. This avoids ambiguous cases in real French words.

## Terminal Fallback

Some terminal apps do not give Keyman enough surrounding text to rewrite the previous character reliably. For those cases, French Telex also supports an explicit compose path after backslash:

- `\1a \1e \1i \1o \1u` -> `á é í ó ú`
- `\2a \2e \2u` -> `à è ù`
- `\5a \5e \5i \5o \5u \5y` -> `â ê î ô û ŷ`
- `\3a \3e \3i \3o \3u \3y` -> `ä ë ï ö ü ÿ`
- `\1c` -> `ç`
- `\4o` -> `œ`, `\4a` -> `æ`

This mode is intended as a compatibility fallback for apps such as Ghostty or Neovim. The usual postfix rules still work in compliant apps.

## Word Boundaries

Typing a space inserts an invisible word-boundary marker. A custom backspace rule preserves that marker if you then delete the space again, so accent rules no longer modify the previous word.

Example:

- `a` then `space` then `backspace` then `1` -> `a1`

## Double-Space Shortcuts

Some common shortcuts expand only when you press `space` twice after the shortcut. The first space keeps the shortcut literal; the second space commits the expansion, so it won't trigger inside a larger word.

- `qcq` then `space` then `space` -> `qu'est-ce que `
- `Qcq` then `space` then `space` -> `Qu'est-ce que `
- `ya` then `space` then `space` -> `il y a `
- `Ya` then `space` then `space` -> `Il y a `
- `nya` then `space` then `space` -> `il n'y a `
- `Nya` then `space` then `space` -> `Il n'y a `
- `qun` then `space` then `space` -> `quelqu'un `
- `Qun` then `space` then `space` -> `Quelqu'un `
- `qch` then `space` then `space` -> `quelque chose `
- `Qch` then `space` then `space` -> `Quelque chose `
- `yat` then `space` then `space` -> `y-a-t'il `
- `nyat` then `space` then `space` -> `n'y-a-t'il `
- `cest` then `space` then `space` -> `c'est `
- `ceso` then `space` then `space` -> `ce sont `
- `resto` then `space` then `space` -> `restaurant `
- `jen` then `space` then `space` -> `je ne `
- `p` then `space` then `space` -> `pas `

## Examples

- `e1le2ve` -> `élève`
- `garc1on` -> `garçon`
- `maiitre` -> `maître`
- `No3el` -> `Noël`
- `hootel` -> `hôtel`

## Source

- Main Keyman source: `source/french_telex.kmn`
- Customization and local build guide: [`CONTRIBUTING.md`](/Users/kylepham/Code/keyman-french-telex/CONTRIBUTING.md)
- Build command: `kmc build /Users/kylepham/Code/keyman-french-telex`
- Local build output is generated under `build/`
- Tagged releases publish `french_telex.kmp` and related artifacts to GitHub Releases via GitHub Actions
