# Customizing and Building French Telex

This repository is source-driven. If you want to add more typing rules or build your own `.kmp` package, edit the source files directly and rebuild from the repository root.

## Requirements

- Keyman Developer 18.x with the `kmc` command available on `PATH`
- A local clone of this repository

Check that the compiler is installed:

```bash
kmc --version
```

## Project Layout

- `source/french_telex.kmn`: keyboard rules
- `source/french_telex.kps`: package definition for the `.kmp`
- `source/readme.htm`: package readme shown by Keyman
- `source/welcome.htm`: package welcome page
- `README.md` and `README.fr.md`: repository documentation
- `french_telex.kpj`: Keyman project file used by `kmc build`
- `build/`: local compiler output

## Adding Rules

Edit [`source/french_telex.kmn`](/Users/kylepham/Code/keyman-french-telex/source/french_telex.kmn).

Useful patterns from the current keyboard:

- Simple postfix rule:

```kmn
'e' + 's' > U+00E9
'E' + 's' > U+00C9
'e' + 'S' > U+00C9
'E' + 'S' > U+00C9
```

- Output based on a store lookup:

```kmn
any(dia_base) + 'w' > index(dia_out,1)
any(dia_base) + 'W' > index(dia_out,1)
```

- Double-space shortcut that only expands at a word boundary:

```kmn
nul 'c' 'd' 'l' 't' deadkey(boundary) ' ' + ' ' > "cordialement" deadkey(boundary) ' '
notany(wordchars) 'c' 'd' 'l' 't' deadkey(boundary) ' ' + ' ' > context(1) "cordialement" deadkey(boundary) ' '
```

## Rule Design Notes

- Keyman rules are matched top to bottom. Put more specific rules before more general ones.
- If a new trigger character should be escapable with backslash, add it under the `deadkey(1)` escape rules near the top of the file.
- If a rule should only fire within a word, follow the existing direct postfix style such as `'e' + 's' > ...`.
- If a rule should only fire after a completed word or shortcut, reuse the existing `deadkey(boundary)` pattern instead of matching a raw space directly.
- Keep uppercase behavior explicit. The current keyboard usually defines lower, upper, and mixed-case variants instead of relying on a single rule.
- If you add characters that should count as part of a word, update `store(wordchars)`.

## Keep the Docs in Sync

If you change visible typing behavior, update the relevant docs in the same change:

- [`README.md`](/Users/kylepham/Code/keyman-french-telex/README.md)
- [`README.fr.md`](/Users/kylepham/Code/keyman-french-telex/README.fr.md)
- [`source/readme.htm`](/Users/kylepham/Code/keyman-french-telex/source/readme.htm)
- [`source/welcome.htm`](/Users/kylepham/Code/keyman-french-telex/source/welcome.htm) if the welcome text mentions the changed behavior
- [`HISTORY.md`](/Users/kylepham/Code/keyman-french-telex/HISTORY.md) for user-visible changes

If you rename files or add package assets, also update [`source/french_telex.kps`](/Users/kylepham/Code/keyman-french-telex/source/french_telex.kps).

## Build the Keyboard and Package

From the repository root, run:

```bash
kmc build /Users/kylepham/Code/keyman-french-telex
```

This uses [`french_telex.kpj`](/Users/kylepham/Code/keyman-french-telex/french_telex.kpj) and builds both:

- `build/french_telex.kmx`: compiled keyboard
- `build/french_telex.kmp`: installable package

The package definition in [`source/french_telex.kps`](/Users/kylepham/Code/keyman-french-telex/source/french_telex.kps) includes the compiled `.kmx`, the HTML docs, and the license file.

## Install Your Local Build

After a successful build, open:

```text
build/french_telex.kmp
```

Keyman will install the local package just like a release build.

## Validation Checklist

Before sharing a custom build:

- Run `kmc build /Users/kylepham/Code/keyman-french-telex`
- Test each new rule in Keyman
- Test literal escaping if you introduced a new trigger character
- Re-check examples in the README and package HTML

If the build fails, fix the source files first. The `.kps` package references `build/french_telex.kmx`, so package compilation depends on the keyboard compiling cleanly.
