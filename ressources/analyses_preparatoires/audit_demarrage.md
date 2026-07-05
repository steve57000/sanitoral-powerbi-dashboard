# Audit de demarrage - Projet Power BI Sanitoral

## 1. Synthese executive

Le projet consiste a construire un tableau de bord Power BI dynamique pour Sanitoral, une entreprise internationale de soins bucco-dentaires, afin de suivre l'avancement des projets IT et Marketing, identifier les retards et alerter les directeurs lorsqu'un ecart significatif apparait.

Les fichiers fournis permettent de realiser un projet solide et professionnel :

- un cadrage metier clair avec 3 profils utilisateurs : directeur general, directeur regional, directeur pays ;
- un seuil d'alerte explicite : 15 % d'ecart entre prevu et realise sur les couts, les delais ou les livrables ;
- des donnees exploitables entre 2018 et debut 2022 ;
- 104 projets, 520 phases, 52 pays et 4 grandes regions ;
- un besoin de mise a jour hebdomadaire avec nettoyage automatique dans Power Query ;
- un livrable Power BI qui doit contenir a la fois les visualisations, le Product Strategy Canvas, la procedure de mise a jour et le modele de donnees.

Orientation recommandee : construire un rapport Power BI en 4 pages principales, avec une page d'accueil executive, une page performance projets, une page geographique, une page diagnostic phases, puis une page documentation/methode. Le rapport doit fonctionner pour les trois niveaux de direction grace aux filtres, aux drill-through, aux infobulles et a une logique de niveau de lecture, plutot que par une page separee pour chaque role.

## 2. Attendus pedagogiques et livrables

Competences visees :

- identifier les enjeux client ;
- formaliser les user stories dans un Product Strategy Canvas ;
- preparer et transformer les donnees dans Power Query ;
- creer un modele relationnel propre ;
- developper des visualisations interactives adaptees aux utilisateurs ;
- produire un reporting qui facilite la decision ;
- presenter les resultats avec une narration claire et professionnelle.

Livrables a preparer :

- Product Strategy Canvas complete ;
- fichier Power BI Desktop `.pbix` ;
- tableau de bord multi-pages ;
- captures ou page explicative des etapes Power Query ;
- modele de donnees documente ;
- axe strategique issu de l'analyse ;
- support de presentation ou script oral de soutenance ;
- eventuellement un mockup initial valide par le mentor.

## 3. Audit des sources

Fichiers analyses :

- `Note de cadrage Sanitoral-3.pdf` : contexte, utilisateurs, indicateurs, specifications fonctionnelles ;
- `Objectif_pedagogique.pdf` : competences et logique du projet ;
- `OptionA_le_scenario.pdf` : scenario complet, livrables attendus, etapes de projet ;
- `Modele de Product Strategy Canvas a completer.docx` : structure du PSC ;
- `Dictionnaire des donnees.xlsx` : definitions metier des champs ;
- `Donnees Sanitoral.xlsx` : jeu de donnees principal.

Structure du fichier de donnees :

| Feuille | Role | Lignes utiles |
|---|---:|---:|
| `Projects_plans` | previsions par projet et phase | 520 |
| `Project type` | type projet IT ou Marketing | 104 |
| `Actual_Costs` | couts reels par phase | 520 |
| `Actual_Duration` | durees reelles par phase | 520 |
| `Actual_Delivrable` | livrables reels par phase | 520 |
| `Projects_Locations` | pays par projet | 104 |
| `Country_Profiles` | region et type pays | 52 |

Constat important : plusieurs feuilles contiennent des lignes descriptives et vides avant les vrais en-tetes. Le nettoyage devra donc etre fait dans Power Query avec suppression des premieres lignes, promotion des en-tetes et typage automatique. Il ne faut pas modifier le fichier Excel source manuellement.

## 4. Audit qualite des donnees

Points positifs :

- 104 projets dans les plans, types et localisations ;
- 520 cles projet-phase uniques ;
- aucune cle dupliquee apres creation de la cle `Project ID + Phase` ;
- aucune valeur manquante apres jointure des tables nettoyees ;
- les tables de cout, duree et livrables couvrent toutes les phases planifiees ;
- correspondance complete entre pays et profils pays.

Risques et corrections a prevoir :

