# Procedure de mise a jour

Ce document explique comment mettre a jour le rapport Power BI Sanitoral lorsque de nouvelles donnees sont disponibles.

## Objectif

Sanitoral souhaite mettre a jour l'analyse toutes les semaines.

La procedure doit permettre de remplacer ou actualiser le fichier source sans refaire manuellement le nettoyage.

## Pre-requis

- Power BI Desktop installe.
- Fichier Excel source Sanitoral disponible.
- Rapport Power BI final ouvert.
- Structure des feuilles conservee dans le fichier source.

## Procedure utilisateur

1. Ouvrir le fichier Power BI `Sanitoral_Dashboard.pbix`.
2. Verifier que le nouveau fichier Excel conserve les memes feuilles.
3. Dans Power BI, ouvrir `Transformer les donnees`.
4. Verifier le chemin du fichier source si besoin.
5. Cliquer sur `Actualiser l'apercu`.
6. Verifier que les etapes Power Query ne contiennent pas d'erreur.
7. Cliquer sur `Fermer et appliquer`.
8. Cliquer sur `Actualiser` dans Power BI.
9. Controler les KPI principaux.
10. Exporter le rapport si une version PDF est necessaire.

## Controles apres mise a jour

Verifier :

- nombre de projets ;
- nombre de phases ;
- absence d'erreur Power Query ;
- absence de valeur vide dans les colonnes critiques ;
- coherence des totaux de couts, durees et livrables ;
- fonctionnement des filtres ;
- affichage correct de la carte geographique.

## Colonnes critiques

| Colonne | Pourquoi elle est critique |
|---|---|
| `Project_ID` | Identifie les projets |
| `Phase` | Identifie les phases |
| `ProjectPhaseKey` | Permet les jointures au niveau projet-phase |
| `Start Date` | Permet l'analyse temporelle |
| `Country` | Permet l'analyse geographique |
| `Region` | Permet l'analyse par zone |
| `Planned_Cost` / `Actual_Cost` | Mesure les ecarts de couts |
| `Planned_Duration` / `Actual_Duration` | Mesure les ecarts de delais |
| `Planned_Deliverables` / `Actual_Deliverables` | Mesure les ecarts de livrables |

## Points de vigilance

- Ne pas renommer les feuilles du fichier Excel source.
- Ne pas supprimer les colonnes utilisees par Power BI.
- Ne pas changer le sens des donnees prevues et reelles.
- Verifier les nouveaux pays si une carte Power BI est utilisee.
- Controler les valeurs nulles ou egales a zero dans les colonnes de reference.

