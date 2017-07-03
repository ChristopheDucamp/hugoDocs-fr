+++

title = "Configurer Hugo"
description = "Les variables de configuration Hugo."
weight = 5
+++

{{% notice note %}}
[Source "Configuring Hugo](http://gohugo.io/overview/configuration/ "Permalien vers Hugo - Configuring Hugo") - documentation officielle Hugo, demeurant le seul lien de référence.
{{% /notice %}}

La structure de répertoire d'un site Web Hugo - ou plus précisément, des fichiers source contenant son contenu et ses modèles - fournit la plupart des informations de configuration dont Hugo a besoin. Ce qui fait que par essence, de nombreux sites Web n'auraient pas besoin d'un tel fichier de configuration. Et ceci parce que Hugo est conçu pour reconnaître certains modèles d'utilisation typiques (et il les attend par défaut).

Néanmoins, Hugo recherche un fichier de configuration portant un nom particulier à la racine du répertoire source de votre site web. Tout d'abord, il recherche un fichier `./config.toml`. S'il  n'est pas présent, il recherchera un fichier `./config.yaml`, suivi d'un fichier `./config.json`.

Dans ce fichier de `config` pour votre site Web, vous pouvez placer des indications précises pour Hugo concernant la manière avec laquelle Hugo produira votre site, tout comme la définition des menus et d'autres paramètres divers du site.

Une autre façon de réaliser la configuration du site Web peut se faire dans les variables de l'environnement du système d'exploitation. Par exemple, la commande suivante fonctionnera sur des systèmes similaires à Unix : elle définit le titre d'un site Web

    $ env HUGO_TITLE="Un Titre" hugo
    
(**Note :** de tels noms de variables d'environnement doivent être préfixés par `HUGO_`.)

## Exemples

Ce qui suit est un exemple typique de fichier de configuration YAML. Trois points finissent le document :
    
    ---
    baseURL: "http://votresite.exemple.com/"
    ...
    

Ce qui suit est un exemple du fichier de config TOML avec quelques valeurs par défaut. Les valeurs `[params]` rempliront la variable `.Site.Params` pour utilisation dans les modèles :
    
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
    

Voici un fichier de configuration YAML qui règle un peu plus d'options : 
    
    ---
    baseURL: "http://votresite.exemple.com/"
    title: "Widget Blog Yoyodyne"
    footnoteReturnLinkContents: "↩"
    permalinks:
      post: /:year/:month/:title/
    params:
      Subtitle: "Spinning the cogs in the widgets"
      AuthorName: "Jean Dupont"
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
    ---
    

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
