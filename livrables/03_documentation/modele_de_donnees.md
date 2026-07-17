# Modèle de données

Ce document décrit le modèle relationnel cible du rapport Power BI Sanitoral après les retours de mentorat du 17 juillet 2026.

## Grain d'analyse

Le grain principal est la phase d'un projet :

```text
1 ligne = 1 projet + 1 phase
```

Le jeu de données contient 104 projets et 520 couples projet-phase uniques.

## Clé projet-phase

`Project_ID` seul ne suffit pas, car un projet possède plusieurs phases. `Phase` seule n'est pas unique, car plusieurs projets suivent les mêmes phases.

Une clé texte est donc créée dans les quatre tables au grain projet-phase :

```powerquery
Text.From([Project_ID]) & "|" & [Phase]
```

Nom : `ProjectPhaseKey`.

Cette colonne doit être de type Texte et contenir 520 valeurs distinctes dans `Projects_Plans`, `Actual_Costs`, `Actual_Duration` et `Actual_Deliverables`.

## Tables chargées

| Table | Grain | Rôle |
|---|---|---|
| `Projects_Plans` | Projet-phase | Dates, durées, coûts et livrables prévus ; indicateurs d'alerte. |
| `Actual_Costs` | Projet-phase | Coût réel. |
| `Actual_Duration` | Projet-phase | Durée réelle. |
| `Actual_Deliverables` | Projet-phase | Nombre de livrables réels. |
| `Project_Type` | Projet | Type IT ou Marketing. |
| `Projects_Locations` | Projet | Pays du projet. |
| `Country_Profiles` | Pays | Région et type d'entité locale. |

La feuille Excel source conserve son nom d'origine `Actual_Delivrable`. Seule la requête Power Query est renommée `Actual_Deliverables` afin d'utiliser l'orthographe anglaise correcte et de rester cohérent avec le dictionnaire.

## Relations

| Côté 1 | Côté lié | Clé | Cardinalité | Active |
|---|---|---|---|---|
| `Project_Type` | `Projects_Plans` | `Project_ID` | 1 vers plusieurs | Oui |
| `Projects_Locations` | `Projects_Plans` | `Project_ID` | 1 vers plusieurs | Oui |
| `Country_Profiles` | `Projects_Locations` | `Country` | 1 vers plusieurs | Oui |
| `Projects_Plans` | `Actual_Costs` | `ProjectPhaseKey` | 1 vers 1 | Oui |
| `Projects_Plans` | `Actual_Duration` | `ProjectPhaseKey` | 1 vers 1 | Oui |
| `Projects_Plans` | `Actual_Deliverables` | `ProjectPhaseKey` | 1 vers 1 | Oui |

Les tables `Actual_Costs`, `Actual_Duration` et `Actual_Deliverables` ne doivent pas être reliées directement à `Project_Type`. Une relation par `Project_ID` ne contrôle pas le grain phase et peut créer plusieurs chemins de filtrage.

Pour les relations 1-* utiliser un filtrage à sens unique du côté `1` vers le côté `plusieurs`. Power BI impose un filtrage bidirectionnel sur les relations 1-1 ; l'absence de chemins concurrents évite les ambiguïtés.

## Stratégie de chargement

Le modèle antérieur chargeait uniquement `Fact_ProjectPhasePerformance`. Cette table fusionnée produisait les bons résultats, mais ne montrait aucune relation dans la vue Modèle.

Après remappage des mesures et des visuels :

- charger les sept tables relationnelles décrites ci-dessus ;
- désactiver le chargement de `Fact_ProjectPhasePerformance` ;
- ne pas conserver simultanément la table fusionnée et les sept tables comme deux modèles concurrents ;
- masquer dans l'affichage du rapport les clés et colonnes techniques inutiles, sans désactiver le chargement des tables relationnelles.

## Colonnes calculées dans Projects_Plans

`Projects_Plans` porte les calculs au niveau phase :

- `Cost_Difference_Pct` ;
- `Duration_Difference_Pct` ;
- `Deliverables_Difference_Pct` ;
- `Cost_Alert` ;
- `Duration_Alert` ;
- `Deliverables_Alert` ;
- `Any_Alert` ;
- `Alert_Count` ;
- `Alert_Status` ;
- `Gantt_Task`.

Les valeurs réelles sont récupérées par `RELATED()` grâce aux relations sur `ProjectPhaseKey`. Les formules sont documentées dans [`mesures_dax.md`](mesures_dax.md).

## Contrôles de qualité

- 520 clés distinctes dans chacune des quatre tables projet-phase ;
- aucun doublon sur `ProjectPhaseKey` ;
- aucune clé manquante ou supplémentaire entre les plans et les tables de réalisé ;
- 104 `Project_ID` distincts dans `Project_Type` et `Projects_Locations` ;
- 52 pays distincts dans `Country_Profiles` ;
- aucune relation plusieurs-à-plusieurs ;
- six relations actives visibles dans la vue Modèle.

## État d'application

Cette documentation définit le modèle cible. Le PBIX doit être mis à jour manuellement dans Power BI Desktop puis accompagné d'une nouvelle capture de la vue Modèle.
