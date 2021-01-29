# openvaccine_algoritm_prediction
ce document propose une étude pour la prédiction de la dégradation de l'ARNm du vaccin COVID-19 afin de trouver une séquence stable de cette molécule.

	1. Problématique générale du projet.
Pour gagner le combat contre la pandémie COVID-19, il faudra un vaccin efficace qui
peut être distribué équitablement et largement. S'appuyant sur des décennies de
recherche a permis aux scientifiques d'accélérer la recherche d'un vaccin contre le
COVID-19, mais chaque jour qui se passe sans vaccin a néanmoins des coûts énormes
pour le monde.

Les vaccins à ARNm ont pris les devants en tant que candidats vaccins les plus rapides
pour le COVID-19, mais actuellement, ils font face à des limitations potentielles clés.
L'un des plus grands défis à l'heure actuelle est de savoir comment concevoir des
molécules d'ARN messager (ARNm) super stables.

Les chercheurs ont observé que les molécules d'ARN ont tendance à se dégrader
spontanément, c'est une limitation sérieuse - une seule coupure peut rendre le vaccin à
ARNm inutile.
Actuellement, on sait peu de choses sur les détails de l'endroit où dans le squelette d'un
ARN donné est le plus susceptible d'être affecté.

L'amélioration de la stabilité des vaccins à ARNm était un problème qui était à l'étude
avant la pandémie mais qui devrait prendre de nombreuses années à résoudre.
Maintenant, nous devons résoudre ce défi scientifique profond en des mois, voire des
semaines, pour accélérer la recherche sur le vaccin à ARNm et fournir un vaccin stable
au réfrigérateur contre le SRAS-CoV-2, le virus derrière COVID-19.

	2. Cadre générale du projet 
Les vaccins à ARNm suscitent un intérêt croissant en tant qu'alternatives potentielles
aux méthodes conventionnelles pour la prévention de plusieurs maladies, y compris
Covid-19, ce virus n'a besoin d'aucune introduction, il a déjà tué des millions de
personnes dans le monde.
	
Le but de cette compétition était de prédire, pour chacune des bases (A, C, G ou U) des
séquences d'ARN fournies, la réactivité et la dégradation dans certaines circonstances
comme l'incubation avec ou sans magnésium à haute température ou à pH élevé. En
résumé, nous devons prédire trois valeurs continues (c.-à-d. Régression) pour chacune
des bases de la séquence (c.-à-d. Séquence à séquence).
Cet article propose et évalue trois modèles d'apprentissage (GRU, CNN et T-SNE)
comme méthode pour prédire la stabilité / réactivité et le risque de dégradation des séquences d'ARN. 
	3. Description du Dataset.
	
Kaggle prend en charge divers formats de publication d'ensembles de données, mais elle
recommande vivement les éditeurs d'ensembles de données à partager leurs données
dans un format accessible et non propriétaire si possible. Non seulement les formats de
données ouverts et accessibles sont mieux pris en charge sur la plateforme, mais ils sont
également plus faciles à utiliser pour un plus grand nombre de personnes, quels que
soient leurs outils.

Dans cette compétition, il faut prédire les taux de dégradation à divers endroits le long
de la séquence d'ARN.

