<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8"/>
    <title>Trafic cycliste à Paris de septembre 2024 à octobre 2025</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="author" content="Marie Berthiau"/>
    <meta name="description" content="Rapport final individuel de projet dans le cadre de la formation Data Analyst de DataScientest"/>
</head>
<body>
    <div><center><img src=".\images\pont_concorde.png" style="height:200px"></center></div>
    <h1>Trafic cycliste à Paris de septembre 2024 à octobre 2025</h1>


#

Pour répondre à ces questions, il faut parler de trafic induit : c’est l’aménagement qui entraîne l’augmentation du trafic et non l’inverse :
En l’absence de pont, pas de nageur pour traverser un fleuve, cela ne veut pas dire qu’un pont est inutile. Les études scientifiques le prouvent, l’ajout d’une voie de circulation ne “fluidifie” jamais le trafic, elle l’augmente toujours, quel que soit le moyen de déplacement.
La part modale du vélo à Paris, qui a connu un doublement entre 2015 et entre 2020 tourne aujourd’hui autour de 10%, ce qui reste relativement faible et donc améliorable, un flux faible dans une rue sur laquelle un compteur est installé est donc un flux à augmenté (l’installation du compteur étant une preuve de la volonté de suivre le développement en ce point).





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

## Bibliographie

### Déplacements à Paris

[Bilan des déplacements à Paris en 2024 - page web Ville de Paris - oct 2025](https://www.paris.fr/pages/le-bilan-des-deplacement-a-paris-en-2024-31371)

[Les déplacements en vélo à Paris en 2024 - Edition Ville de Paris - 2025](https://cdn.paris.fr/paris/2025/06/02/paris_ra2024-deplacements-en-velo-8-pages-26-05-copie-3dZs.pdf)

### Qualité des aménagements cyclables (Guides officiels )

[Annexe 3 : Note de recommendations techniques du CEREMA](https://www.ecologie.gouv.fr/sites/default/files/documents/Annexe%203%20%20Recommandations%20techniques%20du%20CEREMA.pdf)

[Guide de conception des aménagements cyclables - Métropole de Lyon - 2019](https://www.grandlyon.com/fileadmin/user_upload/media/pdf/voirie/20190621_guide-amenagement-cyclable.pdf)

[Guide des aménagements cyclables - Direction de la Voirie des tdes Déplacements de la Ville de Paris - 16/06/2023](https://cdn.paris.fr/paris/2024/09/30/guide-amenagements-cyclables-partie-1-generalites-hors-dsc-juin-2024-light-CFZy.pdf)

### Paris en Selle <img src=".\images\logo_pes.png" style="height:100px">

[Plateforme dédiée aux compteurs vélo](https://parisenselle.fr/2020/10/06/une-plateforme-pour-recenser-les-compteurs-velo/#:~:text=Nous%20sommes%20heureux%20de%20vous%20pr%C3%A9senter%20https%3A%2F%2Fcompteurs.parisenselle.fr%2C%20qui,grand%20merci%20%C3%A0%20Tristram%20pour%20ce%20gros%20boulot.)

Qualité des aménagements cyclables (nombreuses photos et exemples) pour la compréhension des sites de comptage :
[Guide des aménagements cyclables - Edition : Paris en Selle - mise à jour de 20121](https://parisenselle.fr/telecharger-guide-amenagements-cyclables/) => 

### Seuils de saturation des bandes et pistes cyclables

[8 recommandation pou réussir votre piste cyclable - Actualités du Cerema - 24/02/2021](https://www.cerema.fr/fr/actualites/8-recommandations-reussir-votre-piste-cyclable) => seuils de saturation des bandes et pistes cyclables

### Compréhension des fonctionnement des capteurs

[Données de mobilité pour la modélisation des déplacements - fiche n°9 : données issues des capteurs routiers - Edition : Cerema - 2025](https://doc.cerema.fr/Default/doc/SYRACUSE/605087/donnees-de-mobilite-pour-la-modelisation-des-deplacements-fiche-n-9-donnees-issues-des-capteurs-rout)

[[Technologies de comptage proposées pour les cyclistes par eco-compteur - page web - 2025]](https://www.eco-compteur.com/solutions/produits/)


[Etude de simulation dynamique de trafic : guide de réalisation - Edition : Cerema - 2015](https://doc.cerema.fr/Default/doc/SYRACUSE/14114/etudes-de-simulation-dynamique-de-trafic-guide-de-realisation) => perspectives (analyse dynamique des flux)

## Documentation technique complémentaire

[[Librairie SpaCy en français - page web - oct 2025]](https://spacy.io/models/fr)

[[Créer un script Python pour Power Bi - page Web Microsoft Learn - oct 2025]](https://learn.microsoft.com/fr-fr/power-bi/connect-data/desktop-python-scripts)

## Annexes - extrait de code


### Annexe 1 : Script "normalisation et lemmatisation des avis"

### Annexe 2 : Script "nuage de mot" dans Power BI

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

### Annexe 3 :
 Mesure DAX de calcul des sensibilités météo

</body>
</html>