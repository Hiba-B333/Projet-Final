**Le 27 novembre 2023**<br>
**CMN 4500**<br>
**Hiba Belmaalem**<br> 
**Présenté à Jean-Sébastien Marier**<br>

# Projet 2 : Analyse et de visualisation de données simples

## Avant-propos
Dans le cadre du cours CMN 4500 Jounalisme numérique II, nous avons procéder par extraire des données d'un jeu de données disponible au niveau du site web de la ville d'Ottawa afin d'en extraire une histoire.

## 1. Introduction
Nous allons analyser un jeu de données de la ville d'Ottawa. Ce jeu de données est un sous-ensemble d'un jeu de données de la Ville  appelé « Demandes mensuelles de service en 2023 ». Les données offrent une vue d'ensemble des demandes de service nécessitant une intervention du personnel de la Ville, elles sont présentées par quartier, indiquent le service municipal responsable, et fournissent une description des demandes de service. Ces demandes peuvent provenir de résidents par les moyens suivants: Centre d’appels 311, Centres du service à la clientèle, Courriel au 311,  Portail Web en libre-service. Les données sont mises à jour  de manière mensuelle.
En d'autres termes, les données sont des plaintes et requêtes de particuliers, reçus au niveau du Service des Règlements Municipaux de la ville d'Ottawa. Ces dernières proviennent soit du site web de la Ville d'Ottawa où d'appels ou encore l'application éléctronique de la ville. Ces plaintes touchent majoritairement les problèmes causés par des animaux domestiques (Chats, chiens, etc.).

