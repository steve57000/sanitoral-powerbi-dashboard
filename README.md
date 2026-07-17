# Sanitoral - Tableau de bord Power BI

Projet de data visualisation réalisé dans le cadre du parcours Data Analyst OpenClassrooms.

L'objectif est de fournir à Sanitoral un tableau de bord Power BI permettant de suivre les projets IT et Marketing, d'identifier les écarts de coûts, de délais et de livrables, puis de prioriser les actions correctives.

## État du projet

La documentation a été révisée le 17 juillet 2026 à la suite des retours de mentorat.

Le modèle cible est désormais relationnel : `Projects_Plans` constitue la table centrale au grain projet-phase et les tables de réalisé sont reliées par `ProjectPhaseKey`. Cette structure rend les relations visibles dans Power BI et répond explicitement à l'étape pédagogique consacrée au modèle de données.

Le fichier `.pbix` et les exports binaires présents dans le dépôt correspondent encore à la version antérieure à cette révision. Les opérations manuelles à réaliser dans Power BI Desktop sont décrites dans [`plan_corrections_powerbi.md`](livrables/02_powerbi/plan_corrections_powerbi.md).

## Modèle relationnel cible

Tables chargées dans le modèle :

- `Projects_Plans` : données prévues et indicateurs au grain projet-phase ;
- `Actual_Costs` : coûts réels par projet-phase ;
- `Actual_Duration` : durées réelles par projet-phase ;
- `Actual_Deliverables` : livrables réels par projet-phase ;
- `Project_Type` : type de chaque projet ;
- `Projects_Locations` : pays de chaque projet ;
- `Country_Profiles` : région et type d'entité de chaque pays.

Les trois tables de réalisé sont reliées à `Projects_Plans` par la clé texte `ProjectPhaseKey`. Elles ne sont pas reliées directement à `Project_Type`.

## Pages finales du rapport Power BI

Le rapport contient 4 pages :

1. **Vue exécutive**
   - KPI : projets, projets en alerte, phases en alerte, taux d'alerte, coût réel et écart de coût.
   - Filtres : type de projet, pays, région, statut, phase et période.
   - Visuels cibles : barres par région, colonnes empilées à 100 % par type de projet, anneau par nature d'alerte et carte mondiale.
2. **Détail des alertes**
   - Tableau filtré sur les phases en alerte.
   - Écarts de coût, de durée et de livrables, triés par criticité.
3. **Planning Gantt**
   - Planning des phases coloré selon le statut d'alerte.
4. **Documentation du rapport**
   - Product Strategy Canvas, procédure de mise à jour, transformations Power Query, modèle relationnel et contrôles qualité.

Les cinq vues envisagées dans le Product Strategy Canvas ont été regroupées en quatre pages finales : l'analyse géographique est intégrée à la vue exécutive et le diagnostic opérationnel à la page de détail.

## Valeurs de contrôle

Valeurs attendues sans filtre actif :

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
| Écart de coût | 7,29 % |

## Règle d'alerte

Une phase est en alerte lorsqu'au moins une des conditions suivantes est remplie :

- coût réel supérieur au coût prévu de plus de 15 % ;
- durée réelle supérieure à la durée prévue de plus de 15 % ;
- livrables réels inférieurs aux livrables prévus de plus de 15 %.

## Livrables principaux

- `livrables/01_product_strategy_canvas/Product_Strategy_Canvas_Sanitoral_Bell_Steve.docx`
- `livrables/02_powerbi/Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`
- `livrables/03_documentation/`
- `livrables/04_exports/`
- `livrables/05_soutenance/`

## Structure du repository

```text
mission/
  01_enonce_et_cadrage/       Fichiers de cadrage et consignes d'origine
  02_donnees_originales/      Jeu de données et dictionnaire fournis
  03_templates/               Modèles fournis pour les livrables

livrables/
  01_product_strategy_canvas/ Product Strategy Canvas final
  02_powerbi/                 PBIX et plan de corrections Power BI
  03_documentation/           Modèle, DAX, Power Query et contrôles
  04_exports/                 Exports PDF et captures du dashboard
  05_soutenance/              Script oral et questions probables

ressources/
  analyses_preparatoires/     Audits et analyses internes
  theme_powerbi/              Thème JSON Power BI
  mockups/                    Maquettes et propositions visuelles

notes/
  journal_de_bord.md          Suivi chronologique du travail
  decisions_projet.md         Décisions de conception et arbitrages
```

## Outils utilisés

- Power BI Desktop
- Power Query
- DAX
- Excel
- Git et GitHub
- Markdown
