# PROJET : Diversité & Inclusion – Analyse RH

Analyse complète des métriques D&I : audit qualité des données sensibles, représentation par genre/âge/nationalité, équité salariale (écart brut vs contrôlé), pipeline de promotion, et calcul de l'Index Égalité Professionnelle F/H.

## Contexte métier

En France, les entreprises de plus de 50 salariés sont tenues de publier chaque **1er mars** leur **Index Égalité Professionnelle** (score sur 100 pts). Un score < 75 déclenche une obligation de plan d'action sous 3 ans. Ce projet simule le travail d'un(e) analyste RH chargé(e) de préparer ce reporting légal.

## Obligations légales couvertes

| Obligation | Description |
|-----------|-------------|
| Index Égalité F/H | Score 5 indicateurs sur 100 pts (loi Pénicaud 2018) |
| DOETH | Déclaration obligatoire emploi travailleurs handicapés |
| Taux BOETH | Objectif légal de 6% de travailleurs handicapés |
| Bilan Social | Pyramide des âges, répartition genre, nationalités |

## Objectifs

- Auditer 9 types de défauts dans les données démographiques (genres multiples, nationalités variantes...)
- Analyser la représentation par genre, âge, grade et département
- Calculer l'écart salarial brut ET contrôlé (régression)
- Mesurer les taux de promotion par genre et tester leur significativité (χ²)
- Calculer une version simplifiée de l'Index Égalité Professionnelle
- Formuler un plan d'action D&I priorisé

## Contenu du notebook

| Section | Description |
|---------|-------------|
| 1. Génération des données | 600 employés avec biais genre intentionnels + 9 défauts |
| 2. Audit Qualité D&I | Spécificités des données sensibles (BOETH, genres multiples) |
| 3. Nettoyage | Standardisation genres, nationalités, éducation, âges, salaires |
| 4. Représentation | % femmes par grade (plafond de verre), pyramide des âges, internationalisation |
| 5. Équité Salariale | Écart brut (t-test de Welch) + écart contrôlé (régression log-linéaire) |
| 6. Pipeline Promotion | Taux de promotion par genre + test χ² d'indépendance |
| 7. Index Égalité F/H | Calcul des 5 indicateurs + score total |
| 8. Dashboard | Vue direction multi-KPIs + plan d'action |

## Défauts qualité simulés

| # | Défaut | Cause réelle simulée |
|---|--------|---------------------|
| 1 | 35 genres mal encodés | Fusion de 2 systèmes (H/F vs Homme/Femme/Male) |
| 2 | 5 âges impossibles | Inversion de chiffres (18 → 81) |
| 3 | 25 nationalités non standardisées | Abréviations, accents manquants, noms en anglais |
| 4 | 5 salaires invalides (négatifs/zéros) | Valeurs par défaut non remplacées |
| 5 | 4 salaires outliers > 500k€ | Copier-coller erroné |
| 6 | 4 anciennetés incohérentes | Saisie en mois au lieu d'années (×12) |
| 7 | 6 grades invalides | Fusion d'une filiale avec référentiel différent |
| 8 | 3 dates d'embauche futures | Contrats pré-signés saisis avec erreur |
| 9 | 20 niveaux éducation non standardisés | Ancien système en anglais (Master/PhD/BTS) |

## Indicateurs D&I calculés

| Indicateur | Formule |
|------------|---------|
| Taux de féminisation | % employées F / effectif total |
| Indice de parité par grade | % F dans le grade / 50% |
| Écart salarial brut | (μH - μF) / μH × 100 |
| Écart salarial contrôlé | Coeff. genre dans régression log(salaire) |
| Taux de promotion | % promus 2022-2024 par genre |
| Index Égalité F/H | Somme pondérée de 5 indicateurs (max 100) |
| Taux BOETH | % de BOETH déclarés / effectif |

## Stack technique

- Python 3
- pandas, numpy
- matplotlib, seaborn
- scipy (stats.ttest_ind, stats.chi2_contingency)
- numpy.linalg.lstsq (régression OLS manuelle)

## Fichiers

```
diversite_inclusion_rh.ipynb            # notebook principal (8 sections)
dashboard_diversite_inclusion.png       # export dashboard D&I (généré à l'exécution)
README.md                               # ce fichier
```

## Concepts pédagogiques couverts

- Gestion des données sensibles (conformité CNIL)
- Normalisation d'encodages multiples (mapping exhaustif)
- Écart salarial brut vs contrôlé (décomposition Oaxaca-Blinder simplifiée)
- Régression log-linéaire avec variables dummy
- Test t de Welch (variances inégales)
- Test χ² d'indépendance pour la promotion
- Calcul de l'Index Égalité Professionnelle F/H (loi Pénicaud)
- Pyramide des âges et anticipation des départs à la retraite
- Biais de composition (glass ceiling vs discrimination directe)
