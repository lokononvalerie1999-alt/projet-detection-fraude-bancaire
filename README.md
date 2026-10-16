# Détection de transactions bancaires frauduleuses

Projet personnel de Data Science consacré à l’analyse et à la détection de transactions bancaires potentiellement frauduleuses.

> Ce projet est réalisé dans une démarche d’apprentissage pratique afin de transformer progressivement les connaissances acquises en statistique, Python et Machine Learning en compétences appliquées à un problème concret.

## Objectif

L’objectif est d’étudier un jeu de données de transactions bancaires, de comprendre les caractéristiques des fraudes et de comparer plusieurs modèles de classification.

La question métier est la suivante :

> Comment identifier les transactions potentiellement frauduleuses tout en limitant les fausses alertes et les fraudes non détectées ?

## Jeu de données

Le projet utilise le jeu de données public **Credit Card Fraud Detection**, associé à ULB et Worldline.

Il contient :

- 284 807 transactions ;
- 492 transactions frauduleuses ;
- 30 variables explicatives ;
- une variable cible `Class`.

Codage de la cible :

- `0` : transaction légitime ;
- `1` : transaction frauduleuse.

Les variables `V1` à `V28` sont anonymisées. `Time` représente le temps écoulé depuis la première transaction et `Amount` représente le montant de la transaction.

Sources :

- [Jeu de données sur Kaggle](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- [Jeu de données sur OpenML](https://www.openml.org/d/42175)

Le fichier brut n’est pas inclus dans ce dépôt en raison de sa taille. Pour le télécharger localement :

```bash
python src/download_data.py
```

Le fichier doit être placé dans :

```text
data/raw/creditcard.csv
```

## Étapes réalisées

- cadrage de la problématique métier ;
- chargement et inspection des données avec pandas ;
- vérification des types et des dimensions ;
- contrôle des valeurs manquantes ;
- détection et analyse des doublons ;
- étude du déséquilibre des classes ;
- analyse descriptive de la variable `Amount` ;
- séparation des variables explicatives et de la cible ;
- séparation stratifiée des données d’entraînement et de test ;
- comparaison d’une baseline, d’une régression logistique et d’un Random Forest.

## Premier benchmark

L’évaluation a été réalisée sur un échantillon de test contenant 56 746 transactions, dont 95 fraudes.

| Modèle | PR-AUC | Rappel | Précision | F1-score |
|---|---:|---:|---:|---:|
| Baseline classe majoritaire | 0,002 | 0,000 | 0,000 | 0,000 |
| Régression logistique équilibrée | 0,672 | 0,874 | 0,056 | 0,106 |
| Random Forest équilibré | **0,807** | 0,737 | **0,886** | **0,805** |

Au seuil provisoire de 0,5, le Random Forest a détecté 70 fraudes sur 95 et produit 9 fausses alertes parmi les transactions légitimes.

Ces résultats sont préliminaires. Le choix du modèle et du seuil doit dépendre du coût métier d’une fraude manquée et d’une fausse alerte.

## Technologies utilisées

- Python ;
- pandas ;
- NumPy ;
- scikit-learn ;
- Matplotlib ;
- Seaborn ;
- Joblib ;
- Jupyter Notebook prévu pour les analyses détaillées.

## Structure du projet

```text
projet-detection-fraude-bancaire/
│
├── README.md
├── requirements.txt
├── .gitignore
├── GUIDE_MODELISATION_PAS_A_PAS.md
├── PARCOURS_MENTORAT.md
│
├── data/
│   ├── raw/
│   └── processed/
│
├── models/
│
├── notebooks/
│
├── reports/
│   ├── rapport_projet_1_intermediaire.md
│   ├── benchmark_modeles.csv
│   └── figures/
│
├── app/
├── api/
│
└── src/
    ├── download_data.py
    ├── eda.py
    └── modelisation_benchmark.py
```

## Installation

Créer un environnement virtuel :

```bash
python -m venv .venv
```

Activer l’environnement sous Windows :

```bash
.venv\Scripts\activate
```

Activer l’environnement sous Linux ou macOS :

```bash
source .venv/bin/activate
```

Installer les dépendances :

```bash
pip install -r requirements.txt
```

Télécharger les données :

```bash
python src/download_data.py
```

Lancer l’analyse exploratoire :

```bash
python src/eda.py
```

Lancer le benchmark de modélisation :

```bash
python src/modelisation_benchmark.py
```

## Prochaines étapes

- étudier plusieurs seuils de décision ;
- relier le seuil aux coûts métier ;
- approfondir l’interprétabilité des modèles ;
- réaliser une validation temporelle ;
- comparer d’autres modèles ;
- créer une application Streamlit ;
- préparer une API FastAPI ;
- documenter les conditions de mise en production.

## Limites

- les données couvrent une période limitée ;
- les variables principales sont anonymisées ;
- les informations métier sur les clients, les commerçants et les terminaux ne sont pas disponibles ;
- les performances obtenues sur ce jeu de données ne constituent pas une garantie de performance en production ;
- le seuil de décision n’a pas encore été validé avec un scénario métier réel.

## Auteur

**Valérie Rosemonde LOKONON**  
Statisticienne | Analyste de données | Data Scientist en formation

Projet réalisé dans le cadre d’une démarche personnelle d’apprentissage et de constitution de portfolio.
