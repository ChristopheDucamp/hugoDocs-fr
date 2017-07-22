---
title: Configurer Hugo
description: Souvent les réglages par défaut sont suffisamment bons, mais le fichier de configuration peut fournir un haut niveau de contrôle sur la façon dont votre site est rendu.
date: 2013-07-01
publishdate: 2017-01-02
lastmod: 2017-07-22
categories: [démarrage, fondamentaux]
#tags: [configuration,toml,yaml,json]
menu:
  docs:
    parent: "Démarrage"
    weight: 60
weight: 60
sections_weight: 60
draft: false
aliases: [/demarrage/configurer-hugo]
toc: true
---
La [structure des dossiers][] d'un site Web Hugo - ou plus précisément, l'organisation source des fichiers contenant le contenu du site web et ses modèles - fournit la plupart des informations de configuration dont Hugo a besoin pour générer un site web fini.

Hugo ayant pré-réglé les valeurs sensibles par défaut, de nombreux sites web n'auront pas besoin d'un tel fichier de configuration. Hugo a été conçu pour reconnaître certains modèles d'utilisation typiques.

### Ordre de Recherche de Configuration

Similaire à l'[ordre de recherche][] de modèle, Hugo a un ensemble de règles par défaut pour chercher un fichier de configuration à la racine du répertoire source de votre site web avec un comportement par défaut :

1. `./config.toml`
2. `./config.yaml`
3. `./config.json`

Dans votre fichier `config`, vous pouvez indiquer à Hugo comment vous souhaitez que votre site web soit rendu, contrôler les menus de votre site et définir arbitrairement des paramètres pour tout le site et spécifiques à votre projet.

### Configuration YAML

Voici un exemple typique d'un fichier de configuration YAML. Notez que le document s'ouvre avec 3 traits d'union et se ferme avec 3 périodes. Les valeurs imbriquées dans les `params:` rempliront la variable [`.Site.Params`] à utiliser dans les [modèles](/templates/) :

{{% code file="config.yml"%}}
```yaml
---
baseURL: "https://votresite.exemple.com/"
title: "Mon Site Hugo"
footnoteReturnLinkContents: "↩"
permalinks:
  post: /:year/:month/:title/
params:
  Subtitle: "Hugo is Absurdly Fast!"
  AuthorName: "Jon Doe"
  GitHubUser: "spf13"
  ListOfFoo:
    - "foo1"
    - "foo2"
  SidebarRecentLimit: 5
...
```
{{% /code %}}

## Toutes les variables, YAML

Ce qui suit est une liste de variables définies-par-Hugo dans un fichier exemple YAML. Les valeurs fournies dans cet exemple représentent les valeurs par défaut utilisées par Hugo.

```yaml
---
archetypeDir:               "archetypes"
# hostname (and path) to the root, e.g. http://spf13.com/
baseURL:                    ""
# include content marked as draft
buildDrafts:                false
# include content with publishdate in the future
buildFuture:                false
# include content already expired
buildExpired:               false
# enable this to make all relative URLs relative to content root. Note that this does not affect absolute URLs. See the "URL Management" page
relativeURLs:               false
canonifyURLs:               false
# config file (default is path/config.yaml|json|toml)
config:                     "config.toml"
contentDir:                 "content"
dataDir:                    "data"
defaultExtension:           "html"
defaultLayout:              "post"
# Missing translations will default to this content language
defaultContentLanguage:     "en"
# Renders the default content language in subdir, e.g. /en/. The root directory / will redirect to /en/
defaultContentLanguageInSubdir: false
disableLiveReload:          false
# Do not build RSS files
disableRSS:                 false
# Do not build Sitemap file
disableSitemap:             false
# Enable GitInfo feature
enableGitInfo:              false
# Build robots.txt file
enableRobotsTXT:            false
# Do not render 404 page
disable404:                 false
# Do not inject generator meta tag on homepage
disableHugoGeneratorInject: false
# Allows you to disable all page types and will render nothing related to 'kind';
# values = "page", "home", "section", "taxonomy", "taxonomyTerm", "RSS", "sitemap", "robotsTXT", "404"
disableKinds: []
# Do not make the url/path to lowercase
disablePathToLower:         false                   ""
# Enable Emoji emoticons support for page content; see emoji-cheat-sheet.com
enableEmoji:                false
# Show a placeholder instead of the default value or an empty string if a translation is missing
enableMissingTranslationPlaceholders: false
footnoteAnchorPrefix:       ""
footnoteReturnLinkContents: ""
# google analytics tracking id
googleAnalytics:            ""
# if true, auto-detect Chinese/Japanese/Korean Languages in the content. (.Summary and .WordCount can work properly in CJKLanguage)
hasCJKLanguage:             false
languageCode:               ""
layoutDir:                  "layouts"
# Enable Logging
log:                        false
# Log File path (if set, logging enabled automatically)
logFile:                    ""
# "toml","yaml", or "json"
metaDataFormat:             "toml"
newContentEditor:           ""
# Don't sync permission mode of files
noChmod:                    false
# Don't sync modification time of files
noTimes:                    false
# Pagination
paginate:                   10
paginatePath:               "page"
# See "content-management/permalinks"
permalinks:
# Pluralize titles in lists using inflect
pluralizeListTitles:        true
# Preserve special characters in taxonomy names ("Gérard Depardieu" vs "Gerard Depardieu")
preserveTaxonomyNames:      false
# filesystem path to write files to
publishDir:                 "public"
# enables syntax guessing for code fences without specified language
pygmentsCodeFencesGuessSyntax: false
# color-codes for highlighting derived from this style
pygmentsStyle:              "monokai"
# true use pygments-css or false will color code directly
pygmentsUseClasses:         false
# maximum number of items in the RSS feed
rssLimit:                   15
# see "Section Menu for Lazy Bloggers", /templates/menu-templates for more info
SectionPagesMenu:           ""
# default sitemap configuration map
sitemap:
# filesystem path to read files relative from
source:                     ""
staticDir:                  "static"
# display memory and timing of different steps of the program
stepAnalysis:               false
# theme to use (located by default in /themes/THEMENAME/)
themesDir:                  "themes"
theme:                      ""
title:                      ""
# if true, use /filename.html instead of /filename/
uglyURLs:                   false
# verbose output
verbose:                    false
# verbose logging
verboseLog:                 false
# watch filesystem for changes and recreate as needed
watch:                      true
taxonomies:
  - category:               "categories"
  - tag:                    "tags"
---
```


