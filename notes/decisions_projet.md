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

- construire un rapport multi-pages, mais utilisable par tous les roles grace aux filtres et interactions.

Raison :

- le scenario demande un rapport accessible aux trois types de directeurs ;
- il ne faut pas creer une page totalement separee par role si les filtres permettent une lecture adaptee.