Le jeu de données orginal provient du [Portail de données ouvertes de la ville d'Ottawa](https://ouverte.ottawa.ca/datasets/demandes-mensuelles-de-service-en-2023/explore) et comportait près de 234 673 entrées, cependant, et comme mentionné ci-haut, nous allons nous concentrer sur les données pour le mois de janvier 2023. Le jeu de données réduit et abrégé que nous utilisons peut être accéder [ici](https://raw.githubusercontent.com/jsmarier/course-datasets/main/ottawa-311-service-requests-january-2023.csv).

Afin d'effectuer ce travail il nous faut tout d'abord les obtenir et importer notre jeu de données dans Google Feuilles de calcul. Nous allons par suite le nettoyer et l'analyser , trouver une histoire potentielle et créer une visualisation de ces données.

## 2. Obtenir les données

Pour obtenir le jeu données, nous les avons téléchargé à partir du document CSV précédement mentionné plus haut. Ensuite, nous avons ouvert une nouvelle feuille de calcul dans Google Feuille de calcul accessible [ici](https://docs.google.com/spreadsheets/d/18LAhyoRg6ZoHfws7tV3sDOFnfQk55sRMk-BhypLNG4Y/edit?usp=sharing), et avons procédé par les importer. Pour ce fait, il faut cliquer sur Fichier en haut à gauche, puis sur importer. Ensuite nous avons téléversé le document CSV dans la section Téléverser. Pour plus de détails voir les captures d'écran ci-dessous.

![](File-Import.png)<br>
*Figure 1 : Onglet fichier de Google Feuilles de calcul.*

![](Upload.png)<br>
*Figure 2 : La fenêtre d'importation d'un fichier de Google Feuilles de calcul.*


![](Jeudedonnées-projet%202.png)<br>
*Figure 3 : Apreçu du jeu de données des demandes mensuelles de service en janvier 2023 de la ville d'Ottawa.*

## Observations générales concernant le jeu de données 
* Le jeu de donnée comprend sept colones
* Le jeu de donnée comprend 26846 lignes
* Les demandes semblent touchées plusieurs secteurs des services de la ville
* Les données ne semblent pas propres, on peut voir qu'il y a des `00:00:00+00` inutles qui devaient forcément désigner l'heure à laquelle la demande a été faite dans la colone `DATE_RAISED` .
* Dans la colone SUBJECT on remarque que les demandes relatives à Corp Complaints ne proviennent d'aucun quartier
* La colone G intitulé ObjectId semble être inutile et d'aucun intérêt au jeu de donnée


## Observations spécifiques sur les colonnes B, D et F
* La colone B contient des variables catégoriques 
* La colone D contient des variables contient des variables numériques discrètes puisque puisque l'heure n'est pas précisée
* Les dates dans la colone D ne sont pas classées par ordre chronologique. Les réaranger pourrait donc influencer notre analyse et peut mettre en évidence de nouveaux paternes.
* La colone F contient des variables catégoriques nominales 

Quel est le ou quels sont les quartiers qui ont généré le plus de requêtes au mois de janvier  auprès de la ville Ottawa à propos d'aboiements de chien ?


## 3. Comprendre les données

### 3.1. Nettoyage des données
* Afin de répondre à la question précédente, il nous faut tout d'abord analyser les données que l'on a en suivant l'approche VIMA. 
Nous avons entre nos mains des données que l’on considère exactes puisqu'elles décrivent adéquatement le phénomène qu'elles sont conçues pour mesurer ou représenter (Statistiques Canada, 2021). L'acronyme VIMA  signifie Valides, Invalides, Manquantes et Aberrantes (Statistiques Canada, 2021), nous allons donc procédé par évaluer l'exatitude des données que nous avons.

#### 3.1.1 Analyse de bases des données

* Il semblerait y avoir 12 valeurs uniques valides dans la colonne A faisant référence à 12 sujets distincts, ce qui semble adéquat
* La colonne E a quatre valeurs uniques valides mais semble avoir 24 valeurs manquantes selon l’outil statistique de colonnes.
* La colonne F comprend 53 valeurs uniques qui désignent 53 quartiers, ce qui est raisonnable pour une ville comme Ottawa
* Le jeu de données ne semble pas avoir de données aberrantes
* La colonne F compte près de 1382 valeurs manquantes, ce qui ne semble pas très normal
* Les 00:00:00+00 dans la colonne D sont des valeurs invalides puisqu’elles se répètent tout au long de la colonne et ne donne aucune information pertinente

#### 3.1.2 Nettoyage des données
* Nous avons tout d'abord commencer par figer la première ligne du tableau 
* Les données de la colonne B nous semblent être de trop et seront donc supprimées, nous sommes plus intéressés par le détail du type de la demande plutôt que sa raison
* La colonne F est aussi supprimée car elle ne nous servira pas dans notre analyse
* Dans la colonne C et en utilisant l’outil de recherche avancée, nous avons élever les ​​ 00:00:00+00 à côté des dates pour aérer le jeu de données. Pour ce fait nous avons fait une “control F”, puis nous avons cliqué au niveau des trois points à droite. Ensuite nous avons copié puis collé  00:00:00+00 dans la première case, et avons ajouté un espace dans la deuxième. Enfin, en cliquant sur tout remplacé, les  00:00:00+00 sont remplacés par un vide, aérant ainsi la colonne.
* Nous avons ajouté un filtre à la colonne A pour arranger les cellules par ordre alphabétique croissant (A à Z)
* Nous remarquons que certaines demandes ne sont pas assignées à des quartiers, nous allons donc les supprimer. Pour ce fait, nous avons ajouté un filtre à colonne E l’arranger par ordre alphabétique croissant (A à Z). Les demandes sans quartier apparaîtront à la fin.
* Certains quartiers ont un numéro de rue aussi, mais ce n’est pas le cas pour toute la colonne E.En utilisant la même méthode que celle pour supprimer 00:00:00+00, nous allons supprimer les numéros de rues présents dans certaines entrées dans la colonne.
* Nous avons par la suite enlevé les espaces de trop dans la colonne E en utilisant l'outil de nettoyage de données.
* Certaines entrées dans la colonne A n’ont pas de traduction et n’ont pas d’information pertinentes (ex:Additional ) dans la colonne B, nous les avons donc supprimées.
* Nous nous intéressons aux nombre d’appels effectués par quartier, nous avons précisé à partir du filtre de la colonne D que nous ne voulons que les valeurs Voice In.
* Nous avons par la suite utilisé la fonction split pour découper la colonne A. Nous n’avons pas besoin de la traduction des mots et ne voulons garder que ceux en français. De ce fait nous avons ajouté deux colonnes à droite de la colonne A et nous avons utilisé la fonction suivante :  `=SPLIT(A2,"|")`
Ensuite nous avons coupé et collé la cellule avec les données désirées et supprimé les deux autres.


### 3.2. Analyse exploratoire des données
Comme l'affirme Alden Chen (2021), La visualisation des données est un élément clé de nombreux projets de science des données. il est donc important de bien choisir les outils qui permetteront à nos données de parler, mais aussi de bien définir nos variables. Nous avons donc choisi dans ce cas la  variable WARD car elle représente les différents quartiers de la ville d’Ottawa. Faire l’analyse des données en fonction du quartier peut révéler  des tendances géographiques importantes, comme les zones les plus  touchées par les problèmes d’aboiements de chiens. En analysant les données par quartier, nous pouvons identifier des modèles ou des problèmes locaux qui pourront mieux informer les responsables municipaux sur les besoins spécifiques de chaque quartier.

D’autres part, la variable CHANNEL désigne le moyen par lequel les requêtes ont été soumises (par exemple, en ligne, par téléphone, etc.). Cette variable peut aider à fournir des informations sur la manière dont les ménages interagissent avec les services offerts par la ville. L'analyse du canal utilisé pour les requêtes peut révéler des préférences dans la communication, indiquer des lacunes dans l'accessibilité des services, ou montrer l'efficacité des différents canaux de communication.

Dans notre cas, nous cherchons à trouver si il y a une  corrélation entre  la fréquence des requêtes concernant les aboiements de chien dans différents quartiers et le canal de communication choisi pour les plaintes sur ce sujet.

![](Graphe-Google.png)<br>
*Figure 1: Le graphique créée avec Google Feuille de calcul.*


## 4. Publier les données

Nous avons utilisé les données présentes dans le tableau croisé dynamique présent dans la Google feuille de calcul. Nous avons sélectionné nos données présentes dans le tableau croisé dynamique  (y compris la ligne/colonne d'en-tête) au niveau de notre feuille de calcul Google et l'avons collé les dans le champ de texte. Ensuite, nous avons rectifié quelques coquilles de formatage à l’aide des outils de DataWrapper. Les données que nous avons sont des variables nominales catégorielles, un graphique à barres empilées était la meilleure option pour visualiser nos données. En effet,un diagramme à barres empilées est un outil efficace pour présenter une vue d'ensemble claire et compréhensible des données impliquant plusieurs variables catégorielles, permet une analyse nuancée et facilite l'identification de modèles spécifiques ou d'écarts intéressants dans les données. (Statistiques Canada, 2021).
La palette de couleur choisie est la suivante: Le rouge représente Voice In, jaune la donnée WAP, la couleur cyan représente la donnée WEB, la couleur gris représente le Grand total. Ces couleurs attirent l’attention sans pour autant heurter les yeux des usagers, en particulier ceux qui souffrent de problèmes de vue. Nous avons aussi déplacé les étiquettes sur une ligne séparée et avons réarrangé les lignes de manière décroissante.  

![](DATAWRAPPER-PROJET2.png)<br>
*Figure 2 : Le graphique créée avec Datawrapper.*
[Version interactive ici](https://www.datawrapper.de/_/s69lE/)

## 5. Conclusion

L’analyse approfondie des plaintes pour aboiements de chiens par quartier et canal de communication offre un aperçu du des défis auxquels les communautés sont confrontées. En effet, en analysant les plaintes par quartier, on peut identifier les zones avec un nombre élevé de plaintes, ce qui pourrait indiquer des problèmes locaux spécifiques, tels qu’un manque d'espaces ouverts pour les chiens, un nombre élevé de propriétaires de chiens dans certains quartiers, ou d'autres facteurs environnementaux et sociaux. Cette analyse peut de plus montrer quels canaux de communication sont préférés dans certains quartiers. 
Elle aiderait aussi  les administrations municipales à allouer les ressources de manière plus ciblée, à développer des stratégies de communication plus efficaces, et à initier des programmes de sensibilisation et d'éducation adaptés. Cela contribue non seulement à améliorer la gestion des plaintes, mais aussi à renforcer la relation entre les citoyens et les services municipaux, en assurant une réponse plus réactive et adaptée aux besoins de la communauté.

## 6. Références

 * Alden, Chen.(2021).*Créer des visualisations de données convaincantes*. Statistiques Canada. [https://www.statcan.gc.ca/fr/science-donnees/reseau/visualisations-donnees](https://www.statcan.gc.ca/fr/science-donnees/reseau/visualisations-donnees)
 * *Exactitude et validation des données : méthodes pour assurer la qualité des données* (2021). Statistique Canada 
 [https://www.statcan.gc.ca/fr/afc/litteratie-donnees/catalogue/892000062020008](https://www.statcan.gc.ca/fr/afc/litteratie-donnees/catalogue/892000062020008)
 * *Les statistiques : le pouvoir des données!*.(2021). Satistique Canada
 [https://www150.statcan.gc.ca/n1/edu/power-pouvoir/toc-tdm/5214718-fra.htm](https://www150.statcan.gc.ca/n1/edu/power-pouvoir/toc-tdm/5214718-fra.htm)

[jeu de données-projet2]: jeudedonnées-projet2.png