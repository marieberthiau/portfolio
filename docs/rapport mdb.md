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

- [I. Découverte des données et du projet ](#i-découverte-des-données-et-du-projet-)
  - [I.A. Objectifs du projet et enjeux ](#ia-objectifs-du-projet-et-enjeux-)
  - [I.B. Structure du projet et organisation du groupe ](#ib-structure-du-projet-et-organisation-du-groupe-)
  - [I.C. Mise en contexte ](#ic-mise-en-contexte-)
    - [I.C.1. Contexte politique ](#ic1-contexte-politique-)
    - [I.C.2. Contexte technique ](#ic2-contexte-technique-)
    - [I.C.3. Intérêt personnel au projet ](#ic3-intérêt-personnel-au-projet-)
  - [I.D. Découverte du jeu de données ](#id-découverte-du-jeu-de-données-)
    - [I.D.1 Biais et difficultés potentielles *a priori* ](#id1-biais-et-difficultés-potentielles-a-priori-)
    - [I.D.2 Exploration du jeu sur l'OpenData de la ville de Paris. ](#id2-exploration-du-jeu-sur-lopendata-de-la-ville-de-paris-)
  - [I.E. Bilan de l'étape de découverte des données](#ie-bilan-de-létape-de-découverte-des-données)
- [II.A. Préprocessing du jeu principal avec Python ](#iia-préprocessing-du-jeu-principal-avec-python-)
  - [II.A.1. Exploration détaillée des jeux de données 'comptage \& compteurs' ](#iia1-exploration-détaillée-des-jeux-de-données-comptage--compteurs-)
  - [II.A.2. Préparation du jeu principal ](#iia2-préparation-du-jeu-principal-)
    - [II.A.2.a. Préparation du jeu principal](#iia2a-préparation-du-jeu-principal)
    - [II.A.2.c. Extraction du jeu de comptage](#iia2c-extraction-du-jeu-de-comptage)
    - [II.A.2.b. Extraction du jeu de compteur](#iia2b-extraction-du-jeu-de-compteur)
  - [II.A.3. Géolocalisation des compteurs](#iia3-géolocalisation-des-compteurs)
- [II.B. Exploration et Préprocessing des jeux d'enrichissement avec Python  ](#iib-exploration-et-préprocessing-des-jeux-denrichissement-avec-python--)
    - [II.B.1 Jeu de données météorologique ](#iib1-jeu-de-données-météorologique-)
    - [II.B.2. Jeu de données de l'enquête de la FUB ](#iib2-jeu-de-données-de-lenquête-de-la-fub-)
      - [II.B.2.a. Exploration des clusters du baromètre FUB ](#iib2a-exploration-des-clusters-du-baromètre-fub-)
      - [II.B.2.b. Bilan de l'exploration du baromètre FUB et préparation des points ](#iib2b-bilan-de-lexploration-du-baromètre-fub-et-préparation-des-points-)
    - [II.B.3. Préparation des avis pour l'analyse textuelle ](#iib3-préparation-des-avis-pour-lanalyse-textuelle-)
      - [II.B.3.a. Regroupemeent des données ](#iib3a-regroupemeent-des-données-)
      - [II.B.3.b. Normalisation et lemmatisation du texte en français ](#iib3b-normalisation-et-lemmatisation-du-texte-en-français-)
      - [II.B.3.c. Choix de l'algorithme le plus pertinent ](#iib3c-choix-de-lalgorithme-le-plus-pertinent-)
    - [II.B.4. Jointure géospatiale des avis ](#iib4-jointure-géospatiale-des-avis-)
    - [II.B.5. Fichiers obtenus à l'issu de cette étape ](#iib5-fichiers-obtenus-à-lissu-de-cette-étape-)
  - [II.B. Préprocessing dans Power Query ](#iib-préprocessing-dans-power-query-)
    - [II.B.1. Collecte des données ](#iib1-collecte-des-données-)
    - [II.B.2. Suppression des champs inutiles et convivialité des champs ](#iib2-suppression-des-champs-inutiles-et-convivialité-des-champs-)
    - [II.B.3. Amélioration des noms de compteurs et sites de comptage ](#iib3-amélioration-des-noms-de-compteurs-et-sites-de-comptage-)
    - [II.B.4. Création d'un score météo ](#iib4-création-dun-score-météo-)
  - [II.C. Préprocessing dans Power BI ](#iic-préprocessing-dans-power-bi-)
    - [II.C.1. Modélisation en étoile ](#iic1-modélisation-en-étoile-)
    - [II.C.2. Création des tables de date ](#iic2-création-des-tables-de-date-)
    - [II.C.3. Création des hiérarchies ](#iic3-création-des-hiérarchies-)
    - [II.C.4. Création des mesures de sensibilité à la météo ](#iic4-création-des-mesures-de-sensibilité-à-la-météo-)
    - [II.C.5. Création des mesures de saturation des aménagements ](#iic5-création-des-mesures-de-saturation-des-aménagements-)
  - [II.D. Visualisations dans Power BI ](#iid-visualisations-dans-power-bi-)
- [III. Analyse des données ](#iii-analyse-des-données-)
- [Conclusion](#conclusion)
  - [Bilan](#bilan)
  - [Perspectives :](#perspectives-)
  - [Les difficultés qu'il a fallu relever](#les-difficultés-quil-a-fallu-relever)
- [Bibliographie](#bibliographie)
  - [1. Plans vélo et qualité de l'air](#1-plans-vélo-et-qualité-de-lair)
  - [2. Déplacements à Paris](#2-déplacements-à-paris)
  - [3. Qualité des aménagements cyclables (Guides officiels )](#3-qualité-des-aménagements-cyclables-guides-officiels-)
  - [4. Paris en Selle ](#4-paris-en-selle-)
  - [5. Compréhension des fonctionnement des capteurs et des méthodes de suivi du trafic](#5-compréhension-des-fonctionnement-des-capteurs-et-des-méthodes-de-suivi-du-trafic)
  - [6. Documentation technique complémentaire](#6-documentation-technique-complémentaire)
- [Annexes - extrait de code](#annexes---extrait-de-code)
  - [Annexe 1 : 🗂️ Structure du projet](#annexe-1--️-structure-du-projet)
  - [Annexes 2 : Struture des jeux de donnéees initiaux](#annexes-2--struture-des-jeux-de-donnéees-initiaux)
    - [Annexe 2a : Structure du jeu de données initial brut](#annexe-2a--structure-du-jeu-de-données-initial-brut)
    - [Annexe 2b : Structure du jeu de données météo](#annexe-2b--structure-du-jeu-de-données-météo)
    - [Annexe 2c : Notice du jeu de données du baromètre FUB](#annexe-2c--notice-du-jeu-de-données-du-baromètre-fub)
  - [Annexe 3 : Script "normalisation et lemmatisation des avis"](#annexe-3--script-normalisation-et-lemmatisation-des-avis)
  - [Annexe 4 : Script "rayon de proximité" pour jointure géospatiale](#annexe-4--script-rayon-de-proximité-pour-jointure-géospatiale)
  - [Annexe 5 : Transformation des noms de compteurs et sites de comptage](#annexe-5--transformation-des-noms-de-compteurs-et-sites-de-comptage)
  - [Annexe 6 : Colonnes calculées de score météo](#annexe-6--colonnes-calculées-de-score-météo)
  - [Annexe 7 : Mesure DAX de calcul des sensibilités météo](#annexe-7--mesure-dax-de-calcul-des-sensibilités-météo)
  - [Annexe 8 : Mesure DAX de calcul des jours dépassant un seuil journalier](#annexe-8--mesure-dax-de-calcul-des-jours-dépassant-un-seuil-journalier)
  - [Annexe 9 : Script "nuage de mot" dans Power BI](#annexe-9--script-nuage-de-mot-dans-power-bi)

<hr class="page-break">

## I. Découverte des données et du projet <a id="I"></a>

### I.A. Objectifs du projet et enjeux <a id="IA"></a>

Le jeu de donnée sur lequel nous avons travaillé est celui des [comptages Vélo de la Ville de Paris](https://opendata.paris.fr/explore/dataset/comptage-velo-donnees-compteurs/information/?disjunctive.id_compteur&disjunctive.nom_compteur&disjunctive.id&disjunctive.name).
C'est un jeu relativement lourd de 1,44Go, mis à jour quotidiennement sur une période de 13 mois glissants.<br><br>

La fiche projet mentionne explicitement les attendus suivants :

* **livrable :** doit permettre de visualiser les *horaires* et les *zones d'affluences*;
* **public concerné :** Mairie de Paris (public de décideur jugeant des décisions d'améliorations à apporter sur les aménagements).

Notre objectif était donc de préaprer un rapport destiné aider ces décideurs à programmer les futurs aménagements cyclables.<br>
S'agissant d'un public de décideur, nous aurons pour objectif de limiter le nombre d'écran sur notre rapport et de données des clefs de priorisation des actions.

Le présent rapport à quant à lui pour objectif de vous présenter notre démarche et comment nous avons mis en place cette exploitation de données.<br>

### I.B. Structure du projet et organisation du groupe <a id="IB"></a>

Le projet est stocké sur un [dépôt GitHub privé de Marie](https://github.com/marieberthiau/trafic_cycliste_a_Paris), les autres membres de l'équipe y étant collaborateurs.
Chaque membre du projet travaille localement avec VS Code, sur une branche <u>distincte</u> et des fusions sont faites ponctuellement après demande de tirage.
L'architecture générale du projet est détaillée en <a href="#ann1">Annexe 1</a>.
Je reviendrai dans le bilan sur la découverte de Git qui a été en soi un <a href="#defi1">défi à relever</a>.

### I.C. Mise en contexte <a id="IC"></a>

#### I.C.1. Contexte politique <a id="IC1"></a>

Le [Plan National Vélo et Marche 2023-2027](https://www.ecologie.gouv.fr/politiques-publiques/velo-marche-modes-deplacement-vertueux-avantageux) prévoit le financement d’infrastructures cyclables.

La Ville de Paris, comme de nombreuses autre ville, déploie depuis plusieurs années des compteurs à vélo permanents pour évaluer le développement de la pratique cycliste.
En particulier, l'équipe municipale actuelle à déployé un [Plan vélo 2021-2026](https://www.paris.fr/pages/un-nouveau-plan-velo-pour-une-ville-100-cyclable-19554) qui met en avant :
* le recensement des “points noirs”;
* la sécurisation des carrefours, le jalonnement et le nettoiement des aménagements cyclables.

Ceci correspond à un objectif de favoriser la transition vers des mobilités douces et/ou actives.<br><br>

La mise en place de ces compteurs a donc généralement pour objectif :
* de promouvoir la mobilité durable en suivant la progression du vélo dans les trajets urbains;
* d'identifier les axes de transits principaux afin de hierarchiser un réseau cyclable en développement en fonction des débits <b>souhaités</b> (postulat de trafic induit : l'aménagement va être le déclencheur de l'augmentation du trafic<a href="#bib101" class="ref">[1a]</a>. Ce n'est pas l'augmentation de trafic qui doit être le déclencheur de l'aménagement d'une voirie.)
* de mesurer l'efficacité des aménagements mis en place (effet avant/après) ainsi que de faciliter l'estimation de la part modale du vélo à Paris.<br>

Si cette part modale a en effet connu un doublement entre 2015 et entre 2020, elle tourne aujourd’hui autour de 10% <a href="#bib201" class="ref">[2a]</a>, ce qui reste relativement faible par rapport à d'autres capitales européenne. L'objectif est donc d'augmenter cette part et un flux faible dans une rue sur laquelle un compteur est installé sera donc un flux sur lequel on recherche une tendance haussière à moyen-long terme.<br><br>

<div style="display: table; width: 100%;">
  <div style="display: table-cell; width: 65%; vertical-align: top; padding-right: 12px;">
      Il est intéressant de noter que la ville de Paris a mis en place un suivi d'indicateur sur la base de ces relevés de compteurs qui est publié annuellement <a href="#bib202" class="ref">[2b]</a>.
      Nous pouvons ainsi consulter le bilan 2024 des déplacements à vélo à Paris et remarquer par exemple que le premier indicateur est basé sur l'identification des sites de comptage dépassant les 3000 cyclistes / jour ouvré.<br>
      Nous reviendrons sur la prise en compte de ce seuil issu des recommandations du Cerema (Centre d'études et d'expertise sur les risques, l'environnement, la mobilité et l'aménagement, établissement public relevant du ministère de la Transition écologique et de la Cohésion des territoires) lors de la <a id="#IIC4">préparation de notre rapport Power Bi</a>.
  </div>
  <div style="display: table-cell; width: 30%; vertical-align: top;">
    <figure style="margin:0;">
        <img src="images/debit_souhaité_et_aménagements.png" alt="débit cycliste souhaité et type d'aménagement" style ="max-width: 200px; max-height: 200px;">
        <figcaption>
        Figure 1 — Recommandations du Cerema
        </figcaption>
    </figure>
   </div>
</div>

#### I.C.2. Contexte technique <a id="IC2"></a>

[EcoCompteur](https://www.eco-compteur.com/expertise/?gclid=EAIaIQobChMI1e_cneec6QIV1PhRCh0XbQAyEAAYASAAEgL9gvD_BwE) qui gère les compteurs vélo met à disposition les données à la Ville de Paris via une API basée sur REST et utilisant JSON.
EcoCompteur est également partenaire d'autres agglomérations (Lyon, Toulouse, Rennes, Tours, Saint-Nazaire...), le type d'analyse que nous allons réaliser devrait théoriquement pouvoir être transposés à ces localités... sous réserve de prise en compte des retraitements.

Il faut noter que le jeu de données ne concerne que les compteurs de type "permanents", à l'exclusion des compteurs de "caméras thermique".<br>
La technologie <a href="#bib501" class="ref">[5a]</a> utilisée est majoritairement celle du magnétomètre noyé dans le revêtement de la bande ou piste cyclable (détection de la signature magnétique des roues de vélo). Les compteurs mis en place à Paris sont en mesure de distinguer les véhicules motorisés et les trotinettes des vélos <a href="#bib502" class="ref">[5b]</a>.
Cela signifie qu'un vélo est décompté lorsqu'il passe sur le compteur... mais pas à côté (en cas de circulation déviée ou de véhicule stationné sur l'aménagement par exemple).

La Ville de Paris charge quotidiennement le jeu de donnée sur la base de cette API et effectue des retraitements pour au moins 2 raisons :

 - palier au fait que l'API Eco Compteur ne fournit pas nativement le comptage par sens de circulation,
 - effectuer une jointure avec un autre jeu de donnée, correspondant à la description des compteurs, leurs localisations et dates d'installation.

Il faut noter que  ce jeu conserve uniquement les données sur 13 mois glissants à J-1 mais qu'elle met également à jour des jeux de données sur d'autres plages temporelles (par exemple depuis 2019).

#### I.C.3. Intérêt personnel au projet <a id="IC3"></a>

D'un point de vue individuel, le sujet m'intéressait particulièrement.<br>

Je fais en effet partie d'une association de promotion du vélo (La Ville à Vélo Lyon Métropole) membre de la FUB et soeur de l'association Paris en Selle. Nos associations interviennent régulièrement auprès des décideurs pour favoriser la transition modale et l'usage du vélo en ville en analysant d'un point de vue de l'usager les aménagements, en proposant des idées à l'origine d'évolution (Vélopolitain à Paris ou Voies Lyonnaises à Lyon par exemple) et en participant aux concertations et études publiques.<br>

Comme Paris, la métropole de Lyon dispose de compteurs Eco-Compteur et mon association a mis en place un site de suivi en temps quasi réel de ces compteurs, tout comme peut d'ailleurs le faire Paris en Selle.

J'ai donc convaincu mes collègues de ne pas refaire ce qui était déjà très bien fait par Paris en Selle <a href="#bib402" class="ref">[4b]</a>et donc de ne pas "cloner" ces visualisations et de travailler sur une approche d'analyse allant au delà du simple "je constate une hausse à tel endroit" mais d'aider à analyser les besoins.

### I.D. Découverte du jeu de données <a id="ID"></a>

#### I.D.1 Biais et difficultés potentielles *a priori* <a id="ID1"></a>

La fiche descriptive du jeu de donnée mentionne les informations suivantes :

* **Un** site de comptage peut être équipé d'**un** compteur dans le cas d'un aménagement cyclable *unidirectionnel* ou de **deux** compteurs dans le cas d'un aménagement cyclable *bi-directionnel*.

* **Le nombre de compteurs évolue** au fur et à mesure des aménagements cyclables:

 - Certains compteurs peuvent être désactivés pour travaux ou même définitivement... nous verrons dans le <a href="#IIA2">pré-processing Power Query</a> que nous avons du effectuer des retraitements pour cette raison ;
 - ou subir ponctuellement une panne;
 - ou tout simplement avoir une date d'installation au cours de la période.

* Les compteurs sont situés sur des aménagements soient mixtes (couloirs bus-vélo) soient dédiés aux cyclistes (bandes et/ou pistes cyclables).
 **L'hypothèse est faite que l'algorithme de traitement des données réalisé par les compteurs retire correctement les autres véhicules** qui pourraient emprunter ces voies, qu'ils y soient autorisés (trotinettes) ou non (deux-roues motorisés).

* Le jeu de donnée étant **mis à jour quotidiennement**, il n'est pas figé.
Pour l'exploration ce n'est pas grave.
 Dans le contexte de notre projet, nous n'avons pas le temps de rendre le rapport dynamique sur la base du dernier jeu publié, nous avons donc choisi de figer la période d'analyse, du 1er septembre 2024 au 30 septembre 2025. Le choix de cette période nous permet en effet de :
  - travailler sur des mois complets;
  - ne pas être pénalisé par les anomalies de l'été 2024 liées aux restrictions de circulation dans Paris pendant les JO et qui ont fortement impactés les déplacements à vélo dans Paris<a href="#bib202" class="ref">[2b]</a>.

#### I.D.2 Exploration du jeu sur l'OpenData de la ville de Paris. <a id="ID2"></a>

Le jeu de données est disponible sur l'OpenData de la Ville de Paris [ici](https://opendata.paris.fr/explore/dataset/comptage-velo-donnees-compteurs/information/?disjunctive.id_compteur&disjunctive.nom_compteur&disjunctive.id&disjunctive.name).

Il est possible de naviguer dans les données directement sur le site et ainsi de se faire une première idée des éléments.<br>

<div style="text-align:center; margin: 20px 0;">
  
  <figure style="display:inline-block; width:100%; margin:0 1%;">
    <img src="images/carte_open_data.png" alt="emplacement des compteurs dans le plan vélo 2021-2026" style="width:100%; display:block;">
    <figcaption style="font-size:0.66em; margin-top:6px;">
      Figure 2 — Emplacement des compteurs dans le Plan Vélo 2021-2026
    </figcaption>
  </figure>

</div>

En première approche, nous pouvons ainsi observer la localisation des compteurs et visualiser les photos intégrées au jeu de données.<br><br>
Ainsi, nous notons que ces photos, avec un cadrage resséré sur la boucle de comptage, ne sont pas très intéressantes car elles ne nous apportent rien sur la qualité de l'aménagement en lui-même, nous ne les conserverons pas, *cf.* <a href="#IIA1">pré-processing python</a>.<br>
Géographiquement, les compteurs sont principalement situés aux portes (notamment sud) de Paris, sur les ponts (emplacement stratégique car difficilement contournables) et sur les grands axes identifiés dans le Plan Vélo 2021-2026.<br>
Nous remarquons que le croisement avec ce jeu de données est intéressant à étudier car il nous informe de la qualité de l'aménagement en place (vélopolitain, réseau secondaire... correspondent à des qualités bien précises et définies <a href="#bib304" class="ref">[3d], </a><a href="#bib401" class="ref">[4a]</a>) mais que l'analyse avec ce jeu est complexe, nous en rediscuterons dans les <a href="#persp1" >perspectives</a>.

La donnée principale étant une notion de comptage, on peut en deuxième approche regarder si des variations temporelles sont à prévoir.

<div style="display: table; width: 100%; margin-bottom: 1em;">
  <div style="display: table-cell; width: 45%; vertical-align: top;">
    <figure style="margin:0;">
        <img src="images/saison.png" alt="Trafic median mensuel entre le 01/09/2024 et 30/09/2025" style="width:100%;">
        <figcaption>
         Figure 3 — Effet des saisons sur le trafic median mensuel
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
         Figure 4 — Effet des jours ouvrés sur le trafic journalier
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
      Figure 5 — Pics d'affluence un jour ouvré
    </figcaption>
  </figure>

  <figure style="display:inline-block; width:50%; margin:0 1%;">
    <img src="images/horaire_we.png" alt="trafic cycliste moyen les samedi 20 et dimanche 21 septembre 2025 à Paris" style="width:100%; display:block;">
    <figcaption style="font-size:0.66em; margin-top:6px;">
      Figure 6 — Pics d'affluence les week-ends
    </figcaption>
  </figure>

</div>

La difficulté d'interprétation d'une variation dans les comptages et du niveau de fréquentation des compteurs nous semble problématique par rapport à notre objectif de fournir de quoi décider d'un aménagement en effet, avoir un trafic faible ou au contraire, qu'est-ce que cela veut vraiment dire ?<br>

Compte-tenu de notre objectif d'analyser également les **zones** d'affluence, il pourra être intéressant de comparer les compteurs entre-eux :

* les compteurs **sur-performant** pouvant être interprétés comme :
  - des zones où les aménagements fonctionnent pour favoriser la transition modale sans nécessiter d'action à prévoir pour la Mairie de Paris si ce n'est de continuer de suivre leur fréquentation ?
  - ou bien des zones où les aménagements saturent et sont peut-être sous-dimensionnés et qu'il est tempts de revoir l'aménagement cyclable ?

* les compteurs **sous-performant** pouvant également être interprétés comme situés dans des zones où des aménagements cyclables sont nécessaires pour encourager le développement du trafic cycliste... ou peut être que l'aménagement existant est mal adapté, inutile....<br>

Les variations de trafic ne sont pas non plus faciles à interpréeter : traduisent-elles un effet de la qualité de l'aménagement ou d'un autre facteur ?<br>

Pour répondre à ces questions, il nous faut des variables explicatives... mais notre jeu de donnée n'en dispose que d'une seule : l'heure et la date du comptage.<br><br>

L'exploration nous a permis de voir des variations horaires mais aussi saisionnières... cela nous pousse à regarder du côté de la météo : si les conditions climatiques sont plus clémentes, la mobilité à vélo augmente-t-elle ? et si oui, est-ce partout la même chose ou des lieux y sont-ils plus sensibles ?<br>
Il faut noter d'ailleurs que dans son rapport d’analyse de fréquentation<a href="#bib201">[2a]</a>, la Ville de Paris met sur le compte de la forte pluviométrie de 2024 (900 mm sur l’année) la stagnation de la fréquentation par rapport à 2023, mais cela touche-t-il tous les sites de la même manière et la pluie est-elle toujours le facteur le plus explicatif ?<br><br>

Pour expliquer les variations qui seraient liés à la **qualité** de l'aménagement cyclable, nous avons besoin d'une variables explicative, l'opportunité de la sortie, le 1er octobre, du jeu de donnéesdes [résultats du Baromètre Parlons Vélo 2025](https://opendata.parlons-velo.fr/) qui identfie notamment la position GPS des points à améliorer en priorité selon les cyclistes interrogés au printemps 2025 (données explorables en direct [ici](https://www.barometre-velo.fr/2025/carte/#12.27/48.85887/2.34703).)<br><br>

Cette première analyse nous conduit donc à la décision d'enrichir notre jeu de données avec 2 jeux de données complémentaires issus des sources suivantes :

* le jeu de donnée des [résultats du Baromètre vélo 2025](https://opendata.parlons-velo.fr/) de la Fédération des Usagers de la Bicyclette (FUB), paru ce 1er octobre 2025 et qui recense les résultats de la dernière enquête d'usage (réalisé au printemps 2025), avec notamment les identifications, par les usagers de zones d'aménagements à améliorer ("points rouges") et de zones sur lesquels les aménagements ont été améliorés depuis 2021 (date de l'enquête précédente, "points verts") ainsi que de points sur lesquels il existe des attentes en matière d'équipement (notamment stationnement ("points bleus")).<br>
Chacun de ces points ayant été éventuellement regroupés en "clusters" lorsque 14 points sont identifiés par les répondants dans une zone de 50m sur une même rue, un même carrefour, une zone a été tracée. Les données textuelles (commentaire individuels des sondés) associés à chaque point géographique pourront éventuellement être utilisé pour affiner l'analyse.<br>
Ces jeux permettront d'enrichier la table des sites de comptage afin de croiser les analyses avec une cartographie précise.<br><br>

* les données météo quotidiennes (on a vu lors du rapport de découverte que certaines semaines semblent plus faibles que d'autres en période hivernale) : on pourra utiliser le [jeu de donnée météo des 6 capteurs météo de la capitale](https://www.data.gouv.fr/api/1/datasets/r/aba837dc-fc7c-4010-ab5e-0eb02feb0010) pour référence.

<hr class="page-break">

### I.E. Bilan de l'étape de découverte des données

À l'issue de cette étape, nous décidons de centrer notre analyse sur une visualisation graphique : 
* **temporelle** centrée sur l'heure de la journée, le jour de la semaine ainsi que la météo
* **géographique** avec une cartographie des zones les plus fréquentées, à croiser avec le ressenti des cyclistes en matière de qualité d'aménagement (nuage de mot).<br><br>

Nous compléterons d'une analyse de l'effet de la météo et ses différentes composantes (température, pluviométrie, vent) et de son effet sur le flux de cycliste.<br>
Nous essaierons de mesurer son effet sur les zones de comptage : les cyclistes évitent-ils certains secteurs les jours de pluie (effet de qualité du revêtement (pavé...)) ou au contraire en période de forte chaleur (revêtement à fort albedo, absence d'ombre ?)<br><br>

## II.A. Préprocessing du jeu principal avec Python <a id="IIA"></a>

### II.A.1. Exploration détaillée des jeux de données 'comptage & compteurs' <a id="IIA1"></a>

Pour explorer le jeu de données, il faut d'abord y accéder... Pandas montre ici ses limites sur un jeu de données de 1,44 Go : en fonction de la configuration de nos ordinateurs, nous ne sommes que 2 sur 3 à pouvoir charger un dataframe avec la méthode `pandas.read_csv()`.<br>
Nous aurions pu basculer sur une autre librairie mais nous avons simplement opté pour un chargement "par morceaux" du jeu de données via une boucle de découpe par lot de 200 000 lignes puis un regroupement des données.<br><br>

Une fois le dataframe créé, nous avons étudié ses différentes colonnes en créant une fonction d'analyse de ces dernières et en écrivant le résultat de cette analyse dans un fichier de métadonnées. La fonction est présentée en <a href="#ann2">Annexe 2</a> et son résultat sur le jeu de donnée principal en <a href="#ann2a">Annexe 2a</a>.<br><br>

Il est utile de remaquer à ce stade le fait que la dénomination des colonnes, quoique parfois un peu longue, est explicite, avec des identifiants clairement identifiables ce qui simplifie l'utilisation du jeu.<br><br>

Ces informations nous permettent de voir que les données brutes issues des capteurs sont relativement complètes, mais pas immédiatement exploitables.  <br>
Certaines colonnes contiennent plusieurs informations (comme la date et l’heure combinées ou les coordonnées géographiques sous forme de texte), tandis que d’autres sont purement illustratives (notamment la partie photo que nous avions déjà décidé d'écarter).<br><br>

Un travail de pré-traitement est donc nécessaire pour rendre les variables :
- plus **claires**,
- plus **structurées**,
- et plus **pertinentes** pour l’analyse métier.<br><br>

La présence de quelques données manquantes (moins de 4% des lignes étant concernée) nécessitait une analyse complémentaire pour savoir ce que nous allions faire, nous avons donc réalisé une visualisation de ces données manquantes afin de mieux cerner leur origine:

<div style="text-align:center; margin: 20px 0;">
  <figure style="display:inline-block; width:100%; margin:0 1%;">
    <img src="images/heatmap_manquants.png" alt="données manquantes dans le jeu principal" style="width:100%; display:block;">
    <figcaption style="font-size:0.66em; margin-top:6px;">
      Figure 7 — Visualisation des données manquantes par lignes et colonnes dans le jeu de donnée principal
    </figcaption>
  </figure>
</div>

On constate que les données manquantes sont concentrées sur certaines lignes mais concernent la majorité des colonnes d'informations.
2 types de profils de manquants apparaissent :

1. Lorsque l'identifiant du compteur est absent, il manque toutes les données d'informations du compteur et les comptages correspondants (qui par ailleurs sont vides) ne seront pas exploitables : nous pourrons donc supprimer ces lignes.
2. Lorsque l'identifiant du compteur est présent MAIS que l'ID Photos est absent, alors on a malgré tout les informations principales de disponibles, et notamment celles de comptage et de géolocalistion des compteurs => il sera donc possible de conserver ces lignes de comptages.<br>

Compte-tenu de ces constatations, il est conclu qu'il sera judicieux de nettoyer les données APRES avoir séparé les données en 2 jeux distincts (comptage et compteurs) et supprimer les colonnes inutiles de photos.<br><br>

Il faut note que le jeu ne présente aucune ligne en doublon.<br>
La structure du jeu, issue d'une jointure entre les données de comptage fournies par Eco-Compteur et les données d'identification et localisation des compteurs, conduit par contre à une multiplication d'information liées à ces compteurs : on s'attend à avoir les informations relatives à chaque compteurs pour les 24h de chacune des 395 jours de comptage soit 9480 lignes potentielles lorsque le compteur n'a pas subi d'interruption.<br><br>

Cela alourdit le dataframe et justifie d'autant plus la scission avec un jeu "données de faits" pour les données de comptage et "données dimensionnelles" pour les données des compteurs.<br>
Nous en profiterons pour scinder la colonne de coordonnées géographique afin de récupérer la latitude et la longitude, format plus pratique pour le visualisation dans Power BI et basculerons les données temporelles au format datetime.<br>

### II.A.2. Préparation du jeu principal <a id="IIA2"></a>

#### II.A.2.a. Préparation du jeu principal

Cette préparation s'est déroulée en plusieurs étapes, principalement dans le Jupyter Notebook nommé `rapport_d_exploration.ipynb`.

1. **Séparation des colonnes composites, conversion des types de données et extraction des coordonnées géographiques**  

* Conversion des dates en format `datetime`, des coordonnées en `float`, et que les nombres de comptages sont bien de type `int`.

* Conversion du champ `Date et heure de comptage` du format 'object' en format `datetime` en prenant en compte le fuseau horaire parisien et création des champs de `Date` et `Heure`pour faciliter les regroupements temporels :
  - `Date` (pour l’analyse par jour, mois, saison)
  - et `Heure` (pour les pics horaires)
Après tergiversations, nous avons finalement choisi de conserver néanmoins la colonne au format 'datetime' initial car elle sera utile dans l'utilisation ultérieure sur PowerBi (création de hiérarchie temporelle jusqu'à l'heure).

* Transformation de la colonne `Coordonnées géographiques` du jeu de données des compteurs en deux variables numériques distinctes `latitude` et `longitude` format plus pratique pour les visualisations cartographiques dans Power BI.

2. **Simplification de certains noms de colonnes** pour faciliter les manipulations car certains noms étaient très longs.

<table class="table-compact">
  <thead>
    <tr><th>Nom de colonne initial</th><th>Nouveau nom</th></tr>
  </thead>
  <tbody>
    <tr><td>`Comptage horaire`</td><td>`comptage_horaire`</td></tr>
    <tr><td>`Date et heure de comptage`</td><td>`date_heure`</td></tr>
    <tr><td>`Identifiant du compteur`</td><td> id_compteur`</td></tr>
    <tr><td>`Nom du compteur`</td><td>`nom_compteur`</td></tr>
    <tr><td>`Identifiant du site de comptage`</td><td> `id_site`</td></tr>
    <tr><td>`Nom du site de comptage`</td><td>`nom_site`</td></tr>
    <tr><td>`Identifiant technique compteur`</td><td>`id_technique_compteur`</td></tr>
    <tr><td>`Date d\'installation du site de comptage`</td><td>`date_installation`</td></tr>
    <tr><td>`Lien vers photo du site de comptage`</td><td>`photo_site`</td></tr>
    <tr><td>`Coordonnées géographiques`</td><td>`coordonnees`</td></tr>
  </tbody>
</table>

3. **Correction du format de l'identifiant du site de comptage :** sur certaines lignes, le site de comptage présentait une altération du format avec présence de virgule. Nous avons donc supprimé ces dernières et converti en entier pour avoir un format cohérent avec la nature d'identifiant de la colonne.

#### II.A.2.c. Extraction du jeu de comptage

Sur le jeu de donnée de comptage, on va venir conserver les colonnes suivantes:
   * `id_compteur`
   * `id_site`
   * `comptage_horaire`
   * `date_heure`
   * `mois_annne_comptage`
   * `date`
   * `heure`

Il faut noter que bien que nous ayons une relation de type *One to Many* entre l'identifiant du site de comptage et l'identifiant du compteur (un compteur n'appartient jamais qu'à un seul site de comptage, et il y a fréquemment 2 compteurs (1 dans chaque direction) pour un même site), nous avons sciemment choisi de conserver l'identifiant du site de comptage dans notre jeu de données alors que nous aurions pu l'éliminer.<br>
Cependant, à ce stade de notre étude, nous ne savions pas si nous allions nous focaliser sur les sites de comptage ou les compteurs dans notre analyse : nous avons donc décider de conserver cette colonne.<br><br>

Le jeu ainsi créé ne contenait ni doublon ni manquant et ne nécessitait donc pas de nettoyage supplémentaire.<br><br>

A l'issu de cette étape, nous avons donc créé un fichier `comptage-velo-donnees-compteurs-allege.csv` dans notre répertoire \data\processed et un fichier de métadonnées `metadatas-donnees-comptage.txt` dans note répertoire \references.

#### II.A.2.b. Extraction du jeu de compteur

On utilisera `id_compteur` comme clé unique pour faciliter les jointures et les regroupements futurs entre les jeux compteurs et comptage.<br>

Bien que certaines colonnes (photos notamment) aient été identifiés comme inutiles, certains membres du groupe n'ont pas voulu les éliminer à ce stade, nous avons donc repris l'ensemble des colonnes et simplement écarté les informations liées au comptage horaire. Bien que seule les informations géographiques et les couples id_compteur et id_site associés à leurs noms nous aient été utiles, nous avons donc conservé les colonnes suivantes :
* `id_compteur`
* `nom_compteur`
* `id_site`
* `nom_site`
* `date_installation`
* `photo_site`
* `coordonnees`
* `id_technique_compteur`
* `ID Photos`
* `test_lien_vers_photos_du_site_de_comptage_`
* `id_photo_1`
* `url_sites`
* `type_dimage`
* `latitude`
* `longitude`

Une fois les nombreux doublons supprimés, il restait quelque valeurs manquantes mais uniquement sur des colonnes qui ne nous intéressait pas (photos) et nous n'avons donc pas cherché à les remplacer.

### II.A.3. Géolocalisation des compteurs

Nous avons cherché à situer nos compteurs sur une carte, ceci afin de pouvoir valider ultérieurement l'intérêt de croiser ou non ces positions avec celles des commentaires du baromètre FUB.
Pour cela, si nous avions effectivement créé une colonne de `latitude` et `longitude` pour faciliter l'usage dans Power BI, nous avons préféré opter pour la création d'une colonne de type GEOMETRY pour une visualisation Python avec `geopandas`. Nous avons donc créé un point géographique à partir des coordonnées pour créé un GeoDataFrame.
Pour cette visualisation, nous avons utilisé le système de référence de coordonnées (CRS) du système GPS en latitude/longitude en WGS84. Nous avons donc utilisé la projet "EPSG:4326" et nous avons stocké ce point dans un champ nommé `geometry`.

A l'issu de cette étape, nous avons créé un fichier `compteurs_velo.csv` dans notre répertoire \data\processed et un fichier de métadonnées `metadatas-donnees-compteur.txt` dans note répertoire \references.

La création de ce point géographique nous a permis ensuite de positionner chaque compteur sur une carte de Paris dynamique avec la librairie folium (cf. rapport d'exploration), carte que nous avons mise de côté pour superposer plus tard avec les avis des cyclistes.
<div style="text-align:center; margin: 20px 0;">
  <figure style="display:inline-block; width:100%; margin:0 1%;">
    <img src="images/carte_compteur.png" alt="emplacement des compteurs" style="width:100%; display:block;">
    <figcaption style="font-size:0.66em; margin-top:6px;">
      Figure 8 — Emplacement des compteurs
    </figcaption>
  </figure>
</div>

## II.B. Exploration et Préprocessing des jeux d'enrichissement avec Python  <a id="IIB"></a>

#### II.B.1 Jeu de données météorologique <a id="IIB1"></a>

L'exploration et la préparation du jeu de donnée météo a été faite dans un Jupyter Notebook nommé `méteo.ipynb`.

Le jeu de données téléchargé `Q_75_latest-2024-2025_RR-T-Vent.csv` contenait l'intégralité des données de 2024 et 2025, soit 3875 lignes et 57 colonnes. nous avons donc commencé par le restreindre à la même plage de date que notre jeu de comptage soit du 01/09/2024 au 30/09/2025.

D'autre part, le jeu de donnée correspondait aux résultats de 6 capteurs météo de la capitale.
Nous avons considèrer ces 6 stations météo comme complémentaires : s'il y a quelque différence d'altitude entre la Tour Eiffel et les jardins du Luxembourg, il n'y a cependant pas de différences climatiques significatives par rapport à notre analyse. Nous aovns donc agrègé les données en prenant la moyenne des non nuls pour chaque paramètre n'identifiant pas le capteur.

Nous avons ensuite cherché à supprimer les colonnes ne nous intéressant pas. Pour cela nous avons consulté la notice en ligne du jeu de donnée afin de comprendre les intitulés peu explicites pour les non météorologues.
Il s'est avéré que toutes les colonnes commençant par la lettre 'Q' étaient des colonnes techniques qualifiant le niveau de qualité de la mesure et non la mesure elle-même, nous pouvions donc les éliminer.
L'analyse des manquants nous a par ailleurs permis de supprimer d'autres colonnes, intégralement vides car ne correspondant tout simplement pas au climat parisien sur notre période.
Il nous restait alors une série de colonne que nous avons pu renommer avec leur définition respectives plutôt que leurs abbreviations anglosaxonnes:

<table class="table-compact">
  <thead>
    <tr><th>Nom de colonne initial</th><th>Nouveau nom</th></tr>
  </thead>
  <tbody>
    <tr><td>RR</td><td>RR précipitations (mm)</td></tr>
    <tr><td>DRR</td><td>DRR durée de précipitations (mn)</td></tr>
    <tr><td>TN</td><td>TN temp. mini (°C)</td></tr>
    <tr><td>HTN</td><td>HTN heure la + froide (hhmn)</td></tr>
    <tr><td>TX</td><td>TX temp. max (°C)</td></tr>
    <tr><td>HTX</td><td>HTX heure la + chaude (hhmn)</td></tr>
    <tr><td>TNTXM</td><td>TNTXM temp. moyenne quotidienne (°C)</td></tr>
    <tr><td>TAMPLI</td><td>TAMPLI amplitude thermique (°C)</td></tr>
    <tr><td>TNSOL</td><td>TNSOL temp. mini à 10cm du sol (°C)</td></tr>
    <tr><td>TN50</td><td>TNSOL temp. mini à 50cm du sol (°C)</td></tr>
    <tr><td>DG</td><td>DG durée de gel sous abri (mn)</td></tr>
    <tr><td>FFM</td><td>FFM force moyenne sur 10mn du vent à 10m (m/s)</td></tr>
    <tr><td>FF2M</td><td>FF2M force moyenne sur 10mn du vent à 2m (m/s)</td></tr>
    <tr><td>FXY</td><td>FXY force max du vent moyen sur 10mn à 10m (m/s)</td></tr>
    <tr><td>DXY</td><td>DXY direction du vent moyen à 10m (rose de 360)</td></tr>
    <tr><td>FXI</td><td>FXI force max instantanée du vent à 10m (m/s)</td></tr>
    <tr><td>HXI</td><td>HXI heure du vent max instantanée à 10m (hhmm)</td></tr>
    <tr><td>DXI</td><td>DXY direction du vent max instantanée à 10m (rose de 360)</td></tr>
    <tr><td>FXI2</td><td>FXI force max instantanée du vent à 2m (m/s)</td></tr>
    <tr><td>HXI2</td><td>HXI heure du vent max instantanée à 2m (hhmm)</td></tr>
    <tr><td>DXI2</td><td>DXY direction du vent max instantanée à 2m (rose de 360)</td></tr>
    <tr><td>FXI3S</td><td>FXI3S force max quotidienne sur 3sec du vent à 10m (m/s)</td></tr>
    <tr><td>HXI3S</td><td>HXI3S heure du vent max sur 3 sec à 10m (m/s)</td></tr>
  </tbody>
</table>



#### II.B.2. Jeu de données de l'enquête de la FUB <a id="IIB2"></a>

Après en avoir fait la demande auprès de la FUB, nous avons téléchargé les jeux de données du baromètre 2025 pour la ville de Paris.
La notice du jeu de données est présentée en <a href="#ann2c">Annexe 2c</a>. Dans le cadre de notre projet, nous avons uniquement utilisé les fichiers .geojson contenant les descriptions données par les répondant pour chacun des points (max 9) qu'ils avaient pu identfier.

Deux types de fichiers .geojson étaient disponibles :

* les 3 fichiers de clusters, issu du prétraitement de la FUB et correspondant à un regroupement de points identifiés par les répondants, ces clusters formant des "zones prioritaires". À noter que les fichiers de cluster pour la ville de Paris étant vide (erreur de création ?), nous nous sommes rabattus sur les fichiers de clustering du département 75.
* les 3 fichiers correspondants à chacune des catégories de points (vert, rouge, bleu). Ces fichiers étant naturellement plus complets que les fichiers de clusters puisque exhaustif.

Dans un premier temps, nous avons commencé notre exploration par les données de clustering, pour voir si les clusters identifiés étaient ou non à proximité de nos compteurs afin de nous assurer de la pertinence du croisement des données.

L'exploration et la préparation du jeu de donnée a été faite dans un Jupyter Notebook nommé `barometre2025.ipynb` ainsi que dans `rapport_d_exploration.ipynb`.

##### II.B.2.a. Exploration des clusters du baromètre FUB <a id="IIB2a"></a>

Surces fichiers, nous avons conservé pour l'exploration le format spécifique des polygones des clusters (avec une liste des points définissant la zone), comme par exemple :
`MULTIPOLYGON (((2.285062579 48.880798105, 2.284173146 48.880794376, 2.283934653 48.881017294, 2.284509497 48.881230919, 2.285062579 48.880798105)))` et avons cherché à superposer ces clusters sur la carte des compteurs.

##### II.B.2.b. Bilan de l'exploration du baromètre FUB et préparation des points <a id="IIB2b"></a>

#### II.B.3. Préparation des avis pour l'analyse textuelle <a id="IIB3"></a>

##### II.B.3.a. Regroupemeent des données <a id="IIB3a"></a>

##### II.B.3.b. Normalisation et lemmatisation du texte en français <a id="IIB3b"></a>

<a href="#ann3">Annexe 3</a>

<a href="#ann4">Annexe 4</a>

##### II.B.3.c. Choix de l'algorithme le plus pertinent <a id="IIB3c"></a>


#### II.B.4. Jointure géospatiale des avis <a id="IIB4"></a>



#### II.B.5. Fichiers obtenus à l'issu de cette étape <a id="IIB5"></a>

À la fin de cette étape, nous disposons de jeu csv retraités :
- propres et homogènes,  
- allégés des variables inutiles,  
- structurés pour les analyses temporelles et spatiales.  

<a href="#bib601" class="ref">[6a]</a>

### II.B. Préprocessing dans Power Query <a id="IIB"></a>

#### II.B.1. Collecte des données <a id="IIB1"></a>

#### II.B.2. Suppression des champs inutiles et convivialité des champs <a id="IIB2"></a>

**Suppression des colonnes inutiles** qui pénalise fortement les performances car le jeu est trop encombrant. Nous éléminons donc les variables purement descriptives (comme celles liées aux photos) ou redondantes :
   * `Identifiant technique compteur`,
   * `Date d\'installation du site de comptage`,
   * `Lien vers photo du site de comptage`,
   * `ID Photos`,
   * `test_lien_vers_photos_du_site_de_comptage_`,
   * `id_photo_1`,
   * `url_sites`.

#### II.B.3. Amélioration des noms de compteurs et sites de comptage <a id="IIB3"></a>

<a href="#ann4">Annexe 4</a>

#### II.B.4. Création d'un score météo <a id="IIB4"></a>

<a href="#ann5">Annexe 5</a>

### II.C. Préprocessing dans Power BI <a id="IIC"></a>

#### II.C.1. Modélisation en étoile <a id="IIC1"></a>

Résolution du problème de cardinalité
nos commentaires sont associé à un SITE de comptage et non à un COMPTEUR et donc on se retrouvait avec une relation Many to Many pas top.... on aurait pu transformer le modèle en étoile en flocon mais c'est pas top en terme de performance, donc j'ai préféré modifier le script de Mohammed Bourquia pour récupérer l'id du compteur le plus proche en considérant arbitrairement le 1er des id trouvés pour un même site de comptage. Ceci m'a permis de modifier le modèle sémantique et de créer la liaison.

#### II.C.2. Création des tables de date <a id="IIC2"></a>

#### II.C.3. Création des hiérarchies <a id="IIC3"></a>

#### II.C.4. Création des mesures de sensibilité à la météo <a id="IIC4"></a>

<a href="#ann6">Annexe 6</a>

#### II.C.5. Création des mesures de saturation des aménagements <a id="IIC5"></a>

<a href="#ann7">Annexe 7</a>

### II.D. Visualisations dans Power BI <a id="IID"></a>

<a href="#bib602" class="ref">[6b]</a>

<a href="#ann8">Annexe 8</a>

<hr class="page-break">

## III. Analyse des données <a id="III"></a>

<hr class="page-break">

## Conclusion

### Bilan

### Perspectives :

1. **Enrichir le jeu de données avec celui des aménagements cyclables.**<a id="persp1"></a>

Ceci nous aurait permis d'analyser séparément les compteurs sur bande cyclables de ceux sur pistes cyclables par exemple ou de prendre en compte pour ces dernières la largeur de l'aménagement afin de préciser les risques de saturation.
Un tel jeu existe et est disponible [ici](https://www.openstreetmap.org/search?query=Paris&zoom=5&minlon=-34.40917968750001&minlat=38.03078569382294&maxlon=34.23339843750001&maxlat=61.897577621605016#map=13/48.85890/2.33116&layers=C) grace au travail des contributeurs d'OpenStreeMap.<br>

La Ville de Paris ne produit pas sa propre carte mais retraite cette carte collaborative en qualifiant la qualité de la donnée et en la mettant à disposition sur son propre OpenData  [ici](https://opendata.paris.fr/explore/dataset/amenagements-cyclables/information/?disjunctive.arrondissement&disjunctive.position_amenagement&disjunctive.vitesse_maximale_autorisee&disjunctive.source&disjunctive.amenagement).<br>

Mais son traitement pour intégration dans le jeu de donnée nous aurait pris trop de temps et nous nous sommes donc contenté d'une analyse visuelle de l'aménagement au travers de la photo du site. En effet, le jeu est plus complexe qu'il n'y paraît : 

* plusieurs traces GPS peuvent être superposées sur une même voie lorsque l'aménagement est bidirectionnel ou être unique lorsqu'il est unidirectionnel, le nombre de catégorie d'aménagement listé est bien plus important que celui à proximité des compteurs (du double sens cyclable à la piste bidirectionnelle en passant par la voie verte, la vélorue où la voie partagée avec les bus pour n'en citer que quelques uns.)
* les aménagements se gèrent comme des dimensions à évolution lente (une fois tous les x mois, un aménagement va être mis à jour pour indiquer par exemple la fin des travaux de création d'une voie de vélopolitain) tandis que notre jeu de donnée à une temporalité courte avec des données horaires.

1. **Identifier l’ordre d’importance des facteurs responsables des variations de flux :** <a id="persp2"></a>

Que ces variations soient horaires (effet de journée de travail), hebdomadaires (semaine de travail vs weekend), saisonnières (effet des vacances d'étét ou des fêtes de fin d'années) ou météorogoliques, nous avons en effet pu voir que de nombreux éléments étaient à l'origine des variations.<br>
Si nous avions eu le temps d'aborder les cours de machine learning un peu plus tôt.<br>
Ainsi, nous aurions par exemple pu utiliser un arbre de régression pour ajuster notre calcul de scoring météo, qui est actuellement basé avant tout sur une approche "mon vécu de cycliste" que sur une démarche statistique.<br>
Nous aurions par ailleurs pu tenter d'identifier l'ordre d'importance de ces facteurs pour affiner l'identification des sites nécessitant des modifications d'aménagements.

1. **Rendre dynamique le rapport en le raccordant directement via API.**<a id="persp3"></a>

Ceci nous aurait permis d'élargir la période de donnée utilisée plutôt que de se restreindre à 13 mois (donc d'avoir plusieurs étés, plusieurs vacances d'hiver...).<br>

Le jeu étant actualisé quotidiennement avec de nombreux compteurs installés depuis plus de 6 ans, nous aurions ainsi pu étudier des tendances et les données supplémentaires nous auraient permis de commencer à faires des prédictions de trafic pour affiner l'identification des sites :

  * pour lesquels un aménagement permettrait d'éviter une future saturation,
  * ou pour lesquels un aménagement favoriserait le développement de la part modale cycliste.

4. **Enrichir le jeu de données avec les jeux de données sur l'accidentologie.**<a id="persp4"></a>

Le jeu ddit "fichier BAAC" (Base de données Annuelles des Accidents Corporels de la circulation routière de l'Observatoire National Interministériel de la Sécurité Routiers (ONISR) est librement accessible [ici](https://www.data.gouv.fr/datasets/bases-de-donnees-annuelles-des-accidents-corporels-de-la-circulation-routiere-annees-de-2005-a-2024), inclue une localisation des accidents et permetttrait d'améliorer l'identification et la quantification les zones dangereuses afin de prioriser les travaux sur ces zones.

### Les difficultés qu'il a fallu relever

1. **Les contraintes du travail d'équipe en mode projet :**
<a id="defi1"></a>
> Nous avons découvert GitHub tous ensemble en collaborant sur un repository privé hébergé sur mon GitHub personnel. Le principe était d'avoir chacun sa branche pour travailler et de consolider nos avancées dans la branche *main*.
> Mais les débuts ont été compliqué et j'ai du à plusieurs reprises utiliser les fonctions de revert ou reset suite à des *merge* "à l'envers" de certains de mes collègues… l’absence de formation à l'utilisation d'un outil de versionning dans le cadre de la formation a été un réel manque même si nous avons pu nous appuyer sur ls modules Microsoft Learn.

2. **La compréhension des notions d’environnements python et de gestion de version des librairies Python :**
<a id="defi2"></a>
>Nous avons été confronté à des erreurs liés à ce type de problème car nous avions tous les 3 des versions différentes de Python (3.13.5 pour moi et Ghizlane sur oc, 3.14 pour Mohammed sur mac).
>J'ai également eu des conflits de versions de librairies Python et il aurait été judicieux de mettre en place un environnement partageable pour stabiliser notre travail, d'autant que sans Power BI Service, chaque utilisateur doit pour l'instant déclarer son propre environnement python pour faire fonctionner le rapport.
>Un module de formation sur les bonnes pratiques d’utilisation d’un EDI aurait été apprécié, ainsi que sur les modalités de création d'un environnement Python et son partage.

3. **L’analyse de texte en français :** 
<a id="defi3"></a>
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

Qualité des aménagements cyclables (nombreuses photos et exemples) pour la compréhension des sites de comptage :
<a id="bib401">[4a]-</a>[Guide des aménagements cyclables - Edition : Paris en Selle - mise à jour de 20121](https://parisenselle.fr/telecharger-guide-amenagements-cyclables/)

<a id="bib402">[4b]-</a>[Plateforme dédiée aux compteurs vélo](https://parisenselle.fr/2020/10/06/une-plateforme-pour-recenser-les-compteurs-velo/#:~:text=Nous%20sommes%20heureux%20de%20vous%20pr%C3%A9senter%20https%3A%2F%2Fcompteurs.parisenselle.fr%2C%20qui,grand%20merci%20%C3%A0%20Tristram%20pour%20ce%20gros%20boulot.)


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

### <a id="ann2">Annexes 2</a> : Struture des jeux de donnéees initiaux

Les informations ci-dessous ont été extraites des jeux par l'application de la fonction ci-dessous :

```python
def info_colonnes(df):
    infos = []  # liste qui va contenir les infos de chaque colonne
    
    for col in df.columns:
        # Récupérer le type de la colonne
        dtype = df[col].dtype
        nb_unique=df[col].nunique()
        nb_manquant=df[col].isnull().sum()
        pct_manquant=f"{df[col].isnull().mean() * 100:.2f}%"
        nb_doublon=df[col].duplicated().sum()
        nb_identifiant_non_unique=df[col].duplicated(keep=False).sum()
        ex_unique=f" {df[col].unique()[:5]}"  # Affiche les 5 premières valeurs uniques  
                    
        infos.append(f"</p><p>Nom de la colonne: {col}\n Type : {str(dtype)}\nNombre de valeurs uniques : {str(nb_unique)}\nNombre de valeurs manquantes : {str(nb_manquant)}\nPourcentage de valeurs manquantes : {str(pct_manquant)}\nNb élements utilisés plusieurs fois : {str(nb_doublon)}\nsoit nb lignes avec un élément non unique : {str(nb_identifiant_non_unique)}\nExemples de valeurs uniques : {str(ex_unique)}\n")
        
    # Retourner une seule chaîne composée des descriptions de chaque colonne
    # pour pouvoir l'écrire facilement dans un fichier de métadonnées.
    return "\n\n".join(infos)

# on va venir enregistrer la description des données brutes dans un fichier txt de métadonnées

file_metadonnees=chemin_user+"references/metadatas-donnees-brutes.txt"
   
with open(file_metadonnees,"w") as f:
    f.write("Structure du jeu de données initial brut :\n")

with open(file_metadonnees,"a") as f:
    content=str(info_colonnes(df))
    f.write(content)
    f.close()

```

<hr class="page-break">

#### <a id="ann2a">Annexe 2a</a> : Structure du jeu de données initial brut

<div class="two-columns">
<p>Nom de la colonne: Identifiant du compteur<br>
 Type : object<br>
Nombre de valeurs uniques : 98<br>
Nombre de valeurs manquantes : 24533<br>
Pourcentage de valeurs manquantes : 2.77%<br>
Nb éléments utilisés plusieurs fois : 885145<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['100003098-101003098' '100006300-101006300' '100007049-102007049'
 '100007049-101007049' '100036718-104036718']<br>
</p>
<p>Nom de la colonne: Nom du compteur<br>
 Type : object<br>
Nombre de valeurs uniques : 109<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 885135<br>
soit nb lignes avec un élément non unique : 885243<br>
Exemples de valeurs uniques :  ['106 avenue Denfert Rochereau NE-SO' '135 avenue Daumesnil SE-NO'
 '28 boulevard Diderot E-O' '28 boulevard Diderot O-E'
 '39 quai Fran�ois Mauriac NO-SE']<br>
</p>
<p>Nom de la colonne: Identifiant du site de comptage<br>
 Type : float64<br>
Nombre de valeurs uniques : 69<br>
Nombre de valeurs manquantes : 24533<br>
Pourcentage de valeurs manquantes : 2.77%<br>
Nb éléments utilisés plusieurs fois : 885174<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  [1.00003098e+08 1.00006300e+08 1.00007049e+08 1.00036718e+08
 1.00036719e+08]<br>
</p>
<p>Nom de la colonne: Nom du site de comptage<br>
 Type : object<br>
Nombre de valeurs uniques : 66<br>
Nombre de valeurs manquantes : 24533<br>
Pourcentage de valeurs manquantes : 2.77%<br>
Nb éléments utilisés plusieurs fois : 885177<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['106 avenue Denfert Rochereau' '135 avenue Daumesnil'
 '28 boulevard Diderot' '39 quai François Mauriac'
 "18 quai de l'Hôtel de Ville"]<br>
</p>
<p>Nom de la colonne: Comptage horaire<br>
 Type : int64<br>
Nombre de valeurs uniques : 1384<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 883860<br>
soit nb lignes avec un élément non unique : 884963<br>
Exemples de valeurs uniques :  [  0   6  34 165 195]<br>
</p>
<p>Nom de la colonne: Date et heure de comptage<br>
 Type : object<br>
Nombre de valeurs uniques : 9474<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 875770<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['2024-09-01T06:00:00+02:00' '2024-09-01T08:00:00+02:00'
 '2024-09-01T05:00:00+02:00' '2024-09-01T15:00:00+02:00'
 '2024-09-01T09:00:00+02:00']<br>
</p>
<p>Nom de la colonne: Date d'installation du site de comptage<br>
 Type : object<br>
Nombre de valeurs uniques : 39<br>
Nombre de valeurs manquantes : 24533<br>
Pourcentage de valeurs manquantes : 2.77%<br>
Nb éléments utilisés plusieurs fois : 885204<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['2012-02-22' '2013-01-19' '2013-01-18' '2017-07-12' '2013-01-17']<br>
</p>
<p>Nom de la colonne: Lien vers photo du site de comptage<br>
 Type : object<br>
Nombre de valeurs uniques : 68<br>
Nombre de valeurs manquantes : 33582<br>
Pourcentage de valeurs manquantes : 3.79%<br>
Nb éléments utilisés plusieurs fois : 885175<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['https://filer.eco-counter-tools.com/file/09/73f38aaf49fa85ee19ee67277787a24af6b31b497e0fbf06bf2970b4449a0409/Y2H16029278_20200818121425.jpg'
 'https://filer.eco-counter-tools.com/file/0f/72fcbc343c96fd864d33966e6ca86ed6454fe348c579812ed9c674cf39d1310f/X2H18086316_20240618155704.jpg'
 'https://filer.eco-counter-tools.com/file/4a/2e6127480864e11e9bd152969a114c01c26ea9434bdd7813bc618f511a21b04a/Y2H21015011_20220407110543.jpg'
 'https://filer.eco-counter-tools.com/file/16/35f6b42be906d8dc8ac074b0bfc2683cec4aa3aa4cff6e964ff4a73697ed8816/Y2H21015068_20240618150003.jpg'
 'https://filer.eco-counter-tools.com/file/31/7a51f8668baa67fe9fbc33f577ca62cffa13fab69148810676d42c23d007dc31/15374519009810.png']<br>
</p>
<p>Nom de la colonne: Coordonnées géographiques<br>
 Type : object<br>
Nombre de valeurs uniques : 69<br>
Nombre de valeurs manquantes : 24533<br>
Pourcentage de valeurs manquantes : 2.77%<br>
Nb éléments utilisés plusieurs fois : 885174<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['48.83507, 2.33305' '48.843435, 2.383378' '48.84613, 2.37559'
 '48.83436, 2.377' '48.85372, 2.35702']<br>
</p>
<p>Nom de la colonne: Identifiant technique compteur<br>
 Type : object<br>
Nombre de valeurs uniques : 68<br>
Nombre de valeurs manquantes : 33582<br>
Pourcentage de valeurs manquantes : 3.79%<br>
Nb éléments utilisés plusieurs fois : 885175<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['Y2H20114504' 'X2H18086316' 'Y2H21015011' 'Y2H21015068' 'Y2H21015012']<br>
</p>
<p>Nom de la colonne: ID Photos<br>
 Type : object<br>
Nombre de valeurs uniques : 68<br>
Nombre de valeurs manquantes : 33582<br>
Pourcentage de valeurs manquantes : 3.79%<br>
Nb éléments utilisés plusieurs fois : 885175<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['https://filer.eco-counter-tools.com/file/09/73f38aaf49fa85ee19ee67277787a24af6b31b497e0fbf06bf2970b4449a0409/Y2H16029278_20200818121425.jpg/https://filer.eco-counter-tools.com/file/1e/766b4ae7bba5ee2e4e87b5ed3990964e393647406bf7169c7b948612c014911e/15977456895210.jpg/https://filer.eco-counter-tools.com/file/96/cf95805b6c2fba4a722174ed6d93acf65a2503bbf41ad417508b20e10ebb6496/Y2H16029278_20220803102622.jpg/https://filer.eco-counter-tools.com/file/9c/21fe20ab12a64990b0db744ec805262d6ac64fca0800e5dc887432307ffab29c/Y2H21110997_20231031090022.jpg/https://filer.eco-counter-tools.com/file/ad/53597f9018bb78ed4018cccaf73e0d792319673f5297297e72b624b221788cad/13305145395420.jpg/https://filer.eco-counter-tools.com/file/ae/9bc3209eb84338645b0dbe0b578336e0e5e9c0103bb2119f6a4694ae5defa0ae/Y2H20114504_20240611133259.jpg/https://filer.eco-counter-tools.com/file/bd/ae1f16033631d0af335022b99f8d2de3e823a970d8b4ae1cc349b2339a6bd2bd/Y2H16029278_20210810113212.jpg'
 'https://filer.eco-counter-tools.com/file/0f/72fcbc343c96fd864d33966e6ca86ed6454fe348c579812ed9c674cf39d1310f/X2H18086316_20240618155704.jpg/https://filer.eco-counter-tools.com/file/33/72900abae7cbd8648f613c39f98f2766804530fc2fd9004fcca1ac282a9b5c33/X2H18086316_20220803114717.jpg/https://filer.eco-counter-tools.com/file/4c/44ca3caef446f2d0daf95d1d603651d16f794169bfb14df76d2afc8daac93b4c/X2H18086316_20211004180732.jpg/https://filer.eco-counter-tools.com/file/97/3f31a803a3d2e6dc1b985b032528ea836d3e53685058af9f542c006a7de4a197/15765762690330.jpg/https://filer.eco-counter-tools.com/file/cb/ea232c18c5891153f2c0b47062b73ecc1310e9c41a33239f7f1a6a5fcf2210cb/X2H18086316_20250729134753.jpg/https://filer.eco-counter-tools.com/file/e1/6ef39ee97d7f723c14b8fe9ec91840266b3f3add70e0a817bafd66adc553c9e1/15809064565060.jpg'
 'https://filer.eco-counter-tools.com/file/4a/2e6127480864e11e9bd152969a114c01c26ea9434bdd7813bc618f511a21b04a/Y2H21015011_20220407110543.jpg/https://filer.eco-counter-tools.com/file/6b/84e46df62589a66a0827954c6c07947e87f1e1d5c80724efc19efaf54a67386b/Y2H21015011_20250729122942.jpg/https://filer.eco-counter-tools.com/file/81/7d5f7058df9d97404fb0067e49039a2a022ea3f5a732b5e54b7d2ed90afab981/Y2H21015011_20240618154402.jpg/https://filer.eco-counter-tools.com/file/9b/531a0daddb4be5433a86cb09dc36f92b25c7bd4ea5c93c7c3146181d9625539b/13585075886520.jpg/https://filer.eco-counter-tools.com/file/d0/5539296cbf2bbb9fb37428bdb5bd6fe499ea5843de9de9605700c783eaa879d0/Y2H21015011_20220407110305.jpg/https://filer.eco-counter-tools.com/file/f7/4f2f37a5b343c214e4cc32c80e8de78de6afb907af12505592b2bd2f190671f7/Y2H21015011_20220725182819.jpg'
 'https://filer.eco-counter-tools.com/file/16/35f6b42be906d8dc8ac074b0bfc2683cec4aa3aa4cff6e964ff4a73697ed8816/Y2H21015068_20240618150003.jpg/https://filer.eco-counter-tools.com/file/1b/6c9013a542a3c751f94c8b9a00db0ad3485054953a37aeddf45830482d5d311b/Y2H17021629_20200818165643.jpg/https://filer.eco-counter-tools.com/file/85/6f1a65ada98e5b9c30af21c28ced81ae2d1a3a91d27f7a5ec23a04f8e64dd185/15374559754710.png/https://filer.eco-counter-tools.com/file/89/a417e0e7a5a6a0be002e6b9f7f43b4db5eb3f1c15aa348294378f2b8d6cfa089/Y2H21015068_20220407102319.jpg/https://filer.eco-counter-tools.com/file/92/8dd0832756788947862701438d96ba9ac1f7524794109c2db14efa91a3e5bc92/Y2H21015068_20220803125012.jpg/https://filer.eco-counter-tools.com/file/9e/f997ab4793874f0832ae24c89ef2cafc87a78e90336527f7e9be38d0f4fec39e/15977626284870.jpg/https://filer.eco-counter-tools.com/file/a3/eb19fabc6ac19ee165b9a3d367b75c23705c0bc2ef3c0b7b4950e921840633a3/15765770808100.jpg/https://filer.eco-counter-tools.com/file/c3/3cc5746fc201948a4f89469db101780cf29dcc2c29e350f53351732871bfa5c3/Y2H17021629_20210810135800.jpg/https://filer.eco-counter-tools.com/file/d4/e8110bccec80e42806d28ea2f102e3cf93875f3e8add5dfa4ea0672af45ee3d4/14997911465211.jpg/https://filer.eco-counter-tools.com/file/d9/e055c4b719c875d6a250c8caf4ed5962c847d9d3b04251f053e86b5d088c2ad9/15767555313320.jpg/https://filer.eco-counter-tools.com/file/f2/1f6decacff618a4b568543f90909d8f562fd951737e6b8f53dbe567d64f87cf2/Y2H21015068_20250729150243.jpg'
 'https://filer.eco-counter-tools.com/file/31/7a51f8668baa67fe9fbc33f577ca62cffa13fab69148810676d42c23d007dc31/15374519009810.png/https://filer.eco-counter-tools.com/file/54/8946a312899f621b1e2c7007e9f490f297cd915b9dfee93b4c96c557d5179c54/Y2H21015012_20240613112601.jpg/https://filer.eco-counter-tools.com/file/6c/7219aac71d6d7c03b90a5eb4b59de532d908084b261509e268a150be6948b76c/Y2H21015012_20250729103525.jpg/https://filer.eco-counter-tools.com/file/9d/176068e8b3503f6b68c846ec1741b3a744b56aede12fa81bfc29fa2c82f96d9d/X2H19027732_20190507110918.jpg/https://filer.eco-counter-tools.com/file/bd/7b7d73a0893fc9813d303fa82a8aec6a2888b910e721b344fe519737bf51e1bd/14997911939232.jpg/https://filer.eco-counter-tools.com/file/cc/7ee37fd33279ac655cb94dac2f5cabe37169064be3d172305eee095aa8eb48cc/Y2H21015012_20220407113640.jpg/https://filer.eco-counter-tools.com/file/cd/d97fc859bef5a19d217f46db0a4ee144cfc19d12fe12a8f8f8d6d837dd05f3cd/Y2H19027732_20210810183209.jpg/https://filer.eco-counter-tools.com/file/d0/1aba92aeca91f0ea6146e062f7994959da2ade84f8c5cded3b9f1e8424ea98d0/15718218590430.jpg/https://filer.eco-counter-tools.com/file/d7/030e39ece3b9677fd4ab1c1de4370b0613ad1c4cafd810f4b06b6489f8304cd7/Y2H21015012_20220803103347.jpg/https://filer.eco-counter-tools.com/file/db/b61f852e0d3afa4b9be0cdcfe0046cb3bb330efa17c3941fae25199cf2134fdb/14997911938171.jpg']<br>
</p>
<p>Nom de la colonne: test_lien_vers_photos_du_site_de_comptage_<br>
 Type : object<br>
Nombre de valeurs uniques : 68<br>
Nombre de valeurs manquantes : 33582<br>
Pourcentage de valeurs manquantes : 3.79%<br>
Nb éléments utilisés plusieurs fois : 885175<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['https://filer.eco-counter-tools.com/file/09/73f38aaf49fa85ee19ee67277787a24af6b31b497e0fbf06bf2970b4449a0409/Y2H16029278_20200818121425.jpg'
 'https://filer.eco-counter-tools.com/file/0f/72fcbc343c96fd864d33966e6ca86ed6454fe348c579812ed9c674cf39d1310f/X2H18086316_20240618155704.jpg'
 'https://filer.eco-counter-tools.com/file/4a/2e6127480864e11e9bd152969a114c01c26ea9434bdd7813bc618f511a21b04a/Y2H21015011_20220407110543.jpg'
 'https://filer.eco-counter-tools.com/file/16/35f6b42be906d8dc8ac074b0bfc2683cec4aa3aa4cff6e964ff4a73697ed8816/Y2H21015068_20240618150003.jpg'
 'https://filer.eco-counter-tools.com/file/31/7a51f8668baa67fe9fbc33f577ca62cffa13fab69148810676d42c23d007dc31/15374519009810.jpg']<br>
</p>
<p>Nom de la colonne: id_photo_1<br>
 Type : object<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 33582<br>
Pourcentage de valeurs manquantes : 3.79%<br>
Nb éléments utilisés plusieurs fois : 885242<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['https:' nan]<br>
</p>
<p>Nom de la colonne: url_sites<br>
 Type : object<br>
Nombre de valeurs uniques : 69<br>
Nombre de valeurs manquantes : 24533<br>
Pourcentage de valeurs manquantes : 2.77%<br>
Nb éléments utilisés plusieurs fois : 885174<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['https://www.eco-visio.net/Photos/100003098'
 'https://www.eco-visio.net/Photos/100006300'
 'https://www.eco-visio.net/Photos/100007049'
 'https://www.eco-visio.net/Photos/100036718'
 'https://www.eco-visio.net/Photos/100036719']<br>
</p>
<p>Nom de la colonne: type_dimage<br>
 Type : object<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 33582<br>
Pourcentage de valeurs manquantes : 3.79%<br>
Nb éléments utilisés plusieurs fois : 885242<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['jpg' nan]<br>
</p>
<p>Nom de la colonne: mois_annee_comptage<br>
 Type : object<br>
Nombre de valeurs uniques : 13<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 885231<br>
soit nb lignes avec un élément non unique : 885244<br>
Exemples de valeurs uniques :  ['2024-09' '2024-10' '2024-11' '2024-12' '2025-01']</p>
</div>

<hr class="page-break">

#### <a id="ann2b">Annexe 2b</a> : Structure du jeu de données météo

<div class="two-columns">
<p>Nom de la colonne: NUM_POSTE<br>
 Type : int64<br>
Nombre de valeurs uniques : 6<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 3870<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [75106001 75107005 75110001 75114001 75114007]<br>
</p>
<p>Nom de la colonne: NOM_USUEL<br>
 Type : object<br>
Nombre de valeurs uniques : 6<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 3870<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  ['LUXEMBOURG' 'TOUR EIFFEL' 'LARIBOISIERE' 'PARIS-MONTSOURIS'
 'PARIS-MONTSOURIS-DOUBLE']<br>
</p>
<p>Nom de la colonne: LAT<br>
 Type : float64<br>
Nombre de valeurs uniques : 5<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 3871<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [48.844667 48.858333 48.882833 48.821667 48.854833]<br>
</p>
<p>Nom de la colonne: LON<br>
 Type : float64<br>
Nombre de valeurs uniques : 5<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 3871<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [2.333833 2.2945   2.352    2.337833 2.233667]<br>
</p>
<p>Nom de la colonne: ALTI<br>
 Type : int64<br>
Nombre de valeurs uniques : 5<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 3871<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 46 330  55  75  27]<br>
</p>
<p>Nom de la colonne: AAAAMMJJ<br>
 Type : int64<br>
Nombre de valeurs uniques : 646<br>
Nombre de valeurs manquantes : 0<br>
Pourcentage de valeurs manquantes : 0.00%<br>
Nb éléments utilisés plusieurs fois : 3230<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [20240101 20240102 20240103 20240104 20240105]<br>
</p>
<p>Nom de la colonne: RR<br>
 Type : float64<br>
Nombre de valeurs uniques : 172<br>
Nombre de valeurs manquantes : 1292<br>
Pourcentage de valeurs manquantes : 33.33%<br>
Nb éléments utilisés plusieurs fois : 3703<br>
soit nb lignes avec un élément non unique : 3799<br>
Exemples de valeurs uniques :  [9.6 7.1 3.2 0.2 1. ]<br>
</p>
<p>Nom de la colonne: QRR<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 1292<br>
Pourcentage de valeurs manquantes : 33.33%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 1. nan]<br>
</p>
<p>Nom de la colonne: TN<br>
 Type : float64<br>
Nombre de valeurs uniques : 279<br>
Nombre de valeurs manquantes : 9<br>
Pourcentage de valeurs manquantes : 0.23%<br>
Nb éléments utilisés plusieurs fois : 3596<br>
soit nb lignes avec un élément non unique : 3858<br>
Exemples de valeurs uniques :  [ 6.8  9.  10.4  8.3  6.7]<br>
</p>
<p>Nom de la colonne: QTN<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 9<br>
Pourcentage de valeurs manquantes : 0.23%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3875<br>
Exemples de valeurs uniques :  [ 1. nan  0.]<br>
</p>
<p>Nom de la colonne: HTN<br>
 Type : float64<br>
Nombre de valeurs uniques : 902<br>
Nombre de valeurs manquantes : 20<br>
Pourcentage de valeurs manquantes : 0.52%<br>
Nb éléments utilisés plusieurs fois : 2973<br>
soit nb lignes avec un élément non unique : 3532<br>
Exemples de valeurs uniques :  [ 713. 2030. 1750.  801.  807.]<br>
</p>
<p>Nom de la colonne: QHTN<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 20<br>
Pourcentage de valeurs manquantes : 0.52%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 9. nan  1.]<br>
</p>
<p>Nom de la colonne: TX<br>
 Type : float64<br>
Nombre de valeurs uniques : 375<br>
Nombre de valeurs manquantes : 10<br>
Pourcentage de valeurs manquantes : 0.26%<br>
Nb éléments utilisés plusieurs fois : 3500<br>
soit nb lignes avec un élément non unique : 3833<br>
Exemples de valeurs uniques :  [11.5 12.7 13.  11.6 10.1]<br>
</p>
<p>Nom de la colonne: QTX<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 9<br>
Pourcentage de valeurs manquantes : 0.23%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 1. nan]<br>
</p>
<p>Nom de la colonne: HTX<br>
 Type : float64<br>
Nombre de valeurs uniques : 755<br>
Nombre de valeurs manquantes : 19<br>
Pourcentage de valeurs manquantes : 0.49%<br>
Nb éléments utilisés plusieurs fois : 3120<br>
soit nb lignes avec un élément non unique : 3613<br>
Exemples de valeurs uniques :  [ 301. 1850. 1137. 1406. 1136.]<br>
</p>
<p>Nom de la colonne: QHTX<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 18<br>
Pourcentage de valeurs manquantes : 0.46%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 9.  1. nan]<br>
</p>
<p>Nom de la colonne: TM<br>
 Type : float64<br>
Nombre de valeurs uniques : 319<br>
Nombre de valeurs manquantes : 21<br>
Pourcentage de valeurs manquantes : 0.54%<br>
Nb éléments utilisés plusieurs fois : 3556<br>
soit nb lignes avec un élément non unique : 3847<br>
Exemples de valeurs uniques :  [ 8.9 11.4 11.2 10.1  8.1]<br>
</p>
<p>Nom de la colonne: QTM<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 20<br>
Pourcentage de valeurs manquantes : 0.52%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3875<br>
Exemples de valeurs uniques :  [ 1. nan  9.]<br>
</p>
<p>Nom de la colonne: TNTXM<br>
 Type : float64<br>
Nombre de valeurs uniques : 317<br>
Nombre de valeurs manquantes : 10<br>
Pourcentage de valeurs manquantes : 0.26%<br>
Nb éléments utilisés plusieurs fois : 3558<br>
soit nb lignes avec un élément non unique : 3850<br>
Exemples de valeurs uniques :  [ 9.2 10.9 11.7 10.   8.4]<br>
</p>
<p>Nom de la colonne: QTNTXM<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 10<br>
Pourcentage de valeurs manquantes : 0.26%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 1. nan]<br>
</p>
<p>Nom de la colonne: TAMPLI<br>
 Type : float64<br>
Nombre de valeurs uniques : 199<br>
Nombre de valeurs manquantes : 10<br>
Pourcentage de valeurs manquantes : 0.26%<br>
Nb éléments utilisés plusieurs fois : 3676<br>
soit nb lignes avec un élément non unique : 3857<br>
Exemples de valeurs uniques :  [4.7 3.7 2.6 3.3 3.4]<br>
</p>
<p>Nom de la colonne: QTAMPLI<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 10<br>
Pourcentage de valeurs manquantes : 0.26%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 1. nan]<br>
</p>
<p>Nom de la colonne: TNSOL<br>
 Type : float64<br>
Nombre de valeurs uniques : 266<br>
Nombre de valeurs manquantes : 2586<br>
Pourcentage de valeurs manquantes : 66.72%<br>
Nb éléments utilisés plusieurs fois : 3609<br>
soit nb lignes avec un élément non unique : 3840<br>
Exemples de valeurs uniques :  [nan 4.  8.  7.8 5. ]<br>
</p>
<p>Nom de la colonne: QTNSOL<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 2586<br>
Pourcentage de valeurs manquantes : 66.72%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  9.  1.]<br>
</p>
<p>Nom de la colonne: TN50<br>
 Type : float64<br>
Nombre de valeurs uniques : 219<br>
Nombre de valeurs manquantes : 3232<br>
Pourcentage de valeurs manquantes : 83.38%<br>
Nb éléments utilisés plusieurs fois : 3656<br>
soit nb lignes avec un élément non unique : 3820<br>
Exemples de valeurs uniques :  [nan 5.4 8.  8.6 6.6]<br>
</p>
<p>Nom de la colonne: QTN50<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 3232<br>
Pourcentage de valeurs manquantes : 83.38%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  9.  1.]<br>
</p>
<p>Nom de la colonne: DG<br>
 Type : float64<br>
Nombre de valeurs uniques : 193<br>
Nombre de valeurs manquantes : 63<br>
Pourcentage de valeurs manquantes : 1.63%<br>
Nb éléments utilisés plusieurs fois : 3682<br>
soit nb lignes avec un élément non unique : 3707<br>
Exemples de valeurs uniques :  [   0. 1406. 1440. 1099.  987.]<br>
</p>
<p>Nom de la colonne: QDG<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 63<br>
Pourcentage de valeurs manquantes : 1.63%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ 9. nan  1.]<br>
</p>
<p>Nom de la colonne: FFM<br>
 Type : float64<br>
Nombre de valeurs uniques : 137<br>
Nombre de valeurs manquantes : 1939<br>
Pourcentage de valeurs manquantes : 50.03%<br>
Nb éléments utilisés plusieurs fois : 3738<br>
soit nb lignes avec un élément non unique : 3853<br>
Exemples de valeurs uniques :  [ nan 13.  16.5 15.3 12.1]<br></p>
<p>Nom de la colonne: QFFM<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 1939<br>
Pourcentage de valeurs manquantes : 50.03%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  1.]<br>
</p>
<p>Nom de la colonne: FF2M<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: QFF2M<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: FXY<br>
 Type : float64<br>
Nombre de valeurs uniques : 182<br>
Nombre de valeurs manquantes : 1988<br>
Pourcentage de valeurs manquantes : 51.29%<br>
Nb éléments utilisés plusieurs fois : 3693<br>
soit nb lignes avec un élément non unique : 3851<br>
Exemples de valeurs uniques :  [ nan 17.9 23.2 20.7 17.7]<br>
</p>
<p>Nom de la colonne: QFXY<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 1988<br>
Pourcentage de valeurs manquantes : 51.29%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  1.]<br>
</p>
<p>Nom de la colonne: DXY<br>
 Type : float64<br>
Nombre de valeurs uniques : 36<br>
Nombre de valeurs manquantes : 1988<br>
Pourcentage de valeurs manquantes : 51.29%<br>
Nb éléments utilisés plusieurs fois : 3839<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ nan 200. 210. 240. 250.]<br>
</p>
<p>Nom de la colonne: QDXY<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 1988<br>
Pourcentage de valeurs manquantes : 51.29%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  9.  1.]<br>
</p>
<p>Nom de la colonne: HXY<br>
 Type : float64<br>
Nombre de valeurs uniques : 1003<br>
Nombre de valeurs manquantes : 1988<br>
Pourcentage de valeurs manquantes : 51.29%<br>
Nb éléments utilisés plusieurs fois : 2872<br>
soit nb lignes avec un élément non unique : 3404<br>
Exemples de valeurs uniques :  [  nan 2226. 1403. 1343.   37.]<br>
</p>
<p>Nom de la colonne: QHXY<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 1988<br>
Pourcentage de valeurs manquantes : 51.29%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  9.  1.]<br>
</p>
<p>Nom de la colonne: FXI<br>
 Type : float64<br>
Nombre de valeurs uniques : 245<br>
Nombre de valeurs manquantes : 1939<br>
Pourcentage de valeurs manquantes : 50.03%<br>
Nb éléments utilisés plusieurs fois : 3630<br>
soit nb lignes avec un élément non unique : 3823<br>
Exemples de valeurs uniques :  [ nan 31.  36.7 29.2 31.7]<br>
</p>
<p>Nom de la colonne: QFXI<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 1939<br>
Pourcentage de valeurs manquantes : 50.03%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  1.]<br>
</p>
<p>Nom de la colonne: DXI<br>
 Type : float64<br>
Nombre de valeurs uniques : 36<br>
Nombre de valeurs manquantes : 1962<br>
Pourcentage de valeurs manquantes : 50.62%<br>
Nb éléments utilisés plusieurs fois : 3839<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [ nan 200. 210. 250. 230.]<br>
</p>
<p>Nom de la colonne: QDXI<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 1962<br>
Pourcentage de valeurs manquantes : 50.62%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  9.  1.]<br>
</p>
<p>Nom de la colonne: HXI<br>
 Type : float64<br>
Nombre de valeurs uniques : 990<br>
Nombre de valeurs manquantes : 1963<br>
Pourcentage de valeurs manquantes : 50.64%<br>
Nb éléments utilisés plusieurs fois : 2885<br>
soit nb lignes avec un élément non unique : 3409<br>
Exemples de valeurs uniques :  [  nan 2305. 1435. 1334. 1903.]<br>
</p>
<p>Nom de la colonne: QHXI<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 1963<br>
Pourcentage de valeurs manquantes : 50.64%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  9.  1.]<br>
</p>
<p>Nom de la colonne: FXI2<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: QFXI2<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: DXI2<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: QDXI2<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: HXI2<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: QHXI2<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: FXI3S<br>
 Type : float64<br>
Nombre de valeurs uniques : 221<br>
Nombre de valeurs manquantes : 1996<br>
Pourcentage de valeurs manquantes : 51.50%<br>
Nb éléments utilisés plusieurs fois : 3654<br>
soit nb lignes avec un élément non unique : 3833<br>
Exemples de valeurs uniques :  [ nan 29.4 33.2 27.9 30.3]<br>
</p>
<p>Nom de la colonne: QFXI3S<br>
 Type : float64<br>
Nombre de valeurs uniques : 1<br>
Nombre de valeurs manquantes : 1996<br>
Pourcentage de valeurs manquantes : 51.50%<br>
Nb éléments utilisés plusieurs fois : 3874<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  1.]<br>
</p>
<p>Nom de la colonne: DXI3S<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: QDXI3S<br>
 Type : float64<br>
Nombre de valeurs uniques : 0<br>
Nombre de valeurs manquantes : 3876<br>
Pourcentage de valeurs manquantes : 100.00%<br>
Nb éléments utilisés plusieurs fois : 3875<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan]<br>
</p>
<p>Nom de la colonne: HXI3S<br>
 Type : float64<br>
Nombre de valeurs uniques : 961<br>
Nombre de valeurs manquantes : 1997<br>
Pourcentage de valeurs manquantes : 51.52%<br>
Nb éléments utilisés plusieurs fois : 2914<br>
soit nb lignes avec un élément non unique : 3414<br>
Exemples de valeurs uniques :  [  nan 2305. 1356. 1334. 1903.]<br>
</p>
<p>Nom de la colonne: QHXI3S<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 1997<br>
Pourcentage de valeurs manquantes : 51.52%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  9.  1.]<br>
</p>
<p>Nom de la colonne: DRR<br>
 Type : float64<br>
Nombre de valeurs uniques : 233<br>
Nombre de valeurs manquantes : 3245<br>
Pourcentage de valeurs manquantes : 83.72%<br>
Nb éléments utilisés plusieurs fois : 3642<br>
soit nb lignes avec un élément non unique : 3724<br>
Exemples de valeurs uniques :  [ nan 647. 692. 265.  18.]<br>
</p>
<p>Nom de la colonne: QDRR<br>
 Type : float64<br>
Nombre de valeurs uniques : 2<br>
Nombre de valeurs manquantes : 3235<br>
Pourcentage de valeurs manquantes : 83.46%<br>
Nb éléments utilisés plusieurs fois : 3873<br>
soit nb lignes avec un élément non unique : 3876<br>
Exemples de valeurs uniques :  [nan  1.  9.]</p>
</div>

<hr class="page-break">

#### <a id="ann2c">Annexe 2c</a> : Notice du jeu de données du baromètre FUB

<div style="text-align:center;">  
  <figure style="display:inline-block; width:92%;">
    <img src="images/notbaro1.png" alt="notice baromètre FUB page 1" style="width:100%; display:block;">
  </figure>
</div>

<div style="text-align:center;">  
  <figure style="display:inline-block; width:85%;">
    <img src="images/notbaro2.png" alt="notice baromètre FUB page 2" style="width:100%; display:block;">
  </figure>
</div>

<div style="text-align:center;">  
  <figure style="display:inline-block; width:85%;">
    <img src="images/notbaro3.png" alt="notice baromètre FUB page 3" style="width:100%; display:block;">
  </figure>
</div>

<div style="text-align:center;">  
  <figure style="display:inline-block; width:100%;">
    <img src="images/notbaro4.png" alt="notice baromètre FUB page 4" style="width:100%; display:block;">
  </figure>
</div>

<hr class="page-break">

### <a id="ann3">Annexe 3</a> : Script "normalisation et lemmatisation des avis"

<hr class="page-break">

### <a id="ann4">Annexe 4</a> : Script "rayon de proximité" pour jointure géospatiale

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

### <a id="ann5">Annexe 5</a> : Transformation des noms de compteurs et sites de comptage

<hr class="page-break">

### <a id="ann6">Annexe 6</a> : Colonnes calculées de score météo

<hr class="page-break">

### <a id="ann7">Annexe 7</a> : Mesure DAX de calcul des sensibilités météo

<hr class="page-break">

### <a id="ann8">Annexe 8</a> : Mesure DAX de calcul des jours dépassant un seuil journalier

<hr class="page-break">

### <a id="ann9">Annexe 9</a> : Script "nuage de mot" dans Power BI
