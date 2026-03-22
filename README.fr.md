# French Telex pour Keyman

French Telex est un clavier Keyman personnalisé pour taper le français avec des règles postfixées inspirées de Telex sur macOS, Windows et Linux.

Il s'adresse surtout aux personnes qui ont déjà la mémoire musculaire de la saisie vietnamienne Telex et qui veulent écrire les accents français sans passer à une disposition positionnelle comme Canadian CSA.

Version anglaise : [README.md](/Users/kylepham/Code/keyman-french-telex/README.md)

## Installation

1. Installez Keyman.
2. Ouvrez [build/french_telex.kmp](/Users/kylepham/Code/keyman-french-telex/build/french_telex.kmp).
3. Ajoutez `Keyman` comme source d'entrée dans macOS.
4. Sélectionnez `French Telex` dans le menu des claviers Keyman.

## Règles de saisie

- Accent aigu : `as es is os us` -> `á é í ó ú`
- Accent grave : `af ef uf` -> `à è ù`
- Accent circonflexe : `aa ee ii oo uu` -> `â ê î ô û`
- Tréma : `aw ew iw ow uw yw` -> `ä ë ï ö ü ÿ`
- Cédille : `cw` -> `ç`
- Ligatures : `o/` -> `œ`, `a/` -> `æ`

## Texte littéral

Pour conserver une suite littérale sans déclencher une règle, utilisez l'antislash :

- `a\s` -> `as`
- `e\s` -> `es`
- `c\w` -> `cw`

L'antislash est la seule règle d'échappement littérale. Cela évite les ambiguïtés dans les vrais mots français.

## Frontières de mot

Quand vous tapez un espace, le clavier insère un marqueur invisible de fin de mot. Si vous effacez ensuite cet espace avec `Backspace`, ce marqueur est conservé, ce qui empêche les règles d'accent de modifier rétroactivement le mot précédent.

Exemple :

- `a` puis `espace` puis `backspace` puis `s` -> `as`

## Exemples

- `eslesves` -> `élévé`
- `francwais` -> `français`
- `maiitre` -> `maître`
- `Noewl` -> `Noël`
- `hootel` -> `hôtel`

## Source

- Source principale Keyman : `source/french_telex.kmn`
- Commande de build : `kmc build /Users/kylepham/Code/keyman-french-telex`
