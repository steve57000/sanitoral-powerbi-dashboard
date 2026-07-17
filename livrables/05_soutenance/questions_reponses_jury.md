# Questions / réponses probables du jury

## Pourquoi avoir créé ProjectPhaseKey ?

Chaque ligne représente une phase d'un projet. `Project_ID` seul se répète donc plusieurs fois et `Phase` seule est partagée par plusieurs projets.

`ProjectPhaseKey` combine les deux informations et permet de rattacher le coût, la durée et les livrables réels à la bonne phase planifiée. Les 520 clés sont uniques dans chacune des quatre tables projet-phase.

## Pourquoi les tables Actual doivent-elles être reliées à Projects_Plans ?

Les données prévues et réelles sont toutes au grain projet-phase. Les relier par `ProjectPhaseKey` garantit que la comparaison porte sur la même phase du même projet.

Une relation directe avec `Project_Type` par `Project_ID` filtre bien le type de projet, mais elle ne garantit pas le rattachement à la phase et peut créer plusieurs chemins de filtrage. `Projects_Plans` est donc le bon point central.

## Pourquoi ne pas conserver uniquement la table fusionnée ?

La table fusionnée produisait les bons résultats, mais elle ne montrait aucune relation dans la vue Modèle. Or la mission demande de créer, capturer et expliquer le modèle de données.

Le modèle relationnel rend la granularité et les cardinalités visibles, limite la duplication des attributs et répond mieux à l'objectif pédagogique.

## Pourquoi ne pas charger les sept tables en plus de la table fusionnée ?

Cela créerait deux modèles concurrents contenant les mêmes données. Les utilisateurs pourraient choisir des champs provenant de tables différentes et obtenir des résultats incohérents.

La table fusionnée peut être conservée temporairement pendant le remappage, puis son chargement doit être désactivé.

## Quelle cardinalité utilisez-vous ?

`Project_Type` et `Projects_Locations` sont reliées à `Projects_Plans` en un-vers-plusieurs. `Country_Profiles` est reliée à `Projects_Locations` en un-vers-plusieurs.

Les trois tables de réalisé sont reliées à `Projects_Plans` en un-vers-un, car `ProjectPhaseKey` est unique des deux côtés. Aucune relation plusieurs-à-plusieurs n'est nécessaire.

## Pourquoi Actual_Deliverables et non Actual_Delivrable ?

`Deliverables` est l'orthographe anglaise correcte et le nom utilisé par le dictionnaire pour la colonne de livrables réels.

La feuille Excel source conserve son nom d'origine `Actual_Delivrable`, car le fichier source ne doit pas être modifié. Seule la requête Power Query est renommée `Actual_Deliverables`.

## Pourquoi faire le nettoyage dans Power Query ?

Sanitoral souhaite mettre à jour l'analyse chaque semaine. Power Query mémorise les étapes de suppression des lignes inutiles, promotion des en-têtes, renommage, typage et contrôle des données.

Cela évite de corriger manuellement le fichier Excel à chaque actualisation et rend la procédure reproductible.

## Pourquoi typer ProjectPhaseKey en Texte ?

La clé combine un identifiant numérique et un libellé de phase. Elle doit donc être traitée comme un identifiant texte stable. Le type `Any` peut produire des comportements imprévisibles ou masquer des incohérences.

## Pourquoi ne plus utiliser VALUE et IFERROR dans les mesures d'alerte ?

Les indicateurs d'alerte doivent être créés et typés comme des nombres entiers. Dans ce cas, un simple `SUM` suffit.

`VALUE` et `IFERROR` peuvent masquer un problème de typage. Il est plus propre de corriger le type dans Power Query ou dans la colonne calculée.

## Pourquoi un seuil strictement supérieur à 15 % ?

La règle métier indique qu'une différence de plus de 15 % déclenche une alerte. Les conditions utilisent donc `> 0,15` pour les coûts et durées et `< -0,15` pour les livrables.

