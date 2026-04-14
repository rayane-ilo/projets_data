# PROJET : Turnover & Prédiction de Départ RH

Analyse complète du turnover salarié avec modèle prédictif : audit qualité des données SIRH, analyse des facteurs de départ, régression logistique et identification des profils à risque.

## Contexte métier

Le turnover est l'un des KPIs RH les plus coûteux. Remplacer un salarié coûte entre **50 % et 200 % de son salaire annuel** (recrutement, formation, perte de productivité). Ce projet simule le travail d'un Data Analyst RH chargé d'analyser ce phénomène et de construire un outil de détection précoce.

## Objectifs

- Auditer la qualité des données d'un export SIRH (11 types de défauts simulés)
- Nettoyer les données de façon traçable et documentée
- Analyser le turnover par département, ancienneté, satisfaction et poste
- Construire un modèle prédictif (régression logistique) avec métriques d'évaluation
- Identifier les employés actifs les plus à risque
- Formuler des recommandations RH actionnables

## Contenu du notebook

| Section | Description |
|---------|-------------|
| 1. Génération des données | 500 employés synthétiques + 11 défauts volontaires injectés |
| 2. Audit Qualité | Complétude, unicité, validité, cohérence, exactitude + score global |
| 3. Nettoyage | 10 étapes traçables : doublons, genres, départements, salaires, dates... |
| 4. EDA | Distributions, matrice de corrélations, pyramide des effectifs |
| 5. Analyse Turnover | Taux par département, courbe de rétention, satisfaction vs départ |
| 6. Modèle Prédictif | Régression logistique, split train/test, normalisation |
| 7. Feature Importance | Coefficients logistiques + profils à risque individuels |
| 8. Dashboard | Vue direction multi-KPIs exportée en PNG |

## Défauts qualité injectés

| # | Défaut | Simulation | Cause réelle |
|---|--------|-----------|--------------|
| 1 | Doublons | 5 lignes dupliquées | Export SIRH avec mauvaise jointure |
| 2 | Satisfaction manquante | 8% de NaN | Champ facultatif enquête RH |
| 3 | Noms manquants | 3% de NaN | Intérimaires non saisis |
| 4 | Salaires invalides | Négatifs + 999 999 € | Saisie manuelle inversée |
| 5 | Âges impossibles | < 18 ans et > 75 ans | Inversion chiffres (19 → 91) |
| 6 | Ancienneté négative | -2, -5 ans | Migration entre systèmes |
| 7 | Genres mal codés | M/Homme/male/1/Femme... | Champ libre ancien système |
| 8 | Dates incohérentes | Départ avant embauche | Format JJ/MM vs MM/JJ |
| 9 | Performance hors bornes | 7.5 et -1 | Erreur de saisie |
| 10 | Départements variantes | tech, TECH, Finances... | Fusion de systèmes |
| 11 | Heures sup impossibles | 60–80h/sem | Cumul annuel saisi en hebdo |

## Variables du modèle

| Variable | Type | Rôle |
|----------|------|------|
| `satisfaction_score` | Numérique 1–5 | Principal prédicteur |
| `heures_sup` | Numérique 0–40 | Facteur de départ |
| `dernier_promo` | Entier (années) | Facteur de départ si élevé |
| `anciennete` | Entier (années) | Courbe de rétention |
| `salaire`, `age` | Numériques | Contexte |
| `departement`, `poste`, `contrat` | Catégorielles (dummy) | Segmentation |

## Stack technique

- Python 3
- pandas, numpy
- matplotlib, seaborn
- scipy (stats, mannwhitneyu)
- scikit-learn (LogisticRegression, StandardScaler, métriques ROC)

## Fichiers

```
turnover_prediction.ipynb   # notebook principal (8 sections)
dashboard_turnover.png      # export du dashboard direction (généré à l'exécution)
README.md                   # ce fichier
```

## Concepts pédagogiques couverts

- Détection et correction de 11 types d'anomalies qualité
- Imputation par médiane groupée (par département)
- Encodage one-hot avec `drop_first` pour éviter la multicolinéarité
- Normalisation `StandardScaler` et prévention du data leakage
- Métriques de classification : AUC-ROC, précision, rappel, F1
- Test statistique non-paramétrique (Mann-Whitney U)
- Visualisation : matrice de confusion, courbe ROC, feature importance
