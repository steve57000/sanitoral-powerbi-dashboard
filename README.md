# Sanitoral - Tableau de bord Power BI

Projet de data visualisation realise dans le cadre du parcours Data Analyst.

L'objectif est de construire un tableau de bord Power BI dynamique permettant a Sanitoral de suivre l'avancement de ses projets IT et Marketing, d'identifier les ecarts de performance, et d'aider les directeurs a prioriser les actions correctives.

## Objectifs du projet

- Suivre la performance globale du portefeuille de projets.
- Identifier les projets, pays, regions et phases en alerte.
- Comparer les couts, delais et livrables prevus avec les resultats reels.
- Alerter les directeurs lorsqu'un ecart depasse 15 %.
- Proposer un axe strategique issu de l'analyse.
- Documenter le modele de donnees et la procedure de mise a jour hebdomadaire.

## Structure du repository

```text
mission/
  01_enonce_et_cadrage/       Fichiers de cadrage et consignes d'origine
  02_donnees_originales/      Jeu de donnees et dictionnaire fournis
  03_templates/               Modeles fournis pour les livrables

livrables/
  01_product_strategy_canvas/ Product Strategy Canvas final
  02_powerbi/                 Fichiers Power BI .pbix et .pbit
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

## Regle d'alerte

Sanitoral considere qu'un ecart de 15 % entre le prevu et le reel doit conduire a une alerte.

Les indicateurs surveilles sont :

- les couts des projets ;
- le respect des delais ;
- les livrables produits par rapport au planning.

## Pages prevues du rapport Power BI

1. Vue executive
2. Performance par projet
3. Analyse geographique
4. Diagnostic par phase
5. Documentation et procedure de mise a jour

## Etat d'avancement

| Etape | Statut |
|---|---|
| Structuration du repository | En cours |
| Audit de demarrage | Realise |
| Product Strategy Canvas | A faire |
| Preparation Power Query | A faire |
| Modele de donnees | A faire |
| Mesures DAX | A faire |
| Dashboard Power BI | A faire |
| Documentation finale | A faire |
| Soutenance | A faire |

