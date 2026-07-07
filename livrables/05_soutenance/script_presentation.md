# Script de presentation

## Introduction

Bonjour, je vais vous presenter le tableau de bord Power BI realise pour Sanitoral.

L'objectif de la mission est de rendre les donnees de suivi de projets plus lisibles et plus actionnables pour trois niveaux de direction : la direction generale, les directions regionales et les directions pays.

Le rapport permet de suivre les couts, les delais et les livrables, et d'identifier les projets en alerte lorsqu'un ecart depasse le seuil de 15 % defini par Sanitoral.

## Besoin client

Sanitoral dispose de projets IT et Marketing repartis dans plusieurs regions du monde.

Le besoin principal est de transformer ces donnees en un outil visuel permettant :

- de suivre la performance globale ;
- d'identifier rapidement les retards et derives ;
- de filtrer par type de projet, region, pays, statut d'alerte et phase ;
- d'aider les directeurs a prendre des decisions.

## Methode

J'ai d'abord formalise le besoin avec un Product Strategy Canvas.

Ensuite, j'ai prepare les 7 feuilles sources dans Power Query afin que le nettoyage soit automatique et reproductible.

J'ai cree une cle `ProjectPhaseKey` pour relier correctement les donnees au niveau projet-phase, puis j'ai construit la table finale `Fact_ProjectPhasePerformance`.

Le modele final charge uniquement cette table finale. Les tables sources restent utilisees dans Power Query, mais leur chargement est desactive dans le modele Power BI.

Enfin, j'ai cree les mesures DAX, les indicateurs d'alerte et les visualisations du rapport.

## Resultats cles

Sans filtre actif, le dashboard affiche :

- 104 projets ;
- 520 phases ;
- 348 phases en alerte ;
- 66,92 % de phases en alerte.

Ces resultats montrent qu'une part importante du portefeuille necessite un suivi prioritaire.

## Description des pages du rapport

Le rapport final contient 2 pages.

### Vue executive

La page `Vue executive` donne une lecture globale avec :

- les cartes KPI principales ;
- les filtres par type de projet, pays, region, statut d'alerte et phase ;
- un graphique des phases en alerte par region ;
- un graphique des phases en alerte par type de projet ;
- une repartition des alertes par nature : cout, duree et livrables.

Cette page permet de voir rapidement ou se concentrent les alertes et quel type de probleme domine.

### Detail des alertes

La page `Detail des alertes` contient un tableau filtre sur les phases en alerte.

Le tableau affiche le projet, la phase, le pays, la region, le type de projet, le nombre d'alertes, le statut d'alerte et l'ecart de cout.

Il est trie par `Alert_Count` decroissant et utilise une mise en forme conditionnelle pour faire ressortir les lignes les plus critiques.

## Lecture des alertes

Les alertes peuvent etre lues selon trois axes principaux :

- par region, pour identifier les zones geographiques les plus exposees ;
- par type de projet, pour comparer les projets IT et Marketing ;
- par nature d'alerte, pour distinguer les problemes de cout, de duree et de livrables.

Cette lecture aide Sanitoral a prioriser les actions correctives au bon niveau : portefeuille, region, pays, projet ou phase.

## Conclusion

Ce tableau de bord permet de passer d'un fichier de donnees difficile a exploiter a un outil de pilotage clair, interactif et oriente decision.

Il donne une vision globale au directeur general, une vision filtree aux directeurs regionaux, et une vision operationnelle aux directeurs pays.
