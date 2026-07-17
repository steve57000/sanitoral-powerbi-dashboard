# Décisions projet

Ce document conserve les choix de conception importants et leur évolution.

## Organisation du repository

Décision : séparer les fichiers de mission, les livrables, les ressources de travail et les notes.

Raison : préserver les sources d'origine, faciliter l'audit et identifier clairement les fichiers remis au jury.

## Outil et préparation

Décisions :

- utiliser Power BI Desktop ;
- réaliser le nettoyage dans Power Query ;
- ne pas modifier manuellement le fichier Excel source ;
- documenter les transformations pour la mise à jour hebdomadaire.

## Clé projet-phase

Décision : créer `ProjectPhaseKey` dans les quatre tables au grain projet-phase avec :

```powerquery
Text.From([Project_ID]) & "|" & [Phase]
```

La clé est typée en Texte. `Project_ID` seul et `Phase` seule ne sont pas uniques au grain de l'analyse.

## Révision du modèle après mentorat

Décision initiale du 7 juillet 2026 : charger uniquement `Fact_ProjectPhasePerformance`.

Décision révisée du 17 juillet 2026 : utiliser un modèle relationnel visible avec `Projects_Plans` comme table centrale.

Raisons :

- la mission demande une capture et une explication du modèle de données ;
- les tables de coûts, durées et livrables doivent être reliées au bon grain projet-phase ;
- la vue Modèle doit présenter les relations réellement utilisées par le rapport ;
- conserver la table fusionnée et les sept tables chargerait deux modèles concurrents.

Relations retenues :

- `Project_Type` 1-* `Projects_Plans` par `Project_ID` ;
- `Projects_Locations` 1-* `Projects_Plans` par `Project_ID` ;
- `Country_Profiles` 1-* `Projects_Locations` par `Country` ;
- `Projects_Plans` 1-1 avec chaque table `Actual_*` par `ProjectPhaseKey`.

Les relations directes entre `Project_Type` et les tables `Actual_*` sont supprimées.

## Convention de nommage

Décision : conserver le fichier source inchangé, mais utiliser des noms cohérents dans Power Query.

- `Projects_plans` devient `Projects_Plans` ;
- `Project type` devient `Project_Type` ;
- `Actual_Delivrable` devient `Actual_Deliverables` ;
- `Planned_Delivrable` devient `Planned_Deliverables`.

`Deliverables` est l'orthographe anglaise correcte et correspond au dictionnaire.

## Structure du rapport

Décision : quatre pages finales.

1. `Vue exécutive` ;
2. `Détail des alertes` ;
3. `Planning Gantt` ;
4. `Documentation du rapport`.

Les cinq vues envisagées dans le PSC sont consolidées : la géographie est intégrée à la vue exécutive et le diagnostic à la page de détail.

## Filtres plutôt qu'une page par rôle

Décision : utiliser des segments par type, pays, région, phase, statut et période.

Raison : le même rapport répond aux directions générale, régionales et pays sans multiplier les pages et la maintenance.

## Variété des visuels

Décisions :

- barres par région avec taux d'alerte ;
- colonnes empilées à 100 % par type de projet ;
- anneau par nature d'alerte ;
- carte mondiale par pays ;
- tableau détaillé avec mise en forme conditionnelle ;
- Gantt pour la lecture temporelle ;
- infobulle détaillée prévu/réel/écart.

Raison : chaque visuel répond à une question métier distincte et la carte mondiale est explicitement demandée par la note de cadrage.

## Devise

Décision : afficher les coûts en USD.

Raison : le dictionnaire définit `Planned_Cost` et `Actual_Cost` en dollars. Aucun symbole euro ne doit apparaître sans conversion explicite.

## Axe stratégique

Décision : mettre en avant `Phase D - Testing`, dont les 52 phases sont en alerte.

Recommandation : renforcer les estimations, les contrôles qualité, les critères d'entrée et de sortie et les points de contrôle intermédiaires de la phase de test.
