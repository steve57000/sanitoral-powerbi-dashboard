# Product Strategy Canvas - Sanitoral

## Informations generales

| Champ | Contenu |
|---|---|
| Redacteur | Steve Bell |
| Date | 2026-07-05 |
| Nom du client | Sanitoral |
| Nom du tableau de bord | Sanitoral - Suivi de performance des projets IT et Marketing |

## Objectif du dashboard

Permettre aux directeurs de Sanitoral de suivre l'avancement des projets IT et Marketing, d'identifier rapidement les ecarts de performance, et de prioriser les actions correctives lorsque les couts, les delais ou les livrables s'ecartent du previsionnel.

Le tableau de bord doit rendre les donnees de projets accessibles, visuelles et actionnables pour trois niveaux de responsabilite :

- direction generale ;
- direction regionale ;
- direction pays.

## Utilisateurs cibles

| Utilisateur | Responsabilite | Besoin principal |
|---|---|---|
| Directeur general | Piloter le portefeuille global de projets | Identifier les projets ou zones a risque pour decider de poursuivre, renforcer ou arreter certains projets |
| Directeur regional | Suivre les pays de sa region | Reperer les pays ou projets en derive et intervenir aupres des directeurs pays |
| Directeur pays | Piloter les projets de son pays | Comprendre les ecarts et mettre en place des actions correctives operationnelles |

## User stories

| Utilisateur | User story |
|---|---|
| Directeur general | En tant que directeur general, je veux visualiser la performance globale du portefeuille de projets afin d'identifier rapidement les risques majeurs. |
| Directeur general | En tant que directeur general, je veux connaitre le nombre de projets en alerte afin de prioriser les arbitrages. |
| Directeur general | En tant que directeur general, je veux comparer les projets IT et Marketing afin d'identifier les familles de projets les plus sensibles. |
| Directeur regional | En tant que directeur regional, je veux filtrer les donnees par region afin de suivre uniquement les projets relevant de mon perimetre. |
| Directeur regional | En tant que directeur regional, je veux visualiser les pays les plus en retard afin d'intervenir aupres des directeurs pays concernes. |
| Directeur regional | En tant que directeur regional, je veux identifier les phases les plus problematiques afin de coordonner les plans d'action regionaux. |
| Directeur pays | En tant que directeur pays, je veux consulter les projets de mon pays afin de suivre leur avancement et leurs alertes. |
| Directeur pays | En tant que directeur pays, je veux comprendre si les ecarts viennent des couts, des delais ou des livrables afin d'agir sur le bon levier. |
| Directeur pays | En tant que directeur pays, je veux acceder au detail des phases en alerte afin de prioriser les actions correctives. |

## Indicateurs cles

| Indicateur | Description | Regle d'alerte |
|---|---|---|
| Couts | Comparaison du cout reel avec le cout prevu | Alerte si le cout reel depasse le cout prevu de plus de 15 % |
| Delais | Comparaison de la duree reelle avec la duree prevue | Alerte si la duree reelle depasse la duree prevue de plus de 15 % |
| Livrables | Comparaison des livrables reels avec les livrables prevus | Alerte si les livrables reels sont inferieurs au prevu de plus de 15 % |

## Fonctionnalites attendues

- Vue globale du portefeuille de projets.
- Filtres par type de projet, region, pays, phase et date.
- Carte du monde indiquant les pays les plus en retard ou les plus en alerte.
- Indicateurs visuels sur les couts, delais et livrables.
- Infobulles pour apporter du detail sans surcharger les pages.
- Analyse des phases les plus problematiques.
- Page de documentation expliquant le modele, la mise a jour et les transformations.

## Proposition de pages Power BI

| Page | Objectif | Public principal |
|---|---|---|
| Vue executive | Comprendre rapidement l'etat du portefeuille | Directeur general |
| Performance projets | Identifier les projets et phases en derive | Tous les directeurs |
| Analyse geographique | Localiser les pays et regions a risque | Directeur general et directeurs regionaux |
| Diagnostic phases | Identifier les phases les plus problematiques | Directeurs regionaux et pays |
| Documentation | Expliquer le PSC, le modele et la mise a jour | Sophie / PMO / evaluateur |

## Critere de reussite

Le tableau de bord sera reussi s'il permet a un directeur de :

- comprendre rapidement la situation globale ;
- identifier les projets en alerte ;
- filtrer les donnees selon son niveau de responsabilite ;
- comprendre la cause des ecarts ;
- disposer d'un axe strategique clair pour ameliorer le pilotage des projets.

