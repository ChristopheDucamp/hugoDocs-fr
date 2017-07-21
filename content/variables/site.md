---
title: Site
linktitle: Variables de Site
description: Bon nombre, mais pas toutes, variables sur-tout-le-site sont définies dans votre configuration de site. Cependant, Hugo fournit des variables intégrées pour un accès pratique aux valeurs globales dans vos modèles.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-21
categories: [variables et params]
#tags: [global,site]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 10
weight: 10
sections_weight: 10
aliases: [/variables/site-variables/]
toc: true
---

Voici une liste de variables ("globales) au niveau-site. Bon nombres de ces variables sont définies dans votre [fichier de configuration](/demarrage/configurer-hugo/) du site, tandis que d'autres sont construites à l'intérieur du noyau d'Hugo pour un usage pratique dans vos modèles.

## Liste de Variables Site

`.Site.AllPages`
: array of all pages, regardless of their translation.

`.Site.Author`
: a map of the authors as defined in the site configuration.

`.Site.BaseURL`
: the base URL for the site as defined in the site configuration.

`.Site.BuildDrafts`
: a boolean (default: `false`) to indicate whether to build drafts as defined in the site configuration.

`.Site.Copyright`
: a string representing the copyright of your website as defined in the site configuration.

`.Site.Data`
: custom data, see [Data Templates](/templates/data-templates/).

`.Site.DisqusShortname`
: a string representing the shortname of the Disqus shortcode as defined in the site configuration.

`.Site.Files`
: all source files for the Hugo website.

`.Site.GoogleAnalytics`
: a string representing your tracking code for Google Analytics as defined in the site configuration.

`.Site.IsMultiLingual`
: whether there are more than one language in this site. See [Multilingual](/content-management/multilingual/) for more information.

`.Site.Language.Lang`
: the language code of the current locale (e.g., `en`).

`.Site.Language.LanguageName`
: the full language name (e.g. `English`).

`.Site.Language.Weight`
: the weight that defines the order in the `.Site.Languages` list.

`.Site.Language`
: indicates the language currently being used to render the website. This object's attributes are set in site configurations' language definition.

`.Site.LanguageCode`
: a string representing the language as defined in the site configuration. This is mostly used to populate the RSS feeds with the right language code.

`.Site.LanguagePrefix`
: this can be used to prefix URLs to point to the correct language. It will even work when only one defined language. See also the functions [absLangURL](/functions/abslangurl/) and [relLangURL](/functions/rellangurl).

`.Site.Languages`
: an ordered list (ordered by defined weight) of languages.

`.Site.LastChange`
: a string representing the date/time of the most recent change to your site. This string is based on the [`date` variable in the front matter](/content-management/front-matter) of your content pages.

`.Site.Menus`
: all of the menus in the site.

`.Site.Pages`
: array of all content ordered by Date with the newest first. This array contains only the pages in the current language.

`.Site.Permalinks`
: a string to override the default [permalink](/content-management/urls/) format as defined in the site configuration.

`.Site.RegularPages`
: a shortcut to the *regular* page collection. `.Site.RegularPages` is equivalent to `where .Site.Pages "Kind" "page"`.

`.Site.RSSLink`
: the URL for the site RSS.

`.Site.Sections`
: top-level directories of the site.

`.Site.Taxonomies`
: the [taxonomies](/taxonomies/usage/) for the entire site.  Replaces the now-obsolete `.Site.Indexes` since v0.11. Also see section [Taxonomies elsewhere](#taxonomies-elsewhere).

`.Site.Title`
: a string representing the title of the site.

## La Variable `.Site.Params`

`.Site.Params` is a container holding the values from the `params` section of your site configuration.

### Exemple : `.Site.Params`

Le fichier `config.toml` qui suit définit un param valable sur tout le site pour `description` :

```toml
baseURL = "http://votresite.exemple.com/"

[params]
  description = "Le Superbe Site Hugo de Tesla"
  author = "Nikola Tesla"
```

Vous pouvez utiliser `.Site.Params` dans un [modèle partiel](/templates/partiels/) pour appeler la description du site :

{{% code file="layouts/partials/head.html" %}}
```html
<meta name="description" content="{{if .IsHome}}{{ $.Site.Params.description }}{{else}}{{.Description}}{{end}}" />
```
{{% /code %}}

