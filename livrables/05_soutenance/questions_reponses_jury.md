# Questions / réponses probables du jury

## Pourquoi avoir créé une clé projet-phase ?

Chaque ligne du jeu de données représente une phase d’un projet, et non un projet complet.

`Project_ID` seul ne suffit donc pas, car un même projet apparaît sur plusieurs lignes, une fois par phase. À l’inverse, `Phase` seule ne suffit pas non plus, car plusieurs projets partagent les mêmes noms de phases.

La clé `ProjectPhaseKey` permet de relier correctement les coûts, les durées et les livrables au bon niveau d’analyse : le couple projet-phase.

## Pourquoi faire le nettoyage dans Power Query ?

Le scénario précise que Sanitoral souhaite mettre à jour l’analyse régulièrement.

Power Query permet d’automatiser les transformations : suppression des lignes inutiles, promotion des vrais en-têtes, renommage des colonnes, correction des types, suppression des valeurs vides et jointures entre les tables.

Cela évite de refaire le nettoyage manuellement dans Excel à chaque mise à jour et rend le processus plus fiable et reproductible.

## Pourquoi utiliser un seuil de 15 % ?

Le seuil de 15 % vient de la note de cadrage.

Sanitoral considère qu’un écart supérieur à 15 % entre le prévu et le réel doit déclencher une alerte.

J’ai donc appliqué cette règle aux trois axes principaux du suivi projet : les coûts, les durées et les livrables.

## Pourquoi ne pas faire une page par utilisateur ?

Le rapport doit rester utilisable par trois profils : la direction générale, les directions régionales et les directions pays.

Plutôt que de créer une page différente pour chaque profil, j’ai choisi d’utiliser des filtres et des segments. Cela permet à chacun d’adapter la lecture à son périmètre : global, régional, pays, type de projet ou phase.

Cette approche évite de multiplier les pages et garde le rapport plus simple à maintenir.

## Pourquoi trois pages finales ?

Le rapport final privilégie la lisibilité et l’efficacité avec 3 pages finales complémentaires.

La page `Vue exécutive` donne la synthèse de pilotage avec les KPI, les filtres et les graphiques principaux.

La page `Détail des alertes` permet ensuite d’identifier les phases à traiter en priorité.

La page `Documentation & Méthode` présente le Product Strategy Canvas, les étapes de préparation et de mise à jour des données, le modèle de données, les transformations Power Query, la règle d’alerte à 15 % et les KPI de contrôle.

Cette organisation évite de surcharger la page principale tout en gardant un accès rapide au détail opérationnel et aux éléments méthodologiques utiles pendant la soutenance.

## Pourquoi un modèle final à une seule table ?

Les jointures entre les sources ont déjà été réalisées dans Power Query pour construire la table finale `Fact_ProjectPhasePerformance`.

Charger uniquement cette table simplifie le modèle, évite les relations inutiles et rend le rapport plus facile à expliquer pendant la soutenance.

Les tables sources restent utilisées dans Power Query pour la préparation des données, mais elles ne sont pas chargées dans le modèle final.

## Est-ce qu’un modèle en étoile aurait été possible ?

Oui, un modèle en étoile aurait été possible avec des dimensions comme `Dim_Project`, `Dim_Country`, `Dim_Phase` ou `Dim_ProjectType`.

Cependant, pour ce projet, le grain d’analyse est simple : une ligne correspond à une phase d’un projet. La table finale contient déjà les informations nécessaires pour filtrer et analyser les résultats.

J’ai donc privilégié un modèle plus direct, plus lisible et adapté à la taille du jeu de données.

## Pourquoi documenter les mesures DAX ?

Les mesures DAX sont au cœur de l’analyse.

Elles permettent de calculer les KPI, les écarts et les alertes affichés dans le rapport.

Les documenter rend le dashboard plus maintenable, plus facile à vérifier et plus simple à expliquer au jury ou à un futur utilisateur.

## Pourquoi des mesures DAX robustes avec `VALUE()` et `IFERROR()` ?

Certaines colonnes d’alerte peuvent être interprétées comme du texte selon le typage appliqué dans Power Query ou Power BI.

`VALUE()` permet de convertir la valeur en nombre, et `IFERROR()` évite qu’une valeur non convertible bloque le calcul.

Cela rend les mesures plus robustes et évite les erreurs lors de l’affichage des visuels.

## Comment vérifier que le modèle est fiable ?

Je vérifie plusieurs points :

- le nombre de projets ;
- le nombre de phases ;
- l’unicité de la clé `ProjectPhaseKey` ;
- l’absence d’erreurs Power Query ;
- l’absence de valeurs manquantes après les jointures ;
- la cohérence des totaux de coûts, durées et livrables ;
- le bon fonctionnement des filtres et des visuels.

Je compare aussi les KPI globaux avec les valeurs de contrôle attendues.

## Quelles sont les valeurs de contrôle du dashboard ?

Sans filtre actif, le dashboard doit afficher :

- 104 projets ;
- 520 phases ;
- 348 phases en alerte ;
- 66,92 % de phases en alerte ;
- 214 alertes coût ;
- 159 alertes durée ;
- 96 alertes livrables.

Ces valeurs servent de référence pour vérifier que les transformations, les mesures et les visuels fonctionnent correctement.

## Quelle recommandation stratégique ressort de l’analyse ?

Les projets IT concentrent une part importante des alertes.

Les alertes de coût sont également les plus nombreuses, devant les alertes de durée et de livrables.

Une recommandation possible est donc de renforcer le suivi budgétaire des projets IT, en particulier sur les phases les plus critiques. Sanitoral pourrait aussi revoir ses méthodes d’estimation et ses points de contrôle intermédiaires pour limiter les dérives avant qu’elles deviennent trop importantes.

## Pourquoi avoir utilisé une mise en forme conditionnelle dans le tableau de détail ?

La mise en forme conditionnelle permet d’identifier rapidement les phases les plus critiques.

Dans le tableau `Détail des alertes`, la colonne `Alert_Count` indique si une phase cumule une, deux ou trois alertes.

En colorant cette colonne, on fait ressortir immédiatement les lignes à traiter en priorité.

## Quel est l’intérêt des filtres ?

Les filtres rendent le rapport interactif.

Ils permettent de passer d’une vision globale à une vision plus ciblée : par région, pays, type de projet, phase ou statut d’alerte.

C’est ce qui permet au même rapport de répondre aux besoins de plusieurs profils de direction.

## Quelles limites peut-on identifier ?

Le rapport dépend de la qualité du fichier source.

Si les noms de feuilles, les colonnes ou la structure du fichier Excel changent fortement, certaines étapes Power Query peuvent nécessiter une adaptation.

De plus, le dashboard indique les écarts et les zones à risque, mais il ne donne pas à lui seul la cause métier exacte de chaque dérive. Une analyse complémentaire peut être nécessaire avec les responsables projet.

## Comment le rapport peut-il être mis à jour ?

La mise à jour se fait en remplaçant ou en actualisant le fichier source, puis en lançant l’actualisation dans Power BI.

Les transformations Power Query appliquent automatiquement les étapes de nettoyage et de fusion.

Après actualisation, je vérifie les KPI globaux, l’absence d’erreurs Power Query et la cohérence des visuels.