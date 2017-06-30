+++
title = "Présenter une Slide"
description = ""
date = "2017-04-24T18:36:24+02:00"
+++

Une page basique de contenu md peut être restituée comme une présentation plein écran reveal.js.

{{%alert info%}}Vous pouvez aussi, **embarquer une présentation dans une page** sous forme de petite boîte, en utilisant le raccourci de code (shortcode) [revealjs]({{% relref "shortcodes/revealjs.md"%}}) dans votre fichier md.{{%/alert%}}

## Mise en Page
Utilisez votre syntaxe commune Markdown que vous utilisez dans Hugo, n'oubliez pas que vous pouvez aussi placer des balises HTML.

{{%notice info%}}Une syntaxe spéciale (en commentaire html) est disponible pour ajouter des attribut aux éléments Markdown. Ceci est utile entre autre pour les fragments.{{%/notice%}}

Lisez SVP la [{{%icon book%}} doc d'hakimel](https://github.com/hakimel/reveal.js/#instructions)

## Options
Dans le frontmatter de votre fichier page, réglez les paramètres **type** et **revealOptions**.

Votre contenu sera servi sous forme de présentation plein écran revealjs et revealOptions sera utilisé pour ajuster son comportement.

    +++
	title = "Dia Test"
	type="slide"

	theme = "league"
	[revealOptions]
	transition= 'concave'
	controls= true
	progress= true
	history= true
	
	center= true
	+++
	
	
[apprenez-en plus sur les options reveal ici](https://github.com/hakimel/reveal.js/#configuration)


## Délimiteurs de slides 

Au moment de créer le contenu de votre diaporama pour votre présentation dans le fichier de contenu markdown, vous devez pouvoir faire la distinction entre une dia et la suivante. Ceci peut être simplement réalisé en utilisant une convention dans le Markdown qui indique le démarrage de chaque nouvelle slide.

Le fait que les slides horizontales et verticales soient supportées par reveal.js, chacune d'entre elles dispose de  son propre et unique délimiteur.


Pour indiquer le démarrage d'une slide horizontale, ajoutez simplement le délimiteur suivant dans votre Markdown (3 tirets `---` :

	---


Pour indiquer le démarrage d'une slide verticale, ajoutez simplement le délimiteur suivant dans votre Markdown (3 tirets du bas `___`)  :

    ___

Ainsi en utilisant une combinaison de slides horizontales et verticales, vous pouvez personnaliser la navigation dans votre présentation diaporama. Généralement les slides verticales sont utilisées pour présenter de l'information sous une slide horizontale de niveau le plus haut. 


Par exemple, une présentation de diaporama simple peut être créée comme suit :
```
+++

title = "test"
date = "2017-04-24T18:36:24+02:00"
type="slide"

theme = "league"
[revealOptions]
transition= 'concave'
controls= true
progress= true
history= true
center= true
+++

# Le matin 

___

## Lever

- Couper le réveil
- Sortir du lit

___

## Petit-déjeuner

- Manger des oeufs
- Boire du café

---

# Soirée 

___

## Dîner

- Manger des spaghetti
- Boire du vin

___

## Aller dormir

- Aller au lit
- Compter les moutons

```


[{{%icon expand%}}Cliquez ici pour voir un rendu de cette page]({{%relref "myslide.md"%}})