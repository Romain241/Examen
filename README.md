# Réalisation d'une datavisualisation en lien avec la politique Américaine pour le partiel de dataviz :

Pour réaliser cela, j'ai utilisé plusieurs jeux de données qui vient d'une requête de wikidata du site de wikidata Query Service avec quelles lignes en plus pour avoir d'analyse sur le jeu de données de wikidata . Ce jeux de données sont des données liées à la politique américaine et plus particulièrement au 117th congress des Etats-Unis d'Amérique après l'élection à la président des Etats-Unis de Joe Biden en 2020 mais aussi au présdent des Etats-Unis d'Amerique. 

Le premier jeu de données est la liste des présidents des Etats-Unis d'Amérique. Le seconde sera un jeu de données sur le 117th Congress des Etats-Unis d'amérique 


# La liste des présidents des Etats-Unis (jeu de données): 

![Image de la résident du président des Etats-Uins](https://upload.wikimedia.org/wikipedia/commons/c/c2/Maison_Blanche.jpg)

Pour ce première jeu j'ai utiliser la requête sur Wikidata Query Service qui est la suivante : 

```Query 
#Présidents des États-Unis et leur épouses
#TEMPLATE={"template":"Presidents of ?country and their spouses","variables":{"?country":{"query":" SELECT ?id WHERE { ?id wdt:P31 wd:Q6256 . }"} } }

SELECT ?p ?pLabel ?ppicture ?w ?wLabel ?wpicture WHERE {
  BIND(wd:Q30 AS ?country)
  ?country (p:P6/ps:P6) ?p.
  ?p wdt:P26 ?w.
  OPTIONAL {
    ?p wdt:P18 ?ppicture.
    ?w wdt:P18 ?wpicture.
  }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
}
```
Cette reqûete me données un jeu de données comme vous le voulais ce jeu de données ci-dessus : 

<iframe style="width: 45vw; height: 30vh; border: none;" src="https://query.wikidata.org/embed.html#%23Pr%C3%A9sidents%20des%20%C3%89tats-Unis%20et%20leur%20%C3%A9pouses%0A%23TEMPLATE%3D%7B%22template%22%3A%22Presidents%20of%20%3Fcountry%20and%20their%20spouses%22%2C%22variables%22%3A%7B%22%3Fcountry%22%3A%7B%22query%22%3A%22%20SELECT%20%3Fid%20WHERE%20%7B%20%3Fid%20wdt%3AP31%20wd%3AQ6256%20.%20%7D%22%7D%20%7D%20%7D%0A%0ASELECT%20%3Fp%20%3FpLabel%20%3Fppicture%20%3Fw%20%3FwLabel%20%3Fwpicture%20WHERE%20%7B%0A%20%20BIND(wd%3AQ30%20AS%20%3Fcountry)%0A%20%20%3Fcountry%20(p%3AP6%2Fps%3AP6)%20%3Fp.%0A%20%20%3Fp%20wdt%3AP26%20%3Fw.%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fp%20wdt%3AP18%20%3Fppicture.%0A%20%20%20%20%3Fw%20wdt%3AP18%20%3Fwpicture.%0A%20%20%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

## Explication de cette visualisation de ce jeu de données présidentiels par les différentes étpaes dans une datavisualisation.

Là on est dans la première étapes qui est la saisie de données. Puis j'ai utilisé OpenRafine qui n'a permis de modifier, rajouter un président qui manquant dans la liste et d'autres information qui est visible dans le fichier Json de toutes les modifications. Mais j'ai enrichie ces données avec ajouts d'une date de naissance, le lieu de naissance, les pères des présidents, la date de morts, la cause de la mort et d'autres choses comme le parti politique. Cela à était permis gràce à l'enrichissement réalise sur OpenRafine au niveau de la réconcilie des colonnes puis leurs optimisation par l'ajout de nouvelles colonnes par la réconciliées comme les colonnes sur le lieu de naissance, Etat de naissance etc...  Tous cela pour arriver une liste de président en carrousiel que je vous présente : 

<div class="flourish-embed flourish-cards" data-src="visualisation/5151986"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Cette visualisation, permet de voir les présidents américains, leurs dates de naissance, leurs lieux de naissance, ... 
Source du jeux de données : wikidata 

Cependant, j'ai utilisé ce jeu de données pour montrer des choses comme par exemple là dans cette visualisation. Ou je montre qu'il y a eu plus de présidents républicains que démoncrates dans l'histoire des Etats-Unis. 19 présidents républicains contre 16 présidents démoncrates. On peux voir un filtre qui nous permet de savoir combien de président sont originaire d'un Etat des Etats-Unis.


<div class="flourish-embed flourish-hierarchy" data-src="visualisation/4874708"><script src="https://public.flourish.studio/resources/embed.js"></script></div>


# Nouveau jeu de données, toujours sur la politique Américaine, le 117th congress des Etats-Unis.


![Image du congress américian](https://upload.wikimedia.org/wikipedia/commons/b/b5/2019_State_of_the_Union_%2840042020903%29_%28cropped%29.jpg)

Ce jeu de données à était acquis par une collecte de deux jeu de données sur Wikidata, l'un sur les senateurs du 117th congress des Etats-Unis et un autre jeu de données sur Wikidata sur les représentants du 117th congress. 

## Explication de cette visualisation de ce jeu de données présidentiels par les différentes étpaes dans cette datavisualisation.

le jeu de données initial sur les senateurs est le suivant : 

<iframe style="width: 80vw; height: 45vh; border: none;" src="https://query.wikidata.org/embed.html#select%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20(sample(%3Fimage)%20as%20%3Fimage)%20where%20%7B%0A%20%20%23%20Get%20all%20senators%0A%20%20%3Fsenator%20p%3AP39%20%3Fposheld%3B%20%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP21%20%3Fgender%3B%23%20With%20position%20held%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP102%20%3Fpartystatement.%20%23%20And%20with%20a%20certain%20party%0A%20%20%0A%20%20%23%20Get%20the%20party%0A%20%20%3Fpartystatement%20ps%3AP102%20%3Fparty.%0A%20%20minus%20%7B%20%3Fpartystatement%20pq%3AP582%20%3FpartyEnd.%20%7D%20%23%20but%20minus%20the%20ones%20the%20senator%20is%20no%20longer%20a%20member%20of%0A%20%20minus%20%7B%20%3Fparty%20wdt%3AP361%20%3FpartOf.%20%7D%20%23%20and%20the%20'Minnesota%20Democratic%E2%80%93Farmer%E2%80%93Labor%20Party'%20and%20such%0A%20%20%0A%20%20%23%20Check%20on%20the%20position%20in%20the%20senate%0A%20%20%3Fposheld%20ps%3AP39%20wd%3AQ4416090%3B%20%23%20Position%20held%20is%20in%20the%20senate%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP768%20%3Fdistrict%3B%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP580%20%3FassumedOffice.%20%23%20And%20should%20have%20a%20starttime%0A%20%20%0A%20%20minus%20%7B%20%3Fposheld%20pq%3AP582%20%3FendTime.%20%7D%20%23%20But%20not%20an%20endtime%20%0A%20%20%0A%20%20%23%20Add%20an%20image%0A%20%20optional%20%7B%20%3Fsenator%20wdt%3AP18%20%3Fimage.%20%7D%0A%20%20%20%20%20%20%20%20%20%0A%20%20service%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%20group%20by%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20order%20by%20%3FsenatorLabel" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>


Pour réaliser la collecte des données pour les représentants du 117th congress j'ai juste modifie ce jeu de données des senateurs par wd:Q4416090 pour le poste par wd:Q13218630. cette collecte pour les représentants est le suivant : 

<iframe style="width: 50vw; height: 45vh; border: none;" src="https://query.wikidata.org/embed.html#select%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20(sample(%3Fimage)%20as%20%3Fimage)%20where%20%7B%0A%20%20%23%20Get%20all%20senators%0A%20%20%3Fsenator%20p%3AP39%20%3Fposheld%3B%20%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP21%20%3Fgender%3B%23%20With%20position%20held%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP102%20%3Fpartystatement.%20%23%20And%20with%20a%20certain%20party%0A%20%20%0A%20%20%23%20Get%20the%20party%0A%20%20%3Fpartystatement%20ps%3AP102%20%3Fparty.%0A%20%20minus%20%7B%20%3Fpartystatement%20pq%3AP582%20%3FpartyEnd.%20%7D%20%23%20but%20minus%20the%20ones%20the%20senator%20is%20no%20longer%20a%20member%20of%0A%20%20minus%20%7B%20%3Fparty%20wdt%3AP361%20%3FpartOf.%20%7D%20%23%20and%20the%20'Minnesota%20Democratic%E2%80%93Farmer%E2%80%93Labor%20Party'%20and%20such%0A%20%20%0A%20%20%23%20Check%20on%20the%20position%20in%20the%20senate%0A%20%20%3Fposheld%20ps%3AP39%20wd%3AQ13218630%3B%20%23%20Position%20held%20is%20in%20the%20senate%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP768%20%3Fdistrict%3B%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP580%20%3FassumedOffice.%20%23%20And%20should%20have%20a%20starttime%0A%20%20%0A%20%20minus%20%7B%20%3Fposheld%20pq%3AP582%20%3FendTime.%20%7D%20%23%20But%20not%20an%20endtime%20%0A%20%20%0A%20%20%23%20Add%20an%20image%0A%20%20optional%20%7B%20%3Fsenator%20wdt%3AP18%20%3Fimage.%20%7D%0A%20%20%20%20%20%20%20%20%20%0A%20%20service%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%20group%20by%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20order%20by%20%3FsenatorLabel" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

Puis j'ai rassemble ces deux jeux de données qui sont simmillaire dans un tableau CSV avec une enrichissement au niveau du poste qu'ils ont soit senateur ou representant. Puis je suis passer à la deuxième étapes qui est la structure des données grâce à OpenRefine. Grace a OpenRefine j'ai pu nettoyer les données au niveau des doublons sur certains senateurs et représentant surtout des doublons en liens avec le parti politique de la personne, puis une optimisation des données au niveau du lieu de naissance, la date de naissance, le parti politique, l'Etat ou la personne est soit la senateur ou représentant. Tous celui est montre par le document Jsons. 

Par contre, en nettoyant, en optimiser les données comme pour le jeu de donnés sur les présidents, j'ai constaté qu'il manquant 25 représentants. J'ai pu compléte les données à la main cette opération à était plus rapide en utilisant OpenRefine pour trouver les données manquantes. J'ai rajouter à la suite du télechargement du document sur le 117th congress sur Excel la suite des représentants qui manquant.

Grace à tous cela j'ai pu faire différentes visualisations sur le 117th congress des Etat-Unis d'Amérique comme par exemple le nombre de senateurs, représentant républicains et démoncrate selon le 117th congress et selon les Etats. Cela donne cette visualisation suivant qui est Treemap.

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/5102340"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Dans cette visualisation, on peux voir en rouge le parti républicain, en bleu le parti démocrate et les indenpendant en Jaune. là au plus au niveau on peut voir que les répresentant démocrates sont plus haut de 10 représentants en comparaison avec les représentants républicains qui sont au nombre de 212. cela fait trés peu. Et en Senat l'ecart est la plus serre, en comptant les senateurs Indepedants qui soutient les démocrates et avec la voix de la vice-président des Etat-Unis, les démocrates on la majorité à une voix au senat. Cette visualisation par le filtre permet de voir la situation entre les démocrates et les républicains dans les différents Etats. Par exemple dans l'Etat de l'Alabama on peux voir que sur 7 représentnant, il y a d'une seule représentant démocrate.

La dans cette autre visualisation dit hierchique en cercle du 117th congrès des Etats-Unis d'Amérique, j'ai rajouté un autre analyse qui est la représentation des femmes politiciens dans ce 117th congrès selon les parti et les poste soit senatrice ou représentant et aussi selon Etats ou elle ou il siège.

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/5102340"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Là on peut voir qu'il y a plus de femmes dans le parti démocrate que dans le parti républicain, par exemple sur 222 représentant démocrates, il y a 89 femmes et 133 hommes en comparaison dans le parti républicain il y a sur 212, 182 hommes et 30 femmes. On peut faire la même étude au niveau du senat entre les senatrices et les senateurs et aussi par Etats. 
Pour différencié les femmes et les hommes dans cette visualisation, j'ai mis les femmes en rose et les hommes en vert et j'ai garde les même couleurs pour les partis politiques.


_________________________________________________________________________________________________________________________________________________________________________________


## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Romain241/Examen/edit/main/README.md) to maintain and preview the content for your website in Markdown files.


Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Romain241/Examen/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
