# Script de présentation

## Introduction

Bonjour, je vais vous présenter le tableau de bord Power BI réalisé pour Sanitoral.

Sanitoral pilote des projets IT et Marketing répartis dans 52 pays et quatre grandes régions. L'objectif de la mission était de transformer plusieurs feuilles de suivi projet en un outil interactif permettant de suivre l'avancement, d'identifier les retards et de contrôler les dérives de performance.

Le rapport s'adresse à trois profils : la direction générale, les directions régionales et les directions pays. Il doit donc proposer une lecture globale, mais aussi permettre de descendre jusqu'au niveau d'une phase de projet.

## Besoin métier

Sanitoral suit trois indicateurs :

- les coûts ;
- les durées ;
- les livrables produits par rapport au planning.

Une alerte est déclenchée lorsqu'un écart défavorable dépasse strictement 15 %. Pour les coûts et les durées, le réel doit dépasser le prévu de plus de 15 %. Pour les livrables, le réel doit être inférieur au prévu de plus de 15 %.

Le besoin n'était donc pas seulement de présenter des données, mais de faire ressortir rapidement les projets et phases qui nécessitent une intervention.

## Product Strategy Canvas

J'ai commencé par formaliser le besoin dans un Product Strategy Canvas. Il m'a permis d'identifier les utilisateurs, leurs décisions, les filtres nécessaires et les indicateurs à afficher.

Le directeur général a besoin d'une vision globale pour arbitrer le portefeuille. Le directeur régional doit comparer les pays de sa région. Le directeur pays doit accéder au détail des phases afin d'engager les actions correctives.

J'ai choisi de répondre à ces trois profils avec un même rapport et des filtres, plutôt que de créer une page différente pour chaque rôle.

## Préparation dans Power Query

Le fichier Excel contient sept feuilles. Elles ne commencent pas toutes à la même ligne et utilisent plusieurs noms pour le même identifiant projet, par exemple `Project ID`, `Proj_ID`, `Project` ou `ID`.

Dans Power Query, j'ai donc :

- supprimé les lignes descriptives et vides ;
- promu les vrais en-têtes ;
- harmonisé les noms de colonnes ;
- nettoyé les espaces ;
- corrigé les types ;
- contrôlé les valeurs manquantes et les doublons.

La feuille source nommée `Actual_Delivrable` n'a pas été modifiée. En revanche, sa requête Power Query a été renommée `Actual_Deliverables`, qui est l'orthographe correcte et celle utilisée dans le dictionnaire.

## Clé ProjectPhaseKey

Chaque ligne représente une phase d'un projet. `Project_ID` seul n'est donc pas unique, car un projet possède plusieurs phases. `Phase` seule n'est pas unique non plus, car plusieurs projets suivent les mêmes phases.

J'ai créé dans les quatre tables au grain projet-phase une clé texte `ProjectPhaseKey`, obtenue en concaténant le projet et la phase avec un séparateur vertical.

Cette clé contient 520 valeurs distinctes dans chaque table et permet de rattacher exactement le coût, la durée et les livrables réels à la bonne phase planifiée.

## Modèle relationnel

Le modèle charge sept tables nettoyées.

`Projects_Plans` constitue la table centrale. Les tables `Actual_Costs`, `Actual_Duration` et `Actual_Deliverables` lui sont reliées par `ProjectPhaseKey`.

`Project_Type` et `Projects_Locations` sont reliées à `Projects_Plans` par `Project_ID`. Enfin, `Country_Profiles` est reliée à `Projects_Locations` par le pays.

Les tables de réalisé ne sont pas reliées directement à `Project_Type`, car cette relation resterait au niveau projet et ne garantirait pas le rattachement à la bonne phase. Le modèle ne contient aucune relation plusieurs-à-plusieurs.

## DAX et contrôles

Les écarts et les alertes sont calculés au niveau de chaque ligne de `Projects_Plans` grâce aux relations et à la fonction `RELATED`.

Les indicateurs d'alerte sont des nombres entiers, ce qui permet ensuite de les agréger simplement avec `SUM` et d'éviter les conversions de texte dans les mesures.

Sans filtre actif, le jeu de données contient :

- 104 projets ;
- 102 projets en alerte ;
- 520 phases ;
- 348 phases en alerte, soit 66,92 % ;
- 214 alertes de coût ;
- 159 alertes de durée ;
- 96 alertes de livrables.

Le coût prévu est de 56 108 000 dollars et le coût réel de 60 200 800 dollars, soit un dépassement global de 7,29 %.

## Page 1 - Vue exécutive

La première page permet de comprendre la situation globale en quelques secondes.

Les cartes KPI affichent les volumes principaux, le nombre de projets et de phases en alerte ainsi que le coût réel en dollars.

Les filtres permettent d'adapter la lecture par type de projet, région, pays, phase, statut et période.

Les visuels sont volontairement variés :

- des barres comparent les régions ;
- des colonnes empilées à 100 % comparent la part de phases en alerte entre IT et Marketing ;
- un graphique en anneau présente la répartition des alertes entre coût, durée et livrables ;
- une carte mondiale localise les pays les plus exposés.

Les infobulles donnent les valeurs prévues, réelles et les écarts sans surcharger la page.

## Page 2 - Détail des alertes

La deuxième page est orientée action.

Elle contient uniquement les phases en alerte et les classe par nombre d'alertes décroissant. Une phase peut cumuler une, deux ou trois alertes. La mise en forme conditionnelle fait ressortir les phases les plus critiques.

Les utilisateurs peuvent filtrer le tableau par type de projet, pays, région et phase, puis consulter les écarts de coût, de durée et de livrables.

## Page 3 - Planning Gantt

La troisième page présente le planning des phases avec le visuel Gantt installé pour la mission.

Chaque tâche combine l'identifiant du projet et le nom de la phase. Les couleurs distinguent les phases en alerte des phases sans alerte. Cette page apporte une lecture temporelle complémentaire au tableau de détail.

## Page 4 - Documentation du rapport

La quatrième page répond à la demande de Sophie concernant l'autonomie et la traçabilité.

Elle présente :

- le Product Strategy Canvas ;
- la procédure de mise à jour hebdomadaire ;
- les principales transformations Power Query ;
- une capture du modèle relationnel et l'explication des cardinalités ;
- la règle d'alerte à 15 % ;
- les KPI de contrôle.

## Axe stratégique

Les projets IT présentent un taux de phases en alerte de 72,12 %, contre 59,13 % pour les projets Marketing.

Le signal le plus fort concerne la phase `Phase D - Testing` : les 52 phases de test sont en alerte, soit 100 %.

Je recommande donc de renforcer la préparation de cette phase, de revoir les estimations de coût et de durée, et de formaliser des critères d'entrée et de sortie plus stricts. Des points de contrôle intermédiaires permettraient d'identifier les dérives avant la fin des tests.

## Conclusion

Ce projet transforme sept feuilles difficiles à exploiter en un modèle relationnel contrôlé et un rapport orienté décision.

La direction générale obtient une vision du portefeuille, les directions régionales peuvent comparer leurs zones et les directions pays peuvent identifier les phases à traiter.

Le modèle, la procédure de mise à jour et les valeurs de contrôle rendent également le rapport maintenable et vérifiable lors des futures actualisations.
