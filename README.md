# Réalisation d'une datavisualisation en lien avec la politique Américaine pour le partiel de dataviz :

Pour réaliser cela, j'ai utilisé plusieurs jeux de données provenant d'une requête de wikidata du site de wikidata Query Service avec quelques lignes en plus pour réaliser une analyse sur le jeu de données de wikidata . Ce jeux de données contient des données liées à la politique américaine et plus particulièrement au 117th congrès des Etats-Unis d'Amérique après l'élection à la présidence des Etats-Unis de Joe Biden en 2020 ainsi qu'aux différents président des Etats-Unis d'Amerique. 

Le premier jeu de données est la liste des présidents des Etats-Unis d'Amérique. Le second est un jeu de données sur le 117th Congrès des Etats-Unis d'Amérique 


# La liste des présidents des Etats-Unis (jeu de données): 

![Image de la résidence du président des Etats-Uins](https://upload.wikimedia.org/wikipedia/commons/c/c2/Maison_Blanche.jpg) 

### Acquisition des données sur le jeu de données sur les présidents : 

Pour ce premier jeu j'ai utilisé la requête sur Wikidata Query Service qui est la suivante : 

```SPARQL

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
Cette reqûete ma donné un jeu de données ci-dessous : 

<iframe style="width: 45vw; height: 30vh; border: none;" src="https://query.wikidata.org/embed.html#%23Pr%C3%A9sidents%20des%20%C3%89tats-Unis%20et%20leur%20%C3%A9pouses%0A%23TEMPLATE%3D%7B%22template%22%3A%22Presidents%20of%20%3Fcountry%20and%20their%20spouses%22%2C%22variables%22%3A%7B%22%3Fcountry%22%3A%7B%22query%22%3A%22%20SELECT%20%3Fid%20WHERE%20%7B%20%3Fid%20wdt%3AP31%20wd%3AQ6256%20.%20%7D%22%7D%20%7D%20%7D%0A%0ASELECT%20%3Fp%20%3FpLabel%20%3Fppicture%20%3Fw%20%3FwLabel%20%3Fwpicture%20WHERE%20%7B%0A%20%20BIND(wd%3AQ30%20AS%20%3Fcountry)%0A%20%20%3Fcountry%20(p%3AP6%2Fps%3AP6)%20%3Fp.%0A%20%20%3Fp%20wdt%3AP26%20%3Fw.%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fp%20wdt%3AP18%20%3Fppicture.%0A%20%20%20%20%3Fw%20wdt%3AP18%20%3Fwpicture.%0A%20%20%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%7D%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe>

## La structuration des données de ce jeu de données sur les présidents.

Après cette première étape qui est celle de la collecte des données sur Wikidata avec l'utilisation d'une requête Sparql, j'ai utilisé OpenRefine qui m'a permis de modifier et d'ajouter un président qui manquait à la liste. Ce président est le 15ème président des Etats-Unis, James Buchaman, qui ne figurait pas dans la liste de wikidata. J'ai supprimé la colonne sur les femmes de président et leur photo puis ajouté d'autres informations par l'intermédaire de l'enrichissement des données réalisé sur OpenRefine au niveau de la réconciliation des colonnes avec le service de Wikidata qui permet une optimisation ainsi que l'ajout de nouvelles informations d'où la création de nouvelles colonnes réalisées par la réconciliation de colonnes comme celle du lieu de naissance, de l'etat de naissance, de la date de naissance, de l'identité des pères des présidents, de la date de mort, de la cause de la mort et d'autres comme celle du parti politique et de la religions qui est une colonne que j'ai supprimé. Tous ce Data Wrangling est montré dans deux fichiers Json car pour ajouter des données, j'ai du télécharger le fichier en Excel puis le modifier pour ensuite le remettre sur OpenRefine. Pour consulter ces fichiers, voir le lien weTransfer, [lien weTransfer](https://we.tl/t-6ZT5stIq8H).

## Visualisation de l'information.

Tous cela a été réalisé dans le but d'arriver à une liste des présidents en carroussel (permet de montrer une liste en défilé) que je vous présente avec comme informations, l'ordre numérique de l'entrée des différents présidents à la Maison Blanche, leur date de naissance, leur lieu de naissance, leur date de mort, leurs épouses si ils sont remariés et d'autres informations telles que le parti politique du président : 

<div class="flourish-embed flourish-cards" data-src="visualisation/5151986"><script src="https://public.flourish.studio/resources/embed.js"></script></div>
Source du jeux de données : wikidata 

##  Editorialisation et visualisation des données 
Cette visualisation en carroussel permet de voir les présidents américains, leur date de naissance, leur lieu de naissance, mais aussi leur parti politique à l'aide d'un jeu de couleurs : rouge pour les républicains, bleu pour les démocrates, gris pour les independants, jaune pour les whigs etc....
Source du jeu de données : wikidata 

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/4874708"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

Cependant, j'ai utilisé ce jeu de données pour montrer des choses comme par exemple, ici, dans cette visualisation en treemap qui permet aux données hiérarchiques de montrer toutes leurs informations et j'utilisé ce type de graphique pour montrer qu'il y a eu plus de présidents républicains que démocrates dans l'Histoire des Etats-Unis : 19 présidents républicains contre 16 présidents démoncrates. On peux voir un filtre qui nous permet de savoir combien de président sont originaires d'un Etat des Etats-Unis.
Cette visualisation dite en Treemap Chart me permet de faire une structure arborescente au niveau des Etats qui on vu des président naître. Je parlerai plus en détail de cette forme de visualisation dans une autre parti de ce document.

# Nouveau jeu de données, toujours sur la politique Américaine, le 117th congrès des Etats-Unis.


![Image du congrès américain](https://upload.wikimedia.org/wikipedia/commons/b/b5/2019_State_of_the_Union_%2840042020903%29_%28cropped%29.jpg)

Ce jeu de données a été acquis par une collecte de deux jeux de données sur Wikidata, l'un sur les sénateurs du 117th congrès des Etats-Unis et un autre jeu de données sur Wikidata sur les représentants du 117th congrès. 

## Acquisition des données sur le jeu de données sur le 117th congrès des Etats-Unis : 


le jeu de données initial sur les senateurs est le suivant, c'est un jeu de données qui viens de wikidata, voici la requête pour les sénateurs : 

```SPARQL

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


Pour également réaliser la collecte des données qui concernent les représentants du 117th congrès, j'ai juste modifié ce jeu de données des sénateurs par wd:Q4416090 pour le poste par wd:Q13218630. Cela me permet d'avoir les représentants présents dans ce 117th congrès des Etats-Unis. Ce jeu de données, qui est aussi un jeu de données wikidata est un jeu de données sur les représentants. Ce jeu de données est le suivant : 

```SPARQL
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

Pour utiliser ces deux jeux de données et en créer un seul, j'ai rassemblé ces deux jeux de données qui sont similaires dans un tableau CSV avec une enrichissement au niveau du poste (représentant ou sénateur). Je suis ensuite passé à la deuxième étape qui est la structure des données grâce à OpenRefine, ce qui explique le travail de datawrangling. Grâce à OpenRefine j'ai pu nettoyer les données au niveau des doublons sur certains sénateurs et représentant, en particulier les doublons en lien avec le parti politique de la personne, la requête de wikidata indiquait les partis régionalistes des démocrates et des républicains, j'ai donc dû, grâce au fitre sur OpenRefine, rapidement trouvé les doublons, puis réaliser une optimisation des données au niveau du lieu de naissance, la date de naissance, le parti politique, l'Etat où la personne réside et, entre autre, le poste (soit sénateur ou représentant). Tous cela est illustré par les document Jsons suivants, qui sont disponibles dans des fichiers weTransfer qui sont les suivants : [lien weTransfer](https://we.tl/t-A8uwNRhthf)

Cependant, en réalisant le datawrangling sur OpenRefine et en optimisant les données comme pour le jeu de donnés sur les présidents, j'ai constaté qu'il manquait 25 représentants dans le fichier. J'ai donc dû compléter les données à la main. Cette opération a été plus rapide en utilisant OpenRefine pour trouver les représentants manquants selon les Etats. J'ai ajouté à la suite du télechargement du document d'OpenRefine sur le 117th congrès sur Excel pour ajouter les représentants qui manquaient puis j'ai remis ce fichier excel sur OpenRefine et j'ai refait un datawrangling comme vous le verrez sur le document Json sur Wetransfer.

## Visualisation de l'information sur ce jeu de données sur le 117th congrès des Etats-Unis.

Grace à tous cela j'ai pu faire différentes visualisations sur le 117th congrès des Etat-Unis d'Amérique comme par exemple le nombre de sénateurs, représentants républicains et démoncratse selon le 117th congrès et selon les Etats. Cela donne la visualisation suivante qui est encore un Treemap et qui me permet de faire des visualisations de données qualifiés de hiérarchiques avec une arborescence selon la représentation demandée : ici, les sénateurs ou les représentants selon les partis avec des valeurs quantitative qui permettent de donner un chiffre aux données et quelques informations supplementaires. Grâce à cette visualisation on peut faire varier les données selon leurs tailles dans le jeu de données et leurs couleurs.

##  Editorialisation et visualisation des données 

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/5159833"><script src="https://public.flourish.studio/resources/embed.js"></script></div>


Dans cette visualisation, on peux voir en rouge le parti républicain, en bleu le parti démocrate et les indenpendant en jaune. Ici, au plus haut niveau, on peut voir que les répresentants démocrates sont plus nombreux (10 représentants de plus) en comparaison avec les représentants républicains qui sont au nombre de 212. Cela fait très peu et montre donc la fracture de l'Amérique en deux entre le camps de progressistes et les convervateurs. L'écart est le plus serré au Senat, en effet, en comptant les sénateurs Indepedants qui soutienent les démocrates et avec la voix de la vice-présidente des Etat-Unis, les démocrates ont la majorité à une voix près au Sénat. Cette visualisation, par le filtre, permet de voir la situation entre les démocrates et les républicains dans les différents Etats. Par exemple dans l'Etat de l'Alabama on peux voir que sur 7 représentants, il n'y a qu'une seule représentante démocrate, ce qui permet de faire différentes interprétations.

Ici, dans cette autre visualisation dite hiérarchique en Sunburst qui permet de visualiser les données dite hiérarchiques en secteurs et sur différents niveaux est réalisée la visualisation du 117th congrès des Etats-Unis d'Amérique. Il y a un niveau qui qualifie les politiciens au niveau de leur parti, puis un autre niveau sur leurs fonctions et pour finir le dernier niveau sur leur genre. J'ai ajouté la représentation des femmes politiciennes dans ce 117th congrès selon les partis et les postes : sénatrice ou représentante et aussi selon Etats où elles est siègent.

<div class="flourish-embed flourish-hierarchy" data-src="visualisation/5102340"><script src="https://public.flourish.studio/resources/embed.js"></script></div>

On peut voir ici qu'il y a plus de femmes dans le parti démocrate que dans le parti républicain, par exemple sur 222 représentants démocrates, il y a 89 femmes et 133 hommes en comparaison avec le parti républicain qui compte parmi 212 représentants, 182 hommes et 30 femmes. On peut faire la même étude au niveau du Sénat entre les sénatrices et les sénateurs et aussi par Etats. Il y a un Etat, l'Etat de Washigton pour lequel le nombre de femmes dans la représentation politique est le plus élèvé et dépasse celui des hommes. 
Pour différencier les femmes et les hommes dans cette visualisation, j'ai mis les femmes en rose, mis les hommes en vert en gardant les mêmes couleurs pour les partis politiques.


Dans cette dernière visualisation, je vous montre la liste définitive des politiciens du 117th congrès des Etats-Unis d'Amérique qui est un tableau qui est a été travaillé grâce au logiciel Datawrapper

<iframe title="La liste des politiciens du 117th congrès" aria-label="chart" id="datawrapper-chart-S23X1" src="https://datawrapper.dwcdn.net/S23X1/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="1488"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",(function(a){if(void 0!==a.data["datawrapper-height"])for(var e in a.data["datawrapper-height"]){var t=document.getElementById("datawrapper-chart-"+e)||document.querySelector("iframe[src*='"+e+"']");t&&(t.style.height=a.data["datawrapper-height"][e]+"px")}}))}();
</script>

Grâce a cette visualisation réalisée sur Darawrapper, j'ai mis en avant le genre des politiciens avec la couleur rose pour les femmes et la couleur bleu pour les hommes mais aussi des couleurs pour les partis politiques, en bleu, le parti démocrate et en rouge le parti républicain. Pour finir, j'ai ajouté un mini-moteur de recherche et un filtre au niveau des dates de naissance des politiciens. Grâce a cela on peut savoir qui est le plus jeune politicien du congrès qui est Madison Cawthorn, né en 1995 et les plus anciens qui sont nés en 1933 et qui sont au nombre de 3. Cette représentation permet également d'avoir la liste complète de la représentation du pouvoir législatif aux Etats-Unis.
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
