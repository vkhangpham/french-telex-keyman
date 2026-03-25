# French Telex pour Keyman

French Telex est un clavier Keyman personnalisé pour taper le français avec des règles postfixées inspirées de Telex sur macOS, Windows et Linux.

Il s'adresse surtout aux personnes qui ont déjà la mémoire musculaire de la saisie vietnamienne Telex et qui veulent écrire les accents français sans passer à une disposition positionnelle comme Canadian CSA.

Version anglaise : [README.md](/Users/kylepham/Code/keyman-french-telex/README.md)

## Installation

1. Installez Keyman.
2. Téléchargez le fichier `french_telex.kmp` le plus récent depuis [GitHub Releases](https://github.com/vkhangpham/french-telex-keyman/releases/latest).
3. Ouvrez le paquet `.kmp` téléchargé.
4. Ajoutez `Keyman` comme source d'entrée dans macOS.
5. Sélectionnez `French Telex` dans le menu des claviers Keyman.

## Règles de saisie

- Accent aigu : `a1 e1 i1 o1 u1` -> `á é í ó ú`
- Accent grave : `a2 e2 u2` -> `à è ù`
- Accent circonflexe : `aa ee ii oo uu` -> `â ê î ô û`
- Tréma : `a3 e3 i3 o3 u3 y3` -> `ä ë ï ö ü ÿ`
- Cédille : `c1` -> `ç`
- Ligatures : `o4` -> `œ`, `a4` -> `æ`
- Guillemets : `"` ouvre `« ` en début de texte ou après un espace, sinon insère ` »`

## Texte littéral

Pour conserver une suite littérale sans déclencher une règle, utilisez l'antislash :

- `a\1` -> `a1`
- `e\2` -> `e2`
- `u\3` -> `u3`
- `o\4` -> `o4`
- `c\1` -> `c1`
- `\"` -> `"`

L'antislash est la seule règle d'échappement littérale. Cela évite les ambiguïtés dans les vrais mots français.

## Frontières de mot

Quand vous tapez un espace, le clavier insère un marqueur invisible de fin de mot. Si vous effacez ensuite cet espace avec `Backspace`, ce marqueur est conservé, ce qui empêche les règles d'accent de modifier rétroactivement le mot précédent.

Exemple :

- `a` puis `espace` puis `backspace` puis `1` -> `a1`

## Raccourcis par double espace

Certains raccourcis courants ne s'étendent qu'après deux frappes sur `espace`. Le premier espace laisse le raccourci tel quel ; le second valide l'expansion, ce qui évite un déclenchement au milieu d'un mot plus long.

- `qcq` puis `espace` puis `espace` -> `qu'est-ce que `
- `Qcq` puis `espace` puis `espace` -> `Qu'est-ce que `
- `ya` puis `espace` puis `espace` -> `il y a `
- `Ya` puis `espace` puis `espace` -> `Il y a `
- `nya` puis `espace` puis `espace` -> `il n'y a `
- `Nya` puis `espace` puis `espace` -> `Il n'y a `
- `qun` puis `espace` puis `espace` -> `quelqu'un `
- `Qun` puis `espace` puis `espace` -> `Quelqu'un `
- `qch` puis `espace` puis `espace` -> `quelque chose `
- `Qch` puis `espace` puis `espace` -> `Quelque chose `
- `yat` puis `espace` puis `espace` -> `y-a-t'il `
- `nyat` puis `espace` puis `espace` -> `n'y-a-t'il `
- `cest` puis `espace` puis `espace` -> `c'est `
- `ceso` puis `espace` puis `espace` -> `ce sont `
- `resto` puis `espace` puis `espace` -> `restaurant `
- `jen` puis `espace` puis `espace` -> `je ne `
- `p` puis `espace` puis `espace` -> `pas `

## Exemples

- `e1le2ve` -> `élève`
- `garc1on` -> `garçon`
- `maiitre` -> `maître`
- `No3el` -> `Noël`
- `hootel` -> `hôtel`

## Source

- Source principale Keyman : `source/french_telex.kmn`
- Guide de personnalisation et de build local : [`CONTRIBUTING.md`](/Users/kylepham/Code/keyman-french-telex/CONTRIBUTING.md)
- Commande de build : `kmc build /Users/kylepham/Code/keyman-french-telex`
- La sortie de build locale est générée dans `build/`
- Les versions taguées publient `french_telex.kmp` et les artefacts associés dans GitHub Releases via GitHub Actions
