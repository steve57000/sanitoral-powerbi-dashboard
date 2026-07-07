# Exports du dashboard

Ce dossier regroupe les exports visuels du rapport Power BI.

## Captures attendues

Placer dans `captures_dashboard/` :

- une capture de la page `Vue executive` en version desktop ;
- une capture de la page `Vue executive` en version mobile si elle est produite ;
- une capture de la page `Detail des alertes` en version desktop ;
- une capture de la page `Detail des alertes` en version mobile si elle est produite.

## Export PDF

Placer dans `export_pdf/` l'export PDF du rapport si demande pour la remise ou la soutenance.

## Controle avant export

- Les filtres de la page executive doivent etre remis sur `Tout`.
- Les titres doivent etre lisibles.
- Les KPI doivent afficher les valeurs globales attendues.
- Le tableau de detail doit rester filtre sur `Alert_Status = En alerte`.

Les fichiers images, PDF et `.pbix` sont ajoutes manuellement par l'utilisateur. L'assistant ne doit pas generer ces fichiers binaires dans le repository.
