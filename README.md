# Trafic routier à Paris : rue Lecourbe, avenue Foch et avenue Daumesnil

## La question

Quel est l'état du trafic routier sur trois axes parisiens (rue Lecourbe, avenue Foch et avenue Daumesnil), et lequel de ces axes supporte le débit horaire le plus élevé ?

## Les données

Les données proviennent du jeu « Comptages routiers permanents » de la Ville de Paris, importé via l'API Open Data. Elles couvrent la période de mars à août 2026 et concernent les trois axes suivants :

- rue Lecourbe (`Lecourbe`)
- avenue Foch (`Av_Foch`)
- avenue Daumesnil (`Av_Daumesnil`)

## Résultats

Nous pouvons faire plusieurs remarques sur les données :

1. 50 % des lignes ont des valeurs manquantes dans les colonnes `k` ou `q`. Ces lignes ont dû être supprimées afin d'obtenir une analyse pertinente.
2. Le trafic est principalement fluide sur l'ensemble des axes (voir le graphique circulaire).
3. L'axe qui présente le débit horaire moyen le plus élevé est l'avenue Foch.

## Limites

Les données comportent beaucoup de valeurs manquantes, ce qui a pu fausser les résultats. De plus, il aurait été pertinent d'analyser le trafic selon les heures de passage.

## Lancer le projet

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python download_data.py
```

Puis exécuter le notebook `projet_data.ipynb`.

## Utilisation de l'IA

J'ai utilisé l'IA pour m'accompagner dans l'écriture du code et la correction d'erreurs.