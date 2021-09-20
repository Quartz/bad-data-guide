# Le guide de Quartz pour résoudre les problèmes de qualité des données

**Une liste des problèmes pouvant être rencontrés dans des jeux de données et des suggestions pour les résoudre.**

En tant que journaliste, vous êtes amenés à travailler de plus en plus avec des données. Mais celles-ci ne sont pas toujours d’une qualité suffisante pour être exploitées. Ce guide présente des descriptions détaillées des problèmes relatifs à la qualité des données et suggère des solutions pour résoudre une large part des problèmes rencontrés.

La plupart de ces problèmes peuvent être résolus. Lorsque cela n’est pas possible, cela signifie que les données seront inutilisables. Dans certains cas, une solution est possible mais moyennant quelques précautions. De manière à tenir compte de ces ambigüités, ce guide est organisé en fonction de la personne la plus adéquate pour résoudre le problème : vous, votre source, un expert, etc. Vous trouverez également des suggestions sur ce qu’il est possible de faire lorsqu’il n’est pas possible de trouver une personne-ressource.

C'est en vous familiarisant avec les types de problèmes que vous êtes susceptibles de rencontrer que vous aurez les meilleures chances de les identifier. Prévenir, c'est guérir ! 

Pour toute question à propos de ce guide ou proposer une traduction dans votre langue, contactez, en anglais, [Chris](mailto:chrisgroskopf@gmail.com).

