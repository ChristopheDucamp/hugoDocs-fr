---
title: Front Matter
linktitle:
description: Hugo vous permet d'ajouter un front matter en yaml, toml, ou json à vos fichiers de contenu.
date: 2017-01-09
publishdate: 2017-01-09
lastmod: 2017-07-19
categories: [gestion de contenu]
#tags: [front matter, yaml, "toml", "json", "metadata", archetypes]
draft: false
aliases: [/content/front-matter/]
toc: true
---

Le **Front matter** vous permet de garder les métadonnées attachées à une instance d'un [type de contenu][content type]  ---c'est-à-dire incorporée dans un fichier de contenu--- et c'est l'une des nombreuses fonctionnalités qui donne à Hugo sa force.

## Formats de Front Matter

Hugo prend en charge trois formats pour le front matter, chacun avec ses propres jetons d'identification.

TOML
: identifié par des `+++` d'ouverture et de fermeture.

YAML
: identifié par des `---` d'ouverture et de fermeture.

JSON
: un objet unique JSON entouré de '`{`' and '`}`', suivi par une nouvelle ligne.

### Exemple TOML

```toml
+++
title = "spf13-vim 3.0 release and new website"
description = "spf13-vim is a cross platform distribution of vim plugins and resources for Vim."
tags = [ ".vimrc", "plugins", "spf13-vim", "vim" ]
date = "2012-04-06"
categories = [
  "Development",
  "VIM"
]
slug = "spf13-vim-3-0-release-and-new-website"
+++
```

### Exemple YAML

```yaml
---
title: "spf13-vim 3.0 release and new website"
description: "spf13-vim is a cross platform distribution of vim plugins and resources for Vim."
#tags: [ ".vimrc", "plugins", "spf13-vim", "vim" ]
lastmod: 2015-12-23
date: "2012-04-06"
categories:
  - "Development"
  - "VIM"
slug: "spf13-vim-3-0-release-and-new-website"
---
```

### Exemple JSON

```json
{
    "title": "spf13-vim 3.0 release and new website",
    "description": "spf13-vim is a cross platform distribution of vim plugins and resources for Vim.",
    "tags": [ ".vimrc", "plugins", "spf13-vim", "vim" ],
    "date": "2012-04-06",
    "categories": [
        "Development",
        "VIM"
    ],
    "slug": "spf13-vim-3-0-release-and-new-website"
}
```

## Variables du Front Matter

### Prédéfinies

Il existe quelques variables prédéfinies reconnues par Hugo. Voir [Variables de page][pagevars] pour savoir comment appeler plusieurs de ces variables prédéfinies dans vos modèles.


`aliases`
: une liste d'un ou plusieurs alias (par ex. les chemins anciennement publiés ou le contenu renommé) qui sera créé dans la sortie de la structure de dossiers. Voir [Alias][aliases] pour les détails.

`date`
: la datetime à laquelle le contenu a été créé ; notez que cette valeur est auto-remplie selon l'[archetype][] intégré dans Hugo.

`description`
: la description pour le contenu.

`draft`
: si `true`, le contenu ne sera pas sorti à moins que le flag  `--buildDrafts` ne soit passé dans la commande `hugo`.

`expiryDate`
: la datetime à laquelle le contenu ne devrait plus être publié par Hugo ; le contenu expiré ne sera pas sorti à moins que le flag `--buildExpired` ne soit passé dans la commande `hugo`.

`isCJKLanguage`
: if `true`, Hugo will explicitly treat the content as a CJK language; both `.Summary` and `.WordCount` work properly in CJK languages.

`keywords`
: les mots-clés méta pour le contenu.

`layout`
: le  layout qu'Hugo devrait sélectionner à partir de l'[ordre de recherche][lookup] au moment de sortir le contenu. Sin un  `type` n'est pas spécifié dans le front matter, Hugo cherchera le layout du même nom dans le dossier layout qui correspond à une section de contenu. Voir ["Définir un Type de Contenu"][definetype]

`lastmod`
: la datetime à laquelle le contenu a été dernièrement modifié.

`linkTitle`
: utilisé pour créer des liens vers le contenu ; s'il est réglé,    les valeurs par défaut seront d'utliser le `linktitle` avant le `title`. Hugo peut aussi [trier des listes de contenu par  `linktitle`][bylinktitle].

`markup`
: **expérimental**; spécifier `"rst"` pour reStructuredText (requiert`rst2html`) ou `"md"` (default) pour le Markdown.

`outputs`
: vous permet de spécifier les formats de sortie spéciques au contenu. Voir [formats de sortie][outputs].

