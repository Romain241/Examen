# Réalisation d'une datavisualisation en lien avec la politique Américaine pour le partiel de dataviz :

Pour réaliser cela, j'ai utilisé plusieurs jeux de données qui vient d'une requête de wikidata du site de wikidata Query Service avec quelles lignes en plus pour avoir d'analyse sur le jeu de données de wikidata . Ce jeux de données sont des données liées à la politique américaine et plus particulièrement au 117th congress des Etats-Unis d'Amérique après l'élection à la président des Etats-Unis de Joe Biden en 2020 mais aussi au présdent des Etats-Unis d'Amerique. 

Le premier jeu de données est la liste des présidents des Etats-Unis d'Amérique. Le seconde sera un jeu de données sur le 117th Congress des Etats-Unis d'amérique 


# La liste des présidents des Etats-Unis (jeu de données): 

![Image de la résident du président des Etats-Uins](https://upload.wikimedia.org/wikipedia/commons/c/c2/Maison_Blanche.jpg) 

### Acquisition des données sur le jeu de données sur les présidents : 

Pour ce première jeu j'ai utiliser la requête sur Wikidata Query Service qui est la suivante : 

```Sparlq
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
Cette reqûete ma données un jeu de données ci-dessus : 

<iframe style="width: 45vw; height: 30vh; border: none;" src="https://query.wikidata.org/embed.html#%23Pr%C3%A9sidents%20des%20%C3%89tats-Unis%20et%20leur%20%C3%A9pouses%0A%23TEMPLATE%3D%7B%22template%22%3A%22Presidents%20of%20%3Fcountry%20and%20their%20spouses%22%2C%22variables%22%3A%7B%22%3Fcountry%22%3A%7B%22query%22%3A%22%20SELECT%20%3Fid%20WHERE%20%7B%20%3Fid%20wdt%3AP31%20wd%3AQ6256%20.%20%7D%22%7D%20%7D%20%7D%0A%0ASELECT%20%3Fp%20%3FpLabel%20%3Fppicture%20%3Fw%20%3FwLabel%20%3Fwpicture%20WHERE%20%7B%0A%20%20BIND(wd%3AQ30%20AS%20%3Fcountry)%0A%20%20%3Fcountry%20(p%3AP6%2Fps%3AP6)%20%3Fp.%0A%20%20%3Fp%20wdt%3AP26%20%3Fw.%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fp%20wdt%3AP18%20%3Fppicture.%0A%20%20%20%20%3Fw%20wdt%3AP18%20%3Fwpicture.%0A%20%20%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

## La structuration des données de ce jeu de données sur les présidents.

Après cette première étapes qui est la collecte des données sur Wikidata avec l'utilisation d'une requête Sparql. J'ai utilisé OpenRafine qui n'a permis de modifier, rajouter un président qui manquant dans la liste le 15ème président James Buchaman qui était pas dans la liste de wikidata, j'ai supprimé la colonne sur les femmes de président et leurs photos et  rajouter d'autres information par l'intermédaire de l'enrichissement des données réalise sur OpenRafine au niveau de la réconcilie des colonnes avec le services de Wikidata qui permet optimisation et l'ajout de nouvelles information d'ou de nouvelles colonnes réaliser par  réconciliées comme les colonnes lieu de naissance, Etat de naissance, date de naissance, les pères des présidents, la date de morts, la cause de la mort et d'autres choses comme le parti politique et la religions mais j'ai supprimer cette colonne. Tous ce Data Wrangling est montre dans deux fichier Json car pour rajouter des données j'ai du télécharge le fichier en Excel puis le modifier puis le remettre sur OpenRefine, pour voir ces fichiers voir le lien weTransfer, [lien weTransfer](https://we.tl/t-6ZT5stIq8H).

## Visualisation de l'information.

Tous cela pour arriver une liste de président en carrousiel ( permet de montre une liste en difilé) que je vous présente avec comme information, l'ordre numérique de son entre à la maison blanche, sa date de naissance, son lieu de naissance, sa date de mort, ses épouses si il s'est remarie et d'autres choses comme le parti politique du président : 

<div class="flourish-embed flourish-cards" data-src="visualisation/5151986"><script src="https://public.flourish.studio/resources/embed.js"></script></div>
Source du jeux de données : wikidata 

##  Editorialisation et visualisation des données 
Cette visualisation en carrousiel , permet de voir les présidents américains, leurs dates de naissance, leurs lieux de naissance, mais aussi leurs partis politique par un jeu de couleurs, rouge pour les républicains, bleu pour les démocrates, en gris les independants, en jaune les whigs etc....
Source du jeux de données : wikidata 

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/4874708"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Cependant, j'ai utilisé ce jeu de données pour montrer des choses comme par exemple là dans cette visualisation en treemap qui permet au données hiérarchiques de montre toutes leurs informations et j'utilisé cette graphique pour montre qu'il y a eu plus de présidents républicains que démoncrates dans l'histoire des Etats-Unis. 19 présidents républicains contre 16 présidents démoncrates. On peux voir un filtre qui nous permet de savoir combien de président sont originaire d'un Etat des Etats-Unis.
Cette visualisation dit Treemap Chart me permet de faire une structure arborescente au niveau des Etats qui on vu des président naître dans leurs Etats. je parlerai plus en détaille de cette forme de visualisation dans une autre parti de ce documents.

# Nouveau jeu de données, toujours sur la politique Américaine, le 117th congress des Etats-Unis.


![Image du congress américian](https://upload.wikimedia.org/wikipedia/commons/b/b5/2019_State_of_the_Union_%2840042020903%29_%28cropped%29.jpg)

Ce jeu de données à était acquis par une collecte de deux jeu de données sur Wikidata, l'un sur les senateurs du 117th congress des Etats-Unis et un autre jeu de données sur Wikidata sur les représentants du 117th congress. 

## Acquisition des données sur le jeu de données sur le 117th congrès des Etats-Unis : 


le jeu de données initial sur les senateurs est le suivant, c'est un jeu de données qui viens de wikidata, voici la requête pour les senateurs : 

```Sparql
select ?senator ?senatorLabel ?districtLabel ?partyLabel ?genderLabel ?assumedOffice (sample(?image) as ?image) where {
  # Get all senators
  ?senator p:P39 ?posheld; 
           wdt:P21 ?gender;# With position held
           p:P102 ?partystatement. # And with a certain party
  
  # Get the party
  ?partystatement ps:P102 ?party.
  minus { ?partystatement pq:P582 ?partyEnd. } # but minus the ones the senator is no longer a member of
  minus { ?party wdt:P361 ?partOf. } # and the 'Minnesota Democratic–Farmer–Labor Party' and such
  
  # Check on the position in the senate
  ?posheld ps:P39 wd:Q4416090; # Position held is in the senate
           pq:P768 ?district;
           pq:P580 ?assumedOffice. # And should have a starttime
  
  minus { ?posheld pq:P582 ?endTime. } # But not an endtime 
  
  # Add an image
  optional { ?senator wdt:P18 ?image. }
         
  service wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
} group by ?senator ?senatorLabel ?districtLabel ?partyLabel ?genderLabel ?assumedOffice order by ?senatorLabel

```

<iframe style="width: 45vw; height: 45vh; border: none;" src="https://query.wikidata.org/embed.html#select%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20(sample(%3Fimage)%20as%20%3Fimage)%20where%20%7B%0A%20%20%23%20Get%20all%20senators%0A%20%20%3Fsenator%20p%3AP39%20%3Fposheld%3B%20%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP21%20%3Fgender%3B%23%20With%20position%20held%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP102%20%3Fpartystatement.%20%23%20And%20with%20a%20certain%20party%0A%20%20%0A%20%20%23%20Get%20the%20party%0A%20%20%3Fpartystatement%20ps%3AP102%20%3Fparty.%0A%20%20minus%20%7B%20%3Fpartystatement%20pq%3AP582%20%3FpartyEnd.%20%7D%20%23%20but%20minus%20the%20ones%20the%20senator%20is%20no%20longer%20a%20member%20of%0A%20%20minus%20%7B%20%3Fparty%20wdt%3AP361%20%3FpartOf.%20%7D%20%23%20and%20the%20'Minnesota%20Democratic%E2%80%93Farmer%E2%80%93Labor%20Party'%20and%20such%0A%20%20%0A%20%20%23%20Check%20on%20the%20position%20in%20the%20senate%0A%20%20%3Fposheld%20ps%3AP39%20wd%3AQ4416090%3B%20%23%20Position%20held%20is%20in%20the%20senate%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP768%20%3Fdistrict%3B%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP580%20%3FassumedOffice.%20%23%20And%20should%20have%20a%20starttime%0A%20%20%0A%20%20minus%20%7B%20%3Fposheld%20pq%3AP582%20%3FendTime.%20%7D%20%23%20But%20not%20an%20endtime%20%0A%20%20%0A%20%20%23%20Add%20an%20image%0A%20%20optional%20%7B%20%3Fsenator%20wdt%3AP18%20%3Fimage.%20%7D%0A%20%20%20%20%20%20%20%20%20%0A%20%20service%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%20group%20by%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20order%20by%20%3FsenatorLabel" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>


Pour réaliser aussi la collecte des données pour les représentants du 117th congress j'ai juste modifie ce jeu de données des senateurs par wd:Q4416090 pour le poste par wd:Q13218630. Cela me permet d'avoir les représentants présent de ce 117th congrès des Etats-Unis. Ce jeu de données qui est aussi un jeu de données wikidata est un jeu de données sur les représentants. Ce jeu de données est le suivant : 

```Sparql
select ?senator ?senatorLabel ?districtLabel ?partyLabel ?genderLabel ?assumedOffice (sample(?image) as ?image) where {
  # Get all senators
  ?senator p:P39 ?posheld; 
           wdt:P21 ?gender;# With position held
           p:P102 ?partystatement. # And with a certain party
  
  # Get the party
  ?partystatement ps:P102 ?party.
  minus { ?partystatement pq:P582 ?partyEnd. } # but minus the ones the senator is no longer a member of
  minus { ?party wdt:P361 ?partOf. } # and the 'Minnesota Democratic–Farmer–Labor Party' and such
  
  # Check on the position in the senate
  ?posheld ps:P39 wd:Q13218630; # Position held is in the senate
           pq:P768 ?district;
           pq:P580 ?assumedOffice. # And should have a starttime
  
  minus { ?posheld pq:P582 ?endTime. } # But not an endtime 
  
  # Add an image
  optional { ?senator wdt:P18 ?image. }
         
  service wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en". }
} group by ?senator ?senatorLabel ?districtLabel ?partyLabel ?genderLabel ?assumedOffice order by ?senatorLabel
```

<iframe style="width: 45vw; height: 45vh; border: none;" src="https://query.wikidata.org/embed.html#select%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20(sample(%3Fimage)%20as%20%3Fimage)%20where%20%7B%0A%20%20%23%20Get%20all%20senators%0A%20%20%3Fsenator%20p%3AP39%20%3Fposheld%3B%20%0A%20%20%20%20%20%20%20%20%20%20%20wdt%3AP21%20%3Fgender%3B%23%20With%20position%20held%0A%20%20%20%20%20%20%20%20%20%20%20p%3AP102%20%3Fpartystatement.%20%23%20And%20with%20a%20certain%20party%0A%20%20%0A%20%20%23%20Get%20the%20party%0A%20%20%3Fpartystatement%20ps%3AP102%20%3Fparty.%0A%20%20minus%20%7B%20%3Fpartystatement%20pq%3AP582%20%3FpartyEnd.%20%7D%20%23%20but%20minus%20the%20ones%20the%20senator%20is%20no%20longer%20a%20member%20of%0A%20%20minus%20%7B%20%3Fparty%20wdt%3AP361%20%3FpartOf.%20%7D%20%23%20and%20the%20'Minnesota%20Democratic%E2%80%93Farmer%E2%80%93Labor%20Party'%20and%20such%0A%20%20%0A%20%20%23%20Check%20on%20the%20position%20in%20the%20senate%0A%20%20%3Fposheld%20ps%3AP39%20wd%3AQ13218630%3B%20%23%20Position%20held%20is%20in%20the%20senate%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP768%20%3Fdistrict%3B%0A%20%20%20%20%20%20%20%20%20%20%20pq%3AP580%20%3FassumedOffice.%20%23%20And%20should%20have%20a%20starttime%0A%20%20%0A%20%20minus%20%7B%20%3Fposheld%20pq%3AP582%20%3FendTime.%20%7D%20%23%20But%20not%20an%20endtime%20%0A%20%20%0A%20%20%23%20Add%20an%20image%0A%20%20optional%20%7B%20%3Fsenator%20wdt%3AP18%20%3Fimage.%20%7D%0A%20%20%20%20%20%20%20%20%20%0A%20%20service%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D%20group%20by%20%3Fsenator%20%3FsenatorLabel%20%3FdistrictLabel%20%3FpartyLabel%20%3FgenderLabel%20%3FassumedOffice%20order%20by%20%3FsenatorLabel" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

## La structuration des données de ce jeu de données sur le 117th congrès des Etats-Unis.

Pour utiliser ces deux jeu de données et en créer un seul jeu de données, j'ai rassemble ces deux jeux de données qui sont simmillaire dans un tableau CSV avec une enrichissement au niveau du poste (représentant ou senateur). Puis je suis passer à la deuxième étapes qui est la structure des données grâce à OpenRefine d'ou le travail de datawrangling. Grâce à OpenRefine j'ai pu nettoyer les données au niveau des doublons sur certains senateurs et représentant surtout des doublons en liens avec le parti politique de la personne, la requête de wikidata mettait les parti régionalistes des démocrates et des républicains et donc j'ai du grace au fitre sur OpenRefine, j'ai pu rapidement trouver les doublons, puis faire réaliser une optimisation des données au niveau du lieu de naissance, la date de naissance, le parti politique, l'Etat ou la personne est soit la senateur ou représentant et d'autres choses. Tous celui est montre par les document Jsons suivant qui sont disponible dans des fichiers weTransfer qui sont les suivants : [lien weTransfer](https://we.tl/t-A8uwNRhthf)

Par contre, en réalisant le datawrangling sur OpenRefine, en optimiser les données comme pour le jeu de donnés sur les présidents, j'ai constaté qu'il manquant 25 représentants dans la fichier. J'ai du compléte les données à la main cette opération à était plus rapide en utilisant OpenRefine pour trouver représentants manquant selon les Etats. J'ai rajouter à la suite du télechargement du document d'Openrefine sur le 117th congress sur Excel pour rajouter les représentants qui manquant puis j'ai remis ce fichier excel sur OpenRefine et j'ai refait un datawrangling comme vous le verrai sur le document Json sur Wetransfer.

## Visualisation de l'information sur ce jeu de données sur le 117th congrès des Etats-Unis.

Grace à tous cela j'ai pu faire différentes visualisations sur le 117th congress des Etat-Unis d'Amérique comme par exemple le nombre de senateurs, représentant républicains et démoncrate selon le 117th congress et selon les Etats. Cela donne cette visualisation suivant qui est encore un Treemap qui me permet de faire des visualisation de données qualifiés d'hiérarchiques avec une arborescente selon la représentation demande là les senateurs ou les représentants selon les partis avec des valeurs quantitative qui permet de données un chiffre au données et quelques informations supplementaire. Grâce à cette visualisation on peut faure les données selon leurs tailles dans le jeu de données et leurs couleurs.

##  Editorialisation et visualisation des données 

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/5159833"><script src="https://public.flourish.studio/resources/embed.js"></script></div>


Dans cette visualisation, on peux voir en rouge le parti républicain, en bleu le parti démocrate et les indenpendant en Jaune. là au plus haut niveau on peut voir que les répresentant démocrates qui sont plus haut de 10 représentants en comparaison avec les représentants républicains qui sont au nombre de 212. cela fait trés peu et dont montre la facture de l'amérique en deux entre les progressites et les convervateurs. Et en Senat l'ecart est la plus serre, en comptant les senateurs Indepedants qui soutient les démocrates et avec la voix de la vice-président des Etat-Unis, les démocrates on la majorité à une voix au senat. Cette visualisation par le filtre permet de voir la situation entre les démocrates et les républicains dans les différents Etats. Par exemple dans l'Etat de l'Alabama on peux voir que sur 7 représentnant, il y a d'une seule représentante démocrate et en peux faire différentes interpretation.

La dans cette autre visualisation dit hierchique en Sunburst qui permet de visualisé les données dit hierchique en secteurs et sur différents niveaux, dans cette visualisation du 117th congrès des Etats-Unis d'Amérique, il y a un niveau qui qualifier les politiciens au niveau de leurs parti, puis un autre niveau sur leurs fonctions et pour finir le dernier niveau sur leurs genre. J'ai rajouté la représentation des femmes politiciens dans ce 117th congrès selon les parti et les poste soit elle est senatrice ou représentant et aussi selon Etats ou elle est siège.

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/5102340"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Là on peut voir qu'il y a plus de femmes dans le parti démocrate que dans le parti républicain, par exemple sur 222 représentant démocrates, il y a 89 femmes et 133 hommes en comparaison dans le parti républicain il y a sur 212, 182 hommes et 30 femmes. On peut faire la même étude au niveau du senat entre les senatrices et les senateurs et aussi par Etats. Il y a un Etat, l'Etat de Washigton ou le nombre de femme dans la représentation politique est le plus élèvé et dépasse les hommes. 
Pour différencié les femmes et les hommes dans cette visualisation, j'ai mis les femmes en rose et les hommes en vert et j'ai garde les même couleurs pour les partis politiques.


Dans cette dernière visualisation, je vous montre la liste définitive des politiciens du 117th congrès des Etats-Unis d'Amérique qui est un tableau qui est à était travaillé grâce au logiciel Datawrapper

<iframe title="La liste des politiciens du 117th congrès" aria-label="chart" id="datawrapper-chart-S23X1" src="https://datawrapper.dwcdn.net/S23X1/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="1488"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"])for(var e in a.data["datawrapper-height"]){var t=document.getElementById("datawrapper-chart-"+e)||document.querySelector("iframe[src*='"+e+"']");t&&(t.style.height=a.data["datawrapper-height"][e]+"px")}}))}();
</script>

Gràce a cette visualisation réaliser sur Darawrapper, j'ai mise en avant le genre des politiciens avec une couleurs Rose pour les femmes et une couleurs bleu pour les hommes mais aussi des couleurs pouur les partis politiques, en bleu , le parti démocrate et en rouge le parti républicain. Et pour finir j'ai rajouter un mini-moteur de recherche et un filtre au niveau des dates de naissances des politiciens. Grâce a cela on peutsavoir qui est le plus jeune politicien du congrès qui est Madison Cawthorn né en 1995 et les plus ancien qui sont nés en 1933 et il sont au montre de 3 politiciens nés en 1933et avoir la liste complté de la représentation du pouvoir législatif au Etats-Unis.
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