Ce document est sous licence [Creative Commons Attribution-Pas d'utilisation commerciale 4.0 License Internationale](http://creativecommons.org/licenses/by-nc/4.0/). Send your pull requests!

# Traductions

* [Anglais - version originale](https://github.com/Quartz/bad-data-guide)
* [Chinois](http://djchina.org/2016/07/12/bad_data_guide/) (complet)
* [Chinois](http://cn.gijn.org/2016/01/10/quartz%E5%9D%8F%E6%95%B0%E6%8D%AE%E6%8C%87%E5%8D%97%E7%B2%BE%E9%80%89%EF%BC%9A%E5%A4%84%E7%90%86%E6%95%B0%E6%8D%AE%E7%9A%84%E6%AD%A3%E7%A1%AE%E6%96%B9%E5%BC%8F%E4%B8%80%E8%A7%88/) (partiel)
* [Japonais](https://github.com/piyo-ko/bad-data-guide/blob/master/README_ja.md)
* [Portugais](http://escoladedados.org/2016/09/08/guia-quartz-para-limpeza-de-dados/)
* [Espagnol](http://es.schoolofdata.org/guia-quartz/)

# Index

## Problèmes que vos sources peuvent vous aider à résoudre

* [Valeurs manquantes](#valeurs-manquantes)
* [Valeurs manquantes remplacées par zéro](#zeros-remplacent-valeurs-manquantes)
* [Données manquantes mais existantes](#donnees-existantes-manquantes)
* [Lignes ou valeurs dupliquées](#lignes-ou-valeurs-dupliquees)
* [Incohérence orthographique](#incoherence-orthographique)
* [Incohérence dans l'ordre des noms](#incoherence-ordre-des-noms)
* [Incohérence des formats de date](#incoherence-formats-de-date)
* [Type de valeur non spécifié](#type-de-valeur-non-specifie)
* [Catégories mal choisies](#mauvais-choix-categorie)
* [Etiquetage des colonnes ambigu](#etiquetage-ambigu)
* [Provenance non documentée](#provenance-non-documentee)
* [Présence de valeurs suspectes](#valeurs-suspectes)
* [Données trop grossières](#donnees-grossieres)
* [Les totaux diffèrent des agrégats publiés](#totaux-differents-agregats)
* [La feuille de calcul comporte 65.536 lignes](#nombre-de-lignes-eleve)
* [La feuille de calcul comporte 255 colonnes](#nombre-de-colonnes-eleve)
* [La feuille de calcul comporte des dates en 1900 ou 1904](#ecarts-dates)
* [Textes convertis en nombres](#textes-en-nombres)
* [Numéros stockés en tant que texte](#nombres-en-textes)

## Problèmes que vous pouvez résoudre

* [Problème d'encodage](#texte-confus)
* [Les fins de ligne sont confuses/brouillées](#fin-de-lignes-confuses)
* [Données au format PDF](#donnees-pdf)
* [Données trop granulaires](#donnees-granulaires)
* [Encodage humain des données](#encodage-humain)
* [Données mélangées avec le formatage et les annotations](#donnees-melangees-formatage-annotations)
* [Agrégations calculées avec des valeurs manquantes](#agregations-valeurs-manquantes)
* [Echantillon non aléatoire](#echantillon-non-aleatoire)
* [Marge d'erreur trop importante](#marge-d-erreur-trop-importante)
* [Marge d'erreur inconnue](#marge-d-erreur-inconnue)
* [Echantillon biaisé](#echantillon-biaise)
* [Données éditées manuellement](#donnees-editees-manuellement)
* [L'inflation fausse les données](#inflation-fausse-donnees)
* [Des variations naturelles / saisonnières faussent les données](#donnees-saisonnieres-faussent-donnees)
* [Manipulation des périodes de temps](#manipulation-periodes-temps)
* [Manipulation du cadre de référence](#manipulation-cadre-reference)

## Problèmes qu'un expert peut vous aider à résoudre

* [Source ou auteur non fiables](#auteur-non-fiable)
* [Opacité du processus de collecte des données](#opacite-processus-collecte)
* [Précision irréaliste des données](#assertions-irrealistes)
* [Valeurs aberrantes inexplicables](#valeurs-aberrantes-inexplicables)
* [Un index masque la variation sous-jacente](#variation-masquee)
* [Résultats piratés](#resultats-pirates)
* [Echec de la loi de Benford](#echec-loi-benford)
* [Trop bon pour être vrai](#trop-bon-pour-etre-vrai)

## Problèmes qu'un développeur peut vous aider à résoudre

* [Données agrégées dans une mauvaise catégorie ou zone géographique](#donnees-agregees-mauvaise-categorie)
* [Données dans un document scanné](#donnees-dans-document-scanne)

# Liste détaillée de tous les problèmes relatifs à la qualité des données

## Problèmes que vos sources peuvent vous aider à résoudre

### Valeurs manquantes

Méfiez-vous des valeurs vides ou « nulles » dans un jeu de données, à moins que vous ne soyez certain de savoir ce qu'elles signifient. Si les données sont annuelles, la valeur de cette année n'a-t-elle jamais été collectée ? Si c'est un sondage, un répondant a-t-il refusé de répondre à la question ?

Chaque fois que vous travaillez avec des jeux de données qui comportent des valeurs manquantes, vous devriez vous demander : « Est-ce que je sais ce que signifie l'absence de cette valeur ? » Si la réponse est non, vous devriez demander à votre source pourquoi ces valeurs sont manquantes.

### Valeurs manquantes remplacées par zéro

Il y a pire qu’une valeur manquante : lorsque celle-ci est remplacée par une valeur arbitraire. Cela peut être le fait d’un humain qui n’a pas réfléchi aux implications de ce remplacement ou cela peut se produire dans le résultat d’un processus automatisé qui n’avait pas été paramétré pour gérer les valeurs nulles. Si vous voyez des valeurs « zéro » (ou nulles), demandez-vous si elles sont vraiment nulles ou ce qu’elles peuvent signifier. Si vous n’en n’êtes pas certain, interrogez la source des données (idéalement, le producteur plutôt que le diffuseur car il s’agit de la source primaire des données).

La même prudence doit être de rigueur pour toute autre valeur non numérique où un « 0 » peut être représenté d'une autre manière. Par exemple, une valeur fausse '0' pour une date est souvent affichée en tant que' 1970-01-01T00: 00: 00Z' ou '1969-12-31T24: 59: 59Z' - ce format date de [l'époque Unix pour les horodatages] (https: //en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number). En matière de géolocalisation, cela peut conduire à la représentation de localisations erronées telles que "0 ° 00'00.0" N + 0 ° 00'00.0 "E" ou simplement "0 ° N 0 ° E" qui est un point qui se trouve dans l'océan Atlantique, au sud du Ghana aussi appelé [Null Island] (https://en.wikipedia.org/wiki/Null_Island).
Voir aussi:

* [Présence de valeurs suspectes](#valeurs-suspectes)
* [La feuille de calcul comporte des dates en 1900 ou 1904](#ecarts-dates)

### Données manquantes mais existantes

Des données sont parfois manquantes dans un jeu de données. Il est toutefois possible de vérifier la complétude d’un jeu de données : par exemple, vous disposez d’un jeu de données à propos des Etats-Unis, vous pouvez donc contrôler que les 50 états y sont représentés. Si vous traitez des jeux de données à propos d’équipes sportives, assurez-vous d’y trouver le nom de tous les joueurs ou de toutes les équipes attendues dans le jeu de données. Faites confiance à votre intuition si vous pensez que des données sont manquantes et vérifiez auprès de votre source.

### Lignes ou valeurs dupliquées

Si la même ligne apparaît plus d'une fois dans votre jeu de données, vous devriez savoir pourquoi. Il peut s’agir de données dupliquées ou de lignes utilisant les mêmes identifiants uniques. Si vous n’en connaissez pas la raison, toute opération de calcul effectuée à partir de ces données sera erronée. Dans ce cas, demandez des précisions à votre source.

### Incohérence orthographique

L'orthographe est l'un des moyens les plus évidents de savoir si les données ont été compilées à la main. Ne regardez pas seulement les noms des personnes, c'est souvent l'endroit le plus difficile pour détecter les fautes d'orthographe. Cherchez plutôt des endroits où les noms de villes ou les états ne sont pas cohérents. (« Los Angelos » est une erreur très commune.) Si vous les trouvez, vous pouvez être certain que les données ont été compilées ou éditées à la main : c’est donc une raison pour être sceptique. Les données qui ont été éditées à la main sont les plus susceptibles de comporter des erreurs. Cela ne signifie pas que vous ne devriez pas les utiliser mais que vous devriez peut-être corriger ces erreurs manuellement ou en tenir compte dans vos analyses.

[OpenRefine](http://openrefine.org/) est utile pour le [clustering de texte (text clustering)] (https://github.com/OpenRefine/OpenRefine/wiki/Clustering) qui peut aider à rationaliser le processus de correction orthographique en suggérant des correspondances proches entre des valeurs incohérentes dans une colonne (par exemple, en associant « Los Angelos » à « Los Angeles »). Assurez-vous toutefois de [documenter les modifications que vous apportez] (https://github.com/OpenRefine/OpenRefine/wiki/Exporters) afin de documenter [la provenance des données] (# provenance-non-documenté).


Voir aussi : 

* [Encodage humain des données](#encodage-humain)

### Incohérence dans l'ordre des noms

Vos données comportent-elles des noms de pays du Moyen-Orient ou d'Asie de l'Est ? Etes-vous certain que les noms de famille se trouvent toujours au même endroit ? Les producteurs de données se trompent habituellement dans ce type de noms. Si vous travaillez avec une liste de noms étrangers, vous devriez au moins procéder à un examen superficiel avant de supposer que les colonnes « first_name » et « last_name », par exemple, vous donnera quelque chose d’approprié à publier.

* [Encodage humain des données](#encodage-humain)

### Incohérence des formats de date

Quelle est la bonne date pour le mois de septembre ?

* '10/9/15'
* '9/10/15'

La permière date a été rédigée par un Européen et le seconde par un Américain : [les deux sont donc correctes] (https://en.wikipedia.org/wiki/Date_format_by_country). Mais sans connaître l'historique des données, vous ne pouvez pas en être certain à coup sûr. Sachez d'où proviennent vos données et assurez-vous qu'elles ont toutes été créées par des personnes du même continent.

* [Encodage humain des données](#encodage-humain)
* [Provenance non documentée](#provenance-non-documentee)

### Type de valeurs non spécifié

Ni le terme « poids » ni le terme « coût » ne donnent d'informations sur l'unité de mesure utilisée dans un jeu de données. Ne soyez pas trop prompts à supposer que les données produites aux États-Unis sont en livres et en dollars. Les données scientifiques sont souvent métriques. Les prix étrangers peuvent être spécifiés dans leur monnaie locale. Si les données n'épellent pas leurs unités, revenez à votre source. Même si elle précise les unités utilisées, méfiez-vous toujours de significations qui ont pu évoluer dans le temps. Un dollar en 2010 n'est pas un dollar aujourd'hui. 

Voir aussi : 

* [Etiquetage des colonnes ambigu](#etiquetage-ambigu)
* [L'inflation fausse les données](#inflation-fausse-donnees)

### Catégories mal choisies

Méfiez-vous des valeurs qui prétendent être seulement vraies ou fausses mais qui ne le sont pas vraiment. C'est souvent le cas avec les enquêtes où les refus ou les non-réponses sont également des valeurs valables et significatives. Un autre problème consiste dans l'utilisation de n'importe quel type d'autre catégorie. Les mauvaises catégories peuvent également exclure artificiellement les données. Cela arrive souvent avec les statistiques de la criminalité. Le FBI a défini le crime de « viol » de différentes façons au fil du temps. En fait, ils ont fait un travail si médiocre pour déterminer ce qu'est le viol que de nombreux criminologues affirment que leurs statistiques ne devraient pas être utilisées du tout. Une mauvaise définition peut signifier qu'un crime est comptabilisé dans une catégorie différente de celle que vous attendiez ou qu'elle n'a pas été du tout prise en compte. Soyez à l'affût de ce type problème lorsque vous travaillez sur des sujets où les définitions ont tendance à être arbitraires, comme en matière d’origine ethnique.

### Etiquetage des colonnes ambigu

Qu'est-ce qu'une résidence ? Est-ce là où quelqu'un vit ou où il paie ses impôts ? Les étiquettes des colonnes (intitulé des variables) ne sont jamais aussi précises que nous le souhaiterions. Même si vous déduisez correctement ce que les valeurs sont censées signifier, cette ambiguïté pourrait facilement amener la personne qui collecte les données à entrer une valeur erronée.

### Provenance non documentée

Les jeux de données peuvent être créés par une variété de types d'individus et d'organisations, y compris les entreprises, les gouvernements, les organisations à but non lucratif et les théoriciens du complot. Les données sont recueillies de différentes façons, y compris via des enquêtes, des capteurs et des satellites. Le fait de savoir d'où proviennent vos données peut vous donner une bonne idée de leurs limites.

Les données d'enquête, par exemple, sont rarement exhaustives. Les capteurs varient dans leur précision. Les gouvernements sont souvent réticents à vous donner des informations impartiales. Les données provenant d'une zone de guerre peuvent comporter un fort biais géographique en raison du danger de traverser les lignes de bataille. Les données qui ont été écrites par un médecin peuvent être saisies par une infirmière. Chaque étape de la chaîne de collecte des données peut donner lieu à des erreurs. Vous devez savoir d’où proviennent les données que vous utilisez.

Voir aussi : 

* [Type de valeurs non spécifié](#type-de-valeur-non-specifie)

### Présence de valeurs suspectes

Si vous voyez l'une de ces valeurs dans vos données, traitez-les avec beaucoup de prudence :

Nombres :

* ['65,535'](https://en.wikipedia.org/wiki/65535_%28number%29)
* ['255'](https://en.wikipedia.org/wiki/255_%28number%29)
* ['2,147,483,647'](https://en.wikipedia.org/wiki/2147483647_%28number%29)
* ['4,294,967,295'](https://en.wikipedia.org/wiki/4294967295)
* ['555-3485'](https://en.wikipedia.org/wiki/555_%28telephone_number%29)
* '99999' (ou toute autre longue séquence de 9)
* '00000' (ou toute autre séquence de 0)

Dates :

* ['1970-01-01T00:00:00Z'](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number)
* ['1969-12-31T23:59:59Z'](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number)
* ['1er janvier 1900'](#ecarts-dates)

Localisations :

* ['0°00'00.0"N+0°00'00.0"E'](https://en.wikipedia.org/wiki/Null_Island) or simply ['0°N 0°E'](https://en.wikipedia.org/wiki/Null_Island)

Chacun de ces nombres donne l'indice d'une erreur particulière émanant d'un humain ou d'une machine. Si vous les voyez, assurez-vous qu'ils signifient réellement ce que vous pensez qu'ils veulent dire !

Pour en savoir plus sur la standardisation des formats de dates ou données de géolocalisation, consultez le blog de la traductrice de ce guide (@ohmyshambles) : [Qualité des données : standardiser, pourquoi et comment] (http://www.ohmybox.info/qualite-des-donnees-standardiser-pourquoi-et-comment/)

Voir aussi : 

* [La feuille de calcul comporte 65.536 lignes](#nombre-de-lignes-eleve)
* [La feuille de calcul comporte 255 colonnes](#nombre-de-colonnes-eleve)
* [La feuille de calcul comporte des dates en 1900 ou 1904](#ecarts-dates)

### Données trop grossières

Les données dont vous disposez vous proposent des états et vous avez besoin de régions. Vous disposez d’une liste d’employeurs alors que vous avez besoins de celle des employés. Vos données sont ventilées par année mais vous auriez préféré par mois. Dans de nombreux cas, les données ne rencontrent pas nos objectifs. Si vous recevez des données trop grossières, vous devriez demander à votre source des données plus spécifiques. 

Par ailleurs, vous ne devriez jamais diviser une valeur annuelle par 12 puis la nommer « moyenne par mois ». Sans connaître la distribution des valeurs, ce chiffre n'aura aucun sens.

Voir aussi : 

* [Données trop granulaires](#donnees-granulaires)
* [Données agrégées dans une mauvaise catégorie ou zone géographique](#donnees-agregees-mauvaise-categorie)

### Les totaux diffèrent des agrégats publiés

Imaginez que vous obteniez, après un long combat, une liste « complète » d’incidents liés à l’utilisation de la force par la police. Vous ouvrez le fichier et découvrez 2.467 lignes. Mais pas si vite ! Avant de publier quoi que ce soit à partir de ce jeu de données, essayez de retrouver la dernière fois où le chef de la police a parlé du recours à la force par son ministère. Peut-être que dans une interview accordée six semaines plus tôt, il a parlé de « moins de 2.000 fois » ou qu'il a donné un nombre spécifique qui ne correspond pas à votre jeu de données.

Ces types de divergence entre les statistiques publiées et les données brutes peut s’avérer une source d’informations importante. Souvent, la réponse expliquant cette divergence sera simple. Par exemple, les données que vous avez reçues ne couvrent peut-être pas la même période dont il parlait. Mais parfois vous les rattraperez dans leur mensonge. Dans les deux cas, vous devez vous assurer que les chiffres publiés correspondent aux totaux des données qui vous ont été fournies.

### La feuille de calcul comporte 65.536 lignes

Le nombre maximal de lignes autorisées dans une feuille de calcul d’une ancienne version d’Excel était de 65 536. Si vous recevez un jeu de données avec ce nombre de lignes, vous avez probablement reçu un jeu de données incomplet. Les nouvelles versions d'Excel permettent 1.048.576 lignes, donc il est moins probable que vous utilisiez des jeux de données qui atteignent cette limite.

### La feuille de calcul comporte 255 colonnes

L'application Numbers d'Apple ne peut gérer que des feuilles de calcul contenant 255 colonnes et elle tronque les fichiers comportant davantage de colonnes sans avertir l'utilisateur. Si vous recevez un jeu de données avec exactement 255 colonnes, demandez si le fichier a été ouvert ou converti avec Numbers.

### La feuille de calcul comporte des dates en 1900 ou 1904

Pour d’obscures raisons, la date par défaut d’Excel à partir de laquelle le logiciel compte toutes les autres dates est le 1er janvier 1900. Mais si vous utilisez Excel pour Mac, ce sera le 1er janvier 1904. Si vous repérez ces dates dans vos données, il s’agit probablement d’un problème. 

### Textes convertis en nombres

Tous les chiffres ne sont pas des nombres. Par exemple, un code peut être utilisé sans qu’il soit pour autant un nombre et qu’il signifie donc toute autre chose. Essayer de convertir ce type de données en nombres peut entraîner toute une série de problèmes, y compris si vous essayez de les convertir dans un autre format de fichier ou de les fusionner avec d’autres jeux de données.

### Numéros stockés en tant que texte

Lorsque vous travaillez avec des feuilles de calcul, les numéros peuvent être stockés sous forme de texte avec un formatage indésirable. Cela arrive souvent lorsqu'une feuille de calcul est optimisée pour présenter des données plutôt que de les rendre disponibles pour une réutilisation. Par exemple, au lieu de représenter un million de dollars avec le nombre "1000000", une cellule peut contenir la chaîne "1,000,000" ou "1 000 000" ou "USD 1 000 000" avec le formatage des virgules, unités et espaces. Excel peut prendre en charge certains cas simples mais vous devrez souvent utiliser des formules pour supprimer les caractères indésirables, jusqu'à ce que les cellules soient suffisamment propres pour être reconnues comme des nombres. Une bonne pratique consiste à stocker des numéros sans formatage et à inclure des informations de contexte dans les étiquettes de colonnes ou les métadonnées.

## Problèmes que vous pouvez résoudre

### Problème d'encodage

Toutes les lettres sont représentées par des ordinateurs sous la forme de nombres. Les problèmes d'encodage sont des problèmes qui surviennent lorsque le texte est représenté par un ensemble spécifique de nombres (appelé "encodage"). Cela peut donner lieu à du texte illisible, parsemé de caractères spéciaux incompréhensible. Votre source devrait être en mesure de vous indiquer le type d’encodage du jeu de données.

### Les fins de ligne sont confuses/brouillées

Tous les fichiers de textes et de « données de texte », tels qu’au format CSV, utilisent des caractères invisibles pour représenter les extrémités des lignes. Les ordinateurs Windows, Mac et Linux sont historiquement en désaccord sur ce que devraient être ces caractères de fin de ligne. La tentative d'ouverture d'un fichier enregistré sur un système d'exploitation à partir d'un autre système d'exploitation peut parfois empêcher Excel ou d'autres applications d'identifier correctement les sauts de ligne.

En règle générale, il est facile de résoudre ce problème en ouvrant simplement le fichier dans un éditeur de texte général et en le réenregistrant. Si le fichier est exceptionnellement volumineux, vous devrez peut-être envisager d'utiliser un outil de ligne de commande ou d'obtenir l'aide d'un développeur.

### Données au format PDF

Un nombre important de jeux de données n’est disponible qu’au seul format PDF. Pour extraire les données d’un document PDF, il existe plusieurs outils dont Tabula (gratuit). Toutefois, si vous disposez d'Adobe Creative Cloud, vous avez normalement accès à Acrobat Pro, qui dispose d'une fonctionnalité permettant d’exporter des tableaux vers Excel. L'une ou l'autre solution devrait être capable d'extraire la plupart des données tabulaires d'un PDF.

Voir aussi : 

* [Données dans un document scanné](#donnees-dans-document-scanne)

### Données trop granulaires

C'est le contraire des données trop grossières. Dans ce cas vous avez des régions, mais vous voulez des états ou vous avez des mois mais vous voulez des années. 

Les données peuvent être agrégées en utilisant la fonction de tableau croisé dynamique d'Excel ou de Google Docs, en utilisant une base de données SQL ou en écrivant du code personnalisé. Les tableaux croisés dynamiques sont un outil fabuleux que tous les journalistes devraient apprendre, mais ils ont leurs limites. Pour les jeux de données exceptionnellement volumineux, il est préférable de solliciter un développeur.

Voir aussi : 

* [Données trop grossières](#donnees-grossieres)
* [Données agrégées dans une mauvaise catégorie ou zone géographique](#donnees-agregees-mauvaise-categorie).

### Encodage humain des données

La saisie de données par des humains est un problème si courant que ses symptômes sont mentionnés dans au moins 10 des autres problèmes décrits dans ce document. Les erreurs sont humaines et sans procédure stricte de validation, des problèmes de toutes natures peuvent se poser. Surtout, méfiez-vous des données encodées par les utilisateurs qui n’ont sans doute pas la moindre idée de ce à quoi peut se rapporter le concept de qualité des données.

### Données mélangées avec le formatage et les annotations

Les représentations complexes de données telles que HTML et XML permettent une séparation nette entre les données et leur mise en forme mais ce n'est pas le cas pour les formats tabulaires. Un des problèmes courants consiste à annoter ou décrire les données dans l’étiquetage des colonnes. Des lignes en tête de fichier peuvent être dupliquées ou le fichier peut comporter plusieurs feuilles qui comporteront plusieurs tables, lesquelles peuvent présenter un étiquetage différent.

Dans tous les cas, la solution consiste simplement à identifier le problème.

### Agrégations calculées avec des valeurs manquantes

Imaginez un jeu de données avec 100 lignes et une colonne appelée « coût ». Dans 50 lignes, la colonne des coûts est vide. Quelle est la moyenne de cette colonne ? Est-ce sum_of_cost / 50 ou sum_of_cost / 100 ? Il n'y a pas de réponse définitive. En général, si vous voulez calculer des agrégats sur des colonnes qui ne sont pas complètes, vous pouvez le faire en filtrant les lignes manquantes. Dans certains cas, la valeur manquante pourra être légitimement interprétée comme égale à zéro. SI vous n’en êtes pas certain, demandez à un expert. Sinon, cela peut conduire à une erreur d’analyse, une erreur que d’autres peuvent reprendre et ensuite transmettre.

Voir aussi : 

* [Valeurs manquantes](#valeurs-manquantes)
* [Valeurs manquantes remplacées par zéro](#zeros-remplacent-valeurs-manquantes)

### Echantillon non aléatoire

Une erreur d'échantillonnage non aléatoire se produit lorsqu'une enquête ou tout autre jeu de données échantillonnées échoue intentionnellement ou accidentellement à couvrir l'ensemble de la population. Cela peut se produire pour une variété de raisons allant de l'heure de la journée à la langue maternelle du répondant. C’est une source fréquente d'erreur dans la recherche en sociologie. Cela peut aussi se produire pour des raisons moins évidentes, par exemple lorsqu'un chercheur pense avoir un ensemble de données complet et qu’il choisit de ne travailler qu'avec une partie de celui-ci. Si le jeu de données original était incomplet pour une raison quelconque, les conclusions tirées de leur échantillon seront incorrectes. La seule chose que vous pouvez faire pour corriger un échantillon non aléatoire est d'éviter d'utiliser ces données.

Voir aussi : 

* [Echantillon biaisé](#echantillon-biaise)

### Marge d'erreur trop importante

La marge d’erreur est généralement associée aux données d’enquêtes. En règle générale, vous devriez être prudent dans l’utilisation de ce type de données, surtout si la marge d’erreur dépasse les 10%.

Voir aussi : 

* [Marge d'erreur inconnue](#margin-of-error-is-unknown)

### Marge d'erreur inconnue

Parfois, le problème n'est pas que la marge d'erreur soit trop grande, c'est que personne n'a jamais pris la peine de la comprendre. C'est un problème récurrent dans les sondages non-scientifiques. Sans calculer une marge d’erreur, il est impossible de savoir si les résultats sont exacts. En règle générale, chaque fois que vous avez des données provenant d'un sondage, vous devriez vous posez la question de la marge d’erreur. Si votre source ne peut pas vous le dire, ces données ne valent probablement pas la peine d'être utilisées pour une analyse sérieuse.

Voir aussi : 

* [Marge d'erreur trop importante](#marge-d-erreur-trop-importante)

### Echantillon biaisé

A l’instar [d’un échantillon qui n'est pas aléatoire] (# echantillon-non-aleatoire), un échantillon biaisé résulte d'un manque de soin dans la façon dont l'échantillonnage a été exécuté (ou d’une volonté de le déformer). Un échantillon pourrait être biaisé parce que le sondage a été réalisé sur Internet et que les personnes les plus pauvres n'utilisent pas Internet aussi fréquemment que les riches. Les enquêtes doivent être soigneusement pondérées pour s'assurer qu'elles couvrent des segments proportionnels de toute population qui pourraient fausser les résultats. Il est presque impossible de le faire parfaitement…
Voir aussi : 

* [Echantillon non aléatoire](#echantillon-non-aleatoire)

### Données éditées manuellement

L'édition manuelle de données donne lieu quasi aux mêmes problèmes qu’un [encodage humain des données] (# encodage-humain) sauf que cela arrive après coup. En fait, les données sont souvent éditées manuellement dans le but de les corriger.

Les problèmes d'édition manuelle sont une des raisons pour lesquelles vous devez toujours vous assurer que la provenance de vos données soit bien documentée. Dans la mesure du possible, essayez d’obtenir le jeu de données original ou tout au moins sa version la plus ancienne.

Voir aussi : 

* [Provenance non documentée](#provenance-non-documentee)
* [Encodage humain des données](#encodage-humain)

### L'inflation fausse les données

L'inflation monétaire signifie que l'argent change de valeur dans le temps. Il n'y a aucun moyen de dire si les chiffres ont été ajustés en fonction de l'inflation. Si vous obtenez des données et que vous n'êtes pas sûr qu'elles aient été ajustées, vérifiez auprès de votre source. Si ce n'est pas le cas, vous voudrez probablement effectuer cet ajustement. 

Voir aussi : 

* [Des variations naturelles / saisonnières faussent les données](#nationalseasonal-variation-skews-the-data)

### Des variations naturelles / saisonnières faussent les données

De nombreux types de données fluctuent naturellement en raison de certaines forces sous-jacentes. L'exemple le plus connu est celui de l'emploi fluctuant avec les saisons. Les économistes ont développé une variété de méthodes pour compenser cette variation. Les détails de ces méthodes ne sont pas particulièrement importants, mais il est important que vous sachiez si les données que vous utilisez ont été "désaisonnalisées". Si ce n'est pas le cas et que vous voulez comparer le volume de l'emploi d'un mois à l'autre, vous voudrez probablement obtenir des données ajustées auprès de votre source (il est ici beaucoup plus difficile de les ajuster soi-même, contrairement à l’inflation).

Voir aussi : 

* [L'inflation fausse les données](#inflation-fausse-donnees)

### Manipulation des périodes de temps

Une source peut accidentellement ou intentionnellement déformer la réalité en fournissant des données qui démarrent ou s’arrêtent à un moment précis. Par exemple, les données relatives à une « vague de criminalité nationale », qui furent diffusées en 2015, auraient dû être analysées sur une période plus longue : les journalistes auraient vu que les crimes violents étaient plus élevés aux Etats-Unis dix ans auparavant. 

Si vous disposez de données qui couvrent une période limitée, essayez d'éviter de commencer vos calculs dès la toute première période à laquelle commence le jeu de données. 

Voir aussi : 

* [Manipulation du cadre de référence](#manipulation-cadre-reference)

### Manipulation du cadre de référence

Les statistiques criminelles sont souvent manipulées à des fins politiques en les comparant à une année où le crime était très élevé. Cela peut être exprimé soit comme un changement (en baisse de 60% depuis 2004) ou via un indice (40, où 2004 = 100). Dans l'un ou l'autre de ces cas, 2004 peut ou non être une année appropriée pour la comparaison. Cela aurait pu être une année de criminalité anormalement élevée.

Dans la mesure du possible, essayez de comparer les taux de plusieurs points de départ différents pour voir comment les chiffres changent. 

Voir aussi : 

* [Manipulation des périodes de temps](#manipulation-periodes-temps)

## Problèmes qu'un expert peut vous aider à résoudre

### Source ou auteur non fiables

Parfois, les seules données dont vous disposez proviennent d'une source à propos de laquelle il est raisonnable de douter. Dans certaines situations, c'est très bien. Les seules personnes qui savent combien d'armes sont fabriquées sont les fabricants d'armes à feu. Cependant, si vous ces données proviennent d'un fabricant d’armes douteux, vérifiez toujours avec un autre expert. Mieux encore, vérifiez vos données avec deux ou trois experts. Ne publiez pas de données provenant d'une source biaisée à moins d'avoir des preuves permettant de les corroborer de manière substantielle.

### Opacité du processus de collecte des données

Il est très facile d'introduire de fausses suppositions ou des erreurs dans les processus de collecte des données. Pour cette raison, il est important que les méthodes utilisées soient transparentes. Il est rare que vous sachiez exactement comment un jeu de données a été recueilli mais les indications d'un problème peuvent inclure des nombres qui [affirment une précision irréaliste] (# data-asserts-unrealistic-precision) ou des données qui sont trop bonnes pour être vraies. # trop-bon-pour-etre-vrai).

Parfois, l'histoire d'origine peut être louche : est-ce que tel ou tel universitaire a vraiment interviewé 50 membres de gangs actifs du côté sud de Chicago ? Si la façon dont les données ont été recueillies semble douteuse et que votre source ne peut vous founir des données documentées, vous devriez toujours vérifier auprès d'un autre expert que les données auraient pu raisonnablement être collectées de la manière décrite.

Voir aussi : 

* [Provenance non documentée](#provenance-non-documentee)
* [Précision irréaliste des données](#assertions-irrealistes)
* [Trop bon pour être vrai](#trop-bon-pour-etre-vrai)

### Précision irréaliste des données

En dehors des sciences dures, peu de choses sont mesurées de manière routinière avec plus de deux décimales. Si un jeu de données prétend montrer les émissions d'une usine à la 7e décimale. Cela ne constitue peut-être pas un problème en soi mais il est important d'être transparent au sujet des estimations. 

### Valeurs aberrantes inexplicables

Les valeurs aberrantes donnent lieu à des erreurs statistiques, notamment lorsque des moyennes sont utilisées. Un bon réflexe est d’examiner chaque nouveau jeu de données pour déterminer les valeurs les plus grandes et les plus petites, et vous assurer que celles-ci se trouvent dans une fourchette raisonnable. Si les données le justifient, vous pouvez également effectuer une analyse plus rigoureuse sur le plan statistique.

### Un index masque la variation sous-jacente

Les analystes qui veulent suivre la tendance d'un problème créent souvent des indices de diverses valeurs pour en suivre l’évolution. Il n'y a rien d’intrinsèquement mauvais dans l'utilisation d'un index. Ils peuvent avoir un grand pouvoir explicatif. Cependant, il est important de se méfier des indices qui combinent des mesures disparates. Par exemple, l'indice des inégalités de genre des Nations Unies combine plusieurs mesures liées aux progrès des femmes vers l'égalité. L'une des mesures utilisées est la « représentation des femmes au parlement ». Deux pays dans le monde ont des lois qui imposent la représentation des deux sexes dans leurs parlements : la Chine et le Pakistan. En conséquence, ces deux pays obtiennent de bien meilleurs résultats grâce à cet indice.
 
### Résultats piratés

Le piratage peut consister dans la modification intentionnelle des données ou de l'analyse statistique, ou encore dans le signalement d’une sélection de résultats statistiquement significatifs. Si vous tombez sur ce type de cas, il faut arrêter de collecter des données une fois que vous avez obtenu un résultat significatif, supprimer des observations pour obtenir un résultat significatif, ou effectuer de nombreuses analyses et ne rapporter que celles qui seront les plus significatives. Quelques [bonnes informations ici] (http://fivethirtyeight.com/features/science-isnt-broken) à propos de ce problème.

Si vous souhaitez publier les résultats d'une étude, vous devez comprendre ce qu'est la valeur P, ce qu’elle signifie puis prendre une décision éclairée quant à la pertinence de l'utilisation des résultats. 

Voir aussi : 

* [Marge d'erreur trop importante](#marge-d-erreur-trop-importante)

### Echec de la loi de Benford

[La loi de Benford](https://fr.wikipedia.org/wiki/Loi_de_Benford) est une théorie qui dispose que les petits chiffres (1, 2, 3) apparaissent beaucoup plus fréquemment au début des nombres que les grands chiffres (7, 8, 9). En théorie, la loi de Benford peut être utilisée pour détecter des anomalies dans des pratiques comptables ou des résultats d’élections même si, dans la pratique, elle peut facilement être mal appliquée. Si vous pensez qu'un jeu de données a été créé ou modifié pour tromper, la loi de Benford est un excellent premier test, mais vous devriez toujours vérifier vos résultats avec un expert avant de conclure que vos données ont été manipulées.

### Trop bon pour être vrai

Il n'existe pas de jeu de données global relatif à l'opinion publique. Personne ne connaît le nombre exact de personnes vivant en Sibérie. Les statistiques de la criminalité ne sont pas comparables d’un pays à l’autre. 

Méfiez-vous des données qui prétendent représenter quelque chose que vous ne pourriez pas parvenir à connaître. Ce ne sont pas des données. Il s’agit de l'estimation de quelqu'un et elle est probablement fausse. Mais aussi... cela pourrait être une bonne histoire : demandez à un expert de vérifier pour vous.

## Problèmes qu'un développeur peut vous aider à résoudre

### Données agrégées dans une mauvaise catégorie ou zone géographique

Parfois, vos données présentent un bon niveau de détail (ni [trop grossier] (# donnees-grossieres) ni [trop granulaire] (# donnees-granulaires)), mais elles ont été agrégées dans un groupe différent de celui que vous souhaitiez. L'exemple classique est celui des données agrégées via des codes postaux que vous préfériez obtenir par quartier. Dans de nombreux cas, il s'agit d'un problème impossible à résoudre sans obtenir de votre source des données plus granulaires, mais parfois les données peuvent être mappées proportionnellement d'un groupe à l'autre. Cela ne doit être entrepris qu'avec une compréhension minutieuse de la [marge d'erreur] (#marge-d-erreur-trop-importante) qui peut être introduite dans le processus. Si vous avez agrégé des données dans des mauvais groupes, demandez à un développeur s'il est possible de les regrouper. 
Voir aussi : 

* [Données trop grossières](#donnees-grossieres)
* [Données trop granulaires](#donnees-granulaires)
* [Marge d'erreur trop importante](#marge-d-erreur-trop-importante)

### Données dans un document scanné

Grâce aux législations réglementant l’accès aux données publiques, il est fréquent que les autorités soient obligées de vous fournir des données, même si elles ne le souhaitent pas vraiment. Une technique courante consiste alors à vous fournir des scans ou des photographies des pages de données. Il peut s'agir d’un fichier image (JPG, par exemple) ou, plus probablement, d'un fichier PDF.

Il est possible d'extraire du texte à partir d'images et de le restituer en données via un processus de reconnaissance optique des caractères (OCR ou OCR-isation). Si cette technique permet la précision dans la plupart des cas, cela va dépendre aussi de la nature du document. Chaque fois que vous utiliserez OCR pour extraire des données, vous devrez mettre en place une procédure permettant de valider la correspondance des données avec le fichier original.

De nombreux sites web proposent logiciels de conversion. Il existe également des outils gratuits qu’un développeur pourra adapter à des documents spécifiques. Si vous en avez un sous la main, demandez-lui la meilleure stratégie à adopter pour le document dont vous disposez.

Voir aussi : 

* [Données au format PDF](#donnees-pdf)
