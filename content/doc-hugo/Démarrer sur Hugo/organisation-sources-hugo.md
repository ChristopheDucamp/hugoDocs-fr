+++
title = "Organisation des Sources Hugo"
description = "La structure de répertoire Hugo"
weight = 6
+++

{{% notice note %}}
[Source "Source Organization"](http://gohugo.io/overview/source-directory/ "Permalien vers Hugo - Source Organization") - documentation officielle Hugo, demeurant le seul lien de référence.
{{% /notice %}}

Hugo prend un dossier unique et l'utilise comme l'input pour créer un site web complet.

Le niveau supérieur d'un répertoire source aura généralement les éléments suivants :
    
    ▸ archetypes/
    ▸ content/
    ▸ data/
    ▸ i18n/
    ▸ layouts/
    ▸ static/
    ▸ themes/
      config.toml
    

Apprenez-en plus sur les différents dossiers et quels sont leurs objectifs 

  * [config]({{%relref "configurer-hugo.md"%}})
  * [data](http://gohugo.io/extras/datafiles/)
  * [i18n](http://gohugo.io/content/multilingual/#translation-of-strings)
  * [archetypes](http://gohugo.io/content/archetypes/)
  * [content](http://gohugo.io/content/organization/)
  * [layouts](http://gohugo.io/templates/overview/)
  * [static](http://gohugo.io/themes/creation/#static)
  * [themes](http://gohugo.io/themes/overview/)

## Exemple

Un répertoire exemple peut ressembler à ce qui suit :
    
    .
    ├── config.toml
    ├── archetypes
    |   └── default.md
    ├── content
    |   ├── post
    |   |   ├── premierpost.md
    |   |   └── secondpost.md
    |   └── citation
    |   |   ├── premier.md
    |   |   └── second.md
    ├── data
    ├── i18n
    ├── layouts
    |   ├── _default
    |   |   ├── single.html
    |   |   └── list.html
    |   ├── partials
    |   |   ├── header.html
    |   |   └── footer.html
    |   ├── taxonomy
    |   |   ├── category.html
    |   |   ├── post.html
    |   |   ├── quote.html
    |   |   └── tag.html
    |   ├── post
    |   |   ├── li.html
    |   |   ├── single.html
    |   |   └── summary.html
    |   ├── quote
    |   |   ├── li.html
    |   |   ├── single.html
    |   |   └── summary.html
    |   ├── shortcodes
    |   |   ├── img.html
    |   |   ├── vimeo.html
    |   |   └── youtube.html
    |   ├── index.html
    |   └── sitemap.xml
    ├── themes
    |   ├── hyde
    |   └── doc
    └── static
        ├── css
        └── js
    

Cette structure de répertoire nous en dit beaucoup sur ce site : 

  1. le site web prévoit d'avoir deux types de contenus : _posts_ et _citations_.
  2. il appliquera aussi deux taxonomies différentes à ce contenu : _categories_ et _tags_.
  3. il affichera le contenu dans trois vues différentes : une liste, un résumé et une vue pleine page.
  
  
## Contenu pour la page d'accueil et d'autres pages de listes
 
Depuis Hugo 0.18, “tout” est une `Page` qui peut avoir du contenu et des métadonnées, comme les `.Params` qui lui sont attachés – et partager le même ensemble de [variables de page](http://gohugo.io/templates/variables/) (en).

Pour ajouter du contenu et un front matter à la page d'accueil, une section, une taxonomie ou une liste de termes de taxonomie, ajoutez un fichier markdown avec le même nom de base `_index` au bon endroit dans le système de fichiers.

Pour le contenu par défaut Markdown, le nom de fichier sera `_index.md`.

Voir l'arbre exemple de répertoire ci-dessous.

**Notez que vous ne devez pas créer de fichier `_index` pour chaque section, taxonomie et similaires, une page par défaut sera créée si elle n'est pas présente, mais sans contenu et sans valeurs par défaut pour `.Title` etc.**


****
    
    └── content
        ├── _index.md
        ├── categories
        │   ├── _index.md
        │   └── photo
        │       └── _index.md
        ├── post
        │   ├── _index.md
        │   └── firstpost.md
        └── tags
            ├── _index.md
            └── hugo
                └── _index.md
    

[Dernière révision du 11 mai 2017](https://github.com/gohugoio/hugoDocs/commit/5176e52b38ffc1d9f2804dbd9d9371092e2c785a)


  

