# Mesures DAX

Ce document centralise les mesures DAX du rapport Power BI Sanitoral.

Table utilisee :

```text
Fact_ProjectPhasePerformance
```

## Volumetrie

```DAX
Nb Projets =
DISTINCTCOUNT(Fact_ProjectPhasePerformance[Project_ID])
```

```DAX
Nb Phases =
COUNTROWS(Fact_ProjectPhasePerformance)
```

## Couts

```DAX
Cout Prevu =
SUM(Fact_ProjectPhasePerformance[Planned_Cost])
```

```DAX
Cout Reel =
SUM(Fact_ProjectPhasePerformance[Actual_Cost])
```

```DAX
Ecart Cout =
[Cout Reel] - [Cout Prevu]
```

```DAX
Ecart Cout % =
DIVIDE([Ecart Cout], [Cout Prevu])
```

## Durees

```DAX
Duree Prevue =
SUM(Fact_ProjectPhasePerformance[Planned_Duration])
```

```DAX
Duree Reelle =
SUM(Fact_ProjectPhasePerformance[Actual_Duration])
```

```DAX
Ecart Duree =
[Duree Reelle] - [Duree Prevue]
```

```DAX
Ecart Duree % =
DIVIDE([Ecart Duree], [Duree Prevue])
```

## Livrables

```DAX
Livrables Prevus =
SUM(Fact_ProjectPhasePerformance[Planned_Deliverables])
```

```DAX
Livrables Reels =
SUM(Fact_ProjectPhasePerformance[Actual_Deliverables])
```

```DAX
Ecart Livrables =
[Livrables Reels] - [Livrables Prevus]
```

```DAX
Ecart Livrables % =
DIVIDE([Ecart Livrables], [Livrables Prevus])
```

## Alertes

Les mesures d'alerte utilisent `VALUE()` et `IFERROR()` afin de rester robustes si les colonnes d'alerte sont importees ou conservees en texte dans Power BI.

```DAX
Nb alertes cout =
COUNTROWS(
    FILTER(
        Fact_ProjectPhasePerformance,
        IFERROR(VALUE(Fact_ProjectPhasePerformance[Cost_Alert]), 0) = 1
    )
)
```

```DAX
Nb alertes duree =
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
Taux alertes cout =
DIVIDE([Nb alertes cout], [Nb Phases])
```

```DAX
Taux alertes duree =
DIVIDE([Nb alertes duree], [Nb Phases])
```

```DAX
Taux alertes livrables =
DIVIDE([Nb alertes livrables], [Nb Phases])
```

## Valeurs de controle attendues

Sans filtre actif, les mesures doivent retourner :

| Mesure | Valeur attendue |
|---|---:|
| `Nb Projets` | 104 |
| `Nb Phases` | 520 |
| `Nb Phases en alerte` | 348 |
| `Taux phases en alerte` | 66,92 % |
| `Nb alertes cout` | 214 |
| `Nb alertes duree` | 159 |
| `Nb alertes livrables` | 96 |

## Format recommande

| Mesure | Format |
|---|---|
| Montants | Devise, separateur de milliers |
| Pourcentages | Pourcentage, 1 a 2 decimales selon le visuel |
| Volumes | Nombre entier |
| Scores et alertes | Nombre entier |