a. Types de fichiers pris en charge
• CSVs
Le type de fichier le plus simple et le mieux pris en charge disponible sur Kaggle est la
« Liste séparée par des virgules », ou CSV, pour les données tabulaires. Les fichiers
CSV téléchargés sur Kaggle doivent avoir une ligne d'en-tête composée de noms de 
champs lisibles par l'homme. Une représentation CSV d'une liste de courses avec une
ligne d'en-tête.
Les CSV sont les formats de fichiers les plus courants disponibles sur Kaggle et
constituent le meilleur choix pour les données tabulaires.
• JSON
Alors que CSV est le format de fichier le plus courant pour les données "plates", JSON
est le format de fichier le plus courant pour les données "arborescentes" qui ont
potentiellement plusieurs couches.
Pour les fichiers JSON, l'aperçu de l'onglet Données présentera un arbre interactif avec
les nœuds du fichier JSON en pièce jointe. Vous pouvez cliquer sur des touches
individuelles pour ouvrir et réduire des sections de l'arbre, en explorant la structure de
l'ensemble de données au fur et à mesure. Les fichiers JSON ne prennent pas en charge
les descriptions de colonnes ou les métriques.
• SQLite
Kaggle prend en charge les fichiers de base de données en utilisant le format léger
SQLite. Les bases de données SQLite sont constituées de plusieurs tables, chacune
contenant des données au format tabulaire. Ces tableaux prennent mieux en charge les
grands ensembles de données que les fichiers CSV, mais sont par ailleurs similaires dans
la pratique.
L'onglet Données représente chaque table d'une base de données séparément. Tout
comme les fichiers CSV, les tables SQLite seront entièrement remplies par les sections.
• Archives
Bien qu'il ne s'agisse pas techniquement d'un format de fichier en soi, Kaggle prend
également en charge les fichiers compressés au format ZIP ainsi que d'autres formats
d'archives courants comme 7z.
Les fichiers compressés prennent moins d'espace sur le disque que les fichiers non
compressés, ce qui les rend beaucoup plus rapides à télécharger dans Kaggle et vous
permet de télécharger des ensembles de données qui, autrement, dépasseraient les
limites de taille des ensembles de données.
• BigQuery
Kaggle prend également en charge les ensembles de données BigQuery spéciaux.
BigQuery est un magasin SQL « big data » inventé par Google. De nombreux ensembles
de données publics massifs, comme tout le code de GitHub et l'historique complet de la
blockchain Bitcoin, sont disponibles publiquement via l'initiative Google BigQuery
Public Datasets. Certains d'entre eux sont également disponibles sous forme de dataset.
c. Dataset utilise
Dans cette compétition, vous prédirez les taux de dégradation à divers endroits le long
de la séquence d'ARN.
Il existe plusieurs valeurs de vérité terrain fournies dans les données d'apprentissage.
Alors que le format de soumission nécessite que les 5 soient prédits, seuls les éléments
suivants sont notés : réactivité, deg_Mg_pH10 et deg_Mg_50C.
• Fichiers
Il existe 3 types fichiers utilise :
✓ train.json - les données d'entraînement
✓ test.json - l'ensemble de test, sans aucune colonne associée à la vérité terrain.
✓ sample_submission.csv - un exemple de fichier de soumission au format correct.
Nous utiliserons 3 types de fichiers JSON et CSV
• Colonnes
Dans le tableau ci-dessous nous présentons les différents attributs du Dataset
Attribut Description de l’attribut
id Un identifiant arbitraire pour chaque échantillon
seq_scored
Valeur entière indiquant le nombre de positions utilisées dans la notation avec
des valeurs prédites.
seq_length Valeurs entières indique la longueur de la séquence.
sequence
Décrit la séquence d'ARN, une combinaison de A, G, U et C pour chaque
échantillon.
structure
Un tableau de (,) et. Caractères qui décrivent si une base est estimée être
appariée ou non appariée. Les bases appariées sont indiquées par des
parenthèses ouvrantes et fermantes,
reactivity
Un tableau de nombres à virgule flottante Date d’entrée Ces nombres sont
utilisés pour déterminer la structure secondaire probable de l'échantillon d’ARN.
deg_pH10
Un tableau de nombres à virgule flottante. Ces nombres sont utilisés pour
déterminer la probabilité de dégradation au niveau de la base / liaison après
incubation sans magnésium à pH élevé (pH 10).
deg_Mg_pH10
Un tableau de nombres à virgule flottante. Ces nombres sont utilisés pour
déterminer la probabilité de dégradation à la base / liaison après incubation avec
du magnésium à pH élevé (pH 10)
deg_50C
Un tableau de nombres à virgule flottante. Ces nombres sont utilisés pour
déterminer la probabilité de dégradation au niveau de la base / liaison après
incubation sans magnésium à haute température (50 degrés Celsius).
deg_Mg_50C
Un tableau de nombres à virgule flottante. Ces nombres sont utilisés pour
déterminer la probabilité de dégradation au niveau de la base / liaison après
incubation avec du magnésium à haute température (50 degrés Celsius).
*_error_*
	
	5. Outils d’études.
a. Python
Python est un langage orienté objet bénéficiant d’une syntaxe précise et
efficace, interprété, multi-paradigme et multiplateformes. Il favorise la programmation
impérative structurée, fonctionnelle et orientée objet. Il est doté d'un typage
dynamique fort, d'une gestion automatique de la mémoire par ramasse-miettes et
d'un système de gestion d'exceptions, il est ainsi similaire à Perl, Ruby, Scheme,
Smalltalk et Tcl.
Un programme écrit en Python n'est opérationnel que si l'interpréteur est disponible sur
la machine (bien que des solutions de compilation existent). En contrepartie, il peut
fonctionner dès lors que l'interpréteur est présent, quel que soit le système d'exploitation
de la machine. Sous cet angle, on peut le considérer comme un langage multiplateforme.
b. Avantage d’utilisation de python
La syntaxe de Python est simple et claire, elle respecte les standards du domaine. Python
propose les principales fonctionnalités de la programmation (actions conditionnelles,
boucles, programmation modulaire), y compris les mécanismes de classes (héritage,
surcharge des méthodes, polymorphisme). Python se marie très bien avec un cours
d'algorithmie.
La distribution Python intègre un grand nombre de librairies. Elles couvrent un large
choix de domaines (bases de données, accès réseaux, multimédia, traitements systèmes,
compression, multithreading, ...).
Il est couramment utilisé par les Data Scientists grâce à ses librairies d’analyse
numérique et de calcul scientifique (numpy, scipy, pandas) et de visualisation
(matplotlib), mais surtout grâce à sa puissante librairie dédiée au Machine
Learning, scikit-learn.

