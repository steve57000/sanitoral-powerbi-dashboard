# Product Strategy Canvas final - Sanitoral

## Informations générales

| Champ | Contenu |
|---|---|
| Rédacteur | Steve Bell |
| Date | 05/07/2026 |
| Nom du client | Sanitoral |
| Nom du tableau de bord | Sanitoral - Suivi de performance des projets IT et Marketing |

## Objectif du dashboard

Permettre aux directeurs de Sanitoral de piloter l'avancement des projets IT et Marketing, d'identifier rapidement les écarts significatifs entre prévisionnel et réalisé, et de prioriser les actions correctives sur les coûts, les délais et les livrables. Le tableau de bord doit rendre les données de projets accessibles, visuelles et actionnables pour trois niveaux de responsabilité : direction générale, direction régionale et direction pays.

## Utilisateurs et user stories

| Utilisateur | Story 1 | Story 2 | Story 3 |
|---|---|---|---|
| Directeur général | En tant que directeur général, je veux visualiser la performance globale du portefeuille de projets afin d'identifier rapidement les risques majeurs. | En tant que directeur général, je veux connaître le nombre de projets en alerte afin de prioriser les arbitrages d'arrêt, de poursuite ou de renforcement. | En tant que directeur général, je veux comparer les projets IT et Marketing par région afin d'identifier les familles de projets et les zones les plus sensibles. |
| Directeur régional | En tant que directeur régional, je veux filtrer les données sur ma région afin de suivre uniquement les projets relevant de mon périmètre. | En tant que directeur régional, je veux visualiser les pays et projets en dérive afin d'intervenir rapidement auprès des directeurs pays concernés. | En tant que directeur régional, je veux identifier les phases les plus problématiques afin de coordonner les plans d'action régionaux. |
| Directeur pays | En tant que directeur pays, je veux consulter les projets de mon pays afin de suivre leur avancement et leurs alertes. | En tant que directeur pays, je veux comprendre si les écarts proviennent des coûts, des délais ou des livrables afin d'agir sur le bon levier. | En tant que directeur pays, je veux accéder au détail des phases en alerte afin de prioriser les actions correctives opérationnelles. |

## Indicateurs clés et règles d'alerte

| Indicateur | Lecture métier | Règle d'alerte |
|---|---|---|
| Coûts | Comparaison du coût réel avec le coût prévu par projet et par phase. | Alerte si le coût réel dépasse le coût prévu de plus de 15 %. |
| Délais | Comparaison de la durée réelle avec la durée prévue des phases projet. | Alerte si la durée réelle dépasse la durée prévue de plus de 15 %. |
| Livrables | Comparaison des livrables réels avec les livrables prévus. | Alerte si les livrables réels sont inférieurs au prévu de plus de 15 %. |

## Fonctionnalités attendues

| Fonctionnalité | Utilité dans le dashboard |
|---|---|
| Vue exécutive | Cartes KPI, nombre de projets en alerte, synthèse coûts/délais/livrables et lecture rapide du portefeuille. |
| Filtres métier | Filtres par type de projet, région, pays, phase et dates de début/fin des phases. |
| Carte mondiale | Mise en évidence des pays les plus en retard ou les plus exposés aux alertes. |
| Graphiques variés | Comparaisons par indicateur, type de projet, région, pays et phase. |
| Infobulles | Détail complémentaire sans surcharge visuelle des pages principales. |
| Documentation | PSC, préparation Power Query, modèle de données et procédure de mise à jour hebdomadaire. |

## Pages Power BI recommandées

| Page | Objectif | Public principal |
|---|---|---|
| Vue exécutive | Comprendre en 30 secondes l'état du portefeuille et les alertes prioritaires. | Direction générale |
| Performance projets | Identifier les projets, phases et indicateurs responsables des écarts. | Tous les directeurs |
| Analyse géographique | Localiser les pays et régions à risque avec une carte mondiale. | Direction générale et régionale |
| Diagnostic phases | Transformer les écarts observés en axe stratégique d'amélioration. | Direction régionale et pays |
| Documentation | Expliquer le PSC, le modèle, les transformations et la mise à jour. | PMO / Sophie / évaluateur |

## Critères de réussite

| Critère | Résultat attendu |
|---|---|
| Lecture rapide | Comprendre rapidement la situation globale du portefeuille. |
| Priorisation | Identifier les projets, pays, régions ou phases en alerte. |
| Adaptation au rôle | Filtrer les données selon le niveau de responsabilité de chaque directeur. |
| Diagnostic | Distinguer clairement les causes d'écart : coûts, délais ou livrables. |
| Décision | Faire émerger un axe stratégique exploitable pour améliorer le pilotage des projets. |

## Axe stratégique attendu

Le reporting doit permettre de passer du constat à la décision. Un axe stratégique prioritaire sera d'identifier les phases, types de projets ou zones géographiques qui concentrent les alertes, afin de recommander des actions ciblées sur la planification, le contrôle des coûts et la production des livrables.
