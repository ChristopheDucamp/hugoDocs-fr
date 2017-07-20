+++

title = "Configurer Hugo"
description = "Souvent les réglages par défaut sont suffisamment bons, mais le fichier de configuration peut fournir un haut niveau de contrôle sur la façon dont votre site est rendu."
weight = 5
+++

{{% notice note %}}
[Source "Configuring Hugo](https://gohugo.io/getting-started/configuration/) - documentation officielle Hugo, demeurant le seul lien de référence.
{{% /notice %}}

La [structure de répertoire](https://gohugo.io/getting-started/directory-structure) d'un site Web Hugo - ou plus précisément, l'organisation source des fichiers contenant le contenu du site web et ses modèles - fournit la plupart des informations de configuration dont Hugo a besoin pour générer un site web fini. 

Ce qui fait que par essence, de nombreux sites Web n'auraient pas besoin d'un tel fichier de configuration. Et ceci parce que Hugo est conçu pour reconnaître certains modèles d'utilisation typiques (et il les attend par défaut).

### Ordre de recherche de configuration


Similaire à l'ordre de recherche de modèle, Hugo a un ensemble de règles par défaut pour la recherche d'un fichier de configuration dans la racine du répertoire source de votre site web avec un comportement par défaut :

1. `./config.toml`
2. `./config.yaml`
3. `./config.json`

Dans votre fichier de configuration, vous pouvez indiquer à Hugo comment vous souhaitez que votre site Web soit rendu, contrôler les menus de votre site Web et définir arbitrairement les paramètres spécifiques à votre projet.

### Configuration YAML


Voici un exemple typique d'un fichier de configuration YAML. Notez que le document s'ouvre avec 3 traits d'union et se ferme avec 3 périodes. Les valeurs imbriquées dans les `params:` remplissent la variable `.Site.Params` à utiliser dans les [modèles](https://gohugo.io/templates/) :

```
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


## Toutes les variables, YAML

Ce qui suit est une liste de variables définies-par-Hugo dans un fichier exemple YAML. Les valeurs que fournies dans cet exemple représentent les valeurs par défaut utilisées par Hugo.

    
    ---
    archetypeDir:               "archetypes"
    # nom de l'hôte (et chemin) vers la racine, par ex. http://spf13.com/
    baseURL:                    ""
    # inclut le contenu marqué comme draft
    buildDrafts:                false
    # inclut le contenu avec une publishdate dans le futur
    buildFuture:                false
    # inclut le contenu déjà expiré
    buildExpired:               false
    # activer ça pour faire que toutes les URLs soient relatives a la racine du contenu. Notez que cela n'affecte aucunement les URLs absolues.
    relativeURLs:               false
    canonifyURLs:               false
    # config file (la valeur par défaut est path/config.yaml|json|toml)
    config:                     "config.toml"
    contentDir:                 "content"
    dataDir:                    "data"
    defaultExtension:           "html"
    defaultLayout:              "post"
    # Les traductions manquantes seront par défaut sur cette langue de contenu
    defaultContentLanguage:     "en"
    # Restitue la langue de contenu par défaut dans le sous-dossier, par ex. /en/. Le dossier racine / redirigera vers /en/
    defaultContentLanguageInSubdir: false
    # L'exemple en-dessous désactivera tous les types de page et ne restituera rien.
    disableKinds = ["page", "home", "section", "taxonomy", "taxonomyTerm", "RSS", "sitemap", "robotsTXT", "404"]
    disableLiveReload:          false
    # Ne construit pas de fichiers RSS
    disableRSS:                 false
    # Ne construit pas de fichier Sitemap
    disableSitemap:             false
    # Active la fonctionnalité GitInfo
    enableGitInfo:              false
    # Construit un fichier robots.txt
    enableRobotsTXT:            false
    # Ne restitue pas de page 404
    disable404:                 false
    # N'injecte pas le générateur de méta tag sur la homepage
    disableHugoGeneratorInject: false
    # Active le support des emoticons Emoji pour le contenu de page.
    # Voir www.emoji-cheat-sheet.com
    enableEmoji:                false
    # Place un placeholder au lieu de la valeur par défaut ou une chaîne vide si une traduction manque
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
    # Edite le nouveau contenu avec cet éditeur, si fourni
    newContentEditor:           ""
    # Ne synchronise pas le mode permission des fichirs
    noChmod:                    false
    # Ne synchronise pas l'heure de modification des fichiers
    noTimes:                    false
    paginate:                   10
    paginatePath:               "page"
    permalinks:
    # Met au pluriel les titres dans les listes utilisant inflect
    pluralizeListTitles:        true
    # Préserver les caractères spéciaux dans les noms de taxonomies ("Gérard Depardieu" vs "Gerard Depardieu")
    preserveTaxonomyNames:      false
    # chemin du système de fichier pour écrire les fichiers 
    publishDir:                 "public"
    # enables syntax guessing for code fences without specified language
    pygmentsCodeFencesGuessSyntax: false
    # codes-couleur pour illumination dérivée à partir de ce style
    pygmentsStyle:              "monokai"
    # true: utilise pygments-css ou false: color-codes directly
    pygmentsUseClasses:         false
    # nombre max d'items dans le flux RSS
    rssLimit:                   15
    # default sitemap configuration map
    sitemap:
    # chemin du fichier système pour lire les fichiers en rapport
    source:                     ""
    staticDir:                  "static"
    # affiche la mémoire et l'heure des différentes étapes du programme
    stepAnalysis:               false
    # thème à utiliser (situé par défaut dans /themes/NOMTHEME/)
    themesDir:                  "themes"
    theme:                      ""
    title:                      ""
    # si true, utilisez /filename.html au lieu de /filename/
    uglyURLs:                   false
    # Ne pas produire url/path en minuscule
    disablePathToLower:         false
    # si true, auto-detection Langues Chinese/Japanese/Korean dans le contenu. (.Summary and .WordCount can work properly in CJKLanguage)
    hasCJKLanguage:             false
    # verbose output
    verbose:                    false
    # verbose logging
    verboseLog:                 false
    # regarde le système de fichiers pour les modifications et recrée au besoin
    watch:                      true
    taxonomies:
      - category:               "categories"
      - tag:                    "tags"

    ---
    


## Toutes les Variables, TOML

Ce qui suit est la liste complète des variables définis par Hug dans un exemple de fichier TOML. Les valeurs fournies dans cet exemple représenteent les valeurs par défaut utilisées par Hugo.

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


> Si vous développez votre site sur une machine *nix, voici un raccourci pratique pour trouver l'option de configuration à partir de la ligne de commande :
    
    ~/sites/votresitehugo 
    hugo config | grep emoji
    enableemoji: true
    
## Variables environementales 

En plus des 3 options de configuration mentionnées au-dessus, les valeurs-clés de configuration peuvent être définies à travers les variables d'environnement de votre OS.

Par exemple, la commande qui suit réglera le titre d'un site web sur des systèmes Unix 
    
    $ env HUGO_TITLE="Some Title" hugo
    

Les noms doivent être précédés avec `HUGO_` et la clé de configuration doit être en capitale au moment de régler les variables d'environnement du système d'exploitation.

## Ignorer différents fichiers lors du rendu

La déclaration qui suit à l'intérieur de `./config.toml` amènera Hugo à ignorer les fichiers se terminant par `.foo` et `.boo` lors du rendu :

     ignoreFiles = [ "\\.foo$", "\\.boo$" ]
    

Ce qui est au-dessus est une liste d'expressions régulières. Notez que le caractère backslash (`\`) est échappé, pour faire plaisir à TOML.

## Configurer le rendu Blackfriday 

[Blackfriday](https://github.com/russross/blackfriday) est le moteur de rendu du [Markdown](http://daringfireball.net/projects/markdown/)de Hugo.

Dans l'ensemble, Hugo configure généralement Blackfriday avec un ensemble de paramètres plutôt raisonnables. Ces valeurs par défaut devraient correspondre assez bien à la plupart des cas d'utilisation.

Cependant, si vous avez des besoins inhabituels concernant  Markdown, Hugo expose certaines de ses options de comportement Blackfriday afin que vous puissiez les modifier. Le tableau suivant répertorie ces options Hugo, associées aux marqueurs correspondants du code source de Blackfriday (pour ce dernier, voir [html.go](https://github.com/russross/blackfriday/blob/master/html.go) et [Markdown.go](https://github.com/russross/blackfriday/blob/master/markdown.go)) :

| Marqueur |Par défaut | Marqueur BlackFriday |
|:--|:--|:--|
|**`taskLists`** |`true`| |
| *Objectif* :  `false` désactive la tâche automatique style-GitHub/génération TODO liste.|
| **`smartypants`** |`true`|`HTML_USE_SMARTYPANTS`|
|*Objectif* : `false` désactive les substitutions smaart de ponctuation, les smart quotes, smart dashes, smart fractions, etc. Si `true`, ce peut être raffiné avec des marqueurs `angledQuotes`, `fractions`, `smartDashes` et `latexDashes` (voir en-dessous).|
| **`angledQuotes`** | `false`|`HTML_SMARTYPANTS_ANGLED_QUOTES` |
| *Objectif* : `true` active les doubles guillemets intelligents et anglés. Exemple : `"Hugo"` affichera «Hugo» au lieu de “Hugo”.|
|**`fractions`** |`true` |`HTML_SMARTYPANTS_FRACTIONS`|
|*Objectif* : `false` désactive les fractions intelligentes. **Exemple :** `5/12` donnera 5⁄12 (`<sup>5</sup>&frasl;<sub>12</sub>`). <br>**Attention :** Même avec `fractions = false`, Blackfriday convertira encore 1/2, 1/4 et 3/4 respectivement en   ½ (`&frac12;`), ¼ (`&frac14;`) and ¾ (`&frac34;`), mais seulement ces trois-la.. |
| **`smartDashes`** | `true` | `HTML_SMARTYPANTS_DASHES` |
| *Objectif* : `false` désactive les tirets smart ; c'est à dire que la conversion de plusieurs hyphens en en-dash ou em-dash. Si `true`, son comportement peut être modifié avec le marqueur  `latexDashes` en-dessous. |
|**`latexDashes`** | `true` |  `HTML_SMARTYPANTS_LATEX_DASHES` |
| *Objectif* : `false` désactive les tirets intelligents style-LaTeX-style et sélectionne des tirets intelligents conventionnels. <br>En supposant `smartDashes` (au-dessus), si c'est : <br> `true`, puis `--` est traduit en “–” (`&ndash;`), tandis que   `---` est traduit en “—” (`&mdash;`).<br>`false`, puis `--` est traduit en “—” (`&mdash;`), tandis qu'un hyphen à _espace_unique entre deux mots est traduit en un en en dash—e.g., `12 June - 3 July` devient `12 June &ndash; 3 July`. |
| **`hrefTargetBlank`** | `false` | `HTML_HREF_TARGET_BLANK`  |
| *Objectif* : `true` ouvre des liens externes dans une nouvelle fenêtre ou un nouvel onglet. |
| **`plainIDAnchors`**| `true` | `FootnoteAnchorPrefix` et `HeaderIDSuffix` |
| *Objectif* : `true` restitue n'importe quels IDs de header et footnote sans l'ID du document. 
**Exemple :** restitue `#my-header` au lieu de `#my-header:bec3ed8ba720b9073ab75abcf3ba5d97`.|
|`**extensions**`|`[]`|`EXTENSION_*`|
| *Objectif* : active une ou plusieurs extensions Markdown de BlackFriday (si elles ne sont pas par défaut celles d'Hugo).  
**Exemple :**   inclut `"hardLineBreak"` dans la liste pour activer `EXTENSION_HARD_LINE_BREAK` de BlackFriday.|
| **`extensionsmask`** |`[]`|`EXTENSION_*`|
| *Objectif* : désactive une ou plusieurs extensions Markdown de BlackFriday (si ce ne sont pas celles d'Hugo par défaut).
**Exemple :**   Inclut `"autoHeaderIds"` dans la liste pour désactiver `EXTENSION_AUTO_HEADER_IDS` de BlackFriday.|

**Notes**

  * Ces marqueurs sont **sensibles à la casse** (à partir de Hugo v0.15) !
  * Ces marqueurs doivent être groupés sous la clé `blackfriday` et peuvent être réglés  **à la fois au niveau du site et au niveau de la page**. Tout réglage sur une page écrasera ici le réglage pour le site. 
  * Par exemple : 


**- pour TOML :**
       
        [blackfriday]
        angledQuotes = true
        fractions = false
        plainIDAnchors = true
        extensions = ["hardLineBreak"]   
**- pour YAML**

        blackfriday:
        angledQuotes: true
        fractions: false
        plainIDAnchors: true
        extensions:
           - hardLineBreak |


## Configurer des Formats Output supplémentaires

Hugo v0.20 a introduit la capacité de restituer votre contenu vers plusieurs formats output (par ex., vers JSON, AMP html, ou CSV). Voir  [Output Formats](https://gohugo.io/templates/output-formats/) pour savoir comment ajouter ces valeurs à votre fichier de configuration de projet Hugo.

## Specs Configuration Format
  * [TOML Spec](https://github.com/toml-lang/toml)
  * [YAML Spec](http://yaml.org/spec/)
  * [JSON Spec](https://gohugo.io/documents/ecma-404-json-spec.pdf)
