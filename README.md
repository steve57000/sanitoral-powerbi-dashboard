# Sanitoral - Tableau de bord Power BI

Projet de data visualisation realise dans le cadre du parcours Data Analyst.

L'objectif est de fournir a Sanitoral un tableau de bord Power BI finalise permettant de suivre l'avancement des projets IT et Marketing, d'identifier les ecarts de performance et de prioriser les actions correctives.

## Etat final du projet

Le dashboard Power BI est construit autour d'une table finale chargee dans le modele : `Fact_ProjectPhasePerformance`.

Les tables sources nettoyees dans Power Query servent a construire cette table finale, mais leur chargement est desactive dans le modele Power BI afin de conserver un modele simple, lisible et facile a presenter.

## Pages finales du rapport Power BI

Le rapport final contient 2 pages principales :

1. **Vue executive**
   - KPI : Nb Projets, Nb Phases, Nb Phases en alerte, Taux phases en alerte, Cout reel, Ecart cout %.
   - Filtres : `Project_Type`, `Country`, `Region`, `Alert_Status`, `Phase`.
   - Graphiques : phases en alerte par region, phases en alerte par type de projet, repartition des alertes par nature.
2. **Detail des alertes**
   - Tableau filtre sur `Alert_Status = En alerte`.
   - Colonnes : `Project_ID`, `Phase`, `Country`, `Region`, `Project_Type`, `Alert_Count`, `Alert_Status`, Ecart cout %.
   - Tri decroissant sur `Alert_Count` et mise en forme conditionnelle sur `Alert_Count`.

## KPI de controle globaux

Valeurs attendues sans filtre actif :

| Indicateur | Valeur attendue |
|---|---:|
| Nb Projets | 104 |
| Nb Phases | 520 |
| Nb Phases en alerte | 348 |
| Taux phases en alerte | 66,92 % |
| Nb alertes cout | 214 |
| Nb alertes duree | 159 |
| Nb alertes livrables | 96 |

## Regle d'alerte

Sanitoral considere qu'un ecart de 15 % entre le prevu et le reel doit conduire a une alerte.

Les indicateurs surveilles sont :

- les couts des projets ;
- le respect des delais ;
- les livrables produits par rapport au planning.

## Livrables principaux

- `livrables/01_product_strategy_canvas/Product_Strategy_Canvas_Sanitoral_Bell_Steve.docx`
- `livrables/02_powerbi/Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`
- `livrables/03_documentation/`
- `livrables/04_exports/`
- `livrables/05_soutenance/`

Le fichier `.pbix`, les captures et les exports PDF sont ajoutes manuellement par l'utilisateur.

## Structure du repository

```text
mission/
  01_enonce_et_cadrage/       Fichiers de cadrage et consignes d'origine
  02_donnees_originales/      Jeu de donnees et dictionnaire fournis
  03_templates/               Modeles fournis pour les livrables

livrables/
  01_product_strategy_canvas/ Product Strategy Canvas final
  02_powerbi/                 Fichier Power BI final ajoute manuellement
  03_documentation/           Documentation du modele, DAX et Power Query
  04_exports/                 Exports PDF et captures du dashboard
  05_soutenance/              Script oral et questions probables

ressources/
  analyses_preparatoires/     Audits, analyses et notes de cadrage internes
  theme_powerbi/              Theme JSON Power BI
  mockups/                    Maquettes et propositions visuelles

notes/
  journal_de_bord.md          Suivi chronologique du travail
  decisions_projet.md         Decisions de conception et arbitrages
```

## Outils utilises

- Power BI Desktop
- Power Query
- DAX
- Excel
- Git / GitHub
- Markdown
