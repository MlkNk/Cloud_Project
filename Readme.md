# 🌍 Global Health – Analyse, Transformation et Prédiction de Données de Santé Mondiale


**Outils** : Microsoft Fabric, Power BI, Kaggle (Global Health Statistics)

---

## 1. Contexte et Objectifs

Dans le cadre d’un projet de Data Engineering et Data Science, nous avons conçu une architecture complète autour des données de santé mondiale issues d’un dataset Kaggle.  
L’objectif principal était de construire une pipeline de traitement robuste, permettant de :

- Nettoyer et structurer les données brutes de santé publique
- Concevoir un **modèle en étoile** pour une intégration efficace dans Power BI
- Mettre en œuvre des algorithmes de **Machine Learning** pour prédire la mortalité ou la récupération selon les pays
- Valoriser les données via un **dashboard interactif Power BI** pour la prise de décision

---

## 2. Source des Données

Les données utilisées proviennent du dataset **Global Health Statistics** disponible sur Kaggle.  
Elles comprennent de nombreuses variables liées à :

- La mortalité par maladie
- Les systèmes de santé
- Les dépenses publiques de santé
- L'accès aux soins et traitements
- L’espérance de vie et d'autres indicateurs démographiques

Les fichiers initiaux sont fournis au format CSV, avec plusieurs années et pays couverts.

---

## 3. Architecture du Pipeline

Notre pipeline est structuré autour du modèle **Bronze → Silver → Gold** avec 3 notebooks principaux, chacun jouant un rôle spécifique dans le traitement des données :

✨ **Bronze** – Ingestion initiale  
- Chargement brut des fichiers CSV
- Inspection de la qualité et exploration initiale (pandas-profiling)
- Nettoyage de base : gestion des valeurs manquantes, renommage des colonnes

✨ **Silver** – Structuration des données  
- Nettoyage avancé, filtrage des pays/années incohérents
- Transformation des types de données
- Enrichissement de certaines colonnes (catégorisation, regroupement)
- Préparation des dimensions et faits pour un modèle en étoile

✨ **Gold** – Modèle final + Machine Learning  
- Construction de tables `dim_country`, `dim_year`, `dim_disease`, `fact_health`
- Séparation logique des dimensions et faits
- Intégration dans Power BI pour modélisation sémantique
- Entraînement de modèles de machine learning (régression, arbres de décision) pour prédire :
  - Taux de mortalité
  - Probabilité de récupération en fonction des facteurs socio-sanitaires

---

## 4. Modèle en Étoile

Nous avons conçu un **modèle en étoile** adapté à la visualisation et à l’analyse décisionnelle.  
Les tables finales **Gold** sont structurées comme suit :

- **Table de faits** :
  - `fact_health` : mortalité, récupération, dépenses, accès soins, etc.

- **Dimensions** :
  - `dim_country` : pays, région OMS, revenu
  - `dim_year` : année, décennie
  - `dim_disease` : catégorie de maladie, nom, classification OMS

Les relations sont définies sur des clés primaires, avec un filtrage croisé bidirectionnel activé dans Power BI.

---

## 5. Machine Learning

Nous avons mis en œuvre un module de prédiction basé sur **Scikit-learn** pour anticiper certains indicateurs de santé :

- **Objectif** : prédire le taux de mortalité en fonction des caractéristiques pays/année/maladie
- **Données d'entraînement** : fact_health enrichie de variables issues des dimensions
- **Modèles testés** :
  - Régression linéaire
  - Random Forest Regressor
  - Gradient Boosting
- **Évaluation** : métriques RMSE, MAE, R²

Ces modèles permettent de simuler l’impact de certains facteurs sur la mortalité, offrant une couche analytique avancée au-dessus des données explorées.

---

## 6. Dashboard Power BI

Le rapport PBI décrit :

- Une vue interactive sur les principaux **KPI de santé mondiale**
- Des visualisations claires de la mortalité par région, type de maladie, année
- Des comparaisons entre pays selon leur système de santé
- Des filtres dynamiques par région OMS, revenu, maladie

Ce tableau de bord est construit sur la **table Gold**, en exploitant pleinement la modélisation sémantique.

---

## 7. Problèmes rencontrés

- **Qualité des données** : certaines colonnes contenaient des valeurs nulles fréquentes (notamment pour les années 2000-2003), nécessitant des imputations ou des suppressions
- **Hétérogénéité** : beaucoup de variations dans les noms de maladies et des pays (normalisation nécessaire)
- **Modélisation ML** : faible corrélation entre certaines variables a rendu la prédiction plus difficile (feature engineering nécessaire)

---

## Conclusion

Ce projet nous a permis d’appliquer des concepts clés du data engineering et de la data science : ingestion structurée, nettoyage, modélisation en étoile, intégration Power BI et machine learning.  
L’architecture construite autour des couches Bronze/Silver/Gold offre une base robuste, reproductible et scalable pour l’analyse des données de santé publique mondiale.

---

## Arborescence du projet

```text
.
├── data/                    # Données sources (CSV)
├── notebooks/
│   ├── 1_ingestion_cleaning.ipynb       # Bronze → Silver
│   ├── 2_modele_etoile.ipynb            # Silver → Gold
│   └── 3_machine_learning.ipynb         # Analyse prédictive
├── powerbi/
│   └── global_health_dashboard.pbix     # Rapport interactif
├── outputs/                 # Tables finales (Gold), modèles
├── 
└── README.md                # Ce fichier
