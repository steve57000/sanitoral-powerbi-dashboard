# Transformations Power Query

Ce document decrit les transformations appliquees dans Power Query pour construire le modele final du dashboard Power BI Sanitoral.

## Objectif

Preparer les donnees Sanitoral sans modifier manuellement le fichier Excel source, puis produire une table finale unique chargee dans le modele Power BI : `Fact_ProjectPhasePerformance`.

Les tables sources nettoyees restent utilisees dans Power Query pour les jointures et les calculs, mais leur chargement est desactive dans le modele final.

## Feuilles sources documentees

| Feuille source | Role dans la preparation |
|---|---|
| `Projects_plans` | Donnees prevues par projet et phase : dates, durees, couts et livrables planifies. |
| `Project type` | Enrichissement de chaque projet avec son type : IT ou Marketing. |
| `Actual_Costs` | Couts reels observes par projet et phase. |
| `Actual_Duration` | Durees reelles observees par projet et phase. |
| `Actual_Delivrable` | Livrables reels observes par projet et phase. |
| `Projects_Locations` | Association entre les projets et les pays. |
| `Country_Profiles` | Enrichissement pays avec region et type d'entite. |

## Etapes communes de nettoyage

Pour chaque feuille :

1. Importer la feuille Excel dans Power Query.
2. Supprimer les lignes descriptives ou vides avant les vrais en-tetes.
3. Promouvoir la premiere ligne utile comme en-tete.
4. Supprimer les lignes entierement vides.
5. Renommer les colonnes avec une convention stable.
6. Corriger les types de donnees.
7. Nettoyer les espaces inutiles dans les champs texte.
8. Controler les doublons et les valeurs manquantes avant jointure.

## Creation de la cle ProjectPhaseKey

Une cle projet-phase est creee dans les tables au grain projet + phase afin de garantir des jointures fiables.

```powerquery
Text.From([Project_ID]) & "|" & [Phase]
```

Nom de la colonne : `ProjectPhaseKey`.

Cette cle est necessaire car `Project_ID` seul n'est pas unique au niveau phase, et `Phase` seule n'identifie pas un projet.

## Construction de Fact_ProjectPhasePerformance

La table finale `Fact_ProjectPhasePerformance` est construite a partir de `Projects_plans`, enrichie par jointures avec :

- `Actual_Costs` via `ProjectPhaseKey` ;
- `Actual_Duration` via `ProjectPhaseKey` ;
- `Actual_Delivrable` via `ProjectPhaseKey` ;
- `Project type` via `Project_ID` ;
- `Projects_Locations` via `Project_ID` ;
- `Country_Profiles` via `Country`.

Des colonnes de performance et d'alerte sont ensuite ajoutees pour comparer le prevu et le reel.

## Colonnes finales

La table finale chargee contient les colonnes suivantes :

| Colonne | Description |
|---|---|
| `Project_ID` | Identifiant du projet. |
| `Phase` | Phase du projet. |
| `Start_Date` | Date de debut de la phase. |
| `Planned_Duration` | Duree prevue. |
| `Planned_Cost` | Cout prevu. |
| `Planned_Deliverables` | Nombre de livrables prevus. |
| `ProjectPhaseKey` | Cle unique projet-phase. |
| `Actual_Cost` | Cout reel. |
| `Actual_Duration` | Duree reelle. |
| `Actual_Deliverables` | Nombre de livrables reels. |
| `Project_Type` | Type de projet. |
| `Country` | Pays du projet. |
| `Region` | Region du pays. |
| `Entity_Type` | Type d'entite locale. |
| `Cost_Difference_Pct` | Ecart de cout en pourcentage. |
| `Cost_Alert` | Indicateur d'alerte cout. |
| `Duration_Alert` | Indicateur d'alerte duree. |
| `Deliverables_Alert` | Indicateur d'alerte livrables. |
| `Any_Alert` | Indicateur global d'alerte. |
| `Alert_Count` | Nombre d'alertes sur la ligne. |
| `Alert_Status` | Statut lisible : en alerte ou sans alerte. |

## Chargement dans le modele

Seule la table `Fact_ProjectPhasePerformance` est chargee dans le modele Power BI final.

Les tables intermediaires issues des 7 feuilles sources sont conservees dans Power Query pour documenter et automatiser la preparation, mais l'option de chargement est desactivee pour eviter de surcharger le modele.

## Controles qualite

Valeurs attendues sans filtre actif :

| Controle | Valeur attendue |
|---|---:|
| Nombre de projets | 104 |
| Nombre de phases | 520 |
| Phases en alerte | 348 |
| Alertes cout | 214 |
| Alertes duree | 159 |
| Alertes livrables | 96 |

Autres controles :

- absence de doublon sur `ProjectPhaseKey` ;
- absence de valeur manquante apres jointure ;
- correspondance complete entre projets, types, pays et regions ;
- types numeriques correctement reconnus ;
- dates correctement reconnues ;
- colonnes d'alerte exploitables par les mesures DAX robustes.
