# Contrôle qualité final

Cette checklist doit être complétée dans Power BI Desktop après application de la révision mentor.

## Fichiers

- [x] Product Strategy Canvas présent.
- [x] PBIX présent dans `livrables/02_powerbi/`.
- [x] Documentation relationnelle et DAX mise à jour.
- [x] Script de présentation et questions jury présents.
- [ ] PBIX remplacé par la version relationnelle validée.
- [ ] Captures des 4 pages remplacées après révision.
- [ ] Export PDF des 4 pages remplacé après révision.
- [ ] Capture lisible de la vue Modèle ajoutée.

## Power Query

- [ ] Les requêtes sont nommées `Projects_Plans`, `Project_Type`, `Actual_Costs`, `Actual_Duration`, `Actual_Deliverables`, `Projects_Locations`, `Country_Profiles`.
- [ ] La feuille source `Actual_Delivrable` n'a pas été modifiée manuellement.
- [ ] Les lignes descriptives et vides sont supprimées.
- [ ] Les en-têtes et noms de colonnes sont harmonisés.
- [ ] Les types sont appliqués explicitement.
- [ ] `ProjectPhaseKey` utilise `Text.From([Project_ID]) & "|" & [Phase]`.
- [ ] `ProjectPhaseKey` est de type Texte dans les quatre tables projet-phase.
- [ ] Chaque table projet-phase contient 520 clés distinctes et 0 doublon.
- [ ] Les indicateurs d'alerte sont numériques.
- [ ] Les sept tables relationnelles sont chargées.
- [ ] `Fact_ProjectPhasePerformance` n'est plus chargée après remappage.

## Modèle

- [ ] `Project_Type[Project_ID]` est reliée à `Projects_Plans[Project_ID]` en 1-*.
- [ ] `Projects_Locations[Project_ID]` est reliée à `Projects_Plans[Project_ID]` en 1-*.
- [ ] `Country_Profiles[Country]` est reliée à `Projects_Locations[Country]` en 1-*.
- [ ] `Projects_Plans[ProjectPhaseKey]` est reliée à chaque table `Actual_*` en 1-1.
- [ ] Aucune table `Actual_*` n'est reliée directement à `Project_Type`.
- [ ] Aucune relation plusieurs-à-plusieurs n'existe.
- [ ] Les six relations sont actives et visibles dans la vue Modèle.
- [ ] Les clés techniques sont masquées dans l'affichage du rapport si elles ne servent pas aux utilisateurs.

## Vue exécutive

- [ ] Les KPI affichent 104 projets, 102 projets en alerte, 348 phases en alerte et 66,92 %.
- [ ] Le coût réel affiche `60,20 M$` ou une autre présentation en USD, jamais en euros.
- [ ] Le segment de dates fonctionne.
- [ ] Le graphique régional utilise un taux comparable et propose le volume en infobulle.
- [ ] Le graphique par type est empilé à 100 % avec `En alerte` et `OK`.
- [ ] La répartition par nature utilise un anneau ou un autre visuel distinct des barres.
- [ ] Une carte mondiale permet l'analyse par pays.
- [ ] Les infobulles présentent prévu, réel et écart.
- [ ] L'encart stratégique sur `Phase D - Testing` est visible.

## Détail des alertes

- [ ] Le tableau est filtré sur `Alert_Status = En alerte`.
- [ ] `Statut d'alerte` est correctement orthographié.
- [ ] Le tri est décroissant sur `Alert_Count`.
- [ ] La mise en forme conditionnelle fait ressortir les valeurs 1, 2 et 3.
- [ ] Les écarts de coût, durée et livrables sont accessibles dans le tableau ou l'infobulle.
- [ ] Les filtres par type, pays, région et phase fonctionnent.

## Planning Gantt

- [ ] Le visuel Gantt est présent et fonctionnel.
- [ ] Les tâches utilisent `Gantt_Task`.
- [ ] Le début utilise `Start_Date` et la durée `Planned_Duration`.
- [ ] La couleur distingue `En alerte` et `OK`.
- [ ] Les années sont lisibles sur l'axe temporel.

## Documentation du rapport

- [ ] Le Product Strategy Canvas est résumé.
- [ ] La procédure de mise à jour est présente.
- [ ] Une capture de la vue Modèle relationnelle est intégrée.
- [ ] Les relations et cardinalités sont expliquées.
- [ ] Le renommage `Actual_Deliverables` est expliqué.
- [ ] La règle stricte de 15 % et les KPI de contrôle sont expliqués.

## Valeurs de contrôle du fichier de mission

| Indicateur | Valeur attendue |
|---|---:|
| Projets | 104 |
| Projets en alerte | 102 |
| Phases | 520 |
| Phases en alerte | 348 |
| Taux de phases en alerte | 66,92 % |
| Alertes coût | 214 |
| Alertes durée | 159 |
| Alertes livrables | 96 |
| Occurrences d'alerte | 469 |
| Coût prévu | 56 108 000 USD |
| Coût réel | 60 200 800 USD |
| Écart coût | 7,29 % |

## Validation finale

- [ ] Actualisation complète sans erreur.
- [ ] Test des interactions entre visuels.
- [ ] Test des filtres pour les trois niveaux de direction.
- [ ] Vérification de la mise en page desktop.
- [ ] Vérification de la mise en page mobile.
- [ ] Export PDF relu page par page.
- [ ] Documentation GitHub cohérente avec le PBIX livré.
