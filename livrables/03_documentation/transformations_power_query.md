# Transformations Power Query

Ce document liste les transformations a appliquer dans Power Query Editor pour rendre le nettoyage automatique et reproductible.

## Objectif

Preparer les donnees Sanitoral sans modifier manuellement le fichier Excel source.

Le fichier source contient plusieurs feuilles avec :

- des lignes descriptives avant les vrais en-tetes ;
- des noms de colonnes incoherents selon les tables ;
- des types de donnees a corriger ;
- des tables a relier au niveau projet-phase.

## Feuilles a importer

| Feuille source | Role |
|---|---|
| `Projects_plans` | Previsions par projet et phase |
| `Project type` | Type de projet |
| `Actual_Costs` | Couts reels |
| `Actual_Duration` | Durees reelles |
| `Actual_Delivrable` | Livrables reels |
| `Projects_Locations` | Pays des projets |
| `Country_Profiles` | Region et type de pays |

## Etapes communes

Pour chaque table :

1. Importer la feuille depuis Excel.
2. Supprimer les lignes vides ou descriptives avant l'en-tete.
3. Promouvoir la premiere ligne utile comme en-tete.
4. Supprimer les lignes entierement vides.
5. Renommer les colonnes.
6. Corriger les types de donnees.
7. Supprimer les espaces inutiles dans les textes.

## Renommage recommande

| Colonne source | Colonne cible |
|---|---|
| `Project ID` | `Project_ID` |
| `Proj_ID` | `Project_ID` |
| `Project` | `Project_ID` |
| `ID` | `Project_ID` |
| `Project Type` | `Project_Type` |
| `Planned_Delivrable` | `Planned_Deliverables` |
| `Actual_Deliverables` | `Actual_Deliverables` |

## Types de donnees

| Colonne | Type Power BI |
|---|---|
| `Project_ID` | Nombre entier |
| `Project_Type` | Texte |
| `Country` | Texte |
| `Region` | Texte |
| `Type` | Texte |
| `Phase` | Texte |
| `Start Date` | Date |
| `Planned_Duration` | Nombre entier |
| `Actual_Duration` | Nombre entier |
| `Planned_Cost` | Nombre decimal ou entier |
| `Actual_Cost` | Nombre decimal ou entier |
| `Planned_Deliverables` | Nombre entier |
| `Actual_Deliverables` | Nombre entier |

## Cle unique projet-phase

Creer une colonne personnalisee dans les tables de phases :

```powerquery
Text.From([Project_ID]) & "|" & [Phase]
```

Nom recommande :

```text
ProjectPhaseKey
```

## Colonnes d'ecart recommandees

Les colonnes peuvent etre creees dans Power Query ou en DAX. Pour les alertes ligne par ligne, Power Query est pratique.

```text
Cost_Variance = Actual_Cost - Planned_Cost
Duration_Variance = Actual_Duration - Planned_Duration
Deliverables_Variance = Actual_Deliverables - Planned_Deliverables
```

```text
Cost_Variance_Pct = Cost_Variance / Planned_Cost
Duration_Variance_Pct = Duration_Variance / Planned_Duration
Deliverables_Variance_Pct = Deliverables_Variance / Planned_Deliverables
```

## Colonnes d'alerte

Regle Sanitoral :

- alerte cout si le cout reel depasse le cout prevu de plus de 15 % ;
- alerte duree si la duree reelle depasse la duree prevue de plus de 15 % ;
- alerte livrables si les livrables reels sont inferieurs au prevu de plus de 15 %.

```text
Alert_Cost = Cost_Variance_Pct > 0.15
Alert_Duration = Duration_Variance_Pct > 0.15
Alert_Deliverables = Deliverables_Variance_Pct < -0.15
Any_Alert = Alert_Cost or Alert_Duration or Alert_Deliverables
```

## Controles qualite

A verifier apres nettoyage :

- nombre de projets : 104 ;
- nombre de phases : 520 ;
- absence de doublon sur `ProjectPhaseKey` ;
- absence de valeur manquante apres jointure ;
- correspondance complete entre projets, types, pays et regions ;
- types numeriques correctement reconnus ;
- dates correctement reconnues.

