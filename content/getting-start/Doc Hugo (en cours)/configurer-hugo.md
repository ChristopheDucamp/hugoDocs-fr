+++

title = "Configurer Hugo"
description = "."
weight = 5
+++

{{% notice note %}}
[Source "Configuring Hugo](http://gohugo.io/overview/configuration/ "Permalink vers Hugo - Configuring Hugo") - documentation officielle Hugo, demeurant le seul lien de référence.
{{% /notice %}}

La structure de répertoire d'un site Web Hugo - ou plus précisément, des fichiers source contenant son contenu et ses modèles - fournit la plupart des informations de configuration dont Hugo a besoin. Ce qui fait que par essence, de nombreux sites Web n'auraient pas besoin d'un fichier de configuration. C'est parce que Hugo est conçu pour reconnaître certains modèles d'utilisation typiques (et il les attend par défaut).

Néanmoins, Hugo recherche un fichier de configuration portant un nom particulier dans la racine du répertoire source de votre site web. Tout d'abord, il recherche un fichier `./config.toml`. S'il  n'est pas présent, il recherchera un fichier `./config.yaml`, suivi d'un fichier `./config.json`.

Dans ce fichier de `config` pour votre site Web, vous pouvez placer des indications précises pour Hugo concernant la façon dont il devrait produire votre site, tout comme la définition des et divers autres paramètres du site.

Une autre façon de réaliser la configuration du site Web réside dans les variables de l'environnement du système d'exploitation. Par exemple, la commande suivante fonctionnera sur des systèmes similaires à Unix : elle définit le titre d'un site Web

    
    $ env HUGO_TITLE="Some Title" hugo
    

(**Note :** de tels noms de variables d'environnement doivent être préfixés par `HUGO_`.)

## Exemples

Ce qui suit est un exemple typique de fichier de configuration YAML. Trois points finissent le document :
    
    ---
    baseURL: "http://votresite.exemple.com/"
    ...
    

Ce qui suite est un exemple du fichier de config TOML avec quelques valeurs par défaut. Les valeurs `[params]` rempliront la variable `.Site.Params` pour utilisation dans les modèles :
    
    contentDir = "content"
    layoutDir = "layouts"
    publishDir = "public"
    buildDrafts = false
    baseURL = "http://votresite.exemple.com/"
    canonifyURLs = true
    
    [taxonomies]
      category = "categories"
      tag = "tags"
    
    [params]
      description = "Merveilleux Site Hugo de Tesla"
      author = "Nikola Tesla"
    

Voici un fichier de configuration YAML qui règles un peu plus d'options : 
    
    ---
    baseURL: "http://votresite.exemple.com/"
    title: "Yoyodyne Widget Blogging"
    footnoteReturnLinkContents: "↩"
    permalinks:
      post: /:year/:month/:title/
    params:
      Subtitle: "Spinning the cogs in the widgets"
      AuthorName: "John Doe"
      GitHubUser: "spf13"
      ListOfFoo:
        - "foo1"
        - "foo2"
      SidebarRecentLimit: 5
    ...
    

## Variables de configuration

Ce qui suit est une liste de variables définies-par-Hugo que vous pouvez configurer, avec leurs valeurs actuelles par défaut : 

    
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
    # enable this to make all relative URLs relative to content root. Note that this does not affect absolute URLs.
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
    # The below example will disable all page types and will render nothing.
    disableKinds = ["page", "home", "section", "taxonomy", "taxonomyTerm", "RSS", "sitemap", "robotsTXT", "404"]
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
    # Enable Emoji emoticons support for page content.
    # See www.emoji-cheat-sheet.com
    enableEmoji:                false
    # Show a placeholder instead of the default value or an empty string if a translation is missing
    enableMissingTranslationPlaceholders: false
    footnoteAnchorPrefix:       ""
    footnoteReturnLinkContents: ""
    # google analytics tracking id
    googleAnalytics:            ""
    languageCode:               ""
    layoutDir:                  "layouts"
    # Enable Logging
    log:                        false
    # Log File path (if set, logging enabled automatically)
    logFile:                    ""
    # "yaml", "toml", "json"
    metaDataFormat:             "toml"
    # Edit new content with this editor, if provided
    newContentEditor:           ""
    # Don't sync permission mode of files
    noChmod:                    false
    # Don't sync modification time of files
    noTimes:                    false
    paginate:                   10
    paginatePath:               "page"
    permalinks:
    # Pluralize titles in lists using inflect
    pluralizeListTitles:        true
    # Preserve special characters in taxonomy names ("Gérard Depardieu" vs "Gerard Depardieu")
    preserveTaxonomyNames:      false
    # filesystem path to write files to
    publishDir:                 "public"
    # enables syntax guessing for code fences without specified language
    pygmentsCodeFencesGuessSyntax: false
    # color-codes for highlighting derived from this style
    pygmentsStyle:              "monokai"
    # true: use pygments-css or false: color-codes directly
    pygmentsUseClasses:         false
    # maximum number of items in the RSS feed
    rssLimit:                   15
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
    # Do not make the url/path to lowercase
    disablePathToLower:         false
    # if true, auto-detect Chinese/Japanese/Korean Languages in the content. (.Summary and .WordCount can work properly in CJKLanguage)
    hasCJKLanguage:             false
    # verbose output
    verbose:                    false
    # verbose logging
    verboseLog:                 false
    # watch filesystem for changes and recreate as needed
    watch:                      true
    ---
    

## Ignorer différents fichiers lors du rendu

La déclaration qui suit dans `./config.toml` amènera Hugo à ignorer les fichiers se terminant par `.foo` et `.boo` lors du rendu :

     ignoreFiles = [ "\\.foo$", "\\.boo$" ]
    

Au-dessus une liste d'expressions régulières. Notez que le caractère backslash (`\`) est échappé, pour rendre heureux TOML.

## Configurer le rendu Blackfriday 

[Blackfriday](https://github.com/russross/blackfriday) est le moteur de rendu du [Markdown](http://daringfireball.net/projects/markdown/)de Hugo.

Dans l'ensemble, Hugo configure généralement Blackfriday avec un ensemble de paramètres plutôt raisonnables. Ces valeurs par défaut devraient correspondre assez bien à la plupart des cas d'utilisation.

Cependant, si vous avez des besoins inhabituels à l'égard de Markdown, Hugo expose certaines de ses options de comportement Blackfriday pour que vous puissiez les modifier. Le tableau suivant répertorie ces options Hugo, associées aux marqueurs correspondants du code source de Blackfriday (pour ce dernier, voir [html.go](https://github.com/russross/blackfriday/blob/master/html.go) et [Markdown.go](https://github.com/russross/blackfriday/blob/master/markdown.go)):


cf http://gohugo.io/overview/configuration/ pour le tableau qui liste les options Hugo pour BlackFriday.
