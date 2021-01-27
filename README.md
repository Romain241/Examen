# Réalisation d'une datavisualisation des Archives Nationale pour le partiel de dataviz :

Pour réaliser cela, j'ai utilisé un jeux de données qui vient des jeux de données du ministère de la culture. Ce jeux de données sont des données liées aux Archives Nationale de France. 

Le premier jeu de données correspond aux grands documents et images de l'histoire de France conservés par les Archives nationales. 

## Grands documents et images de l'histoire de France conservés par les Archives nationales : 

<iframe src="https://data.culture.gouv.fr/explore/embed/dataset/grands-documents-et-images-de-lhistoire-de-france-conserves-par-les-archives-/table/?&static=false&datasetcard=false" width="700" height="300" frameborder="0"></iframe>


##  Test sur le  github de plusieurs visualisation de données : 

### Nombre de fromages par régions en France:

Cette représentation permet de voir le nombre de fromages par régions en France. Ce graphique utilise le jeu de données qui réunit la liste de 338 fromages en France. Ce jeu de données vient d'une page Wikipédia ( Liste des spécialités régionales française de formages). 
Lien de la page Wikipédia :([https://fr.wikipedia.org/wiki/Liste_des_spécialités_régionales_françaises_de_fromages]).

<iframe src="https://data.opendatasoft.com/explore/embed/dataset/fromagescsv-fromagescsv@public/analyze/?disjunctive.fromage&dataChart=eyJxdWVyaWVzIjpbeyJjb25maWciOnsiZGF0YXNldCI6ImZyb21hZ2VzY3N2LWZyb21hZ2VzY3N2QHB1YmxpYyIsIm9wdGlvbnMiOnsiZGlzanVuY3RpdmUuZnJvbWFnZSI6dHJ1ZX19LCJjaGFydHMiOlt7ImFsaWduTW9udGgiOnRydWUsInR5cGUiOiJjb2x1bW4iLCJmdW5jIjoiQ09VTlQiLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiIjMDA4NkQ2In1dLCJ4QXhpcyI6ImRlcGFydGVtZW50IiwibWF4cG9pbnRzIjo1MCwic29ydCI6IiJ9XSwidGltZXNjYWxlIjoiIiwiZGlzcGxheUxlZ2VuZCI6dHJ1ZSwiYWxpZ25Nb250aCI6dHJ1ZX0%3D&static=false&datasetcard=false" width="700" height="500" frameborder="0"></iframe>

Dans cette représentation, on peut voir que le département de l'Ain à plus de 12 types de formages. ce graphique permet de voir la répartition des formations par région de France. 

### Le type de lait utilisé dans la réalisation des fromages en France:

Cette représentation permet de voir le type de lait utilisé dans la créaction de fromages en France. Pour voir les différents types de lait, on a utiliser le même jeu de données que l'étude précedent. Cette représentation est un Treemap.

<iframe src="https://data.opendatasoft.com/explore/embed/dataset/fromagescsv-fromagescsv@public/analyze/?disjunctive.fromage&dataChart=eyJxdWVyaWVzIjpbeyJjb25maWciOnsiZGF0YXNldCI6ImZyb21hZ2VzY3N2LWZyb21hZ2VzY3N2QHB1YmxpYyIsIm9wdGlvbnMiOnsiZGlzanVuY3RpdmUuZnJvbWFnZSI6dHJ1ZX19LCJjaGFydHMiOlt7ImFsaWduTW9udGgiOnRydWUsInR5cGUiOiJ0cmVlbWFwIiwiZnVuYyI6IkNPVU5UIiwic2NpZW50aWZpY0Rpc3BsYXkiOnRydWUsImNvbG9yIjoicmFuZ2UtY3VzdG9tIiwicG9zaXRpb24iOiJjZW50ZXIifV0sInhBeGlzIjoibGFpdCIsIm1heHBvaW50cyI6NTAsInNvcnQiOiIiLCJzZXJpZXNCcmVha2Rvd24iOiIiLCJzZXJpZXNCcmVha2Rvd25UaW1lc2NhbGUiOiIifV0sInRpbWVzY2FsZSI6IiIsImRpc3BsYXlMZWdlbmQiOnRydWUsImFsaWduTW9udGgiOnRydWV9&static=false&datasetcard=false" width="700" height="500" frameborder="0"></iframe>

On peut dit que sur 338 fromages, 243 des fromages sont réalisé par du lait de Vache, 61 sont réalisé avec du lait de Chèvre, 34 avec du lait de Brebis.

# Exercice sur Wikidata Query Sercice : 

## les peintures de Claude Monet : 

```
select DISTINCT ?peinture 
where {
 ?peinture wdt:P170 wd:Q296.

SERVICE wikibase:label { #pour récuéprer les labels
bd:serviceParam wikibase:language "fr,en"}
}
```
## Avec les labels (via le service wikibase:label) et les images associées :

```
select DISTINCT ?peinture ?peintureLabel ?img 
where {
 ?peinture wdt:P170 wd:Q296.
 ?peinture wdt:P18 ?img.
  
  
SERVICE wikibase:label { #pour récuéprer les labels
bd:serviceParam wikibase:language "fr,en"}
}
```

## Avec en option (via OPTIONAL) les collections/lieux de conservation : 

```
select DISTINCT ?peinture ?peintureLabel ?img ?lieux ?lieuxLabel
where {
 ?peinture wdt:P170 wd:Q296.
 ?peinture wdt:P18 ?img.
OPTIONAL {?peinture wdt:P195 ?lieux
}  
  
SERVICE wikibase:label { #pour récuéprer les labels
bd:serviceParam wikibase:language "fr,en"}
}
```
<iframe src="https://data.culture.gouv.fr/explore/embed/dataset/grands-documents-et-images-de-lhistoire-de-france-conserves-par-les-archives-/images/?dataChart=eyJxdWVyaWVzIjpbeyJjaGFydHMiOlt7InR5cGUiOiJjb2x1bW4iLCJmdW5jIjoiQ09VTlQiLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiIjZmZkOTJmIn1dLCJ4QXhpcyI6ImRhdGUiLCJtYXhwb2ludHMiOiIiLCJ0aW1lc2NhbGUiOiJ5ZWFyIiwic29ydCI6IiIsImNvbmZpZyI6eyJkYXRhc2V0IjoiZ3JhbmRzLWRvY3VtZW50cy1ldC1pbWFnZXMtZGUtbGhpc3RvaXJlLWRlLWZyYW5jZS1jb25zZXJ2ZXMtcGFyLWxlcy1hcmNoaXZlcy0iLCJvcHRpb25zIjp7fX19XSwidGltZXNjYWxlIjoiIiwiZGlzcGxheUxlZ2VuZCI6dHJ1ZSwiYWxpZ25Nb250aCI6dHJ1ZX0%3D&static=false&datasetcard=true" width="800" height="600" frameborder="0"></iframe>
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