| Risque | Impact | Correction recommandee |
|---|---|---|
| En-tetes non situes en ligne 1 | import Power BI fragile | supprimer les lignes inutiles puis promouvoir les vrais en-tetes |
| Noms de colonnes incoherents : `Project ID`, `Proj_ID`, `Project`, `ID` | relations impossibles sans normalisation | renommer en `Project_ID` |
| Orthographe variable : `Delivrable` / `Deliverables` | confusion dans mesures et visuels | standardiser en `Deliverables` dans Power Query |
| Phase seule non unique | jointures erronees possibles | creer une cle `ProjectPhaseKey = Project_ID & "|" & Phase` |
| Type projet avec double espace : `IT -  CRM Implementation` | affichage peu propre | nettoyer les espaces |
| Dates et nombres importes en type texte possible | mesures DAX fausses | typer explicitement les colonnes |
| Pays avec accents et variantes (`Republique Cheque`, `Equateur`, etc.) | carte Power BI parfois imprecise | verifier la geolocalisation, ajouter eventuellement une table latitude/longitude |

## 5. Premiers constats analytiques

Periode couverte : du 01/01/2018 au 13/02/2022.

Volume :

- 104 projets ;
- 520 phases ;
- 52 projets IT et 52 projets Marketing ;
- 52 pays ;
- 4 grandes regions.

Indicateurs globaux :

| Indicateur | Prevu | Reel | Lecture |
|---|---:|---:|---|
| Couts | 56 108 000 USD | 60 200 800 USD | depassement global des couts |
| Duree | 52 722 jours | 45 641 jours | duree globale inferieure au prevu |
| Livrables | 8 735 | 7 819 | deficit global de livrables |

Alertes selon le seuil de 15 % :

- 348 phases en alerte sur 520 ;
- 102 projets touches par au moins une alerte ;
- 214 alertes cout ;
- 159 alertes duree ;
- 96 alertes livrables.

Lecture par type de projet :

| Type projet | Projets | Phases | Phases en alerte | Constat |
|---|---:|---:|---:|---|
| IT - CRM Implementation | 52 | 312 | 225 | risque majeur, surtout couts |
| Marketing - Launch of new product | 52 | 208 | 123 | risque present mais plus modere |

Axe strategique fort pour la soutenance :

> Les projets IT semblent concentrer le risque de performance, notamment sur la phase D - Testing. Cette phase presente 52 alertes sur 52 phases et un ecart moyen de cout exceptionnel. Il faut recommander un audit des estimations, du controle qualite et des criteres d'entree/sortie de la phase de test.

## 6. Modele de donnees recommande

Modele en etoile recommande :

- table de faits principale : `Fact_ProjectPhasePerformance` ;
- dimensions :
  - `Dim_Project` ;
  - `Dim_ProjectType` ;
  - `Dim_Phase` ;
  - `Dim_Country` ;
  - `Dim_Region` ;
  - `Dim_Date`.

Relations recommandees :

- `Fact_ProjectPhasePerformance[Project_ID]` vers `Dim_Project[Project_ID]` ;
- `Fact_ProjectPhasePerformance[Phase]` vers `Dim_Phase[Phase]` ;
- `Dim_Project[Country]` vers `Dim_Country[Country]` ;
- `Dim_Country[Region]` vers `Dim_Region[Region]` ;
- `Fact_ProjectPhasePerformance[Start Date]` vers `Dim_Date[Date]`.

Approche alternative plus simple pour le projet :

- conserver une table centrale deja mergee dans Power Query ;
- garder quelques dimensions de filtrage : projet, pays, region, phase, date.

Pour OpenClassrooms, le modele simple mais propre est souvent plus efficace : il faut pouvoir expliquer clairement les relations, les transformations et les mesures.

## 7. Mesures DAX prioritaires

Mesures de base :

```DAX
Nb Projets = DISTINCTCOUNT(Fact_ProjectPhasePerformance[Project_ID])
Nb Phases = COUNTROWS(Fact_ProjectPhasePerformance)

Cout Prevu = SUM(Fact_ProjectPhasePerformance[Planned_Cost])
Cout Reel = SUM(Fact_ProjectPhasePerformance[Actual_Cost])
Ecart Cout = [Cout Reel] - [Cout Prevu]
Ecart Cout % = DIVIDE([Ecart Cout], [Cout Prevu])

Duree Prevue = SUM(Fact_ProjectPhasePerformance[Planned_Duration])
Duree Reelle = SUM(Fact_ProjectPhasePerformance[Actual_Duration])
Ecart Duree = [Duree Reelle] - [Duree Prevue]
Ecart Duree % = DIVIDE([Ecart Duree], [Duree Prevue])

Livrables Prevus = SUM(Fact_ProjectPhasePerformance[Planned_Deliverables])
Livrables Reels = SUM(Fact_ProjectPhasePerformance[Actual_Deliverables])
Ecart Livrables = [Livrables Reels] - [Livrables Prevus]
Ecart Livrables % = DIVIDE([Ecart Livrables], [Livrables Prevus])
```

