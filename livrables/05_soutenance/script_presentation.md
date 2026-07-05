# Script de presentation - brouillon

Ce document servira de base pour preparer la soutenance finale.

## Introduction

Bonjour, je vais vous presenter le tableau de bord Power BI realise pour Sanitoral.

L'objectif de la mission est de rendre les donnees de suivi de projets plus lisibles et plus actionnables pour trois niveaux de direction : la direction generale, les directions regionales et les directions pays.

Le rapport permet de suivre les couts, les delais et les livrables, et d'identifier les projets en alerte lorsqu'un ecart depasse le seuil de 15 % defini par Sanitoral.

## Besoin client

Sanitoral dispose de nombreux projets IT et Marketing repartis dans plusieurs regions du monde.

Le besoin principal est de transformer ces donnees en un outil visuel permettant :

- de suivre la performance globale ;
- d'identifier rapidement les retards et derives ;
- de filtrer par type de projet, region, pays et phase ;
- d'aider les directeurs a prendre des decisions.

## Methode

J'ai d'abord formalise le besoin avec un Product Strategy Canvas.

Ensuite, j'ai prepare les donnees dans Power Query afin que le nettoyage soit automatique et reproductible.

Puis j'ai construit un modele de donnees permettant de comparer les valeurs prevues et reelles au niveau projet-phase.

Enfin, j'ai cree les mesures DAX et les visualisations necessaires pour analyser les alertes.

## Axe strategique

Un premier axe d'analyse ressort clairement : les projets IT concentrent davantage d'alertes que les projets Marketing.

La phase D - Testing est particulierement critique, car elle cumule de nombreux ecarts, notamment sur les couts.

Cette observation peut orienter Sanitoral vers un audit des estimations et du pilotage de la phase de test des projets IT.

## Conclusion

Ce tableau de bord permet donc de passer d'un fichier de donnees difficile a exploiter a un outil de pilotage clair, interactif et oriente decision.

Il donne une vision globale au directeur general, une vision filtree aux directeurs regionaux, et une vision operationnelle aux directeurs pays.

