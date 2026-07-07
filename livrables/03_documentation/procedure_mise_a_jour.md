# Procedure de mise a jour

Ce document explique comment mettre a jour le rapport Power BI Sanitoral lorsque de nouvelles donnees sont disponibles.

## Objectif

Sanitoral souhaite pouvoir actualiser l'analyse sans refaire manuellement le nettoyage des donnees.

La procedure repose sur Power Query et sur le fichier Power BI final : `Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`.

## Pre-requis

- Power BI Desktop installe.
- Fichier Excel source Sanitoral disponible.
- Fichier `Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix` ouvert.
- Structure des 7 feuilles sources conservee dans le fichier Excel.

## Procedure utilisateur

1. Ouvrir `livrables/02_powerbi/Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`.
2. Verifier que le nouveau fichier Excel conserve les memes feuilles et colonnes.
3. Dans Power BI, ouvrir `Transformer les donnees`.
4. Verifier le chemin du fichier source si besoin.
5. Cliquer sur `Actualiser l'apercu`.
6. Verifier que les etapes Power Query ne contiennent pas d'erreur.
7. Controler que seule la table finale `Fact_ProjectPhasePerformance` est chargee dans le modele.
8. Cliquer sur `Fermer et appliquer`.
9. Cliquer sur `Actualiser` dans Power BI.
10. Controler les KPI principaux.
11. Verifier les pages `Vue executive` et `Detail des alertes`.
12. Exporter le rapport si une version PDF est necessaire.

## Controles apres actualisation

Valeurs attendues sans filtre actif :

| Controle | Valeur attendue |
|---|---:|
| Nb Projets | 104 |
| Nb Phases | 520 |
| Nb Phases en alerte | 348 |
| Taux phases en alerte | 66,92 % |
| Nb alertes cout | 214 |
| Nb alertes duree | 159 |
| Nb alertes livrables | 96 |

Verifier egalement :

- absence d'erreur Power Query ;
- absence de valeur vide dans les colonnes critiques ;
- coherence des totaux de couts, durees et livrables ;
- fonctionnement des filtres `Project_Type`, `Country`, `Region`, `Alert_Status`, `Phase` ;
- affichage correct des KPI et graphiques sur la page `Vue executive` ;
- tableau filtre sur les alertes et tri decroissant sur `Alert_Count` dans la page `Detail des alertes`.

## Colonnes critiques

| Colonne | Pourquoi elle est critique |
|---|---|
| `Project_ID` | Identifie les projets. |
| `Phase` | Identifie les phases. |
| `ProjectPhaseKey` | Permet les jointures au niveau projet-phase. |
| `Start_Date` | Permet l'analyse temporelle. |
| `Country` | Permet l'analyse geographique. |
| `Region` | Permet l'analyse par zone. |
| `Planned_Cost` / `Actual_Cost` | Mesure les ecarts de couts. |
| `Planned_Duration` / `Actual_Duration` | Mesure les ecarts de delais. |
| `Planned_Deliverables` / `Actual_Deliverables` | Mesure les ecarts de livrables. |
| `Alert_Count` / `Alert_Status` | Alimente la page de detail des alertes. |

## Points de vigilance

- Ne pas renommer les feuilles du fichier Excel source.
- Ne pas supprimer les colonnes utilisees par Power BI.
- Ne pas changer le sens des donnees prevues et reelles.
- Ne pas reactiver le chargement des tables intermediaires sauf besoin exceptionnel.
- Controler les valeurs nulles ou egales a zero dans les colonnes de reference.
