# Modèle de données

Ce document décrit le modèle de données final du rapport Power BI Sanitoral.

## Principe retenu

Le modèle final est volontairement simple : une seule table est chargée dans Power BI, `Fact_ProjectPhasePerformance`.

Les 7 tables sources sont utilisées dans Power Query pour nettoyer, typer, créer les clés et réaliser les jointures. Elles ne sont pas chargées dans le modèle final.

## Grain d'analyse

Le grain principal est la phase d'un projet :

```text
1 projet + 1 phase
```

La clé logique est :

```text
ProjectPhaseKey = Text.From([Project_ID]) & "|" & [Phase]
```

## Tables sources Power Query

| Table source | Rôle |
|---|---|
| `Projects_plans` | Données prévues par projet et phase. |
| `Project type` | Type de projet. |
| `Actual_Costs` | Coûts réels par projet et phase. |
| `Actual_Duration` | Durées réelles par projet et phase. |
| `Actual_Delivrable` | Livrables réels par projet et phase. |
| `Projects_Locations` | Pays de chaque projet. |
| `Country_Profiles` | Région et type d'entité. |

## Table finale chargée

`Fact_ProjectPhasePerformance` contient les informations prévues, les valeurs réelles, les attributs projet/pays et les indicateurs d'alerte.

Colonnes principales :

| Colonne | Rôle |
|---|---|
| `Project_ID` | Identifiant du projet. |
| `Phase` | Phase du projet. |
| `Start_Date` | Date de début de la phase. |
| `Planned_Duration` | Durée prévue. |
| `Planned_Cost` | Coût prévu. |
| `Planned_Deliverables` | Livrables prévus. |
| `ProjectPhaseKey` | Clé unique projet-phase. |
| `Actual_Cost` | Coût réel. |
| `Actual_Duration` | Durée réelle. |
| `Actual_Deliverables` | Livrables réels. |
| `Project_Type` | Type de projet. |
| `Country` | Pays. |
| `Region` | Région. |
| `Entity_Type` | Type d'entité locale. |
| `Cost_Difference_Pct` | Écart de coût en pourcentage. |
| `Cost_Alert` | Alerte coût. |
| `Duration_Alert` | Alerte durée. |
| `Deliverables_Alert` | Alerte livrables. |
| `Any_Alert` | Alerte globale. |
| `Alert_Count` | Nombre d'alertes. |
| `Alert_Status` | Statut d'alerte. |

## Relations

Aucune relation n'est nécessaire dans le modèle final, car les jointures ont déjà été intégrées dans `Fact_ProjectPhasePerformance` avec Power Query.

Ce choix réduit le risque d'erreur de relation, facilite la soutenance et rend les mesures DAX plus directes.

## Points de vigilance

- `Phase` seule ne doit pas être utilisée comme clé unique.
- `Project_ID` seul ne suffit pas pour relier les coûts, durées et livrables au niveau phase.
- Les colonnes finales doivent conserver les noms `Start_Date` et `Entity_Type`.
- Les tables intermédiaires doivent rester désactivées au chargement.
- Les valeurs de contrôle doivent être vérifiées après actualisation.
