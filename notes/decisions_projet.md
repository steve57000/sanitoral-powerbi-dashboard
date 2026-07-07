# Decisions projet

Ce document conserve les choix de conception importants pour pouvoir les expliquer pendant la soutenance.

## Organisation du repository

Decision :

- placer les fichiers fournis par la mission dans `mission/` ;
- placer les fichiers produits et rendus dans `livrables/` ;
- placer les analyses internes, themes et maquettes dans `ressources/` ;
- conserver les notes de suivi dans `notes/`.

Raison :

- separer clairement les sources d'origine et le travail realise ;
- faciliter la lecture du repository ;
- rendre le projet plus professionnel et plus facile a auditer.

## Outil principal

Decision :

- utiliser Power BI Desktop comme outil principal.

Raison :

- c'est l'outil attendu par le projet ;
- il permet Power Query, DAX, modele relationnel, filtres, cartes et interactions.

## Nettoyage des donnees

Decision :

- realiser le nettoyage dans Power Query, sans modifier manuellement le fichier Excel source.

Raison :

- le scenario demande une mise a jour hebdomadaire ;
- le nettoyage doit etre reproductible ;
- les etapes appliquees pourront etre documentees dans le rapport.

## Cle projet-phase

Decision :

- creer une cle unique `ProjectPhaseKey` a partir de `Project_ID` et `Phase`.

Raison :

- une phase seule n'est pas unique ;
- un projet seul possede plusieurs phases ;
- les tables de couts, durees et livrables doivent etre reliees au niveau projet-phase.

## Structure du rapport

Decision :

- construire un rapport final en 2 pages principales : `Vue executive` et `Detail des alertes` ;
- rendre ces pages utilisables par tous les roles grace aux filtres et interactions.

Raison :

- le scenario demande un rapport accessible aux trois types de directeurs ;
- il ne faut pas creer une page totalement separee par role si les filtres permettent une lecture adaptee ;
- la premiere page donne une vision de pilotage globale ;
- la seconde page permet d'analyser les phases en alerte ;
- cette structure evite la dispersion et facilite la soutenance.

## Modele final Power BI

Decision :

- conserver un modele final a une seule table chargee : `Fact_ProjectPhasePerformance`.

Raison :

- les jointures sont deja integrees dans Power Query ;
- le modele est plus simple a controler et a expliquer ;
- les mesures DAX restent directes et lisibles.

## Filtres plutot qu'une page par role

Decision :

- utiliser les filtres `Project_Type`, `Country`, `Region`, `Alert_Status` et `Phase` plutot que de creer une page separee par role.

Raison :

- un meme rapport reste utilisable par la direction generale, les directions regionales et les directions pays ;
- les utilisateurs peuvent adapter la lecture a leur perimetre sans dupliquer les visuels.

## Design du dashboard

Decision :

- adopter un design clair avec cartes KPI, graphiques de synthese et tableau detaille.

Raison :

- les cartes KPI donnent les indicateurs prioritaires ;
- les graphiques montrent la repartition des alertes ;
- le tableau detaille permet d'identifier les phases a traiter.

## Mise en forme conditionnelle

Decision :

- appliquer une mise en forme conditionnelle sur `Alert_Count` dans la page `Detail des alertes`.

Raison :

- les lignes les plus critiques sont immediatement visibles ;
- le tri decroissant et la couleur facilitent la priorisation des actions.