Mesures d'alerte :

```DAX
Alerte Cout =
IF([Ecart Cout %] > 0.15, 1, 0)

Alerte Duree =
IF([Ecart Duree %] > 0.15, 1, 0)

Alerte Livrables =
IF([Ecart Livrables %] < -0.15, 1, 0)

Nb Alertes =
[Alerte Cout] + [Alerte Duree] + [Alerte Livrables]
```

Pour compter proprement les phases ou projets en alerte, il faudra privilegier des colonnes calculees d'alerte au niveau ligne dans Power Query ou DAX, puis des mesures `SUM` / `DISTINCTCOUNT` filtrees. Cela sera plus robuste que des mesures d'alerte calculees seulement au niveau agregat.

## 8. Pages Power BI recommandees

### Page 1 - Vue executive

Objectif : permettre au directeur general de comprendre en 30 secondes l'etat du portefeuille.

Visuels :

- cartes KPI : projets, phases, phases en alerte, cout reel vs prevu, livrables manquants ;
- jauges ou barres d'ecart pour couts, durees, livrables ;
- tendance temporelle des alertes par date de debut ;
- top 5 regions/pays a risque ;
- slicers : type projet, region, pays, phase, date.

### Page 2 - Performance par projet

Objectif : identifier les projets ou phases responsables des ecarts.

Visuels :

- matrice projet x indicateurs ;
- bar chart des projets les plus en alerte ;
- decomposition tree par type > region > pays > phase ;
- drill-through vers fiche projet ;
- infobulle detaillee avec couts, durees, livrables.

### Page 3 - Carte mondiale

Objectif : repondre a l'attendu explicite de Sanitoral.

Visuels :

- carte du monde coloree par taux d'alerte ou retard moyen ;
- table detail pays ;
- segmentation par region ;
- infobulle pays : nb projets, nb alertes, ecart cout %, ecart duree %, ecart livrables %.

Point de vigilance : les noms de pays francais peuvent etre mal geocodes par Power BI. Une table de geolocalisation pourra etre ajoutee si necessaire.

### Page 4 - Diagnostic phases

Objectif : transformer le reporting en decision strategique.

Visuels :

- heatmap phase x type projet sur le nombre d'alertes ;
- waterfall ou barres d'ecart cout par phase ;
- comparaison IT vs Marketing ;
- focus sur la phase D - Testing ;
- recommandation strategique affichee dans un encart.

### Page 5 - Documentation et mise a jour

Objectif : repondre au mail de Sophie.

Contenus :

- Product Strategy Canvas resume ;
- procedure de mise a jour hebdomadaire ;
- liste des transformations Power Query ;
- schema du modele de donnees ;
- definitions des indicateurs ;
- regle d'alerte a 15 %.

## 9. Product Strategy Canvas - structure recommandee

Nom du dashboard :

> Sanitoral - Suivi de performance des projets IT et Marketing

Objectif :

> Donner aux directeurs une vision fiable, visuelle et actionnable de l'avancement des projets, afin d'identifier les ecarts de couts, de delais et de livrables et de prioriser les actions correctives.

User stories :

| Utilisateur | User stories recommandees |
|---|---|
| Directeur general | En tant que DG, je veux suivre la performance globale du portefeuille afin de decider de poursuivre, renforcer ou arreter certains projets. |
| Directeur general | En tant que DG, je veux voir le nombre de projets en alerte afin de prioriser les arbitrages. |
| Directeur general | En tant que DG, je veux comparer IT et Marketing afin d'identifier les familles de projets les plus risquees. |
| Directeur regional | En tant que directeur regional, je veux filtrer les projets de ma region afin d'identifier les pays necessitant une intervention. |
| Directeur regional | En tant que directeur regional, je veux recevoir une lecture visuelle des alertes par pays afin de contacter les directeurs pays concernes. |
| Directeur regional | En tant que directeur regional, je veux analyser les phases les plus problematiques afin de coordonner les plans d'action. |
| Directeur pays | En tant que directeur pays, je veux visualiser les projets de mon pays afin de prendre des mesures correctives. |
| Directeur pays | En tant que directeur pays, je veux comprendre les ecarts par indicateur afin d'agir sur les couts, les delais ou les livrables. |
| Directeur pays | En tant que directeur pays, je veux consulter le detail des phases en alerte afin de prioriser les actions terrain. |

