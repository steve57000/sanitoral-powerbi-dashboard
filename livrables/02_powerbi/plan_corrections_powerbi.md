# Plan de corrections Power BI après mentorat

Ce document décrit les opérations à réaliser dans Power BI Desktop pour aligner le fichier `Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix` avec la mission, les données sources et les remarques de mentorat.

## 1. Créer une sauvegarde

Dupliquer le PBIX avant toute modification :

```text
Sanitoral_PowerBI_Dashboard_Bell_Steve_AVANT_MODELE_RELATIONNEL.pbix
```

Conserver uniquement le fichier final sans suffixe dans le dossier de livrables après validation.

## 2. Harmoniser les requêtes Power Query

Renommer les requêtes sans modifier les feuilles du fichier Excel source :

| Nom actuel | Nom cible |
|---|---|
| `Projects_plans` | `Projects_Plans` |
| `Project type` | `Project_Type` |
| `Actual_Delivrable` | `Actual_Deliverables` |

Conserver les autres noms : `Actual_Costs`, `Actual_Duration`, `Projects_Locations`, `Country_Profiles`.

Dans `Projects_Plans`, renommer `Planned_Delivrable` en `Planned_Deliverables` si cette correction n'est pas déjà appliquée.

## 3. Créer et typer ProjectPhaseKey

Créer la colonne dans :

- `Projects_Plans` ;
- `Actual_Costs` ;
- `Actual_Duration` ;
- `Actual_Deliverables`.

Formule Power Query :

```powerquery
Text.From([Project_ID]) & "|" & [Phase]
```

Définir explicitement le type **Texte** dans les quatre tables. L'icône de colonne doit être `ABC`, pas `ABC 123`.

Contrôler 520 valeurs distinctes et aucun doublon dans chaque table.

## 4. Configurer le chargement

Activer le chargement des sept tables du modèle relationnel :

- `Projects_Plans` ;
- `Project_Type` ;
- `Actual_Costs` ;
- `Actual_Duration` ;
- `Actual_Deliverables` ;
- `Projects_Locations` ;
- `Country_Profiles`.

Conserver provisoirement `Fact_ProjectPhasePerformance` pendant le remappage des visuels. Lorsque tous les visuels et mesures utilisent le modèle relationnel, désactiver son chargement afin d'éviter la duplication des données.

## 5. Recréer les relations

Supprimer les relations directes entre `Project_Type` et les trois tables de réalisé.

Créer les relations actives suivantes :

| Côté 1 | Côté lié | Clé | Cardinalité |
|---|---|---|---|
| `Project_Type` | `Projects_Plans` | `Project_ID` | 1 vers plusieurs |
| `Projects_Locations` | `Projects_Plans` | `Project_ID` | 1 vers plusieurs |
| `Country_Profiles` | `Projects_Locations` | `Country` | 1 vers plusieurs |
| `Projects_Plans` | `Actual_Costs` | `ProjectPhaseKey` | 1 vers 1 |
| `Projects_Plans` | `Actual_Duration` | `ProjectPhaseKey` | 1 vers 1 |
| `Projects_Plans` | `Actual_Deliverables` | `ProjectPhaseKey` | 1 vers 1 |

Ne créer aucune relation plusieurs-à-plusieurs. Utiliser un filtrage à sens unique du côté `1` vers le côté `plusieurs` pour les relations 1-* ; Power BI impose un filtrage dans les deux sens sur les relations 1-1.

## 6. Recréer les calculs

Créer dans `Projects_Plans` les colonnes calculées d'écart et d'alerte décrites dans [`../03_documentation/mesures_dax.md`](../03_documentation/mesures_dax.md).

Les colonnes `Cost_Alert`, `Duration_Alert`, `Deliverables_Alert`, `Any_Alert` et `Alert_Count` doivent être des nombres entiers. Ne pas utiliser `VALUE()` ou `IFERROR()` pour compenser un mauvais typage.

## 7. Remapper les visuels

Remplacer les champs de `Fact_ProjectPhasePerformance` par les champs du modèle relationnel :

- dimensions projet : `Project_Type` ;
- pays et région : `Projects_Locations` et `Country_Profiles` ;
- phase, dates, prévu et alertes : `Projects_Plans` ;
- réel : tables `Actual_*` correspondantes.

## 8. Corriger la vue exécutive

KPI recommandés :

- 104 projets ;
- 102 projets en alerte ;
- 348 phases en alerte ;
- 66,92 % de phases en alerte ;
- 60,20 M$ de coût réel ;
- 7,29 % d'écart de coût.

Visuels :

1. conserver les barres par région, mais utiliser le taux de phases en alerte et afficher le volume en infobulle ;
2. remplacer les barres par type de projet par des colonnes empilées à 100 % `En alerte` / `OK` ;
3. remplacer les barres par nature par un graphique en anneau : coût, durée, livrables ;
4. utiliser l'espace libre pour une carte mondiale par pays, colorée selon le taux d'alerte ;
5. ajouter un segment de dates sur `Start_Date` ;
6. ajouter une infobulle détaillée avec prévu, réel et écart pour les trois indicateurs.

Ajouter un encart de conclusion :

> Phase D - Testing : 52 phases sur 52 sont en alerte. Cette phase doit faire l'objet d'un renforcement des estimations, des contrôles qualité et des critères de sortie.

## 9. Corriger les autres pages

### Détail des alertes

- corriger `Staut d'alerte` en `Statut d'alerte` ;
- ajouter les écarts de durée et de livrables, ou les placer dans une infobulle ;
- conserver le filtre `Alert_Status = En alerte` ;
- conserver le tri décroissant sur `Alert_Count`.

### Planning Gantt

- conserver le visuel Gantt installé ;
- vérifier les filtres par type, pays, région et statut ;
- afficher l'année dans l'axe temporel si plusieurs années sont visibles.

### Documentation du rapport

- remplacer l'explication de la table unique par le modèle relationnel ;
- insérer une capture lisible de la vue Modèle avec les cardinalités ;
- expliquer la clé `ProjectPhaseKey` et le renommage `Actual_Deliverables` ;
- conserver le PSC, la procédure de mise à jour et les KPI de contrôle.

## 10. Validation finale

- actualiser les données sans erreur ;
- vérifier les relations dans la vue Modèle ;
- remettre tous les segments sur `Tout` ;
- vérifier les KPI globaux ;
- tester les interactions et les infobulles ;
- vérifier le mode mobile ;
- enregistrer le PBIX final ;
- réexporter les 4 pages en PDF ;
- remplacer les captures obsolètes dans `livrables/04_exports/`.
