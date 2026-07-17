# Procédure de mise à jour

Cette procédure permet à Sanitoral d'actualiser le rapport chaque semaine sans refaire manuellement le nettoyage.

## Pré-requis

- Power BI Desktop installé ;
- PBIX final disponible ;
- nouveau fichier Excel respectant la structure des 7 feuilles sources ;
- droits d'accès au chemin du fichier source.

## Procédure utilisateur

1. Sauvegarder une copie du PBIX avant actualisation.
2. Remplacer le fichier Excel source ou mettre à jour son contenu sans renommer les feuilles ni les colonnes attendues.
3. Ouvrir `Sanitoral_PowerBI_Dashboard_Bell_Steve.pbix`.
4. Sélectionner `Accueil > Transformer les données`.
5. Vérifier le chemin du fichier dans l'étape `Source`.
6. Cliquer sur `Actualiser l'aperçu`.
7. Vérifier l'absence d'erreurs dans les étapes appliquées.
8. Contrôler les profils de colonnes, les types et les valeurs vides.
9. Vérifier que `ProjectPhaseKey` est de type Texte et reste unique dans les quatre tables projet-phase.
10. Sélectionner `Fermer et appliquer`.
11. Dans la vue Modèle, vérifier que les six relations sont actives et qu'aucune relation plusieurs-à-plusieurs n'est apparue.
12. Sélectionner `Accueil > Actualiser`.
13. Remettre les segments sur `Tout` et contrôler les KPI globaux.
14. Tester les filtres, la carte, les infobulles, le tableau de détail et le Gantt.
15. Vérifier les 4 pages : `Vue exécutive`, `Détail des alertes`, `Planning Gantt`, `Documentation du rapport`.
16. Enregistrer le PBIX puis exporter une nouvelle version PDF si nécessaire.

## Valeurs de contrôle du jeu actuel

Ces valeurs sont celles du fichier fourni pour la mission. Elles servent de référence tant que les données ne changent pas.

| Contrôle | Valeur attendue |
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

Si de nouvelles lignes métier sont ajoutées, les valeurs peuvent évoluer. Il faut alors vérifier leur cohérence plutôt que forcer les anciens totaux.

## Contrôles structurels

- 7 tables relationnelles chargées ;
- `Actual_Deliverables` utilisé comme nom de requête ;
- `ProjectPhaseKey` présent dans les quatre tables projet-phase ;
- coûts, durées, livrables et indicateurs d'alerte correctement typés ;
- aucune valeur vide dans les clés ;
- aucune relation directe entre `Project_Type` et les tables `Actual_*` ;
- `Fact_ProjectPhasePerformance` non chargée après migration ;
- coût affiché en USD.

## Points de vigilance

- ne pas modifier manuellement le fichier Excel d'origine pour corriger les noms ;
- ne pas renommer les feuilles sources ;
- ne pas introduire d'espace dans la formule de `ProjectPhaseKey` ;
- ne pas convertir les indicateurs d'alerte en texte ;
- ne pas créer de relation plusieurs-à-plusieurs pour contourner un doublon ;
- rechercher et corriger la cause d'un doublon avant de relancer l'actualisation.
