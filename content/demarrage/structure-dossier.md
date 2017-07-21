---

title: "Structure de Dossier"
description: "La CLI Hugo échafaude une structure de projet en dossiers et puis prend cet unique dossier et l'utilise comme l'input pour créer un site web complet."
weight: 8
aliases: [/démarrage/directory-structure]
toc: true
lastmod: 2017-07-21

---

L'interface de ligne de commande d'Hugo échafaude une structure de projet en dossiers et puis prend cet unique dossier et l'utilise comme l'input pour créer un site web complet.

## Échafaudage de Nouveau Site
L'exécution du générateur `hugo new site` à partir de la ligne de commande créera une structure de répertoire avec les éléments suivants :  

    .
    ├── archetypes
    ├── config.toml
    ├── content
    ├── data
    ├── layouts
    ├── static
    └── themes
    

## Explication de la Structure des Dossiers

Ce qui suit est un survol de chacun des dossiers avec les liens vers leurs sections respectives dans la documentation Hugo.

[`archetypes`](/gestion-contenu/archetypes/)

Vous pouvez créer de nouveaux fichiers de contenu dans Hugo en utilisant la commande `hugo new`. Par défaut, hugo créera de nouveaux fichiers de contenu avec au moins `date`,` title` (déduit du nom du fichier) et `draft = true`. Cela permet d'économiser du temps et favorise la cohérence des sites utilisant plusieurs types de contenu. Vous pouvez créer vos propres [archétypes](/gestion-contenu/archetypes/) avec des champs personnalisés préconfigurés personnalisés.

[`config.toml`](/demarrage/configuration/) 

Chaque projet Hugo devrait avoir un fichier de configuration au format TOML, YAML ou JSON à la racine. De nombreux sites peuvent nécessiter peu ou pas de configuration, mais Hugo est livré avec un grand nombre de [directives de configuration](configuration) pour des instructions plus détaillées sur la façon dont vous voulez que Hugo construise votre site web.

[`content`](/gestion-contenu/organisation/)

Tout le contenu de votre site web vivra dans ce dossier. Chaque dossier de plus haut niveau dans Hugo est considéré comme une [section de contenu](/gestion-contenu/sections/). Par ex., si votre site a trois sections principales —`blog`, `articles`, et  `tutoriels`—vous aurez trois dossiers  sur `content/blog`, `content/articles`, and `content/tutoriels`. Hugo utilise les sections pour assigner des [types de contenus](/gestion-contenu/types/) par défaut.

[`data`](/templates/data-templates/)

Ce répertoire est utilisé pour stocker des fichiers de configuration pouvant être utilisés par Hugo lors de la génération de votre site. Vous pouvez écrire ces fichiers au format YAML, JSON ou TOML. En plus des fichiers que vous ajoutez à ce dossier, vous pouvez également créer [modèles de données](https://gohugo.io/templates/data-templates/) qui tirent du contenu dynamique.

[`layouts`](/templates/) 

Stocke les modèles sous la forme de fichiers `.html` qui spécifient comment les vues de votre contenu seront rendues dans un site Web statique. Les modèles incluent des [pages de liste](/templates/liste/), votre [page d'accueil](/templates/page-accueil/), des [modèles de taxonomie](/templates/taxonomy-templates/), des [partiels](/templates/partials/), des [modèles de page unique](/templates/single-page-templates/), et plus encore.

`static` 

stocke tout le contenu statique pour votre futur site : images, CSS, JavaScript, etc. Lorsque Hugo construit votre site, tous les actifs de votre dossier statique sont copiés au moment où cela se produit. Un bon exemple d'utilisation du dossier `static` est pour [vérifier la propriété du site sur Google Search Console](https://support.google.com/analytics/answer/1142414?hl=fr), où vous souhaitez que Hugo copie un fichier HTML complet sans modifier son contenu.

{{% notice note %}}
Hugo n'est actuellement pas livré avec un pipeline d'asset ([#3207](https://github.com/gohugoio/hugo/issues/3207)). Vous pouvez solliciter la communauté dans les [forums Hugo](https://discourse.gohugo.io) ou regarder quelques [starter kits Hugo](/outils/starter-kits/) pour des exemples sur la façon dont les développeurs gèrent des assets statiques.  
{{% /notice %}}



