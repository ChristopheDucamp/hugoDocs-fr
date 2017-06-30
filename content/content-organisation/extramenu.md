+++
title = "Entrées de menu supplémentaires"
date = "2017-04-29T18:36:24+02:00"
+++

Vous pouvez définir des entrées de menu supplémentaires dans le menu de navigation sans quelque lien vers le contenu.

Modifiez la configuration du site web `config.toml` et ajoutez une entrée `[[menu.shortcuts]]` pour chaque lien que vous voulez ajouter.

Exemple pour le site web actuel, **remarquez le param  `pre`** qui vous permet d'insérer du code HTML et utilisé ici pour séparer le contenu du menu de ce menu "statique".  

	[[menu.shortcuts]]
	pre = "<h3>Plus</h3>"
	name = "<i class='fa fa-github'></i> Repo GitHub"
	identifier = "ds"
	url = "https://github.com/vjeantet/hugo-theme-docdock"
	weight = 1

	[[menu.shortcuts]]
	name = "<i class='fa fa-bookmark'></i> Documentation Hugo"
	identifier = "hugodoc"
	url = "https://gohugo.io/"
	weight = 2


[{{%icon circle-arrow-right%}} Regardez ici la documentation officielle de Hugo sur le menu](https://gohugo.io/extras/menus/)