## Configuration TOML

Voici un exemple de fichier de configuration TOML. Les valeurs sous `[params]` rempliront la variables `.Site.Params` pour utilisation dans les [templates][]

```
contentDir = "content"
layoutDir = "layouts"
publishDir = "public"
buildDrafts = false
baseURL = "https://yoursite.example.com/"
canonifyURLs = true
title = "My Hugo Site"

[taxonomies]
  category = "categories"
  tag = "tags"

[params]
  subtitle = "Hugo is Absurdly Fast!"
  author = "John Doe"
```

### Toutes les Variables, TOML

Voici la liste complète des variables définies par Hugo dans un exemple de fichier TOML. Les valeurs fournies dans cet exemple représentent les valeurs par défaut utilisées par Hugo.

{{% code file="config.toml" download="config.toml"%}}
```
+++
archetypeDir =                "archetypes"
# hostname (and path) to the root, e.g. http://spf13.com/
baseURL =                     ""
# include content marked as draft
buildDrafts =                 false
# include content with publishdate in the future
buildFuture =                 false
# include content already expired
buildExpired =                false
# enable this to make all relative URLs relative to content root. Note that this does not affect absolute URLs.
relativeURLs =                false
canonifyURLs =                false
# config file (default is path/config.yaml|json|toml)
config =                     "config.toml"
contentDir =                  "content"
dataDir =                     "data"
defaultExtension =            "html"
defaultLayout =               "post"
# Missing translations will default to this content language
defaultContentLanguage =      "en"
# Renders the default content language in subdir, e.g. /en/. The root directory / will redirect to /en/
defaultContentLanguageInSubdir =  false
disableLiveReload =           false
# Do not build RSS files
disableRSS =                  false
# Do not build Sitemap file
disableSitemap =              false
# Enable GitInfo feature
enableGitInfo =               false
# Build robots.txt file
enableRobotsTXT =             false
# Do not render 404 page
disable404 =                  false
# Do not inject generator meta tag on homepage
disableHugoGeneratorInject =  false
# Allows you to disable all page types and will render nothing related to 'kind';
# values = "page", "home", "section", "taxonomy", "taxonomyTerm", "RSS", "sitemap", "robotsTXT", "404"
disableKinds = []
# Do not make the url/path to lowercase
disablePathToLower =          false
# Enable Emoji emoticons support for page content; see emoji-cheat-sheet.com
enableEmoji =                 false
# Show a placeholder instead of the default value or an empty string if a translation is missing
enableMissingTranslationPlaceholders = false
footnoteAnchorPrefix =        ""
footnoteReturnLinkContents =  ""
# google analytics tracking id
googleAnalytics =             ""
# if true, auto-detect Chinese/Japanese/Korean Languages in the content. (.Summary and .WordCount can work properly in CJKLanguage)
hasCJKLanguage =              false
languageCode =                ""
layoutDir =                   "layouts"
# Enable Logging
log =                         false
# Log File path (if set, logging enabled automatically)
logFile =
# maximum number of items in the RSS feed
rssLimit =                    15
# "toml","yaml", or "json"
metaDataFormat =              "toml"
newContentEditor =            ""
# Don't sync permission mode of files
noChmod =                     false
# Don't sync modification time of files
noTimes =                     false
# Pagination
paginate =                    10
paginatePath =                "page"
# See "content-management/permalinks"
permalinks =
# Pluralize titles in lists using inflect
pluralizeListTitles =         true
# Preserve special characters in taxonomy names ("Gérard Depardieu" vs "Gerard Depardieu")
preserveTaxonomyNames =       false
# filesystem path to write files to
publishDir =                  "public"
# enables syntax guessing for code fences without specified language
pygmentsCodeFencesGuessSyntax = false
# color-codes for highlighting derived from this style
pygmentsStyle =               "monokai"
# true: use pygments-css or false: color-codes directly
pygmentsUseClasses =          false
# see "Section Menu for Lazy Bloggers", /templates/menu-templates for more info
SectionPagesMenu =
# default sitemap configuration map
sitemap =
# filesystem path to read files relative from
source =                      ""
staticDir =                   "static"
# display memory and timing of different steps of the program
stepAnalysis =                false
# theme to use (located by default in /themes/THEMENAME/)
themesDir =                   "themes"
theme =                       ""
title =                       ""
# if true, use /filename.html instead of /filename/
uglyURLs =                    false
# verbose output
verbose =                     false
# verbose logging
verboseLog =                  false
# watch filesystem for changes and recreate as needed
watch =                       true
[taxonomies]
  category = "categories"
  tag = "tags"
+++
```
{{% /code %}}

