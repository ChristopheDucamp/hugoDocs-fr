---
title: Mode Multilingue
linktitle: Multilinguisme et i18n
description: Hugo supporte la création de sites web avec plusieurs langues côte à côte.
date: 2017-01-10
publishdate: 2017-01-10
lastmod: 2017-07-20
categories: [content management, gestion de contenu]
#tags: [multilingual,i18n, internationalization, internationalisation, multilinguisme, ébauche]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 150
weight: 150	#rem
draft: false
aliases: [/content/multilingual/,/content-management/multilingual/]
toc: true
---

Vous devriez définir les langues disponibles dans une section `Languages` à l'intérieur de la configuration de votre site.

## Configurer les Langues

Ce qui suit est un exemple de configuration de site TOML pour un projet Hugo multilingue : 

{{% code file="config.toml" download="config.toml" %}}
```toml
DefaultContentLanguage = "en"
copyright = "Everything is mine"

[params.navigation]
help  = "Help"

[Languages]
[Languages.en]
title = "My blog"
weight = 1
[Languages.en.params]
linkedin = "english-link"

[Languages.fr]
copyright = "Tout est à moi"
title = "Mon blog"
weight = 2
[Languages.fr.params]
linkedin = "lien-francais"
[Languages.fr.navigation]
help  = "Aide"
```
{{% /code %}}

Tout ce qui n'est pas défini dans un bloc `[Languages]` tombera sur la valeur globale pour cette clé (par ex., `copyright` pour la langue anglaise [`en`]).

Avec la configuration au-dessus, toutes les pages de contenus, sitemap, flux RSS, paginations et taxonomie seront restituées sous `/` en Anglais (votre langue par défaut) et puis en dessous `/fr` en Français.

Lorsque vous travaillez avec les `Params` du front matter dans [les modèles de page unique][singles], omettez les `params` dans la clé pour la traduction.

Si vous souhaitez que toutes les langues soient placées sous leur code de langue respectif, activez `defaultContentLanguageInSubdir: true`.

Seules les options non globales évidentes peuvent être remplacées par langue. Des exemples d'options globales sont `baseURL`,` buildDrafts`, etc.

## Taxonomies et Blackfriday

Les taxonomies and la [configuration Blackfriday][config] peuvent être aussi réglées par langue :


{{% code file="bf-config.toml" %}}
```toml
[Taxonomies]
tag = "tags"

[blackfriday]
angledQuotes = true
hrefTargetBlank = true

[Languages]
[Languages.en]
weight = 1
title = "English"
[Languages.en.blackfriday]
angledQuotes = false

[Languages.fr]
weight = 2
title = "Français"
[Languages.fr.Taxonomies]
plaque = "plaques"
```
{{% /code %}}

## Traduisez Votre Contenu

Les articles traduits sont identifiés par le nom du fichier de contenu.

### Exemples d'Articles Traduits

1. `/content/about.en.md`
2. `/content/about.fr.md`

Dans cet exemple, le fichier `about.md` sera assigné au `defaultContentLanguage` configuré.

1. `/content/about.md`
2. `/content/about.fr.md`

De cette façon, vous pouvez commencer lentement à traduire votre contenu actuel sans devoir tout renommer. Si la valeur par défaut de `defaultContentLanguage` n'est pas spécifiée, elle est `en`.

En ayant le même *nom de fichier de base*, les éléments de contenu sont liés ensemble en tant que pièces traduites.

Si vous avez besoin d'URL distinctes par langue, vous pouvez définir le slug dans le fichier de langue qui n'est pas par défaut. Par exemple, vous pouvez définir un slug personnalisée pour une traduction française dans le front matter de `content/ about.fr.md` comme suit :


```yaml
slug: "a-propos"

```

Au rendu, Hugo construira à la fois `/about/` et `/a-propos/` comme pages traduites proprement reliées.

{{% note %}}
Hugo utilise actuellment le nom de fichier de base comme la clé de traduction, ce qui peut être un problème avec des noms de fichiers identiques dans différentes sections. 
Nous réparerons cela dans https://github.com/gohugoio/hugo/issues/2699
{{% /note %}}
{{< todo >}}Récrire/retirer le problème quand ce sera réparér.{{< /todo >}}

## Lier vers du Contenu Traduit

Pour créer une liste de liens de contenus traduits, utilisez un modèle similaire à ce qui suit : 

{{% code file="layouts/partials/i18nlist.html" %}}
```html
{{ if .IsTranslated }}
<h4>{{ i18n "translations" }}</h4>
<ul>
    {{ range .Translations }}
    <li>
        <a href="{{ .Permalink }}">{{ .Lang }}: {{ .Title }}{{ if .IsPage }} ({{ i18n "wordCount" . }}){{ end }}</a>
    </li>
    {{ end}}
</ul>
{{ end }}
```
{{% /code %}}

