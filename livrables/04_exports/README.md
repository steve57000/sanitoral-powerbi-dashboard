# Exports du dashboard

Ce dossier regroupe les captures et l'export PDF du rapport Power BI.

## Statut

Les fichiers binaires actuellement présents correspondent à la version antérieure à la révision mentor du 17 juillet 2026. Ils doivent être remplacés après modification du modèle et des visuels dans Power BI Desktop.

## Captures desktop attendues

- `vue_executive_desktop.png` ;
- `detail_des_alertes_desktop.png` ;
- `planning_gantt_desktop.png` ;
- `documentation_du_rapport_desktop.png` ;
- `modele_relationnel_powerbi.png`.

## Captures mobiles optionnelles

- `vue_executive_mobile.png` ;
- `detail_des_alertes_mobile.png`.

La vue mobile doit notamment éviter la troncature du coût réel et conserver des filtres utilisables.

## Export PDF

Le PDF final doit contenir les 4 pages dans cet ordre :

1. Vue exécutive ;
2. Détail des alertes ;
3. Planning Gantt ;
4. Documentation du rapport.

## Contrôles avant export

- remettre les segments sur `Tout` ;
- afficher les coûts en USD ;
- vérifier les titres et libellés en français ;
- vérifier les KPI globaux ;
- vérifier la carte mondiale et les infobulles ;
- conserver le filtre des phases en alerte sur la page de détail ;
- vérifier que la page Documentation montre le modèle relationnel et non l'ancien modèle à table unique.

Le PBIX, les images et le PDF sont exportés manuellement depuis Power BI Desktop afin de préserver l'intégrité du fichier.
