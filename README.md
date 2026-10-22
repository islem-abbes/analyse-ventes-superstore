# 📊 Analyse des ventes Superstore : Python & Power BI

![Vue d'ensemble du dashboard](images/dashboard_vue_ensemble.png)

## 🎯 Objectif
Identifier où une entreprise de e-commerce gagne et perd de l'argent,
et proposer des recommandations concrètes pour améliorer sa rentabilité.

## 🛠️ Outils
- **Python** (pandas) : exploration, contrôle qualité, nettoyage, feature engineering
- **Power BI** : Power Query, mesures DAX, dashboard interactif

## 📁 Données
Dataset *Sample Superstore* (Kaggle) : 9 994 lignes de ventes (2014-2017), 21 colonnes.
Granularité : **1 ligne = 1 produit dans une commande** (5 009 commandes, 793 clients, 1 862 produits).

## 🔄 Démarche
1. **Exploration (Python)** : granularité, valeurs manquantes, doublons, statistiques descriptives
2. **Nettoyage (Python)** :
   - suppression d'un doublon masqué par l'identifiant technique `Row ID`
   - conversion de `Order Date` et `Ship Date` (texte → date)
   - création de colonnes : `Annee`, `Mois`, `Delai_livraison`, `Marge`
   - export d'un fichier propre (9 993 lignes, 25 colonnes)
3. **Modélisation (Power BI)** : typage des colonnes dans Power Query, mesures DAX
   (`SUM`, `DISTINCTCOUNT`, `DIVIDE`, `CALCULATE`)
4. **Dashboard** : 5 KPI, 3 filtres interactifs (année, catégorie, région),
   4 graphiques, mise en forme conditionnelle des pertes, page scénario

## 📈 Chiffres clés
| Indicateur | Valeur |
|---|---|
| Chiffre d'affaires | 2,30 M$ |
| Profit | 286 K$ |
| Marge | 12,5 % |
| Commandes | 5 009 |
| Panier moyen | 459 $ |

## 🔍 Principales découvertes
1. **Au-delà de 20 % de remise, chaque niveau de remise est déficitaire.**
   Les ventes avec plus de 20 % de remise ont fait perdre **135 K$**.
2. **3 sous-catégories sont déficitaires** : Tables (≈ −17,7 K$), Bookcases et Supplies.
   Les pertes de Tables et Bookcases sont liées à de fortes remises (21 à 26 % en moyenne).
   Supplies perd de l'argent malgré une faible remise (≈ 8 %) : la remise n'explique pas tout.
3. **La région Central est la moins rentable** : 7,9 % de marge, contre 14,9 % pour West,
   avec des remises nettement plus élevées sur plusieurs sous-catégories.
4. **Les ventes ont progressé d'environ +51 %** entre 2014 et 2017, après une légère baisse en 2015.

## 💡 Recommandations
- **Plafonner les remises à 20 %** : profit potentiel de **422 K$ (+47 %)**.
  À tester d'abord sur une région avant de généraliser.
- **Revoir la politique de remises dans la région Central.**
- **Analyser la tarification des Tables**, principale source de pertes.

![Scénario : plafonner les remises à 20 %](images/dashboard_scenario.png)

## ⚠️ Limites
L'estimation de +47 % suppose que les ventes à forte remise disparaissent simplement.
En réalité, certains clients pourraient ne plus acheter, ou acheter quand même avec 20 % de remise.

## 📂 Structure du projet
```
projet-superstore/
├── data/
│   ├── Sample - Superstore.csv      # données brutes
│   ├── superstore_clean.csv         # données nettoyées
│   ├── superstore_clean.xlsx        # données nettoyées (import Power BI)
│   └── dashboard_superstore.pbix    # rapport Power BI
├── images/                          # captures du dashboard
├── notebooks/
│   └── 01_exploration.ipynb         # exploration et nettoyage Python
├── requirements.txt                 # bibliothèques Python
└── README.md
```

## ▶️ Reproduire le projet
```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```
Puis ouvrir `data/dashboard_superstore.pbix` avec Power BI Desktop (gratuit).