Ce qui est au-dessus peut être placé dans un `partial` (par ex., dans `layouts/partials/`) et inclus dans tout modèle, que ce soit pour une [page de contenu unique][contenttemplate] ou la  [page d'accueil][homepage]. Il n'imprimera pas quoi que ce soit s'il n'y a pas de traductions pour une page donnée, ou s'il existe des traductions---dans le cas de la page d'accueil, liste de section, etc.---un site ne fera que sortir une langue.

Ce qui est au-dessus utilise aussi la [fonction `i18n`][i18func] décrite dans la section suivante.

## Traduction de Chaînes

Hugo utilise [go-i18n][] pour prendre en charge les chaînes de traductions. [Voir le repo source du projet][go-i18n-source] pour trouver les outils qui vous aideront à gérer vos workflows de traductions.

Translations are collected from the `themes/<THEME>/i18n/` folder (built into the theme), as well as translations present in `i18n/` at the root of your project. In the `i18n`, the translations will be merged and take precedence over what is in the theme folder. Language files should be named according to [RFC 5646][] with names such as `en-US.toml`, `fr.toml`, etc.

From within your templates, use the `i18n` function like this:

```
{{ i18n "home" }}
```

This uses a definition like this one in `i18n/en-US.toml`:

```
[home]
other = "Home"
```

Often you will want to use to the page variables in the translations strings. To do that, pass on the "." context when calling `i18n`:

```
{{ i18n "wordCount" . }}
```

This uses a definition like this one in `i18n/en-US.toml`:

```
[wordCount]
other = "This article has {{ .WordCount }} words."
```
An example of singular and plural form:

```
[readingTime]
one = "One minute read"
other = "{{.Count}} minutes read"
```
And then in the template:

```
{{ i18n "readingTime" .ReadingTime }}
```
To track down missing translation strings, run Hugo with the `--i18n-warnings` flag:

```bash
 hugo --i18n-warnings | grep i18n
i18n|MISSING_TRANSLATION|en|wordCount
```

## Personnaliser les Dates

A l'heure de cet article, Golang ne supporte pas encore les dates internationalisées, mais si vous travaillez un peu, vous pouvez les simuler. Par exemple, si vous utilisez des noms de mois français, vosu pouvez ajouter un fichier data comme ``data/mois.yaml`` avec ce contenu :

~~~yaml
1: "janvier"
2: "février"
3: "mars"
4: "avril"
5: "mai"
6: "juin"
7: "juillet"
8: "août"
9: "septembre"
10: "octobre"
11: "novembre"
12: "décembre"
~~~

... puis indexez les noms de dates en non-anglais dans vos modèles comme suit : 

~~~html
<time class="post-date" datetime="{{ .Date.Format "2006-01-02T15:04:05Z07:00" | safeHTML }}">
  Article publié le {{ .Date.Day }} {{ index $.Site.Data.mois (printf "%d" .Date.Month) }} {{ .Date.Year }} (dernière modification le {{ .Lastmod.Day }} {{ index $.Site.Data.mois (printf "%d" .Lastmod.Month) }} {{ .Lastmod.Year }})
</time>
~~~

Cette technique extrait le jour, mois et année en spécifiant ``.Date.Day``, ``.Date.Month``, et  ``.Date.Year``, et utilise le numéro de mois comme une clé, au moment d'indexer le fichier data du nom du mois.

## Menus

Vous pouvez définir vos menus pour chaque langue de manière indépendante. La [création d'un menu][menus] fonctionne de manière analogue aux versions antérieures de Hugo, sauf qu'elles doivent être définies dans leur bloc spécifique à la langue dans le fichier de configuration :

```toml
defaultContentLanguage = "en"

[languages.en]
weight = 0
languageName = "English"

[[languages.en.menu.main]]
url    = "/"
name   = "Home"
weight = 0


[languages.de]
weight = 10
languageName = "Deutsch"

[[languages.de.menu.main]]
url    = "/"
name   = "Startseite"
weight = 0
```

The rendering of the main navigation works as usual. `.Site.Menus` will just contain the menu of the current language. Pay attention to the generation of the menu links. `absLangURL` takes care that you link to the correct locale of your website. Otherwise, both menu entries would link to the English version as the default content language that resides in the root directory.

```html
<ul>
    {{- $currentPage := . -}}
    {{ range .Site.Menus.main -}}
    <li class="{{ if $currentPage.IsMenuCurrent "main" . }}active{{ end }}">
        <a href="{{ .URL | absLangURL }}">{{ .Name }}</a>
    </li>
    {{- end }}
</ul>

```

## Traductions Manquantes

If a string does not have a translation for the current language, Hugo will use the value from the default language. If no default value is set, an empty string will be shown.

While translating a Hugo website, it can be handy to have a visual indicator of missing translations. The [`enableMissingTranslationPlaceholders` configuration option][config] will flag all untranslated strings with the placeholder `[i18n] identifier`, where `identifier` is the id of the missing translation.

{{% note %}}
Hugo générera votre site web avec ces gardiens de place de traduction manquants. Cela pourrait ne pas être adapté à des environnements de production.
{{% /note %}}

## Support de Thèmes Multilingue

To support Multilingual mode in your themes, some considerations must be taken for the URLs in the templates. If there is more than one language, URLs must meet the following criteria:

* Come from the built-in `.Permalink` or `.URL`
* Be constructed with
    * The [`relLangURL` template function][rellangurl] or the [`absLangURL` template function][abslangurl] **OR**
    * Prefixed with `{{ .LanguagePrefix }}`

If there is more than one language defined, the `LanguagePrefix` variable will equal `/en` (or whatever your `CurrentLanguage` is). If not enabled, it will be an empty string and is therefore harmless for single-language Hugo websites.

[abslangurl]: /fonctions/abslangurl
[config]: /demarrage/configuration/
[contenttemplate]: /templates/single-page-templates/
[go-i18n-source]: https://github.com/nicksnyder/go-i18n
[go-i18n]: https://github.com/nicksnyder/go-i18n
[homepage]: /templates/homepage/
[i18func]: /fonctions/i18n/
[menus]: /gestion-contenu/menus/
[rellangurl]: /fonctions/rellangurl
[RFC 5646]: https://tools.ietf.org/html/rfc5646
[singles]: /templates/single-page-templates/
