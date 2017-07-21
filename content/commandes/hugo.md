---
date: 2017-07-16T23:23:14+02:00
title: "hugo"
slug: hugo
url: /commands/hugo/
lastmod : 2017-07-21

---
## hugo

hugo construit votre site

### Synopsis


hugo est la commande principale, utilisée pour construire votre site Hugo.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at http://gohugo.io/.

```
hugo [flags]
```

### Options

```
  -b, --baseURL string             hostname (and path) to the root, e.g. http://spf13.com/
  -D, --buildDrafts                include content marked as draft
  -E, --buildExpired               include expired content
  -F, --buildFuture                include content with publishdate in the future
      --cacheDir string            filesystem path to cache directory. Defaults: $TMPDIR/hugo_cache/
      --canonifyURLs               if true, all relative URLs will be canonicalized using baseURL
      --cleanDestinationDir        remove files from destination not found in static directories
      --config string              config file (default is path/config.yaml|json|toml)
  -c, --contentDir string          filesystem path to content directory
  -d, --destination string         filesystem path to write files to
      --disable404                 do not render 404 page
      --disableKinds stringSlice   disable different kind of pages (home, RSS etc.)
      --disableRSS                 do not build RSS files
      --disableSitemap             do not build Sitemap file
      --enableGitInfo              add Git revision, date and author info to the pages
      --forceSyncStatic            copy all files when static is changed.
  -h, --help                       help for hugo
      --i18n-warnings              print missing translations
      --ignoreCache                ignores the cache directory
  -l, --layoutDir string           filesystem path to layout directory
      --log                        enable Logging
      --logFile string             log File path (if set, logging enabled automatically)
      --noChmod                    don't sync permission mode of files
      --noTimes                    don't sync modification time of files
      --pluralizeListTitles        pluralize titles in lists using inflect (default true)
      --preserveTaxonomyNames      preserve taxonomy names as written ("Gérard Depardieu" vs "gerard-depardieu")
      --quiet                      build in quiet mode
      --renderToMemory             render to memory (only useful for benchmark testing)
  -s, --source string              filesystem path to read files relative from
      --stepAnalysis               display memory and timing of different steps of the program
  -t, --theme string               theme to use (located in /themes/THEMENAME/)
      --themesDir string           filesystem path to themes directory
      --uglyURLs                   if true, use /filename.html instead of /filename/
  -v, --verbose                    verbose output
      --verboseLog                 verbose logging
  -w, --watch                      watch filesystem for changes and recreate as needed
```

### Voir aussi
* [hugo benchmark](/commands/hugo_benchmark/)	 - Benchmark Hugo en construisant un site un certain nombre de fois.
* [hugo check](/commands/hugo_check/)	 - Contient quelques points de vérification
* [hugo config](/commands/hugo_config/)	 - Imrpime la configuration du site
* [hugo convert](/commands/hugo_convert/)	 - Convertit votre contenu en différents formats
* [hugo env](/commands/hugo_env/)	 - Imprime la version Hugo et l'info d'environnemnt
* [hugo gen](/commands/hugo_gen/)	 - Une collection de plusieurs générateurs utiles.
* [hugo import](/commands/hugo_import/)	 - Importe votre site à partir d'autres.
* [hugo list](/commands/hugo_list/)	 - Liste différents types de contenus
* [hugo new](/commands/hugo_new/)	 - Crée un nouveau contenu pour votre site
* [hugo server](/commands/hugo_server/)	 - Un serveur web de haute performance
* [hugo undraft](/commands/hugo_undraft/)	 - Undraft réinitialise le statut draft du contenu
* [hugo version](/commands/hugo_version/)	 - Affiche le numéro de version d'Hugo

###### Auto généré par spf13/cobra le 16-Jul-2017
