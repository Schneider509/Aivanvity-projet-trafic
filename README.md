# Trafic routier à Paris : rue Lecourbe, avenue Foch et avenue Daumesnil

## La question

Quel est l'état du trafic routier sur trois axes parisiens (rue Lecourbe, avenue Foch et avenue Daumesnil), et lequel de ces axes supporte le débit horaire le plus élevé ?

## Les données

Les données proviennent du jeu « Comptages routiers permanents » de la Ville de Paris, importé via l'API Open Data. Elles couvrent la période de mars à août 2026 et concernent les trois axes suivants :

- rue Lecourbe (`Lecourbe`), 10 tronçons
- avenue Foch (`Av_Foch`), 12 tronçons
- avenue Daumesnil (`Av_Daumesnil`), 24 tronçons

Le jeu brut compte 200 744 mesures horaires sur 46 tronçons.

## Nettoyage

Chaque choix est justifié par les chiffres dans le notebook.

- **Dates** : les horodatages sont en UTC. Ils sont convertis en heure de Paris, et les 92 lignes qui tombent alors le 1er septembre sont supprimées.
- **Doublons** : aucun, ni en ligne entière ni par tronçon et par heure. En revanche, 52 heures sont absentes de la source pour tous les tronçons.
- **Colonnes** : les codes des carrefours amont et aval sont supprimés, car ils répètent les libellés (33 codes pour 33 noms).
- **Valeurs manquantes** : 50 % des lignes brutes ont `q` ou `k` manquant. Les mesures déclarées invalides ou prises sur une voie barrée sont supprimées (34 428 lignes, 17 %). L'état « Inconnu » est traité comme une valeur manquante, car il correspond exactement aux lignes sans taux d'occupation. Les autres valeurs manquantes sont conservées sans imputation : elles viennent de tronçons où une grandeur n'est jamais mesurée.

- **Valeurs aberrantes** : 8 débits supérieurs à 5 000 véhicules/heure, incohérents avec un taux d'occupation faible au même moment, sont remplacés par une valeur manquante (règle 3 × IQR appliquée tronçon par tronçon).

Après nettoyage, il reste 166 224 mesures sur 43 tronçons.

## Résultats

1. Le trafic est principalement fluide : 61 % des mesures brutes sont classées « Fluide », contre 7,5 % en pré-saturé, saturé ou bloqué. Près d'une mesure sur trois (31 %) n'a pas d'état de trafic connu.
2. L'axe qui présente le débit horaire moyen le plus élevé est l'avenue Foch (environ 620 véhicules par heure), devant la rue Lecourbe (396) et l'avenue Daumesnil (170).
3. Les heures les plus chargées diffèrent selon l'axe : 17 h à 19 h sur l'avenue Foch, 18 h à 20 h sur la rue Lecourbe, et deux maximums à 12 h et 17 h sur l'avenue Daumesnil. Le creux se situe partout entre 4 h et 6 h du matin.

## Limites

Les données comportent beaucoup de valeurs manquantes, concentrées sur certains tronçons, ce qui a pu fausser les moyennes par axe. De plus, plusieurs tronçons voisins portent exactement le même débit (36 tronçons pour 14 profils distincts) : un même point de mesure est compté plusieurs fois dans les moyennes par axe. La comparaison semaine / week-end reste à faire.

## Lancer le projet

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Puis exécuter le notebook `projet_data.ipynb` de haut en bas : il télécharge les données dans `data/` à la première exécution (1 à 3 minutes).

## Utilisation de l'IA

J'ai utilisé l'IA pour m'accompagner dans l'écriture du code et la correction d'erreurs.
