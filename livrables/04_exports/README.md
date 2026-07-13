# Exports du dashboard

Ce dossier regroupe les exports visuels du rapport Power BI.

## Captures attendues

Placer dans `captures_dashboard/` :

- une capture de la page `Vue exécutive` en version desktop ;
- une capture de la page `Vue exécutive` en version mobile si elle est produite ;
- une capture de la page `Détail des alertes` en version desktop ;
- une capture de la page `Détail des alertes` en version mobile si elle est produite ;
- une capture de la page `Documentation & Méthode` en version desktop si elle est demandée.

## Export PDF

Placer dans `export_pdf/` l'export PDF du rapport si demande pour la remise ou la soutenance.

## Contrôle avant export

- Les filtres de la page exécutive doivent être remis sur `Tout`.
- Les titres doivent être lisibles.
- Les KPI doivent afficher les valeurs globales attendues.
- Le tableau de détail doit rester filtré sur `Alert_Status = En alerte`.

Les fichiers images, PDF et `.pbix` sont ajoutés manuellement par l'utilisateur. L'assistant ne doit pas générer ces fichiers binaires dans le repository.
