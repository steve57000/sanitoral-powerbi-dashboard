# Contrôle qualité final

Cette checklist sert à vérifier le dashboard Power BI Sanitoral avant remise.

## Checklist fichiers attendus

- [x] `livrables/01_product_strategy_canvas/Product_Strategy_Canvas_Sanitoral_Bell_Steve.docx` présent.
- [x] `livrables/02_powerbi/Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix` présent.
- [x] Documentation présente dans `livrables/03_documentation/`.
- [x] Captures ajoutées dans `livrables/04_exports/captures_dashboard/`.
- [x] Export PDF ajouté dans `livrables/04_exports/export_pdf/`.
- [x] Script de présentation et questions jury présents dans `livrables/05_soutenance/`.

## Checklist Power Query

- [x] Les 7 feuilles sources sont importées : `Projects_plans`, `Project type`, `Actual_Costs`, `Actual_Duration`, `Actual_Delivrable`, `Projects_Locations`, `Country_Profiles`.
- [x] Les lignes descriptives et vides sont supprimées.
- [x] Les en-têtes sont correctement promus.
- [x] Les noms de colonnes sont harmonisés.
- [x] Les types de données sont corrigés.
- [x] `ProjectPhaseKey` est créée avec `Text.From([Project_ID]) & "|" & [Phase]`.
- [x] Les jointures alimentent correctement `Fact_ProjectPhasePerformance`.
- [x] Les tables intermédiaires sont désactivées au chargement.

## Checklist modèle

- [x] Une seule table est chargée : `Fact_ProjectPhasePerformance`.
- [x] Aucune relation n'est nécessaire dans le modèle final.
- [x] Les colonnes finales attendues sont présentes.
- [x] Les mesures DAX principales sont créées.
- [x] Les mesures d'alerte utilisent `VALUE()` et `IFERROR()` pour gérer les colonnes typées en texte.

## Checklist visuelle - Vue exécutive

- [ ] Les cartes KPI affichent Nb Projets, Nb Phases, Nb Phases en alerte, Taux phases en alerte, Coût réel et Écart coût %.
- [ ] Les filtres `Project_Type`, `Country`, `Region`, `Alert_Status` et `Phase` fonctionnent.
- [ ] Le graphique des phases en alerte par région est lisible.
- [ ] Le graphique des phases en alerte par type de projet est lisible.
- [ ] La répartition des alertes par nature est lisible.
- [ ] Les couleurs et titres sont cohérents avec le design final.

## Checklist visuelle - Détail des alertes

- [ ] Le tableau est filtré sur `Alert_Status = En alerte`.
- [ ] Les colonnes attendues sont présentes : `Project_ID`, `Phase`, `Country`, `Region`, `Project_Type`, `Alert_Count`, `Alert_Status`, Écart coût %.
- [ ] Le tri est décroissant sur `Alert_Count`.
- [ ] La mise en forme conditionnelle sur `Alert_Count` est visible.
- [ ] Les filtres de page permettent une analyse par pays, région, type de projet et phase.

## Checklist visuelle - Documentation & Méthode

- [ ] La page `Documentation & Méthode` est présente dans le rapport.
- [ ] Elle présente le Product Strategy Canvas.
- [ ] Elle rappelle les étapes de préparation et de mise à jour des données.
- [ ] Elle décrit le modèle de données et les transformations Power Query.
- [ ] Elle explique la règle d'alerte à 15 % et les KPI de contrôle.

## Valeurs de contrôle globales

Sans filtre actif :

| Indicateur | Valeur attendue |
|---|---:|
| Nb Projets | 104 |
| Nb Phases | 520 |
| Nb Phases en alerte | 348 |
| Taux phases en alerte | 66,92 % |
| Nb alertes coût | 214 |
| Nb alertes durée | 159 |
| Nb alertes livrables | 96 |

## Points à vérifier dans Power BI Desktop

Ces contrôles doivent rester manuels, car ils nécessitent l'ouverture du fichier `.pbix` dans Power BI Desktop :

- [ ] Présence de la page `Documentation & Méthode`.
- [ ] Lisibilité des visuels sur les 3 pages finales.
- [ ] Fonctionnement des filtres et segments.
- [ ] Export PDF à jour.
- [ ] Valeurs globales conformes sans filtre actif.

## Derniers points avant remise

- [x] Placer le `.pbix` final dans `livrables/02_powerbi/`.
- [x] Ajouter les captures dans `livrables/04_exports/captures_dashboard/`.
- [x] Ajouter le PDF exporté dans `livrables/04_exports/export_pdf/`.
- [x] Vérifier que les fichiers binaires ajoutés manuellement ne remplacent pas la documentation texte.
