+++
title = "Créer une Page"
description = ""
date = "2017-06-30T18:36:24+02:00"
creatordisplayname = "Valere JEANTET"
creatoremail = "valere.jeantet@gmail.com"
lastmodifierdisplayname = "Christophe Ducamp"
lastmodifieremail = "christophe.ducamp@gmail.com"
tags = ["page","creation"]
weight = 10
pre ="<i class='fa fa-edit'></i> "

+++


Le thème Hugo docDock définit deux types de page. _Default_ et _Slide_.

* **Default** est la page commune comme celle que vous êtes en train de lire.
* **Slide** est une page qui utilise le plein écran pour afficher son contenu en markdown sous forme de [présentation reveals.js](http://lab.hakim.se/reveal-js/).
* **HomePage** est un contenu spécial qui sera affiché sous forme de contenu de page d'accueil.

Pour indiquer à au thème docdock Hugo de considérer une page comme un dia, ajoutez simplement un `type="slide"` dans le  frontmatter de votre fichier. [{{%icon circle-arrow-right%}}lire ici pour en savoir plus pour transformer une page en slide]({{%relref "page-slide.md"%}})


Hugo-theme-docdock fournit des archétypes pour vous aider à créer ce type de pages.


## Front Matter
Chaque page Hugo doit définir un Front Matter en yaml, toml ou json.

Hugo-theme-docdock utilise les paramètres qui suivent au-dessus des paramètres déjà existants :

	+++
	# Type de contenu, réglez "slide" pour l'afficher en plein écran avec reveal.js
	type="page"

	# Nom du Créateur
	creatordisplayname = "Valère JEANTET"
	# E-mail du créateur
	creatoremail = "valere.jeantet@gmail.com"
	# Nom du dernier Auteur
	lastmodifierdisplayname = "xtof"
	# Email du dernier Auteur
	lastmodifieremail = "christophe@ducamp.me"
	+++


## Tri

Hugo fournit un moyen flexible pour gérer l'ordre de vos pages.

Le moyen le plus simple est d'utliser un param `weight` dans le front matter de votre page. 

[{{%icon circle-arrow-right%}}Cliquez ici pour en savoir plus sur l'organisation de contenus]({{%relref "content-organisation/_index.md"%}})
