# Stratégie SMA 8/20 + Confirmation Price Action (Velez / EllyDtrade)

Script de stratégie **Pine Script v5** pour TradingView :
[`sma8_20_crossover_price_action.pine`](./sma8_20_crossover_price_action.pine)

## Principe

La stratégie combine un signal de tendance (croisement de moyennes mobiles)
avec une validation par price action pour filtrer les faux signaux (whipsaws) :

1. **Setup** — la SMA 8 croise la SMA 20 :
   - à la hausse → setup **LONG** armé ;
   - à la baisse → setup **SHORT** armé.
   Le plus haut (long) / plus bas (short) de la bougie de croisement est mémorisé.

2. **Confirmation** — dans une fenêtre de N bougies (5 par défaut), on attend une
   bougie de conviction (concepts d'Oliver Velez) qui doit :
   - avoir un **corps plein significatif** (ratio corps/range ≥ 0.55 par défaut) ;
   - **clôturer proche de son extrême** (dans les 30 % supérieurs pour un long) ;
   - optionnellement être une **« Elephant Bar »** : corps ≥ 1.3× le corps moyen
     des 20 dernières bougies ;
   - clôturer **entièrement du bon côté de la SMA 8** (corps entier, ou bougie
     entière mèches comprises selon le réglage) ;
   - **casser l'extrême de la bougie de croisement** (en clôture par défaut,
     méthode d'entrée type EllyDtrade).

3. **Entrée** — à la **clôture de la bougie de confirmation**
   (`process_orders_on_close = true`), soit un fill équivalent à l'ouverture de
   la bougie suivante en conditions réelles.

4. **Gestion du risque** :
   - **Stop Loss** paramétrable : sous/au-dessus de la bougie de confirmation
     (mode « Bougie », avec buffer en ticks) ou derrière la SMA 20
     (mode « SMA 20 », pour laisser respirer le trade) ;
   - **Take Profit** par Risk/Reward paramétrable : TP1 à 1:1.5 (sortie
     partielle, 50 % par défaut) et TP2 à 1:2 ;
   - **Sortie dynamique** optionnelle : clôture du trade si le prix clôture de
     l'autre côté de la SMA 8.

## Installation

1. Ouvrir TradingView → éditeur Pine.
2. Coller le contenu du fichier `.pine` et cliquer sur « Ajouter au graphique ».
3. Ajuster les paramètres dans l'onglet réglages de la stratégie (groupes :
   *Moyennes mobiles*, *Direction*, *Bougie de confirmation*, *Gestion du risque*).

## Alertes disponibles

- **Setup LONG / SHORT** : croisement SMA 8/20 détecté (setup armé, ne pas entrer).
- **Confirmation LONG / SHORT** : bougie de confirmation validée, entrée à la clôture.

## Avertissement

Les performances passées en backtest ne préjugent pas des résultats futurs.
Testez la stratégie sur données historiques et en paper trading avant tout
usage en réel, et adaptez le sizing à votre tolérance au risque.
