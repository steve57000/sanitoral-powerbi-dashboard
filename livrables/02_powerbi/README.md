# Fichier Power BI

Le fichier Power BI du projet est :

```text
Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix
```

## Statut

Le binaire actuellement versionné correspond à la version antérieure aux remarques de mentorat du 17 juillet 2026. Il doit être modifié manuellement dans Power BI Desktop avant la remise finale.

Le plan détaillé se trouve dans [`plan_corrections_powerbi.md`](plan_corrections_powerbi.md).

## Contrôles obligatoires avant remplacement du PBIX

- [ ] Les 7 tables nettoyées sont chargées dans le modèle.
- [ ] `Actual_Delivrable` est renommée `Actual_Deliverables` dans Power Query.
- [ ] `ProjectPhaseKey` est de type Texte dans les quatre tables projet-phase.
- [ ] Les tables de réalisé sont reliées à `Projects_Plans`, pas à `Project_Type`.
- [ ] La table fusionnée `Fact_ProjectPhasePerformance` n'est plus chargée après remappage des visuels.
- [ ] La vue Modèle affiche les six relations documentées.
- [ ] Les 4 pages sont présentes : `Vue exécutive`, `Détail des alertes`, `Planning Gantt`, `Documentation du rapport`.
- [ ] La vue exécutive contient des visuels variés et une carte mondiale.
- [ ] Le coût est formaté en USD et non en euros.
- [ ] `Staut d'alerte` est corrigé en `Statut d'alerte`.
- [ ] Les KPI correspondent aux valeurs de contrôle documentées.
- [ ] L'actualisation se termine sans erreur.

Le `.pbix`, les captures et le PDF doivent être exportés depuis Power BI Desktop afin de préserver l'intégrité du modèle et des visuels.