Un écart exactement égal à 15 % n'est pas compté comme alerte.

## Pourquoi quatre pages ?

La `Vue exécutive` donne la synthèse. `Détail des alertes` permet l'action opérationnelle. `Planning Gantt` apporte la lecture temporelle. `Documentation du rapport` explique le PSC, la mise à jour et le modèle.

Les analyses géographique et stratégique envisagées dans le PSC ont été intégrées aux pages exécutive et détail afin de limiter le nombre d'onglets.

## Pourquoi ne pas faire une page par utilisateur ?

Les trois profils ont besoin des mêmes indicateurs à des niveaux différents. Les segments permettent de passer d'une vision globale à une région ou un pays sans dupliquer les pages et la maintenance.

## Pourquoi varier les graphiques ?

Chaque visuel répond à un besoin différent : les barres classent les régions, les colonnes empilées comparent des proportions, l'anneau montre la composition des alertes et la carte répond à la dimension géographique demandée par Sanitoral.

## Pourquoi utiliser des taux plutôt que seulement des nombres ?

Les projets IT comportent six phases et les projets Marketing quatre. Comparer seulement les volumes favorise mécaniquement l'IT.

Le taux permet une comparaison équitable. Le volume reste disponible dans les étiquettes ou infobulles pour mesurer la charge opérationnelle.

## Pourquoi utiliser une carte mondiale ?

La note de cadrage la demande explicitement. Elle permet aux directions générale et régionales de localiser les pays où le taux d'alerte est élevé.

Les noms de pays sont catégorisés comme pays/région et les variantes ambiguës sont normalisées dans Power Query si nécessaire.

## Pourquoi le coût est-il affiché en dollars ?

Le dictionnaire précise que `Actual_Cost` et `Planned_Cost` sont exprimés en USD. Afficher des euros sans conversion serait incorrect.

## Quelles sont les valeurs de contrôle ?

Sans filtre actif :

- 104 projets ;
- 102 projets en alerte ;
- 520 phases ;
- 348 phases en alerte, soit 66,92 % ;
- 214 alertes coût ;
- 159 alertes durée ;
- 96 alertes livrables ;
- 469 occurrences d'alerte ;
- 56 108 000 USD prévus et 60 200 800 USD réels.

## Pourquoi 469 alertes mais seulement 348 phases en alerte ?

Une même phase peut cumuler une alerte de coût, de durée et de livrables. Les 469 occurrences correspondent à la somme des trois natures d'alerte, tandis que les 348 phases ne sont comptées qu'une seule fois chacune.

## Quel axe stratégique ressort de l'analyse ?

Les projets IT ont un taux d'alerte de 72,12 %, supérieur aux 59,13 % des projets Marketing. Surtout, les 52 phases `Phase D - Testing` sont toutes en alerte.

La recommandation est de revoir les estimations et les contrôles de la phase de test, puis de formaliser des critères d'entrée, de sortie et des points de contrôle intermédiaires.

## Comment vérifier que le modèle est fiable ?

Je vérifie les volumes, l'unicité des clés, l'absence de valeurs manquantes, les cardinalités, l'absence de relation plusieurs-à-plusieurs, les KPI globaux et les interactions des visuels.

J'effectue également une actualisation complète et je compare les résultats aux valeurs de contrôle.

## Comment mettre le rapport à jour ?

Le fichier Excel est remplacé ou complété en conservant la même structure. Power Query rejoue automatiquement les transformations. Après `Fermer et appliquer`, je contrôle les relations, les erreurs, les KPI et les quatre pages avant d'enregistrer et d'exporter.

## Quelles limites peut-on identifier ?

Le rapport dépend de la stabilité des feuilles et colonnes sources. Une modification de structure peut nécessiter une adaptation de Power Query.

Le dashboard identifie les écarts et les zones à risque, mais l'explication métier précise d'une dérive nécessite un échange avec le responsable du projet.