{{% note %}}
Si vous développez votre site sur une machine \*nix, voici un raccourci pratique pour trouver l'option de configuration à partir de la ligne de commande :
```   
~/sites/votresitehugo
hugo config | grep emoji
enableemoji: true
```
{{% /note %}}

## Variables d'environnement

En plus des 3 options de configuration mentionnées au-dessus, les valeurs-clés de configuration peuvent être définies à travers les variables d'environnement de votre OS.

Par exemple, la commande qui suit réglera le titre d'un site web sur des systèmes Unix

```bash
$ env HUGO_TITRE="Un Titre" hugo
```    

{{% note "Régler les Variables d'Environment" %}}
Les noms doivent être précédés par `HUGO_` et la clé de configuration doit être en capitales au moment de régler les variables d'environnement du système d'exploitation.
{{% /note %}}

## Ignorer des Fichiers lors du Rendu

La déclaration qui suit à l'intérieur de `./config.toml` amènera Hugo à ignorer les fichiers se terminant par `.foo` et `.boo` lors du rendu :
```toml
ignoreFiles = [ "\\.foo$", "\\.boo$" ]
```    

Ce qui est au-dessus, c'est une liste d'expressions régulières. Notez que le caractère backslash (`\`) est échappé, pour faire plaisir à TOML.

## Configurer Blackfriday

[Blackfriday](https://github.com/russross/blackfriday) est le moteur de rendu du Markdown intégré dans Hugo.

Hugo configure généralement Blackfriday avec un ensemble de paramètres plutôt raisonnables. Ces valeurs par défaut devraient correspondre à la plupart des cas d'utilisation.

Cependant, si vous avez des besoins spécifiques concernant Markdown, Hugo enrichit certaines de ses options de comportement Blackfriday afin que vous puissiez les modifier. Le tableau suivant liste ces options Hugo, associées aux marqueurs correspondants du code source de Blackfriday (voir [html.go](https://github.com/russross/blackfriday/blob/master/html.go) et [Markdown.go](https://github.com/russross/blackfriday/blob/master/markdown.go)).

{{< readfile file="/content/readfiles/bfconfig.md" markdown="true" >}}



{{% note %}}
1. Les flags Blackfriday sont *sensibles à la casse* à partir de Hugo v0.15) !
2. Ces marqueurs doivent être groupés sous la clé `blackfriday` et peuvent être réglés  à la fois au niveau du site et au niveau de la page. Tout réglage sur une page écrasera son réglage respectif pour le site.
{{% /note %}}


{{% code file="bf-config.toml" %}}
```toml
[blackfriday]
  angledQuotes = true
  fractions = false
  plainIDAnchors = true
  extensions = ["hardLineBreak"]
```
{{% /code %}}

{{% code file="bf-config.yml" %}}
```yaml
blackfriday:
  angledQuotes: true
  fractions: false
  plainIDAnchors: true
  extensions:
    - hardLineBreak
```
{{% /code %}}


## Configurer des Formats Output supplémentaires

Hugo v0.20 a introduit la capacité de restituer votre contenu vers plusieurs formats output (par ex., vers JSON, AMP html, ou CSV). Voir  [Formats Output][] pour savoir comment ajouter ces valeurs à votre fichier de configuration de projet Hugo.

## Specs des Formats de Configuration
  * [TOML Spec](toml)
  * [YAML Spec](yaml)
  * [JSON Spec](json)


[`.Site.Params`]: /variables/site/
[structure des dossiers]: /demarrage/structure-dossier/
[json]: https://gohugo.io/documents/ecma-404-json-spec.pdf
[ordre de recherche]: /templates/ordre-recherche/
[Formats Output]: /templates/formats-output/
[templates]: /templates/
[toml]: https://github.com/toml-lang/toml
[yaml]: http://yaml.org/spec/
