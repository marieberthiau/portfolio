---
title: "Trafic cycliste à Paris de septembre 2024 à octobre 2025"
author: "Marie Berthiau"
date: "Novembre 2024"
description: "Rapport final individuel de projet dans le cadre de la formation Data Analyst de DataScientest"
subject: "Analyse de données"
keywords: ["data analysis", "cyclisme", "Paris", "trafic"]
lang: "fr"
toc: true
toc-title: "Sommaire"
toc-depth: 4
markdown.styles: ["style.css"]
markdown-pdf.styles: ["style.css"]
pdf_options:
  format: A4
  margin: 20mm
  printBackground: true
---

<center><img src=".\images\pont_concorde.jpg" style="height:200px"></center>

# Trafic cycliste à Paris de septembre 2024 à octobre 2025

- [Trafic cycliste à Paris de septembre 2024 à octobre 2025](#trafic-cycliste-à-paris-de-septembre-2024-à-octobre-2025)
  - [Étape 1 : Découverte des données et du projet](#étape-1--découverte-des-données-et-du-projet)
    - [A. Objectifs du projet et enjeux](#a-objectifs-du-projet-et-enjeux)
    - [B. Structure du projet et organisation du groupe](#b-structure-du-projet-et-organisation-du-groupe)
    - [C. Mise en contexte](#c-mise-en-contexte)
      - [C.1. Contexte politique](#c1-contexte-politique)
      - [C.2. Contexte technique](#c2-contexte-technique)
    - [D. Découverte du jeu de données](#d-découverte-du-jeu-de-données)
      - [D.1 Biais et difficultés potentielles *a priori*](#d1-biais-et-difficultés-potentielles-a-priori)
      - [C.2 Exploration du jeu sur l'OpenData de la ville de Paris.](#c2-exploration-du-jeu-sur-lopendata-de-la-ville-de-paris)
  - [Étape 2 : Pré-processing mis en place et création du rapport](#étape-2--pré-processing-mis-en-place-et-création-du-rapport)
    - [A. Préprocessing dans Python](#a-préprocessing-dans-python)
    - [B. Préprocessing dans Power Query](#b-préprocessing-dans-power-query)
    - [C. Préprocessing dans Power BI](#c-préprocessing-dans-power-bi)
    - [D. Visualisations dans Power BI](#d-visualisations-dans-power-bi)
  - [Étape 3 : Analyse des données](#étape-3--analyse-des-données)
  - [Conclusion](#conclusion)
    - [Bilan](#bilan)
    - [Perspectives : ce que nous aurions pu faire si nous en avions eu le temps.](#perspectives--ce-que-nous-aurions-pu-faire-si-nous-en-avions-eu-le-temps)
    - [Les difficultés que nous avons rencontrées :](#les-difficultés-que-nous-avons-rencontrées-)
  - [Bibliographie](#bibliographie)
    - [1. Plans vélo et qualité de l'air](#1-plans-vélo-et-qualité-de-lair)
    - [2. Déplacements à Paris](#2-déplacements-à-paris)
    - [3. Qualité des aménagements cyclables (Guides officiels )](#3-qualité-des-aménagements-cyclables-guides-officiels-)
    - [4. Paris en Selle ](#4-paris-en-selle-)
    - [5. Compréhension des fonctionnement des capteurs et des méthodes de suivi du trafic](#5-compréhension-des-fonctionnement-des-capteurs-et-des-méthodes-de-suivi-du-trafic)
    - [6. Documentation technique complémentaire](#6-documentation-technique-complémentaire)
  - [Annexes - extrait de code](#annexes---extrait-de-code)
    - [Annexe 1 : 🗂️ Structure du projet](#annexe-1--️-structure-du-projet)
    - [Annexe 2 : Script "normalisation et lemmatisation des avis"](#annexe-2--script-normalisation-et-lemmatisation-des-avis)
    - [Annexe 3 : Script "nuage de mot" dans Power BI](#annexe-3--script-nuage-de-mot-dans-power-bi)
    - [Annexe 4 : Transformation des noms de compteurs et sites de comptage](#annexe-4--transformation-des-noms-de-compteurs-et-sites-de-comptage)
    - [Annexe 5 : Colonnes calculées de score météo](#annexe-5--colonnes-calculées-de-score-météo)
    - [Annexe 6 : Mesure DAX de calcul des sensibilités météo](#annexe-6--mesure-dax-de-calcul-des-sensibilités-météo)
    - [Annexe 7 : Mesure DAX de calcul des jours dépassant un seuil journalier](#annexe-7--mesure-dax-de-calcul-des-jours-dépassant-un-seuil-journalier)

<hr class="page-break">

## Étape 1 : Découverte des données et du projet

### A. Objectifs du projet et enjeux

La fiche projet mentionne explicitement les attendus suivants :

* **livrable :** doit permettre de visualiser les *horaires* et les *zones d'affluences*;

* **public concerné :** Mairie de Paris (public de décideur jugeant des décisions d'améliorations à apporter sur les aménagements).

### B. Structure du projet et organisation du groupe

Le projet est stocké sur un [dépôt GitHub privé de Marie](https://github.com/marieberthiau/trafic_cycliste_a_Paris), les autres membres de l'équipe y étant collaborateurs.
Chaque membre du projet travaille localement avec **VS Code**, sur une branche <u>distincte</u> et des fusions sont faites ponctuellement après demande de tirage.
L'architecture générale du projet est détaillée en <a href="#ann1">Annexe 1</a>.

### C. Mise en contexte

#### C.1. Contexte politique

Le [Plan National Vélo et Marche 2023-2027](https://www.ecologie.gouv.fr/politiques-publiques/velo-marche-modes-deplacement-vertueux-avantageux) prévoit le financement d’infrastructures cyclables.

La Ville de Paris, comme de nombreuses autre ville, déploie depuis plusieurs années des compteurs à vélo permanents pour évaluer le développement de la pratique cycliste.
En particulier, l'équipe municipale actuelle à déployé un [Plan vélo 2021-2026](https://www.paris.fr/pages/un-nouveau-plan-velo-pour-une-ville-100-cyclable-19554) qui met en avant :
* le recensement des “points noirs”;
* la sécurisation des carrefours, le jalonnement et le nettoiement des aménagements cyclables.

Ceci correspond à un objectif de favoriser la transition vers des mobilités douces et/ou actives.<br><br>

La mise en place de ces compteurs a donc généralement pour objectif :
* de promouvoir la mobilité durable en suivant la progression du vélo dans les trajets urbains;
* d'identifier les axes de transits principaux afin de hierarchiser un réseau cyclable en développement en fonction des débits <b>souhaités</b> (postulat de trafic induit : l'aménagement va être le déclencheur de l'augmentation du trafic, <a href="#bib101" class="ref">[1a]</a>. Ce n'est pas l'augmentation de trafic qui doit être le déclencheur de l'aménagement d'une voirie.)
* de mesurer l'efficacité des aménagements mis en place (effet avant/après) ainsi que de faciliter l'estimation de la part modale du vélo à Paris.<br>
Si cette part modale a en effet connu un doublement entre 2015 et entre 2020, elle tourne aujourd’hui autour de 10% <a href="#bib201" class="ref">[2a]</a>, ce qui reste relativement faible par rapport à d'autres capitales européenne. L'objectif est donc d'augmenter cette part et un flux faible dans une rue sur laquelle un compteur est installé sera donc un flux sur lequel on recherche une tendance haussière à moyen-long terme.<br>

<div style="display: flex; align-items: center;">
<p style="margin-right: 10px;">
    <div>
    Il est intéressant de noter que la ville de Paris a mis en place un suivi d'indicateur sur la base de ces relevés de compteurs qui est publié annuellement <a href="#bib202" class="ref">[2b]</a>.
    Nous pouvons ainsi consulter le bilan 2024 des déplacements à vélo à Paris et remarquer par exemple que le premier indicateur est basé sur l'identification des sites de comptage dépassant les 3000 cyclistes / jour ouvré.<br>
    Nous reviendrons [plus tard](#c-préprocessing-dans-power-bi) sur ce seuil issu des recommandations du Cerema (Centre d'études et d'expertise sur les risques, l'environnement, la mobilité et l'aménagement), établissement public relevant du ministère de la Transition écologique et de la Cohésion des territoires.
    </div>
</p>
<figure>
    <img src="images/debit_souhaité_et_aménagements.png" alt="débit cycliste souhaité et type d'aménagement" style ="max-width: 200px; max-height: 200px;">
    <figcaption>
      Figure 1 — Recommandations du Cerema
    </figcaption>
</figure>
</div>

#### C.2. Contexte technique

[EcoCompteur](https://www.eco-compteur.com/expertise/?gclid=EAIaIQobChMI1e_cneec6QIV1PhRCh0XbQAyEAAYASAAEgL9gvD_BwE) qui gère les compteurs vélo met à disposition les données à la Ville de Paris via une API basée sur REST et utilisant JSON.
EcoCompteur est également partenaire d'autres agglomérations (Lyon, Toulouse, Rennes, Tours, Saint-Nazaire...), le type d'analyse que nous allons réaliser devrait théoriquement pouvoir être transposés à ces localités... sous réserve de prise en compte des retraitements.

Il faut noter que le jeu de données ne concerne que les compteurs de type "permanents", à l'exclusion des compteurs de "caméras thermique".<br>
La technologie <a href="#bib501" class="ref">[5a]</a> utilisée est majoritairement celle du magnétomètre noyé dans le revêtement de la bande ou piste cyclable (détection de la signature magnétique des roues de vélo). Les compteurs mis en place à Paris sont en mesure de distinguer les véhicules motorisés et les trotinettes des vélos <a href="#bib502" class="ref">[5b]</a>.
Cela signifie qu'un vélo est décompté lorsqu'il passe sur le compteur... mais pas à côté (en cas de circulation déviée ou de véhicule stationné sur l'aménagement par exemple).

La Ville de Paris charge quotidiennement le jeu de donnée sur la base de cette API et effectue des retraitements pour au moins 2 raisons :

 - palier au fait que l'API Eco Compteur ne fournit pas nativement le comptage par sens de circulation,
 - effectuer une jointure avec un autre jeu de donnée, correspondant à la description des compteurs, leurs localisations et dates d'installation.

Il faut noter que  ce jeu conserve uniquement les données sur 13 mois glissants à J-1 mais qu'elle met également à jour des jeux de données sur d'autres plages temporelles (par exemple depuis 2019).

### D. Découverte du jeu de données

#### D.1 Biais et difficultés potentielles *a priori*

La fiche descriptive du jeu de donnée mentionne les informations suivantes :

* **Un** site de comptage peut être équipé d'**un** compteur dans le cas d'un aménagement cyclable *unidirectionnel* ou de **deux** compteurs dans le cas d'un aménagement cyclable *bi-directionnel*.

* **Le nombre de compteurs évolue** au fur et à mesure des aménagements cyclables:

 - Certains compteurs peuvent être désactivés pour travaux ou même définitivement... nous verrons [plus tard](#b-préprocessing-dans-power-query) que nous avons du effectuer des retraitements pour cette raison ;
 - ou subir ponctuellement une panne;
 - ou tout simplement avoir une date d'installation au cours de la période.

* Les compteurs sont situés sur des aménagements soient mixtes (couloirs bus-vélo) soient dédiés aux cyclistes (bandes et/ou pistes cyclables).
 **L'hypothèse est faite que l'algorithme de traitement des données réalisé par les compteurs retire correctement les autres véhicules** qui pourraient emprunter ces voies, qu'ils y soient autorisés (trotinettes) ou non (deux-roues motorisés).

* Le jeu de donnée étant **mis à jour quotidiennement**, il n'est pas figé.
Pour l'exploration ce n'est pas grave.
 Dans le contexte de notre projet, nous n'avons pas le temps de rendre le rapport dynamique sur la base du dernier jeu publié, nous avons donc choisi de figer la période d'analyse, du 1er septembre 2024 au 30 septembre 2025. Le choix de cette période nous permet en effet de :
  - travailler sur des mois complets;
  - ne pas être pénalisé par les anomalies de l'été 2024 liées aux restrictions de circulation dans Paris pendant les JO et qui ont fortement impactés les déplacements à vélo dans Paris<a href="#bib202" class="ref">[2b]</a>.

#### C.2 Exploration du jeu sur l'OpenData de la ville de Paris.

Le jeu de données est disponible sur l'OpenData de la Ville de Paris [ici](https://opendata.paris.fr/explore/dataset/comptage-velo-donnees-compteurs/information/?disjunctive.id_compteur&disjunctive.nom_compteur&disjunctive.id&disjunctive.name).

Il est possible de naviguer dans les données directement sur le site et ainsi de se faire une première idée des éléments.<br>
La donnée principale étant une notion de comptage, on peut en première approche regarder si des variations temporelles sont à prévoir.

<div style="display: table; width: 100%; margin-bottom: 1em;">
  <div style="display: table-cell; width: 45%; vertical-align: top;">
    <figure style="margin:0;">
        <img src="images/saison.png" alt="Trafic median mensuel entre le 01/09/2024 et 30/09/2025" style="width:100%;">
        <figcaption>
         Figure 2 — Effet des saisons sur le trafic median mensuel
        </figcaption>
    </figure>
    </div>
    <div style="display: table-cell; width: 55%; padding-left: 12px; vertical-align: top;">
        Il semble y avoir un effet des <b>saisons</b> avec :
        <ul>
            <li> un creux l'hiver : effet du froid ou des fêtes de fin d'années ?
            <li> des pics au printemps et à l'automne;
            <li> et une légère diminution en août : effet vacances ou chaleur ?
        </ul>
    </div>
</div>

<div style="display: table; width: 100%; margin-top: -40px; margin-bottom: 1em;">
  <div style="display: table-cell; width: 55%; vertical-align: top; padding-right: 12px;">
    Il semble aussi y avoir un effet du <b>jour de la semaine</b> (ou du caractère ouvré ou non de ce jour).<br>
    On voit par exemple ci-contre sur le Pont de la Concorde un effet qui semble correspondre aux week-ends.
  </div>
  <div style="display: table-cell; width: 45%; vertical-align: top;">
    <figure style="margin:0;">
        <img src="images/wejf.png" alt="Flux journalier total sur le Pont de la Concord du 01/09/2024 au 30/09/2025" style="width:100%;">
        <figcaption>
         Figure 3 — Effet des jours ouvrés sur le trafic journalier
        </figcaption>
    </figure>
   </div>
</div>

Un des objectif donné est également d'analyser les <b>périodes et horaires</b> d'affluence.
 Ainsi on observe en semaine (ci-dessous le mardi 17 septembre 2025) un pic autour de 8h le matin et un autre autour de 18h.<br>
 *A contrario*, les week-ends (ici les samedi 20 et dimanche 21 septembre 2025), le trafic tend à former une cloche centrée sur la fin d'après-midi.<br>
 On remarque au passage que le cycliste est relativement noctambule et que les déplacements se poursuivent toute la nuit (avec un pic à la fermeture des bars).

<div style="text-align:center; margin: 20px 0;">
  
  <figure style="display:inline-block; width:40%; margin:0 1%;">
    <img src="images/horaire.png" alt="trafic cycliste moyen le mardi 17 septembre 2025 à Paris" style="width:100%; display:block;">
    <figcaption style="font-size:0.66em; margin-top:6px;">
      Figure 4 — Pics d'affluence un jour ouvré
    </figcaption>
  </figure>

  <figure style="display:inline-block; width:50%; margin:0 1%;">
    <img src="images/horaire_we.png" alt="trafic cycliste moyen les samedi 20 et dimanche 21 septembre 2025 à Paris" style="width:100%; display:block;">
    <figcaption style="font-size:0.66em; margin-top:6px;">
      Figure 5 — Pics d'affluence les week-ends
    </figcaption>
  </figure>

</div>

Compte-tenu de notre objectif d'analyser également les **zones** d'affluence, il pourra être intéressant de comparer les compteurs entre-eux :

* les compteurs **sur-performant** pouvant être interprétés comme :
  - des zones où les aménagements fonctionnent pour favoriser la transition modale 
 => pas forcément d'action à prévoir pour la Mairie de Paris si ce n'est prendre ces compteurs en exemple
  - des zones où les aménagements saturent et sont peut-être sous-dimensionnés
 => cela peut signifier le besoin de revoir un aménagement cyclable

* les compteurs **sous-performant** pouvant être interprétés comme situés dans des zones où des aménagements cyclables sont nécessaires pour encourager le développement du trafic cycliste.

On peut ainsi regarder les compteurs les plus performants et les moins performants et on pourra éventuellement croiser les zones ainsi identifiées avec un autre jeu de données, celui des [résultats du Baromètre Parlons Vélo 2025](https://opendata.parlons-velo.fr/) paru le 1er octobre 2025 qui identfie notamment la position GPS des points à améliorer en priorité selon les cyclistes interrogés au printemps 2025 (données explorables en direct [ici](https://www.barometre-velo.fr/2025/carte/#12.27/48.85887/2.34703).)

<hr class="page-break">

## Étape 2 : Pré-processing mis en place et création du rapport

### A. Préprocessing dans Python

<a href="#ann2">Annexe 2</a>

<a href="#ann3">Annexe 3</a>

<a href="#bib601" class="ref">[6a]</a>

### B. Préprocessing dans Power Query

<a href="#ann4">Annexe 4</a>

<a href="#ann5">Annexe 5</a>

### C. Préprocessing dans Power BI

<a href="#ann6">Annexe 6</a>

<a href="#ann7">Annexe 7</a>

### D. Visualisations dans Power BI

<a href="#bib602" class="ref">[6b]</a>

<hr class="page-break">

## Étape 3 : Analyse des données

<hr class="page-break">

## Conclusion

### Bilan

### Perspectives : ce que nous aurions pu faire si nous en avions eu le temps.

1. **Enrichir le jeu de données avec celui des aménagements cyclables.**
   > Ceci nous aurait permis d'analyser séparément les compteurs sur bande cyclables de ceux sur pistes cyclables par exemple ou de prendre en compte pour ces dernières la largeur de l'aménagement afin de préciser les risques de saturation.
   > Un tel jeu existe et est disponible [ici](https://www.openstreetmap.org/search?query=Paris&zoom=5&minlon=-34.40917968750001&minlat=38.03078569382294&maxlon=34.23339843750001&maxlat=61.897577621605016#map=13/48.85890/2.33116&layers=C) grace au travail des contributeurs d'OpenStreeMap.
   > La Ville de Paris ne produit pas sa propre carte mais retraite cette carte collaborative en qualifiant la qualité de la donnée et en la mettant à disposition sur son propre OpenData  [ici](https://opendata.paris.fr/explore/dataset/amenagements-cyclables/information/?disjunctive.arrondissement&disjunctive.position_amenagement&disjunctive.vitesse_maximale_autorisee&disjunctive.source&disjunctive.amenagement).
   > Mais son traitement pour intégration dans le jeu de donnée nous aurait pris trop de temps et nous nous sommes donc contenté d'une analyse visuelle de l'aménagement au travers de la photo du site.

2. **Identifier l’ordre d’importance des facteurs responsables des variations de flux :**
   > Que ces variations soient horaires (effet de journée de travail), hebdomadaires (semaine de travail vs weekend), saisonnières (effet des vacances d'étét ou des fêtes de fin d'années) ou météorogoliques, nous avons en effet pu voir que de nombreux éléments étaient à l'origine des variations.
   > Si nous avions eu le temps d'aborder les cours de machine learning un peu plus tôt.
   > Ainsi, nous aurions par exemple pu utiliser un arbre de régression pour ajuster notre calcul de scoring météo, qui est actuellement basé avant tout sur une approche "mon vécu de cycliste" que sur une démarche statistique.
   > Nous aurions par ailleurs pu tenter d'identifier l'ordre d'importance de ces facteurs pour affiner l'identification des sites nécessitant des modifications d'aménagements

3. **Rendre dynamique le rapport en le raccordant directement via API.**
   > Ceci nous aurait permis d'élargir la période de donnée utilisée plutôt que de se restreindre à 13 mois (donc d'avoir plusieurs étés, plusieurs vacances d'hiver...).
   > Le jeu étant actualisé quotidiennement avec de nombreux compteurs installés depuis plus de 6 ans, nous aurions ainsi pu étudier des tendances et les données supplémentaires nous auraient permis de commencer à faires des prédictions de trafic pour affiner l'identification des sites :
   > * pour lesquels un aménagement permettrait d'éviter une future saturation,
   > * ou pour lesquels un aménagement favoriserait le développement de la part modale cycliste.

4. **Enrichir le jeu de données avec les jeux de données sur l'accidentologie.**
  > Le jeu ddit "fichier BAAC" (Base de données Annuelles des Accidents Corporels de la circulation routière de l'Observatoire National Interministériel de la Sécurité Routiers (ONISR) est librement accessible [ici](https://www.data.gouv.fr/datasets/bases-de-donnees-annuelles-des-accidents-corporels-de-la-circulation-routiere-annees-de-2005-a-2024), inclue une localisation des accidents et permetttrait d'améliorer l'identification et la quantification les zones dangereuses afin de prioriser les travaux sur ces zones.

### Les difficultés que nous avons rencontrées :

1. **Les contraintes du travail d'équipe en mode projet :**
> Nous avons découvert GitHub tous ensemble en collaborant sur un repository privé hébergé sur mon GitHub personnel. Le principe était d'avoir chacun sa branche pour travailler et de consolider nos avancées dans la branche *main*.
> Mais les débuts ont été compliqué et j'ai du à plusieurs reprises utiliser les fonctions de revert ou reset suite à des *merge* "à l'envers" de certains de mes collègues… l’absence de formation à l'utilisation d'un outil de versionning dans le cadre de la formation a été un réel manque même si nous avons pu nous appuyer sur ls modules Microsoft Learn.

2. **La compréhension des notions d’environnements python et de gestion de version des librairies Python :**
>Nous avons été confronté à des erreurs liés à ce type de problème car nous avions tous les 3 des versions différentes de Python (3.13.5 pour moi et Ghizlane sur oc, 3.14 pour Mohammed sur mac).
>J'ai également eu des conflits de versions de librairies Python et il aurait été judicieux de mettre en place un environnement partageable pour stabiliser notre travail, d'autant que sans Power BI Service, chaque utilisateur doit pour l'instant déclarer son propre environnement python pour faire fonctionner le rapport.
>Un module de formation sur les bonnes pratiques d’utilisation d’un EDI aurait été apprécié, ainsi que sur les modalités de création d'un environnement Python et son partage.

3. **L’analyse de texte en français :** 
> Il a fallu rechercher une bibliothèque python adaptée (celle vu en cours, wordnet étant plutôt anglophone) et qui puisse prendre en compte les formes complexes du français.
> La transformation du script testé sur l’ensemble du jeu en un script intégrable dans Power BI et fonctionnant avec des clusters d’avis de taille nettement plus réduite pour chaque compteur a ensuite nécessité des ajustements  pour ne pas avoir d’erreur lorsque le cluster était petit.
> D'autre part, le rendu de l'affichage du nuage de mot dans Power BI était légèrement différent application arbitraire de marge en haut et en base) que celui obtenu dans Python et j'ai donc du adapter ces paramètres.
> Enfin (et surtout), pour des raisons de performance (temps de chargement qui était trop long), j'ai également du mettre directement dans le script python la définition de la totalité du dictionnaire de mots vides à utiliser au lieu de charger dynamiquement les mots vides "classiques" et de me contenter d'y ajouter les mots spécifiques à mon contexte.

<hr class="page-break">

## Bibliographie

### 1. Plans vélo et qualité de l'air

<a id="bib101">[1a]-</a>[Mesures pour modifier le trafic routier en ville et qualité de l'air extérieur - Edition Ademe - 2021](https://librairie.ademe.fr/urbanisme-territoires-et-sols/4927-mesures-pour-modifier-le-trafic-routier-en-ville-et-qualite-de-l-air-exterieur.html)

### 2. Déplacements à Paris

<a id="bib201">[2a]-</a>[Bilan des déplacements à Paris en 2024 - page web Ville de Paris - oct 2025](https://www.paris.fr/pages/le-bilan-des-deplacement-a-paris-en-2024-31371)

<a id="bib202">[2b]-</a>[Les déplacements en vélo à Paris en 2024 - Edition Ville de Paris - 2025](https://cdn.paris.fr/paris/2025/06/02/paris_ra2024-deplacements-en-velo-8-pages-26-05-copie-3dZs.pdf)

### 3. Qualité des aménagements cyclables (Guides officiels )

<a id="bib301">[3a]-</a>[Annexe 3 : Note de recommendations techniques du CEREMA](https://www.ecologie.gouv.fr/sites/default/files/documents/Annexe%203%20%20Recommandations%20techniques%20du%20CEREMA.pdf)

<a id="bib302">[3b]-</a>[8 recommandation pou réussir votre piste cyclable - Actualités du Cerema - 24/02/2021](https://www.cerema.fr/fr/actualites/8-recommandations-reussir-votre-piste-cyclable) 

<a id="bib303">[3c]-</a>[Guide de conception des aménagements cyclables - Métropole de Lyon - 2019](https://www.grandlyon.com/fileadmin/user_upload/media/pdf/voirie/20190621_guide-amenagement-cyclable.pdf)

<a id="bib304">[3d]-</a>[Guide des aménagements cyclables - Direction de la Voirie des tdes Déplacements de la Ville de Paris - 16/06/2023](https://cdn.paris.fr/paris/2024/09/30/guide-amenagements-cyclables-partie-1-generalites-hors-dsc-juin-2024-light-CFZy.pdf)

### 4. Paris en Selle <img src=".\images\logo_pes.png" style="height:100px">

<a id="bib404">[4a]-</a>[Plateforme dédiée aux compteurs vélo](https://parisenselle.fr/2020/10/06/une-plateforme-pour-recenser-les-compteurs-velo/#:~:text=Nous%20sommes%20heureux%20de%20vous%20pr%C3%A9senter%20https%3A%2F%2Fcompteurs.parisenselle.fr%2C%20qui,grand%20merci%20%C3%A0%20Tristram%20pour%20ce%20gros%20boulot.)

Qualité des aménagements cyclables (nombreuses photos et exemples) pour la compréhension des sites de comptage :
<a id="bib405">[4b]-</a>[Guide des aménagements cyclables - Edition : Paris en Selle - mise à jour de 20121](https://parisenselle.fr/telecharger-guide-amenagements-cyclables/)

### 5. Compréhension des fonctionnement des capteurs et des méthodes de suivi du trafic

<a id="bib501">[5a]-</a>[Données de mobilité pour la modélisation des déplacements - fiche n°9 : données issues des capteurs routiers - Edition : Cerema - 2025](https://doc.cerema.fr/Default/doc/SYRACUSE/605087/donnees-de-mobilite-pour-la-modelisation-des-deplacements-fiche-n-9-donnees-issues-des-capteurs-rout)

<a id="bib502">[5b]-</a>[Technologies de comptage proposées pour les cyclistes par eco-compteur - page web - 2025]](https://www.eco-compteur.com/solutions/produits/)

<a id="bib503">[5c]-</a>[Etude de simulation dynamique de trafic : guide de réalisation - Edition : Cerema - 2015](https://doc.cerema.fr/Default/doc/SYRACUSE/14114/etudes-de-simulation-dynamique-de-trafic-guide-de-realisation) => perspectives (analyse dynamique des flux)

### 6. Documentation technique complémentaire

<a id="bib601">[6a]-</a>[Librairie SpaCy en français - page web - oct 2025](https://spacy.io/models/fr)

<a id="bib602">[6b]-</a>[Créer un script Python pour Power Bi - page Web Microsoft Learn - oct 2025](https://learn.microsoft.com/fr-fr/power-bi/connect-data/desktop-python-scripts)

<hr class="page-break">

## Annexes - extrait de code

### <a id="ann1">Annexe 1</a> : 🗂️ Structure du projet

```text
trafic_cycliste_paris/<br>
│<br>
├── data            → données brutes et nettoyées<br>
|    |── raw        → données brutes<br>
|    └── processed  → données retravaillées
|
├── models          → stockage éventuels des modélisations et calcul prédictif (non utilisé)
├── notebooks       → jupyter notebooks utilisés pour l'exploration et l'analyse
|    └── images     → stockage des éventuelles images d'illustration
|
├── reports         → stockage des projets de datavisualisation (PowerBI)
|    └── Modèle_trafic_cycliste.SemanticModel     → stockage du rapport Power BI et des fichiers associés
|
├── references      → metadatas de fichier sources et documents d'informations diverses
├── utilitaires     → module python de stockage des scripts python utilisées dans les notebooks notamment
└── README.md
```

<hr class="page-break">

### <a id="ann2">Annexe 2</a> : Script "normalisation et lemmatisation des avis"

<hr class="page-break">

### <a id="ann3">Annexe 3</a> : Script "nuage de mot" dans Power BI

````python

# The following code to create a dataframe and remove duplicated rows is always executed and acts as a preamble for your script: 

# dataset = pandas.DataFrame(commentaire, categorie, statut_proximite, Site de comptage)
# dataset = dataset.drop_duplicates()

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import nltk 
from nltk.corpus import stopwords

# pour éviter d'importer des données externes dans Power BI, on importe la liste stop_word directement dans le script
stop_words=['ces', 'qu', 'ayons', 's', 'vraiment', 'seras', 'ait', 'fûmes', 'eûmes', 'auront', 'lui', 'l', 'on', 'fus', 'le', 'serai', 'étant', 'son', 'et', 'sois', 'étaient', 'eue', 'cette', 'aurait', 'quand', 'qui', 'fusses', 'fut', 'ne', 'auraient', 'fût', 'aie', 'mes', 'eusses', 'eûtes', 'tes', 'aies', 'avait', 'fussiez', 'vers', 'était', 'eu', 'avoir', 'avec', 'que', 't', 'aurions', 'seront', 'soient', 'pour', 'n', 'avaient', 'même', 'étants', 'pas', 'c', 'il', 'sur', 'sera', 'au', 'étantes', 'serait', 'fusse', 'serais', 'ayante', 'étées', 'furent', 'rue', 'cycliste', 'soyez', 'fûtes', 'd', 'auras', 'a', 'sont', 'étais', 'eût', 'du', 'me', 'être', 'avez', 'mais', 'aura', 'leur', 'moi', 'été', 'se', 'ayant', 'une', 'vous', 'ayants', 'tu', 'étés', 'suis', 'bd', 'la', 'es', 'aient', 'des', 'ta', 'aux', 'auriez', 'aurais', 'boulevard', 'j', 'vélo', 'ai', 'fussions', 'en', 'nos', 'ses', 'seraient', 'ils', 'eux', 'm', 'ont', 'nous', 'sommes', 'ce', 'je', 'serez', 'te', 'fussent', 'étions', 'mon', 'à', 'avions', 'toi', 'eussent', 'seriez', 'ayantes', 'serons', "c'est", 'cyclable', 'votre', 'eues', 'aurai', 'eussiez', 'ou', 'notre', 'est', 'ayez', 'avenue', 'aurez', 'par', 'êtes', 'y', 'eus', 'de', 'sa', 'étiez', 'étante', 'avais', 'eut', 'aviez', 'route', 'elle', 'étée', 'un', 'ton', 'les', 'vos', 'eurent', 'eusse', 'eussions', 'as', 'dans', 'aurons', 'avons', 'soyons', 'serions', 'soit', 'ma','piste']

corpus=dataset.loc[dataset.statut_proximite == "retenu","commentaire"].astype(str).tolist()

from sklearn.feature_extraction.text import TfidfVectorizer # pour application d'un algorithme TF_IDF

def creer_tfidf_dict(corpus):
    """
    Calcule les poids TF-IDF pour un corpus (liste de textes) et renvoie un dictionnaire {mot: score}.
    Prêt à être utilisé avec WordCloud.generate_from_frequencies().

    corpus : list[str]  Liste de commentaires (déjà nettoyés / lemmatisés / sans accent).
    """
    corpus_clean = [
        " ".join([mot for mot in texte.split() if mot.lower() not in stop_words])
        for texte in corpus
        if isinstance(texte, str) and texte.strip()
    ]
    if not corpus_clean:
        return {}  # sécurité : évite les erreurs sur corpus vide
    
    # Adapter min_df et max_df dans les cas de petits corpus
    n_docs = len(corpus_clean)
    min_df_value = 2 if n_docs >= 2 else 1  # si moins de 2 documents, mettre min_df=1
    max_df_value = 0.9 if n_docs > 1 else 1.0

    vectorizer = TfidfVectorizer(
        max_df=max_df_value,             # ignore les mots trop fréquents
        min_df=min_df_value,    # ignore les mots trop rares... sauf si petit corpus
        norm='l2',              # normalisation standard
    )   
    
    tfidf_matrix = vectorizer.fit_transform(corpus_clean)
    tfidf_scores = np.asarray(tfidf_matrix.mean(axis=0)).ravel()  # on calcule le score moyen de chaque mot
    tfidf_dict = dict(zip(vectorizer.get_feature_names_out(), tfidf_scores))  # on récupère ce score dans un dictionnaire qui va nous servir pour le nuage
    return tfidf_dict

# Compter les occurrences de chaque catégorie
nb_rouge = dataset.loc[dataset.categorie == "rouge"].shape[0]
nb_vert = dataset.loc[dataset.categorie == "vert"].shape[0]

# Choisir la colormap selon la condition
colormap_choice = "inferno" if nb_rouge > nb_vert else "viridis"

from wordcloud import WordCloud  # pour les nuages de mots
tfidf_dict = creer_tfidf_dict(corpus)

plt.figure(figsize=(5,5))

if tfidf_dict:  # si le corpus contient des mots valides
    nuage = WordCloud(
        background_color="white",
        max_words=100,
        stopwords=stop_words,
        max_font_size=80,
        random_state=42,
        colormap=colormap_choice  # mettre inferno viridis sur du positif et inferno sur du négatif, les 2 sont accessibles
    ).generate_from_frequencies(tfidf_dict)
    
    plt.imshow(nuage, interpolation='bilinear')
else:  # corpus vide → affichage d'un message
    plt.text(
        0.5, 0.5,
        "Corpus de commentaire insuffisant\npour générer un nuage",
        fontsize=12,
        ha='center',
        va='center',
        wrap=True
    )    

# Récupérer le site unique correspondant au filtre
sites = dataset.loc[dataset.statut_proximite == "retenu", "Site de comptage"].unique()

# Si plusieurs sites sont retenus, on peut afficher "Plusieurs sites" ou concaténer
if len(sites) == 0:
    titre_site = "Aucun site"
elif len(sites) == 1:
    titre_site = sites[0]
else:
    titre_site = "Plusieurs sites"

plt.figure(figsize= (5,5)) 
plt.imshow(nuage, interpolation='bilinear')
plt.tight_layout(pad=0)  # supprime toute marge autour du graphique
plt.margins(0,0)         # pas d’espace autour du contenu
plt.subplots_adjust(left=0, right=1, top=0.95, bottom=0)
plt.title(titre_site, fontsize=14, fontweight='bold')
plt.axis("off")
plt.show()

````
<hr class="page-break">

### <a id="ann4">Annexe 4</a> : Transformation des noms de compteurs et sites de comptage

### <a id="ann5">Annexe 5</a> : Colonnes calculées de score météo

### <a id="ann6">Annexe 6</a> : Mesure DAX de calcul des sensibilités météo

### <a id="ann7">Annexe 7</a> : Mesure DAX de calcul des jours dépassant un seuil journalier
