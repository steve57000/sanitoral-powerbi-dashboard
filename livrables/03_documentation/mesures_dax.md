# Mesures DAX

Ce document centralise les mesures DAX du rapport Power BI Sanitoral.

Table utilisée :

```text
Fact_ProjectPhasePerformance
```

## Volumétrie

```DAX
Nb Projets =
DISTINCTCOUNT(Fact_ProjectPhasePerformance[Project_ID])
```

```DAX
Nb Phases =
COUNTROWS(Fact_ProjectPhasePerformance)
```

## Coûts

```DAX
Coût Prévu =
SUM(Fact_ProjectPhasePerformance[Planned_Cost])
```

```DAX
Coût Réel =
SUM(Fact_ProjectPhasePerformance[Actual_Cost])
```

```DAX
Écart Coût =
[Coût Réel] - [Coût Prévu]
```

```DAX
Écart Coût % =
DIVIDE([Écart Coût], [Coût Prévu])
```

## Durées

```DAX
Durée Prévue =
SUM(Fact_ProjectPhasePerformance[Planned_Duration])
```

```DAX
Durée Réelle =
SUM(Fact_ProjectPhasePerformance[Actual_Duration])
```

```DAX
Écart Durée =
[Durée Réelle] - [Durée Prévue]
```

```DAX
Écart Durée % =
DIVIDE([Écart Durée], [Durée Prévue])
```

## Livrables

```DAX
Livrables Prévus =
SUM(Fact_ProjectPhasePerformance[Planned_Deliverables])
```

```DAX
Livrables Réels =
SUM(Fact_ProjectPhasePerformance[Actual_Deliverables])
```

```DAX
Écart Livrables =
[Livrables Réels] - [Livrables Prévus]
```

```DAX
Écart Livrables % =
DIVIDE([Écart Livrables], [Livrables Prévus])
```

## Alertes

Les mesures d'alerte utilisent `VALUE()` et `IFERROR()` afin de rester robustes si les colonnes d'alerte sont importees ou conservées en texte dans Power BI.

```DAX
Nb alertes coût =
COUNTROWS(
    FILTER(
        Fact_ProjectPhasePerformance,
        IFERROR(VALUE(Fact_ProjectPhasePerformance[Cost_Alert]), 0) = 1
    )
)
```

```DAX
Nb alertes durée =
COUNTROWS(
    FILTER(
        Fact_ProjectPhasePerformance,
        IFERROR(VALUE(Fact_ProjectPhasePerformance[Duration_Alert]), 0) = 1
    )
)
```

```DAX
Nb alertes livrables =
COUNTROWS(
    FILTER(
        Fact_ProjectPhasePerformance,
        IFERROR(VALUE(Fact_ProjectPhasePerformance[Deliverables_Alert]), 0) = 1
    )
)
```

```DAX
Nb Phases en alerte =
COUNTROWS(
    FILTER(
        Fact_ProjectPhasePerformance,
        IFERROR(VALUE(Fact_ProjectPhasePerformance[Alert_Count]), 0) > 0
    )
)
```

```DAX
Taux phases en alerte =
COALESCE(
    DIVIDE([Nb Phases en alerte], [Nb Phases]),
    0
)
```

```DAX
Nb Alertes =
SUMX(
    Fact_ProjectPhasePerformance,
    IFERROR(VALUE(Fact_ProjectPhasePerformance[Alert_Count]), 0)
)
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

Sans filtre actif, les mesures doivent retourner :

| Mesure | Valeur attendue |
|---|---:|
| `Nb Projets` | 104 |
| `Nb Phases` | 520 |
| `Nb Phases en alerte` | 348 |
| `Taux phases en alerte` | 66,92 % |
| `Nb alertes coût` | 214 |
| `Nb alertes durée` | 159 |
| `Nb alertes livrables` | 96 |

## Format recommandé

| Mesure | Format |
|---|---|
| Montants | Devise, séparateur de milliers |
| Pourcentages | Pourcentage, 1 à 2 décimales selon le visuel |
| Volumes | Nombre entier |
| Scores et alertes | Nombre entier |
