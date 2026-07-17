# Transformations Power Query

Ce document décrit la préparation automatique du jeu de données Sanitoral et le chargement du modèle relationnel cible.

## Objectif

Préparer les données sans modifier manuellement le fichier Excel source, afin de permettre une mise à jour hebdomadaire reproductible dans Power BI Desktop.

## Feuilles sources et requêtes cibles

| Feuille Excel source | Requête Power Query cible | Rôle |
|---|---|---|
| `Projects_plans` | `Projects_Plans` | Prévisions par projet-phase. |
| `Project type` | `Project_Type` | Type de chaque projet. |
| `Actual_Costs` | `Actual_Costs` | Coûts réels. |
| `Actual_Duration` | `Actual_Duration` | Durées réelles. |
| `Actual_Delivrable` | `Actual_Deliverables` | Livrables réels. |
| `Projects_Locations` | `Projects_Locations` | Pays de chaque projet. |
| `Country_Profiles` | `Country_Profiles` | Région et type d'entité. |

Le renommage de la requête `Actual_Deliverables` ne modifie pas le nom de la feuille Excel source.

## Étapes communes

Pour chaque feuille :

1. importer la feuille Excel ;
2. supprimer les lignes descriptives et vides avant les vrais en-têtes ;
3. promouvoir la première ligne utile comme en-tête ;
4. supprimer les lignes entièrement vides ;
5. harmoniser les noms de colonnes ;
6. nettoyer les espaces superflus dans les textes ;
7. appliquer explicitement les types ;
8. contrôler les valeurs nulles et les doublons.

## Harmonisation des colonnes

| Variantes sources | Nom cible |
|---|---|
| `Project ID`, `Proj_ID`, `Project`, `ID` | `Project_ID` |
| `Project Type` | `Project_Type` |
| `Start Date` | `Start_Date` |
| `Planned_Delivrable` | `Planned_Deliverables` |
| `Actual_Deliverables` | `Actual_Deliverables` |
| `Type` dans `Country_Profiles` | `Entity_Type` |

Nettoyer également la valeur `IT -  CRM Implementation` pour obtenir `IT - CRM Implementation`.

## Types attendus

| Colonnes | Type |
|---|---|
| `Project_ID` | Nombre entier |
| `Phase`, `Project_Type`, `Country`, `Region`, `Entity_Type` | Texte |
| `Start_Date` | Date |
| `Planned_Duration`, `Actual_Duration` | Nombre entier |
| `Planned_Cost`, `Actual_Cost` | Nombre entier ou décimal fixe |
| `Planned_Deliverables`, `Actual_Deliverables` | Nombre entier |
| `ProjectPhaseKey` | Texte |

## Création de ProjectPhaseKey

Créer la colonne dans `Projects_Plans`, `Actual_Costs`, `Actual_Duration` et `Actual_Deliverables` :

```powerquery
Text.From([Project_ID]) & "|" & [Phase]
```

Ajouter ensuite une étape `Type modifié` pour définir la colonne en Texte.

## Chargement dans le modèle

Activer le chargement de :

- `Projects_Plans` ;
- `Project_Type` ;
- `Actual_Costs` ;
- `Actual_Duration` ;
- `Actual_Deliverables` ;
- `Projects_Locations` ;
- `Country_Profiles`.

`Fact_ProjectPhasePerformance` peut être conservée temporairement pendant la migration, mais son chargement doit être désactivé lorsque tous les visuels utilisent le modèle relationnel.

## Contrôles attendus

| Contrôle | Valeur attendue |
|---|---:|
| Lignes `Projects_Plans` | 520 |
| Lignes dans chaque table `Actual_*` | 520 |
| Projets distincts | 104 |
| Pays distincts | 52 |
| Doublons `ProjectPhaseKey` | 0 |
| Clés de plan sans réalisé | 0 |
| Clés de réalisé sans plan | 0 |

Après `Fermer et appliquer`, créer les relations décrites dans [`modele_de_donnees.md`](modele_de_donnees.md).
