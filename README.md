# Sanitoral - Tableau de bord Power BI

Projet de data visualisation réalisé dans le cadre du parcours Data Analyst.

L'objectif est de fournir à Sanitoral un tableau de bord Power BI finalisé permettant de suivre l'avancement des projets IT et Marketing, d'identifier les écarts de performance et de prioriser les actions correctives.

## État final du projet

Le dashboard Power BI est construit autour d'une table finale chargée dans le modèle : `Fact_ProjectPhasePerformance`.

Les tables sources nettoyées dans Power Query servent à construire cette table finale, mais leur chargement est désactivé dans le modèle Power BI afin de conserver une structure simple, lisible et facile à présenter.

## Pages finales du rapport Power BI

Le rapport final contient 3 pages finales :

1. **Vue exécutive**
   - KPI : Nb Projets, Nb Phases, Nb Phases en alerte, Taux phases en alerte, Coût réel, Écart coût %.
   - Filtres : `Project_Type`, `Country`, `Region`, `Alert_Status`, `Phase`.
   - Graphiques : phases en alerte par région, phases en alerte par type de projet, répartition des alertes par nature.
2. **Détail des alertes**
   - Tableau filtré sur `Alert_Status = En alerte`.
   - Colonnes : `Project_ID`, `Phase`, `Country`, `Region`, `Project_Type`, `Alert_Count`, `Alert_Status`, Écart coût %.
   - Tri décroissant sur `Alert_Count` et mise en forme conditionnelle sur `Alert_Count`.
3. **Documentation & Méthode**
   - Présentation du Product Strategy Canvas.
   - Rappel des étapes de préparation et de mise à jour des données.
   - Synthèse du modèle de données et des transformations Power Query.
   - Explication de la règle d'alerte à 15 %.
   - KPI de contrôle utilisés pour vérifier la cohérence du rapport.

## KPI de contrôle globaux

Valeurs attendues sans filtre actif :

| Indicateur | Valeur attendue |
|---|---:|
| Nb Projets | 104 |
| Nb Phases | 520 |
| Nb Phases en alerte | 348 |
| Taux phases en alerte | 66,92 % |
| Nb alertes coût | 214 |
| Nb alertes durée | 159 |
| Nb alertes livrables | 96 |

## Règle d'alerte

Sanitoral considère qu'un écart de 15 % entre le prévu et le réel doit conduire à une alerte.

Les indicateurs surveillés sont :

- les coûts des projets ;
- le respect des délais ;
- les livrables produits par rapport au planning.

## Livrables principaux

- `livrables/01_product_strategy_canvas/Product_Strategy_Canvas_Sanitoral_Bell_Steve.docx`
- `livrables/02_powerbi/Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`
- `livrables/03_documentation/`
- `livrables/04_exports/`
- `livrables/05_soutenance/`

Le fichier `.pbix`, les captures et les exports PDF sont présents dans les dossiers de livrables lorsqu'ils ont été ajoutés manuellement par l'utilisateur.

## Structure du repository

```text
mission/
  01_enonce_et_cadrage/       Fichiers de cadrage et consignes d'origine
  02_donnees_originales/      Jeu de données et dictionnaire fournis
  03_templates/               Modèles fournis pour les livrables

livrables/
  01_product_strategy_canvas/ Product Strategy Canvas final
  02_powerbi/                 Fichier Power BI final
  03_documentation/           Documentation du modèle, DAX et Power Query
  04_exports/                 Exports PDF et captures du dashboard
  05_soutenance/              Script oral et questions probables

ressources/
  analyses_preparatoires/     Audits, analyses et notes de cadrage internes
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
- Git / GitHub
- Markdown
