# Modele de donnees

Ce document decrit le modele de donnees final du rapport Power BI Sanitoral.

## Principe retenu

Le modele final est volontairement simple : une seule table est chargee dans Power BI, `Fact_ProjectPhasePerformance`.

Les 7 tables sources sont utilisees dans Power Query pour nettoyer, typer, creer les cles et realiser les jointures. Elles ne sont pas chargees dans le modele final.

## Grain d'analyse

Le grain principal est la phase d'un projet :

```text
1 projet + 1 phase
```

La cle logique est :

```text
ProjectPhaseKey = Text.From([Project_ID]) & "|" & [Phase]
```

## Tables sources Power Query

| Table source | Role |
|---|---|
| `Projects_plans` | Donnees prevues par projet et phase. |
| `Project type` | Type de projet. |
| `Actual_Costs` | Couts reels par projet et phase. |
| `Actual_Duration` | Durees reelles par projet et phase. |
| `Actual_Delivrable` | Livrables reels par projet et phase. |
| `Projects_Locations` | Pays de chaque projet. |
| `Country_Profiles` | Region et type d'entite. |

## Table finale chargee

`Fact_ProjectPhasePerformance` contient les informations prevues, les valeurs reelles, les attributs projet/pays et les indicateurs d'alerte.

Colonnes principales :

| Colonne | Role |
|---|---|
| `Project_ID` | Identifiant du projet. |
| `Phase` | Phase du projet. |
| `Start_Date` | Date de debut de la phase. |
| `Planned_Duration` | Duree prevue. |
| `Planned_Cost` | Cout prevu. |
| `Planned_Deliverables` | Livrables prevus. |
| `ProjectPhaseKey` | Cle unique projet-phase. |
| `Actual_Cost` | Cout reel. |
| `Actual_Duration` | Duree reelle. |
| `Actual_Deliverables` | Livrables reels. |
| `Project_Type` | Type de projet. |
| `Country` | Pays. |
| `Region` | Region. |
| `Entity_Type` | Type d'entite locale. |
| `Cost_Difference_Pct` | Ecart de cout en pourcentage. |
| `Cost_Alert` | Alerte cout. |
| `Duration_Alert` | Alerte duree. |
| `Deliverables_Alert` | Alerte livrables. |
| `Any_Alert` | Alerte globale. |
| `Alert_Count` | Nombre d'alertes. |
| `Alert_Status` | Statut d'alerte. |

## Relations

Aucune relation n'est necessaire dans le modele final, car les jointures ont deja ete integrees dans `Fact_ProjectPhasePerformance` avec Power Query.

Ce choix reduit le risque d'erreur de relation, facilite la soutenance et rend les mesures DAX plus directes.

## Points de vigilance

- `Phase` seule ne doit pas etre utilisee comme cle unique.
- `Project_ID` seul ne suffit pas pour relier les couts, durees et livrables au niveau phase.
- Les colonnes finales doivent conserver les noms `Start_Date` et `Entity_Type`.
- Les tables intermediaires doivent rester desactivees au chargement.
- Les valeurs de controle doivent etre verifiees apres actualisation.