## 10. Strategie GitHub et organisation projet

GitHub est pertinent pour professionnaliser le projet, meme si Power BI reste un outil desktop.

Structure conseillee :

```text
sanitoral-powerbi-dashboard/
  README.md
  data/
    raw/
    dictionary/
  docs/
    cadrage/
    product_strategy_canvas/
    soutenance/
  powerbi/
    Sanitoral_Dashboard.pbix
    Sanitoral_Dashboard.pbit
  powerquery/
    transformations.md
    queries/
  dax/
    measures.md
  theme/
    sanitoral-theme.json
  mockups/
  exports/
    pdf/
    images/
```

Bonnes pratiques :

- versionner le `.pbit` si possible, plus leger et plus reutilisable que le `.pbix` ;
- versionner les mesures DAX dans un fichier Markdown ;
- documenter les etapes Power Query ;
- eviter de publier des donnees sensibles si le depot devient public ;
- creer un README clair avec contexte, objectifs, modele, pages du rapport et procedure de mise a jour.

## 11. Extension web/application possible

Comme tu as deja des competences web/application, on peut pousser le projet au-dela du strict Power BI sans sortir du cadre :

Options pertinentes :

1. Mockup web du dashboard avant Power BI
   - Realiser une maquette HTML/CSS ou Figma-like pour valider la structure visuelle.
   - Utile pour montrer une demarche UX et produit.

2. Mini-site de documentation projet
   - Page web statique avec contexte, PSC, modele de donnees, captures du dashboard et recommandations.
   - Utile pour portfolio et soutenance.

3. Export Power BI embarque
   - Theoriquement possible via Power BI Service, mais probablement hors scope OpenClassrooms si compte/licence non disponible.

4. Script de controle qualite des donnees
   - Script Python optionnel qui verifie les volumes, cles, doublons, valeurs manquantes.
   - Ne remplace pas Power Query, mais montre une rigueur data analyst.

5. Theme Power BI personnalise
   - Fichier JSON avec palette, typographies et couleurs d'alerte.
   - Ameliore le rendu professionnel.

Recommandation : faire simple et solide pour le livrable principal, puis ajouter GitHub + README + theme + documentation. Un mini-site peut etre garde pour le portfolio, pas comme livrable central.

## 12. Plan de travail recommande

### Phase 1 - Cadrage

- relire note de cadrage et scenario ;
- completer le Product Strategy Canvas ;
- definir les pages du rapport ;
- faire un mockup rapide ;
- valider avec mentor avant construction.

### Phase 2 - Preparation data

- importer les feuilles Excel dans Power BI ;
- supprimer les lignes inutiles ;
- promouvoir les en-tetes ;
- renommer les colonnes ;
- typer les champs ;
- creer la cle projet-phase ;
- fusionner ou relier les tables ;
- creer les colonnes d'ecart et d'alerte ;
- documenter les etapes appliquees.

### Phase 3 - Modele et mesures

- construire les relations ;
- ajouter une table calendrier ;
- creer les mesures DAX ;
- verifier les totaux ;
- tester les filtres par region, pays, type et phase.

### Phase 4 - Design du rapport

- appliquer un theme propre ;
- construire les pages ;
- ajouter slicers, infobulles, drill-through ;
- ajouter carte mondiale ;
- ajouter diagnostic strategic phase D ;
- controler lisibilite et accessibilite.

### Phase 5 - Documentation et soutenance

- creer la page documentation dans Power BI ;
- exporter des captures ;
- preparer le discours de presentation ;
- preparer les reponses aux questions du jury ;
- finaliser GitHub/README si besoin.

## 13. Priorites immediates

1. Completer le Product Strategy Canvas.
2. Valider la structure des pages du dashboard.
3. Definir le modele de donnees cible.
4. Preparparer les transformations Power Query.
5. Creer une liste de mesures DAX.
6. Construire le dashboard Power BI.
7. Rediger la procedure de mise a jour.
8. Preparer l'axe strategique : risque IT, phase D - Testing.

## 14. Decision recommandee

Pour maximiser la note et eviter de partir trop large :

- livrable principal : Power BI propre, clair, interactif, avec une vraie histoire ;
- documentation : integree dans Power BI + README projet ;
- GitHub : oui, pour versionner la demarche, les mesures, le theme et les exports ;
- web/app : oui en bonus portfolio, pas comme dependance du projet ;
- analyse strategique : focus IT et phase D - Testing, car les chiffres sont tres parlants.

