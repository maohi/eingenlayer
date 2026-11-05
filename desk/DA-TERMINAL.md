# Desk · direction artistique « Terminal »

Le Desk (`desk/index.html`) reprend les codes visuels du terminal Bloomberg.
Tout le style vit dans la dernière section de la feuille `<style>` du fichier,
sous le titre « DA « TERMINAL » » : elle est appliquée après le reste et a le dernier mot.

## Principes

| Principe | Choix |
|---|---|
| Fond | Noir pur `#000`. Plus de relief 3D, de grain, de dégradé, d'ombre ni de flou. |
| Angles | Aucun arrondi, nulle part (`border-radius:0` sur tout). |
| Police | Une seule famille, JetBrains Mono, chiffres tabulaires, interlignage serré (13 px de base). |
| Libellés, touches, repères | Ambre `#FFA028` (réglable : c'est l'accent du Studio). |
| Données | Blanc `#FFF` ; texte secondaire `#CFCFCF`, discret `#8E8E8E`. |
| Titres de blocs, en-têtes de tableaux, sélection | Bandeau bleu profond `#0B2A7A`, texte blanc. |
| Variations | Vert `#1ED760` / rouge `#FF3B30`. Avertissement jaune `#FFE34D`. Lien cyan `#5CC8FF`. |
| Filets | Gris `#2A2A2A`, plus marqué `#474747`. |
| Menus | Numérotés « 1) 2) 3) », le numéro en ambre devant le nom. |
| Ligne d'état | Style ligne de commande : `>` ambre, curseur bloc clignotant. |
| Curseur | Curseur système (le curseur maison est désactivé). |
| Logos de coins | Masqués : un terminal n'affiche que des symboles. |

Le thème clair reste disponible (fond `#F3F3F3`, texte noir, mêmes bandeaux bleus).

## Ce qui a changé hors CSS

- Police Google Fonts : seule JetBrains Mono (400 à 800) est chargée.
- Accent par défaut de la config : `#FFA028`.
- Couleurs des sept espaces (`col:` dans la liste des mondes) ramenées à la palette terminal.
- Graphiques en bougies : fond noir, texte gris, moyenne mobile cyan.
- Studio : la coche « ✓ » n'est plus doublée sur les puces d'espaces.

## Pour revenir en arrière ou ajuster

Les jetons sont en tête de la section (`--bb-amber`, `--bb-blue`, `--bb-cyan`, `--bb-yellow`,
`--bb-green`, `--bb-red`). Pour un autre bleu de bandeau, changer `--bb-blue` suffit.
