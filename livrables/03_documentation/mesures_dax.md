# Mesures DAX

Ce document centralise les mesures DAX du rapport Power BI Sanitoral.

Le nom de table utilise ci-dessous est :

```text
Fact_ProjectPhasePerformance
```

Il pourra etre adapte selon le nom final dans Power BI.

## Volumetrie

```DAX
Nb Projets =
DISTINCTCOUNT(Fact_ProjectPhasePerformance[Project_ID])
```

```DAX
Nb Phases =
COUNTROWS(Fact_ProjectPhasePerformance)
```

```DAX
Nb Pays =
DISTINCTCOUNT(Fact_ProjectPhasePerformance[Country])
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

Si les colonnes d'alerte sont creees en Power Query sous forme 0/1 :

```DAX
Nb Alertes Cout =
SUM(Fact_ProjectPhasePerformance[Alert_Cost])
```

```DAX
Nb Alertes Duree =
SUM(Fact_ProjectPhasePerformance[Alert_Duration])
```

```DAX
Nb Alertes Livrables =
SUM(Fact_ProjectPhasePerformance[Alert_Deliverables])
```

```DAX
Nb Phases en Alerte =
SUM(Fact_ProjectPhasePerformance[Any_Alert])
```

```DAX
Taux Phases en Alerte =
DIVIDE([Nb Phases en Alerte], [Nb Phases])
```

## Projets en alerte

```DAX
Nb Projets en Alerte =
CALCULATE(
    DISTINCTCOUNT(Fact_ProjectPhasePerformance[Project_ID]),
    Fact_ProjectPhasePerformance[Any_Alert] = 1
)
```

```DAX
Taux Projets en Alerte =
DIVIDE([Nb Projets en Alerte], [Nb Projets])
```

## Mesures de lecture strategique

```DAX
Score Risque =
[Nb Alertes Cout] + [Nb Alertes Duree] + [Nb Alertes Livrables]
```

```DAX
Ecart Global Normalise =
ABS([Ecart Cout %]) + ABS([Ecart Duree %]) + ABS([Ecart Livrables %])
```

## Format recommande

| Mesure | Format |
|---|---|
| Montants | Devise, USD, separateur de milliers |
| Pourcentages | Pourcentage, 1 decimale |
| Volumes | Nombre entier |
| Scores | Nombre entier |

