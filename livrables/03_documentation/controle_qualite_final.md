# Controle qualite final

Cette checklist sert a verifier le dashboard Power BI Sanitoral avant remise.

## Checklist fichiers attendus

- [ ] `livrables/01_product_strategy_canvas/Product_Strategy_Canvas_Sanitoral_Bell_Steve.docx` present.
- [ ] `livrables/02_powerbi/Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix` present.
- [ ] Documentation presente dans `livrables/03_documentation/`.
- [ ] Captures ajoutees dans `livrables/04_exports/captures_dashboard/` si demande.
- [ ] Export PDF ajoute dans `livrables/04_exports/export_pdf/` si demande.
- [ ] Script de presentation et questions jury presents dans `livrables/05_soutenance/`.

## Checklist Power Query

- [ ] Les 7 feuilles sources sont importees : `Projects_plans`, `Project type`, `Actual_Costs`, `Actual_Duration`, `Actual_Delivrable`, `Projects_Locations`, `Country_Profiles`.
- [ ] Les lignes descriptives et vides sont supprimees.
- [ ] Les en-tetes sont correctement promus.
- [ ] Les noms de colonnes sont harmonises.
- [ ] Les types de donnees sont corriges.
- [ ] `ProjectPhaseKey` est creee avec `Text.From([Project_ID]) & "|" & [Phase]`.
- [ ] Les jointures alimentent correctement `Fact_ProjectPhasePerformance`.
- [ ] Les tables intermediaires sont desactivees au chargement.

## Checklist modele

- [ ] Une seule table est chargee : `Fact_ProjectPhasePerformance`.
- [ ] Aucune relation n'est necessaire dans le modele final.
- [ ] Les colonnes finales attendues sont presentes.
- [ ] Les mesures DAX principales sont creees.
- [ ] Les mesures d'alerte utilisent `VALUE()` et `IFERROR()` pour gerer les colonnes typees en texte.

## Checklist visuelle - Vue executive

- [ ] Les cartes KPI affichent Nb Projets, Nb Phases, Nb Phases en alerte, Taux phases en alerte, Cout reel et Ecart cout %.
- [ ] Les filtres `Project_Type`, `Country`, `Region`, `Alert_Status` et `Phase` fonctionnent.
- [ ] Le graphique des phases en alerte par region est lisible.
- [ ] Le graphique des phases en alerte par type de projet est lisible.
- [ ] La repartition des alertes par nature est lisible.
- [ ] Les couleurs et titres sont coherents avec le design final.

## Checklist visuelle - Detail des alertes

- [ ] Le tableau est filtre sur `Alert_Status = En alerte`.
- [ ] Les colonnes attendues sont presentes : `Project_ID`, `Phase`, `Country`, `Region`, `Project_Type`, `Alert_Count`, `Alert_Status`, Ecart cout %.
- [ ] Le tri est decroissant sur `Alert_Count`.
- [ ] La mise en forme conditionnelle sur `Alert_Count` est visible.
- [ ] Les filtres de page permettent une analyse par pays, region, type de projet et phase.

## Valeurs de controle globales

Sans filtre actif :

| Indicateur | Valeur attendue |
|---|---:|
| Nb Projets | 104 |
| Nb Phases | 520 |
| Nb Phases en alerte | 348 |
| Taux phases en alerte | 66,92 % |
| Nb alertes cout | 214 |
| Nb alertes duree | 159 |
| Nb alertes livrables | 96 |

## Derniers points avant remise

- [ ] Placer le `.pbix` final dans `livrables/02_powerbi/`.
- [ ] Ajouter les captures dans `livrables/04_exports/captures_dashboard/`.
- [ ] Ajouter le PDF exporte dans `livrables/04_exports/export_pdf/` si demande.
- [ ] Verifier que les fichiers binaires ajoutes manuellement ne remplacent pas la documentation texte.
