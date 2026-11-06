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
- Marque : plus d'image Captain Trading en haut à gauche. Le nom et le sous-titre s'affichent en texte (ambre, monospace) et le PNG intégré est retiré du fichier. Le favicon est conservé.

## Pour revenir en arrière ou ajuster

Les jetons sont en tête de la section (`--bb-amber`, `--bb-blue`, `--bb-cyan`, `--bb-yellow`,
`--bb-green`, `--bb-red`). Pour un autre bleu de bandeau, changer `--bb-blue` suffit.

## L'or comme actif suivi (XAU)

L'or est un actif du Desk au même titre que BTC, ETH et SOL. Code interne `XAU`, libellé affiché « GOLD ».
Il n'existe pas de marché spot or sur OKX : tout passe par le perpétuel `XAU-USDT-SWAP`
(ticker, bougies, open interest, funding, carnet, liquidations). Alias acceptés dans le Studio,
la palette et les alertes : `GOLD`, `OR`, `XAUT`, `PAXG`.

| Module | Ce qui change |
|---|---|
| Bandeau de prix | `XAU` dans la liste suivie par défaut ; l'ancien repère macro « Or » (TradingView) est retiré, devenu redondant. |
| Espaces et accueil | Les compteurs de liquidations et les libellés affichent « GOLD ». |
| Signaux | Nouvel indicateur « Or » dans la famille Macro (tendance journalière de l'once, source TradingView déjà chargée). |
| Liquidations | Flux en direct et amorçage incluent l'or. Carte : même modèle, sur les bougies 1 h OKX ; faute d'historique d'open interest lisible depuis un navigateur (l'API « rubik » d'OKX n'envoie pas d'en-tête CORS), les positions ouvertes sont estimées à 5 % du volume horaire et la part acheteuse à 60 % sur bougie verte. La légende le dit. |
| Niveaux clés | Sélecteur BTC / ETH / GOLD, bougies du perpétuel. |
| Carnet d'ordres | Sélecteur BTC / ETH / GOLD. Pour l'or, seul le carnet OKX est lu (les autres plateformes ne le cotent pas). |
| Dérivés et positionnement | Sélecteur BTC / ETH / GOLD. Pour l'or : OKX seulement (open interest, funding). L'historique d'open interest se construit en mémoire, relevé toutes les minutes. |
| Agent IA | Carte vivante GOLD (prix, bougies, liquidations 15 min, OI, funding). Les lectures écrites par le robot GitHub n'incluront l'or que lorsque le robot le produira ; l'affichage est prêt. |
| Screener | Le perpétuel or est analysé avec les cryptos ; « gold » ou « xau » dans la recherche le trouve. |
| Alertes et palette | « gold », « or » ou « xau » fonctionnent ; graphique TradingView `OKX:XAUUSDT.P`. |

Hors périmètre, faute de données : options (Deribit ne cote pas l'or), top mouvements (réservé aux cryptos), corrélations (l'or y figurait déjà).
