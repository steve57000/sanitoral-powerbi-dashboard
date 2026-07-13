# Procédure de mise à jour

Ce document explique comment mettre à jour le rapport Power BI Sanitoral lorsque de nouvelles données sont disponibles.

## Objectif

Sanitoral souhaite pouvoir actualiser l'analyse sans refaire manuellement le nettoyage des données.

La procédure repose sur Power Query et sur le fichier Power BI final : `Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`.

## Pré-requis

- Power BI Desktop installé.
- Fichier Excel source Sanitoral disponible.
- Fichier `Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix` ouvert.
- Structure des 7 feuilles sources conservée dans le fichier Excel.

## Procédure utilisateur

1. Ouvrir `livrables/02_powerbi/Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`.
2. Vérifier que le nouveau fichier Excel conserve les mêmes feuilles et colonnes.
3. Dans Power BI, ouvrir `Transformer les données`.
4. Vérifier le chemin du fichier source si besoin.
5. Cliquer sur `Actualiser l'aperçu`.
6. Vérifier que les étapes Power Query ne contiennent pas d'erreur.
7. Contrôler que seule la table finale `Fact_ProjectPhasePerformance` est chargée dans le modèle.
8. Cliquer sur `Fermer et appliquer`.
9. Cliquer sur `Actualiser` dans Power BI.
10. Contrôler les KPI principaux.
11. Vérifier les 3 pages finales : `Vue exécutive`, `Détail des alertes` et `Documentation & Méthode`.
12. Exporter le rapport si une version PDF est nécessaire.

## Contrôles après actualisation

Valeurs attendues sans filtre actif :

| Contrôle | Valeur attendue |
|---|---:|
| Nb Projets | 104 |
| Nb Phases | 520 |
| Nb Phases en alerte | 348 |
| Taux phases en alerte | 66,92 % |
| Nb alertes coût | 214 |
| Nb alertes durée | 159 |
| Nb alertes livrables | 96 |

Vérifier également :

- absence d'erreur Power Query ;
- absence de valeur vide dans les colonnes critiques ;
- cohérence des totaux de coûts, durées et livrables ;
- fonctionnement des filtres `Project_Type`, `Country`, `Region`, `Alert_Status`, `Phase` ;
- affichage correct des KPI et graphiques sur la page `Vue exécutive` ;
- tableau filtré sur les alertes et tri décroissant sur `Alert_Count` dans la page `Détail des alertes` ;
- présence de la page `Documentation & Méthode` avec le Product Strategy Canvas, la préparation des données, le modèle, Power Query, la règle d’alerte à 15 % et les KPI de contrôle.

## Colonnes critiques

| Colonne | Pourquoi elle est critique |
|---|---|
| `Project_ID` | Identifie les projets. |
| `Phase` | Identifie les phases. |
| `ProjectPhaseKey` | Permet les jointures au niveau projet-phase. |
| `Start_Date` | Permet l'analyse temporelle. |
| `Country` | Permet l'analyse géographique. |
| `Region` | Permet l'analyse par zone. |
| `Planned_Cost` / `Actual_Cost` | Mesure les écarts de coûts. |
| `Planned_Duration` / `Actual_Duration` | Mesure les écarts de délais. |
| `Planned_Deliverables` / `Actual_Deliverables` | Mesure les écarts de livrables. |
| `Alert_Count` / `Alert_Status` | Alimente la page de détail des alertes. |

## Points de vigilance

- Ne pas renommer les feuilles du fichier Excel source.
- Ne pas supprimer les colonnes utilisées par Power BI.
- Ne pas changer le sens des données prévues et réelles.
- Ne pas réactiver le chargement des tables intermédiaires sauf besoin exceptionnel.
- Contrôler les valeurs nulles ou égales à zéro dans les colonnes de référence.
