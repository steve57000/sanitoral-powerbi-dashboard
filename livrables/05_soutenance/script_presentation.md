# Script de présentation

## Introduction

Bonjour, je vais vous présenter le tableau de bord Power BI que j’ai réalisé pour Sanitoral.

Sanitoral suit des projets IT et Marketing répartis dans plusieurs pays et plusieurs régions du monde. L’objectif de la mission était de transformer des données de suivi de projet en un outil de pilotage clair, interactif et exploitable par différents niveaux de direction.

Le rapport permet de suivre les coûts, les délais et les livrables, puis d’identifier les phases en alerte lorsqu’un écart dépasse le seuil de 15 % défini par Sanitoral.

## Besoin client

Le besoin principal de Sanitoral était de rendre les données plus lisibles et plus actionnables.

Le tableau de bord devait permettre :

- de suivre la performance globale du portefeuille de projets ;
- d’identifier rapidement les retards, les dérives de coût et les écarts de livrables ;
- de filtrer les résultats par type de projet, région, pays, statut d’alerte et phase ;
- d’aider les directeurs à prioriser leurs actions.

Le rapport s’adresse à trois profils : la direction générale, les directions régionales et les directions pays. Il fallait donc construire un outil synthétique, mais suffisamment détaillé pour permettre l’analyse opérationnelle.

## Méthode

J’ai d’abord formalisé le besoin avec un Product Strategy Canvas. Cela m’a permis de clarifier les utilisateurs, les objectifs du rapport, les indicateurs attendus et la logique de décision.

Ensuite, j’ai préparé les 7 feuilles sources dans Power Query. Le but était d’éviter un nettoyage manuel dans Excel et de rendre les transformations reproductibles lors des futures mises à jour.

J’ai notamment supprimé les lignes descriptives inutiles, promu les vrais en-têtes, harmonisé les noms de colonnes, corrigé les types de données et supprimé les lignes ou colonnes vides.

Pour relier correctement les données, j’ai créé une clé `ProjectPhaseKey`, basée sur le projet et la phase. Cette clé était nécessaire, car un projet peut avoir plusieurs phases, et les analyses doivent se faire au niveau projet-phase.

J’ai ensuite construit une table finale appelée `Fact_ProjectPhasePerformance`. Le modèle Power BI charge uniquement cette table finale. Les tables sources restent utilisées dans Power Query, mais leur chargement est désactivé dans le modèle afin de garder une structure simple et lisible.

Enfin, j’ai créé les mesures DAX, les indicateurs d’alerte et les visualisations du rapport.

## Résultats Clés

Sans filtre actif, le dashboard affiche :

- 104 projets ;
- 520 phases ;
- 348 phases en alerte ;
- 66,92 % de phases en alerte.

Ces résultats montrent qu’une part importante du portefeuille nécessite un suivi prioritaire.

Le rapport met aussi en évidence que les alertes liées aux coûts sont les plus nombreuses, devant les alertes de durée et les alertes de livrables. Cela donne une première orientation pour les actions correctives.

## Description Du Rapport

Le rapport final contient deux pages principales.

La première page est la **Vue exécutive**. Elle donne une lecture globale du portefeuille avec les cartes KPI principales, les filtres interactifs et les graphiques de synthèse.

On y retrouve :

- les phases en alerte par région ;
- les phases en alerte par type de projet ;
- la répartition des alertes par nature : coût, durée et livrables.

Cette page permet de comprendre rapidement où se concentrent les alertes et quel type de problème domine.

La deuxième page est la page **Détail des alertes**. Elle permet d’aller plus loin dans l’analyse.

Elle contient un tableau filtré sur les phases en alerte. On y retrouve le projet, la phase, le pays, la région, le type de projet, le nombre d’alertes, le statut d’alerte et l’écart de coût.

Le tableau est trié par nombre d’alertes décroissant, ce qui permet de faire remonter en priorité les phases les plus critiques. Une mise en forme conditionnelle permet aussi d’identifier visuellement les cas les plus sensibles.

## Lecture Des Alertes

Les alertes peuvent être analysées selon trois axes principaux.

Le premier axe est géographique. L’analyse par région permet d’identifier les zones où les phases en alerte sont les plus nombreuses.

Le deuxième axe concerne le type de projet. La comparaison entre projets IT et projets Marketing permet de voir si un type de projet concentre davantage de risques.

Le troisième axe est la nature de l’alerte. Le rapport distingue les alertes de coût, de durée et de livrables. Cette lecture aide à comprendre si le problème principal vient plutôt d’un dépassement budgétaire, d’un retard ou d’un manque de livrables.

Cette approche permet à Sanitoral de prioriser les actions correctives au bon niveau : portefeuille, région, pays, projet ou phase.

## Conclusion

Ce tableau de bord permet de passer d’un fichier de données difficile à exploiter à un outil de pilotage clair, interactif et orienté décision.

Il donne une vision globale à la direction générale, une vision filtrée aux directions régionales, et une vision opérationnelle aux directions pays.

Le principal intérêt du rapport est de rendre les alertes visibles rapidement, tout en permettant de descendre dans le détail lorsque c’est nécessaire.

Pour conclure, ce dashboard apporte à Sanitoral une base fiable pour suivre ses projets, identifier les priorités et mieux piloter les écarts entre le prévu et le réalisé.