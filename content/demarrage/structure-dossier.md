---
title: Structure de Dossier
linktitle: Stucture de Dossier
description: L'interface de ligne de commande (CLI) d'Hugo échafaude une structure de projet en dossiers et l'utilise ensuite comme l'input pour créer un site web complet.
date: 2017-01-02
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [démarrage,fondamentaux]
#tags: [source, organisation, dossiers]
menu:
  docs:
    parent: "demarrage"
    weight: 50
weight: 50
sections_weight: 50
draft: false
aliases: [/demarrage/directory-structure]
toc: true
---

## Échafaudage de Nouveau Site
Le lancement du générateur `hugo new site` à partir de la ligne de commande créera une structure de répertoire avec les éléments suivants :  

 ```bash
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes
```

## La Structure des Dossiers Expliquée

Ce qui suit est un survol de chacun des dossiers avec les liens vers leurs sections respectives dans la documentation Hugo.

[`archetypes`](/gestion-contenu/archetypes/)
: Vous pouvez créer de nouveaux fichiers de contenu dans Hugo en utilisant la commande `hugo new`. 
Par défaut, hugo créera de nouveaux fichiers de contenu avec au moins `date`,` title` (déduits du nom du fichier) et `draft = true`. Cela permet d'économiser du temps et favorise la cohérence des sites utilisant plusieurs types de contenu. Vous pouvez aussi créer vos propres [archétypes](/gestion-contenu/archetypes/) avec des champs personnalisés de front matter pré-configurés.

[`config.toml`](/demarrage/configuration/)
: Chaque projet Hugo devrait avoir un fichier de configuration à la racine au format TOML, YAML ou JSON. De nombreux sites peuvent nécessiter peu ou pas de configuration, mais Hugo est livré avec un grand nombre de [directives de configuration][] pour des instructions plus détaillées sur la façon dont vous voulez que Hugo construise votre site web.

[`content`][]
: Tout le contenu de votre site web vivra dans ce dossier. Chaque dossier au plus haut niveau dans Hugo est considéré comme une [section de contenu][]. Par ex., si votre site a trois sections principales —`blog`, `articles`, et  `tutoriels`—vous aurez trois dossiers  sur `content/blog`, `content/articles`, and `content/tutoriels`. Hugo utilise les sections pour assigner des [types de contenus](/gestion-contenu/types/) par défaut.

[`data`][]
: Ce répertoire est utilisé pour stocker des fichiers de configuration pouvant être utilisés par Hugo lors de la génération de votre site. Vous pouvez écrire ces fichiers au format YAML, JSON ou TOML. En plus des fichiers que vous ajoutez à ce dossier, vous pouvez également créer [modèles de données][] qui extraient du contenu dynamique.

[`layouts`][] 
: Stocke les modèles sous la forme de fichiers `.html` qui spécifient comment les vues de votre contenu seront rendues dans un site web statique. Les modèles incluent des [pages de listes][], votre [page d'accueil][], des [modèles de taxonomie](/templates/taxonomy-templates/), des [partiels](/templates/partials/), des [modèles de page unique](/templates/single-page-templates/), et plus encore.

`static` 
: stocke tout le contenu statique pour votre futur site : images, CSS, JavaScript, etc. Lorsque Hugo construit votre site, tous les actifs de votre dossier statique sont copiés tels quels. Un bon exemple d'utilisation du dossier `static` est pour [vérifier la propriété du site sur la Consle de Recherche Google][searchconsole], où vous voulez que Hugo copie un fichier HTML complet sans modifier son contenu.

{{% note %}}
Hugo n'est actuellement pas livré avec un pipeline d'asset ([#3207](https://github.com/gohugoio/hugo/issues/3207)). Vous pouvez solliciter la communauté dans les [forums Hugo](https://discourse.gohugo.io) ou regarder quelques [starter kits Hugo](/outils/starter-kits/) pour des exemples sur la façon dont les développeurs gèrent des assets statiques.  
{{% /note %}}


[directives de configuration]: /demarrage/configuration#toutes-variables-yaml
[`content`]: /gestion-contenu/organisation/
[section de contenu]: /gestion-contenu/sections/
[types de contenu]: /gestion-contenu/types/
[`data`]: /templates/data-templates/
[modèles de données]: /templates/data-templates/
[page d'accueil]: /templates/page-accueil/
[`layouts`]: /templates/
[pages de listes]: /templates/listes/
[modèles de taxonomie]: /templates/taxononomie-templates/
[partiels]: /templates/partiels/
[modèles de page unique]: /templates/single-page-templates/
[searchconsole]: https://support.google.com/analytics/answer/1142414?hl=en


