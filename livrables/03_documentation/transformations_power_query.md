# Transformations Power Query

Ce document décrit les transformations appliquées dans Power Query pour construire le modèle final du dashboard Power BI Sanitoral.

## Objectif

Préparer les données Sanitoral sans modifier manuellement le fichier Excel source, puis produire une table finale unique chargée dans le modèle Power BI : `Fact_ProjectPhasePerformance`.

Les tables sources nettoyées restent utilisées dans Power Query pour les jointures et les calculs, mais leur chargement est désactivé dans le modèle final.

## Feuilles sources documentées

| Feuille source | Rôle dans la préparation |
|---|---|
| `Projects_plans` | Données prévues par projet et phase : dates, durées, coûts et livrables planifiés. |
| `Project type` | Enrichissement de chaque projet avec son type : IT ou Marketing. |
| `Actual_Costs` | Coûts réels observés par projet et phase. |
| `Actual_Duration` | Durées réelles observées par projet et phase. |
| `Actual_Delivrable` | Livrables réels observés par projet et phase. |
| `Projects_Locations` | Association entre les projets et les pays. |
| `Country_Profiles` | Enrichissement pays avec région et type d'entité. |

## Étapes communes de nettoyage

Pour chaque feuille :

1. Importer la feuille Excel dans Power Query.
2. Supprimer les lignes descriptives ou vides avant les vrais en-têtes.
3. Promouvoir la première ligne utile comme en-tête.
4. Supprimer les lignes entièrement vides.
5. Renommer les colonnes avec une convention stable.
6. Corriger les types de données.
7. Nettoyer les espaces inutiles dans les champs texte.
8. Contrôler les doublons et les valeurs manquantes avant jointure.

## Création de la clé ProjectPhaseKey

Une clé projet-phase est créée dans les tables au grain projet + phase afin de garantir des jointures fiables.

```powerquery
Text.From([Project_ID]) & "|" & [Phase]
```

Nom de la colonne : `ProjectPhaseKey`.

Cette clé est nécessaire car `Project_ID` seul n'est pas unique au niveau phase, et `Phase` seule n'identifie pas un projet.

## Construction de Fact_ProjectPhasePerformance

La table finale `Fact_ProjectPhasePerformance` est construite à partir de `Projects_plans`, enrichie par jointures avec :

- `Actual_Costs` via `ProjectPhaseKey` ;
- `Actual_Duration` via `ProjectPhaseKey` ;
- `Actual_Delivrable` via `ProjectPhaseKey` ;
- `Project type` via `Project_ID` ;
- `Projects_Locations` via `Project_ID` ;
- `Country_Profiles` via `Country`.

Des colonnes de performance et d'alerte sont ensuite ajoutées pour comparer le prévu et le réel.

## Colonnes finales

La table finale chargée contient les colonnes suivantes :

| Colonne | Description |
|---|---|
| `Project_ID` | Identifiant du projet. |
| `Phase` | Phase du projet. |
| `Start_Date` | Date de début de la phase. |
| `Planned_Duration` | Durée prévue. |
| `Planned_Cost` | Coût prévu. |
| `Planned_Deliverables` | Nombre de livrables prévus. |
| `ProjectPhaseKey` | Clé unique projet-phase. |
| `Actual_Cost` | Coût réel. |
| `Actual_Duration` | Durée réelle. |
| `Actual_Deliverables` | Nombre de livrables réels. |
| `Project_Type` | Type de projet. |
| `Country` | Pays du projet. |
| `Region` | Région du pays. |
| `Entity_Type` | Type d'entité locale. |
| `Cost_Difference_Pct` | Écart de coût en pourcentage. |
| `Cost_Alert` | Indicateur d'alerte coût. |
| `Duration_Alert` | Indicateur d'alerte durée. |
| `Deliverables_Alert` | Indicateur d'alerte livrables. |
| `Any_Alert` | Indicateur global d'alerte. |
| `Alert_Count` | Nombre d'alertes sur la ligne. |
| `Alert_Status` | Statut lisible : en alerte ou sans alerte. |

## Chargement dans le modèle

Seule la table `Fact_ProjectPhasePerformance` est chargée dans le modèle Power BI final.

Les tables intermédiaires issues des 7 feuilles sources sont conservées dans Power Query pour documenter et automatiser la préparation, mais l'option de chargement est désactivée pour éviter de surcharger le modèle.

## Contrôles qualité

Valeurs attendues sans filtre actif :

| Contrôle | Valeur attendue |
|---|---:|
| Nombre de projets | 104 |
| Nombre de phases | 520 |
| Phases en alerte | 348 |
| Alertes coût | 214 |
| Alertes durée | 159 |
| Alertes livrables | 96 |

Autres contrôles :

- absence de doublon sur `ProjectPhaseKey` ;
- absence de valeur manquante après jointure ;
- correspondance complète entre projets, types, pays et régions ;
- types numériques correctement reconnus ;
- dates correctement reconnues ;
- colonnes d'alerte exploitables par les mesures DAX robustes.
