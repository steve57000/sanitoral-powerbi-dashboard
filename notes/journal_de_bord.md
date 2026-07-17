# Journal de bord

Ce journal sert a suivre les etapes du projet, les actions realisees et les points a verifier avant la soutenance.

## 2026-07-05 - Initialisation du projet

Actions realisees :

- creation du repository GitHub ;
- creation de l'arborescence du projet ;
- separation entre les fichiers de mission et les livrables ;
- creation des premiers documents de suivi ;
- audit initial des fichiers fournis.

Constats principaux :

- le projet demande un tableau de bord Power BI dynamique ;
- le nettoyage doit etre automatique dans Power Query ;
- le dashboard doit servir trois profils : directeur general, directeur regional, directeur pays ;
- le seuil d'alerte est fixe a 15 % d'ecart entre le prevu et le reel ;
- un onglet de documentation doit expliquer le PSC, la mise a jour des donnees et le modele de donnees.

Prochaine etape :

- completer le Product Strategy Canvas avant de construire le rapport Power BI.


## 2026-07-07 - Finalisation du dashboard Power BI

Actions realisees :

- nettoyage des 7 feuilles Excel sources ;
- creation de la cle `ProjectPhaseKey` ;
- construction de la table finale `Fact_ProjectPhasePerformance` ;
- desactivation du chargement des tables intermediaires dans le modele final ;
- creation des mesures DAX principales et des mesures d'alerte robustes ;
- creation des pages `Vue executive` et `Detail des alertes` ;
- amelioration du design avec cartes KPI, graphiques, filtres et tableau detaille ;
- validation des controles globaux : 104 projets, 520 phases, 348 phases en alerte, 66,92 % de phases en alerte, 214 alertes cout, 159 alertes duree et 96 alertes livrables.

## 2026-07-17 - Révision après mentorat

Retours analysés :

- la table fusionnée unique ne permet pas de montrer les relations dans la vue Modèle ;
- les tables `Actual_Costs`, `Actual_Duration` et `Actual_Delivrable` doivent être reliées à la table des plans au grain projet-phase ;
- le nom `Actual_Delivrable` doit être harmonisé ;
- les trois graphiques en barres de la vue exécutive doivent être diversifiés.

Décisions prises :

- adoption d'un modèle relationnel avec `Projects_Plans` comme table centrale ;
- relations des tables `Actual_*` par `ProjectPhaseKey` ;
- suppression des relations directes entre les tables de réalisé et `Project_Type` ;
- renommage de la requête en `Actual_Deliverables` sans modifier la feuille Excel source ;
- typage de `ProjectPhaseKey` en Texte ;
- ajout documentaire du KPI `Nb Projets en alerte` avec une valeur de contrôle de 102 ;
- format des coûts corrigé en USD ;
- quatre pages finales documentées, y compris le Gantt ;
- visuels cibles : barres régionales, colonnes empilées à 100 %, anneau, carte mondiale et infobulle détaillée ;
- mise en avant de `Phase D - Testing`, en alerte sur 52 phases sur 52.

Actions restant à réaliser dans Power BI Desktop :

- appliquer le modèle relationnel au PBIX ;
- remapper les mesures et visuels ;
- corriger la devise et les libellés ;
- remplacer le PBIX, le PDF et les captures dans le dépôt.
