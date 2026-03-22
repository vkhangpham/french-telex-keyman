# French Telex for Keyman

This is a small Keyman rule set for typing French with a Vietnamese-Telex-like postfix style.

Files:

- `french_telex.kmn`: the keyboard source

Default mappings:

- `es` -> `é`
- `af` -> `à`
- `ef` -> `è`
- `uf` -> `ù`
- `aa` -> `â`
- `ee` -> `ê`
- `ii` -> `î`
- `oo` -> `ô`
- `uu` -> `û`
- `aw` -> `ä`
- `ew` -> `ë`
- `iw` -> `ï`
- `ow` -> `ö`
- `uw` -> `ü`
- `yw` -> `ÿ`
- `cc` -> `ç`
- `o/` -> `œ`
- `a/` -> `æ`

Literal escape:

- Prefix the trigger with `\` to keep it literal.
- `e\s` -> `es`
- `a\f` -> `af`
- `o\/` -> `o/`
- `c\c` -> `cc`
- `\\` -> `\`

Examples:

- `eslesves` -> `élévé`
- `franccais` -> `français`
- `garcon` stays `garcon`
- `maiitre` -> `maître`
- `hotel` stays `hotel`; `hôtel` is `hootel`

How to use on macOS:

1. Build this `.kmn` into a `.kmp` package with Keyman Developer or the Keyman compiler.
2. Install the package into Keyman.
3. Add `Keyman` as a macOS input source.
4. Select the `French Telex` keyboard from the Keyman menu.

Notes:

- Acute is intentionally limited to `e + s` to avoid too many false conversions like `as`, `is`, or `us`.
- Circumflex uses doubled vowels because that is the closest low-friction mapping to existing Telex muscle memory.
- Diaeresis uses `w`.
- A space inserts an invisible word-boundary marker. If you type `space`, then `backspace`, accent rules no longer modify the previous word. Example: `a` then `space` then `backspace` then `s` gives literal `as`, not an accented letter.
