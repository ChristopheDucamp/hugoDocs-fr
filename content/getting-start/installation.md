+++
title = "Installation"
description = ""
weight = 1
+++

{{% alert theme="warning" %}}HUGO **v0.22** est la version minimum requise pour utiliser ce thème{{%/alert%}}

Les étapes suivantes sont là pour vous aider à initialiser votre nouveau site web. Si vous ne connaissez pas du tout Hugo, nous vous suggérons vraiment de vous entraîner en suivant cette [doc géniale pour les débutants](https://gohugo.io/overview/quickstart/).
<!--more-->

## Créez votre Documentation

Hugo fournit une commande `new` pour créer un nouveau site web.

	$ hugo new site <votre_nouveau_site_web>

## Installez Le Thème

Installez le thème **Hugo-theme-docdock** en suivant ces instructions : 

Rendez-vous à l'intérieur du dossier `themes` et téléchargez le thème 

	$ cd themes
	$ git clone https://github.com/vjeantet/hugo-theme-docdock.git docdock

Autre alternative, vous pouvez [{{%icon download%}} télécharger le thème sous forme de fichier .zip](https://github.com/vjeantet/hugo-theme-docdock/archive/master.zip) et l'extraire dans le dossier `themes`

## Configuration Basique

[Suivez les instructions ici]({{%relref "configuration.md"%}})