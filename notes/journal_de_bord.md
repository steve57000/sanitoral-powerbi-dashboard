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
