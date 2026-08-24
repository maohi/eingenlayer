# Market Dashboard + TREND — Pine Script v6

Indicateur TradingView (`pine/market_dashboard_trend.pine`) qui reproduit le dashboard
« Market » (Squeeze / Strength / Momentum / ADX / MACD / Biais) et y ajoute une ligne
**TREND** qui qualifie le régime de marché : *range de consolidation*, *breakout haussier*
ou *breakout baissier*.

## Installation

1. TradingView → **Pine Editor** → *Ouvrir* → *Nouvel indicateur*.
2. Coller le contenu de `market_dashboard_trend.pine`.
3. *Enregistrer* puis *Ajouter au graphique*.

## Lignes du tableau

| Ligne | Calcul | Lecture |
|---|---|---|
| **Squeeze** | TTM Squeeze : Bollinger(20, 2) à l'intérieur des Keltner(20, 1.5 ATR) | `Compression` = énergie qui s'accumule ; `Breakout ▲/▼` = bandes ressorties, direction donnée par le momentum |
| **Strength** | Score haussier composite 0–100 % (EMA21/50, EMA200, MACD ligne/signal, histogramme, momentum, DI+/DI−, RSI) | > 60 % dominance acheteuse, < 40 % dominance vendeuse |
| **Momentum** | Régression linéaire de l'écart au milieu du canal (momentum TTM) | `Bull` / `Bear`, suffixe *(essouf.)* si le momentum décélère |
| **ADX** | `ta.dmi(14, 14)` | > 25 = tendance réelle ; flèche = ADX qui monte ou qui baisse |
| **MACD** | Histogramme MACD(12, 26, 9) | Signe et amplitude de l'impulsion |
| **Biais** | Dérivé du Strength | `Haussier` / `Neutre` / `Baissier` |
| **TREND** | Machine à états ci-dessous | Régime de marché |

## Logique du TREND

Canal de référence : Donchian(20) **décalé d'une barre** (on casse le niveau précédent, pas
celui que la bougie en cours vient de créer).

- **Range / Consolidation** — prix contenu dans le canal, `ADX < 20` et largeur des Bollinger
  dans les 25 % les plus faibles des 100 dernières barres (percentile BBW). Un squeeze TTM
  actif force également l'état range (affiché « Range (compression) »).
- **Breakout haussier** — clôture au-dessus du haut du canal + marge de `0.1 × ATR`,
  `ADX > 23`, momentum haussier, `DI+ > DI−`, volume > 1.3 × sa moyenne 20 (option),
  et confirmation HTF si activée.
- **Breakout baissier** — condition miroir.
- **Tendance haussière / baissière** — un breakout qui tient plus de `holdBars` barres se
  dégrade en simple tendance ; hors canal sans les critères de cassure, l'état suit
  EMA21/EMA50/EMA200 avec `ADX > 23`.
- **Invalidation** — un breakout retombe en range dès que le prix repasse le milieu du canal
  ou que le momentum change de signe.

## Paramètres utiles

| Paramètre | Défaut | Effet |
|---|---|---|
| `Donchian (canal de range)` | 20 | Largeur du range de référence |
| `Compression max pour Range (%)` | 25 | Plus bas = range plus rare |
| `ADX max en Range` / `ADX min pour valider Breakout` | 20 / 23 | Frontière range ↔ tendance |
| `Marge de cassure (x ATR)` | 0.1 | Filtre les fausses cassures de mèche |
| `Durée max d'un état Breakout` | 10 | Après ce délai le breakout devient « tendance » |
| `Confirmer breakout par volume` | on | Désactiver sur les symboles sans volume (forex, indices) |
| `Confirmation HTF` | off | Exige l'accord de l'EMA lente en 4 h (ou autre UT) |

## Visuel et alertes

- Canal de range tracé sur le graphique, zone remplie en jaune quand l'état est *range*.
- Fond du graphique coloré : vert = breakout haussier, rouge = breakout baissier, jaune = range.
- Flèches `BO▲` / `BO▼` sur les cassures validées.
- Alertes disponibles : *Breakout haussier*, *Breakout baissier*, *Entrée en range*,
  *Sortie de compression*.

L'état est calculé sur la bougie en cours : pour ne travailler que sur des signaux clôturés,
créez les alertes en mode « Une fois par clôture de bougie ».
