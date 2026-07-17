# Mesures et colonnes DAX

Ce document centralise les calculs du modèle relationnel Sanitoral.

## Pré-requis

Les relations sur `ProjectPhaseKey` doivent être actives entre `Projects_Plans` et les trois tables `Actual_*`. Les colonnes numériques et les indicateurs d'alerte doivent être correctement typés ; `VALUE()` et `IFERROR()` ne doivent pas servir à compenser un type Texte incorrect.

## Colonnes calculées dans Projects_Plans

### Écarts

```DAX
Cost_Difference_Pct =
VAR PlannedCost = Projects_Plans[Planned_Cost]
VAR ActualCost = RELATED(Actual_Costs[Actual_Cost])
RETURN
    DIVIDE(ActualCost - PlannedCost, PlannedCost)
```

```DAX
Duration_Difference_Pct =
VAR PlannedDuration = Projects_Plans[Planned_Duration]
VAR ActualDuration = RELATED(Actual_Duration[Actual_Duration])
RETURN
    DIVIDE(ActualDuration - PlannedDuration, PlannedDuration)
```

```DAX
Deliverables_Difference_Pct =
VAR PlannedDeliverables = Projects_Plans[Planned_Deliverables]
VAR ActualDeliverables = RELATED(Actual_Deliverables[Actual_Deliverables])
RETURN
    DIVIDE(ActualDeliverables - PlannedDeliverables, PlannedDeliverables)
```

### Alertes au seuil strict de 15 %

```DAX
Cost_Alert =
IF(Projects_Plans[Cost_Difference_Pct] > 0.15, 1, 0)
```

```DAX
Duration_Alert =
IF(Projects_Plans[Duration_Difference_Pct] > 0.15, 1, 0)
```

```DAX
Deliverables_Alert =
IF(Projects_Plans[Deliverables_Difference_Pct] < -0.15, 1, 0)
```

```DAX
Alert_Count =
    Projects_Plans[Cost_Alert]
    + Projects_Plans[Duration_Alert]
    + Projects_Plans[Deliverables_Alert]
```

```DAX
Any_Alert =
IF(Projects_Plans[Alert_Count] > 0, 1, 0)
```

```DAX
Alert_Status =
IF(Projects_Plans[Any_Alert] = 1, "En alerte", "OK")
```

### Libellé Gantt

```DAX
Gantt_Task =
"P" & FORMAT(Projects_Plans[Project_ID], "0")
    & " - " & Projects_Plans[Phase]
```

## Mesures de volumétrie

```DAX
Nb Projets =
DISTINCTCOUNT(Projects_Plans[Project_ID])
```

```DAX
Nb Projets en alerte =
CALCULATE(
    DISTINCTCOUNT(Projects_Plans[Project_ID]),
    FILTER(Projects_Plans, Projects_Plans[Alert_Count] > 0)
)
```

```DAX
Nb Phases =
COUNTROWS(Projects_Plans)
```

```DAX
Nb Phases en alerte =
CALCULATE(
    COUNTROWS(Projects_Plans),
    Projects_Plans[Alert_Count] > 0
)
```

```DAX
Nb Phases OK =
[Nb Phases] - [Nb Phases en alerte]
```

```DAX
Taux phases en alerte =
COALESCE(DIVIDE([Nb Phases en alerte], [Nb Phases]), 0)
```

## Mesures de coûts

```DAX
Coût Prévu =
SUM(Projects_Plans[Planned_Cost])
```

```DAX
Coût Réel =
SUM(Actual_Costs[Actual_Cost])
```

```DAX
Écart Coût =
[Coût Réel] - [Coût Prévu]
```

```DAX
Écart Coût % =
DIVIDE([Écart Coût], [Coût Prévu])
```

## Mesures de durées

```DAX
Durée Prévue =
SUM(Projects_Plans[Planned_Duration])
```

```DAX
Durée Réelle =
SUM(Actual_Duration[Actual_Duration])
```

```DAX
Écart Durée =
[Durée Réelle] - [Durée Prévue]
```

```DAX
Écart Durée % =
DIVIDE([Écart Durée], [Durée Prévue])
```

## Mesures de livrables

```DAX
Livrables Prévus =
SUM(Projects_Plans[Planned_Deliverables])
```

```DAX
Livrables Réels =
SUM(Actual_Deliverables[Actual_Deliverables])
```

```DAX
Écart Livrables =
[Livrables Réels] - [Livrables Prévus]
```

```DAX
Écart Livrables % =
DIVIDE([Écart Livrables], [Livrables Prévus])
```

## Mesures d'alerte

```DAX
Nb alertes coût =
SUM(Projects_Plans[Cost_Alert])
```

```DAX
Nb alertes durée =
SUM(Projects_Plans[Duration_Alert])
```

```DAX
Nb alertes livrables =
SUM(Projects_Plans[Deliverables_Alert])
```

```DAX
Nb Alertes =
SUM(Projects_Plans[Alert_Count])
```

```DAX
Taux alertes coût =
DIVIDE([Nb alertes coût], [Nb Phases])
```

```DAX
Taux alertes durée =
DIVIDE([Nb alertes durée], [Nb Phases])
```

```DAX
Taux alertes livrables =
DIVIDE([Nb alertes livrables], [Nb Phases])
```

## Valeurs de contrôle attendues

| Mesure | Valeur attendue |
|---|---:|
| `Nb Projets` | 104 |
| `Nb Projets en alerte` | 102 |
| `Nb Phases` | 520 |
| `Nb Phases en alerte` | 348 |
| `Taux phases en alerte` | 66,92 % |
| `Nb alertes coût` | 214 |
| `Nb alertes durée` | 159 |
| `Nb alertes livrables` | 96 |
| `Nb Alertes` | 469 |
| `Coût Prévu` | 56 108 000 USD |
| `Coût Réel` | 60 200 800 USD |
| `Écart Coût %` | 7,29 % |

## Analyses de contrôle utiles

| Segment | Phases en alerte | Total phases | Taux |
|---|---:|---:|---:|
| IT - CRM Implementation | 225 | 312 | 72,12 % |
| Marketing - Launch of new product | 123 | 208 | 59,13 % |
| Phase D - Testing | 52 | 52 | 100,00 % |

## Formats

| Mesure | Format recommandé |
|---|---|
| Coûts | USD, par exemple `60,20 M$` sur les cartes |
| Pourcentages | 1 à 2 décimales |
| Volumes et alertes | Nombre entier |

Le dictionnaire définit les coûts en USD. Aucun visuel ne doit afficher le symbole euro.
