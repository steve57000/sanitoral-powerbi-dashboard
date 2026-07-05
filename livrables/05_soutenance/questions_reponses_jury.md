# Questions / reponses probables du jury

## Pourquoi avoir cree une cle projet-phase ?

Chaque ligne du fichier represente une phase d'un projet, et non un projet complet.

`Project_ID` seul ne suffit donc pas, car un meme projet apparait sur plusieurs lignes.

La cle `ProjectPhaseKey` permet de relier correctement les couts, durees et livrables au bon niveau d'analyse.

## Pourquoi faire le nettoyage dans Power Query ?

Le scenario precise que Sanitoral souhaite mettre a jour l'analyse chaque semaine.

Power Query permet d'automatiser les transformations : suppression des lignes inutiles, promotion des en-tetes, typage et jointures.

Cela evite de refaire le nettoyage a la main a chaque mise a jour.

## Pourquoi utiliser un seuil de 15 % ?

Le seuil de 15 % vient de la note de cadrage.

Sanitoral considere qu'un ecart superieur a 15 % entre le prevu et le reel doit conduire a une alerte.

## Pourquoi ne pas faire une page par utilisateur ?

Le rapport doit rester utilisable par les trois profils de direction.

Les filtres, segments, infobulles et interactions permettent d'adapter la lecture au niveau de responsabilite sans multiplier inutilement les pages.

## Quel est l'interet de la carte geographique ?

Sanitoral est present dans plusieurs regions du monde.

La carte permet d'identifier rapidement les pays ou les projets sont le plus en retard ou le plus souvent en alerte.

Elle repond aussi a une demande explicite du cahier des charges.

## Quelle recommandation strategique ressort de l'analyse ?

Les projets IT concentrent une part importante des alertes, et la phase D - Testing apparait comme une phase critique.

Une recommandation possible est d'auditer la planification, les estimations de couts et les criteres de validation de cette phase.

## Comment verifier que le modele est fiable ?

Je controle :

- le nombre de projets ;
- le nombre de phases ;
- les doublons sur la cle projet-phase ;
- les valeurs manquantes ;
- la coherence des relations ;
- les totaux de couts, durees et livrables.

## Pourquoi documenter les mesures DAX ?

Les mesures DAX sont au coeur de l'analyse.

Les documenter permet de rendre le rapport plus maintenable et plus facile a expliquer pendant la soutenance.