`publishDate`
: si dans le futur, le contenu ne sera pas sorti à moins que le flag `--buildFuture` soit passé à `hugo`.

`slug`
: apparaît comme la queue de la sortie URL. Une valeur spécifiée dans le front matter écrasera le segment de l'URL basé sur le nom de fichier.

`taxonomies`
: these will use the field name of the plural form of the index; see the `tags` and `categories` in the above front matter examples.

`title`
: le titre du contenu.

`type`
: le type de contenu ; cette valeur sera automatiquement dérivée à partir du répertoire (par ex., la [section][]) si non spécifiée ans le front matter.

`url`
: le chemin complet vers le contenu à partir de la racine web. Cela ne fait aucune hypothèse sur le chemin du fichier de contenu. Cela ignore aussi tout préfixe de langue de la fonctionnalité multilingue.

`weight`
: utilisé pour [ordonner votre contenu en listes][trier].

{{% note "URL de destination par défaut dans Hugo" %}}
Si ni le `slug` ni `url` ne sont présents et que les [permalinks ne sont pas configurés autrement dans votre fichier `config` de site](/gestion-contenu/urls/#permalinks), Hugo utilisera le nom de fichier de votre contenu pour créer l'output URL. Voir [Organisation du Contenu](/gestion-contenu/organisation) pour une explication des chemins dans Hugo et la [Gestion d'URL](/gestion-contenu/urls/) sur les moyens de personnaliser les comportements par défaut d'Hugo.
{{% /note %}}

### Définies par l'Utilisateur

Vous pouvez ajouter des champs à votre front matter rbitrairement pour répondre à vos besoins. Ces valeurs-clés définies par l'utilisateur sont placées dans une seule variable `.Params` à utiliser dans vos modèles.

Vous pouvez accéder aux champs suivants via `.Params.include_toc` et` .Params.show_comments`, respectivement. La section [Variables][] fournit plus d'informations sur l'utilisation des variables de niveau de page et de site de Hugo dans vos modèles.

```yaml
include_toc: true
show_comments: false
```

## Ordre de Contenu via le Front Matter

Vous pouvez affecter un "poids" spécifique au contenu dans le front matter de votre contenu. 
Ces valeurs sont particulièrement utiles pour le [classement][ordering] dans les vues de liste. Vous pouvez utiliser `weight` pour l'ordre du contenu et la convention [`<TAXONOMIE>_weight`][taxweight] pour ordonner le contenu dans une taxonomie. Voir [Ordre et regroupement des listes Hugo][lists] pour voir comment le `weight` peut être utilisé pour organiser votre contenu dans les listes.

## Remplacer la Configuration de Markdown Global

Il est possible de définir certaines options pour le rendu Markdown dans un front matter de contenu pour remplacer les options de rendu BlackFriday définies dans la [configuration de votre projet][config].

## Specs des Formats Front Matter

* [TOML Spec][toml]
* [YAML Spec][yaml]
* [JSON Spec][json]

[variables]: /variables/
[aliases]: /gestion-contenu/urls/#aliases/
[archetype]: /gestion-contenu/archetypes/
[bylinktitle]: /templates/lists/#by-link-title
[config]: /demarrage/configuration/ "Documentation Hugo pour la configuration du site"
[content type]: /gestion-contenu/types/
[contentorg]: /gestion-contenu/organisation/
[definetype]: /gestion-contenu/types/#definir-un-type-de-contenu "Apprendre comment spécifier un type et un layout dans un frontmatter de contenu"
[json]: /documents/ecma-404-json-spec.pdf "Specification pour JSON, JavaScript Object Notation"
[lists]: /templates/lists/#ordering-content "Voir comment trier le contenu dans les pages de liste; par exemple, les modèles qui cherchent un _index.md spécifique pour le contenu et le front matter."
[lookup]: /templates/lookup-order/ "Hugo traverse vos modèles dans un ordre spécifique au moment de rendre le contenu pour vous permettre une modélisation DRY."
[trier]: /templates/lists/ "Hugo fournit plusieurs moyens de trier et ordonner votre contenu dans les modèles de liste"
[outputs]: /templates/output-formats/ "Avec la sortie de v22, vous pouvez sortir votre contenu vers n'importe quel format de texte en utilisant la modélisation Hugo"
[pagevars]: /variables/page/
[section]: /gestion-contenu/sections/
[taxweight]: /gestion-contenu/taxonomies/
[toml]: https://github.com/toml-lang/toml "Specification for TOML, Tom's Obvious Minimal Language"
[urls]: /gestion-contenu/urls/
[variables]: /variables/
[yaml]: http://yaml.org/spec/ "Specification for YAML, YAML Ain't Markup Language"
