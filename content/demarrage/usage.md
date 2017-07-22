---
title: Usage Basique
linktitle: Usage Basique
description: La CLI d'Hugo est pleine de fonctionnalités mais simple à utiliser, même pour ceux qui n'ont qu'une expérience très limitée de travail à partir de la ligne de commande.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [demarrage]
#tags: [/demarrage/utiliser-hugo,usage,livereload,command line,flags, ligne de commande]
weight: 40
sections_weight: 40
draft: false
aliases: [/overview/usage/,/extras/livereload/,/doc/usage/,/usage/]
toc: true
---
Voici une description des commandes les plus communes que vous utiliserez pendant le développement de votre projet Hugo. Regardez la [Référence ligne de commande][commandes] pour une vision globale de la CLI d'Hugo.

## Test Installation

Une fois que vous aurez [installé Hugo][install], assurez-vous d'être dans votre chemin `PATH`. Vous pouvez tester que Hugo a été bien installé correctement via la commande `help` :

Assurez-vous que Hugo est bien dans votre `PATH` (ou indiquez un chemin). Testez en lançant :

```bash
hugo help
```

L'output que vous voyez dans votre console devrait ressembler à ce qui suit : 

```bash
hugo is the main command, used to build your Hugo site.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at http://gohugo.io/.

Usage:
  hugo [flags]
  hugo [command]

Available Commands:
  benchmark   Benchmark Hugo by building a site a number of times.
  check       Contains some verification checks
  config      Print the site configuration
  convert     Convert your content to different formats
  env         Print Hugo version and environment info
  gen         A collection of several useful generators.
  help        Help about any command
  import      Import your site from others.
  list        Listing out various types of content
  new         Create new content for your site
  server      A high performance webserver
  undraft     Undraft changes the content's draft status from 'True' to 'False'
  version     Print the version number of Hugo

Flags:
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

## La Commande `hugo    

L'utilisation la plus commune est probablement de lancer `hugo` avec votre répertoire en cours étant le répertoire d'input.

Ceci génère par défaut votre site web vers le dossier `public/`, bien que vous puissiez personnaliser le dossier output dans votre fichier de [configuraiton de site][config] en modifiant le champ  `publishDir`.

Le site Hugo est produit à l'intérieur de `public/` et il est prêt à être déployé sur votre serveur web : 

```bash
hugo
0 draft content
0 future content
99 pages created
0 paginator pages created
16 tags created
0 groups created
in 90 ms
```

## Contenus Brouillons, Futurs et Expirés

Hugo vous permet de régler `draft`, `publishdate` et même `expirydate` dans le [front matter][] de vos contenus. 
Par défaut, Hugo ne publiera pas :

1. Contenu avec une valeur `publishdate` dans le futur
2. Contenu avec `draft: true` status
3. Contenu avec une valeur `expirydate` passée

Ces trois cas peuvent être annulés durant le développement local  *et* le déploiement en ajoutant les options suivantes respectiement à `hugo` et `hugo server`, ou en changeant les valeurs booléennes assignées aux champs du même nom (sans `--`) dans votre [configuration][config] :

1. `--buildFuture`
2. `--buildDrafts`
3. `--buildExpired`

## LiveReload

Hugo est livré avec un [LiveReload](https://github.com/livereload/livereload-js) intégré. Aucun package supplémentaire à installer. Un moyen commun d'utilsier Hugo tout en développant est de lancer un serveur avec la commmande `hugo server` et de regarder les modifications : 

```bash
hugo server
0 draft content
0 future content
99 pages created
0 paginator pages created
16 tags created
0 groups created
in 120 ms
Watching for changes in /Users/yourname/sites/yourhugosite/{data,content,layouts,static}
Serving pages from /Users/yourname/sites/yourhugosite/public
Web Server is available at http://localhost:1313/
Press Ctrl+C to stop
```

Ceci fera fonctionner un serveur web totalement fonctionnel tout en regardant simultanément votre système de fichier pour l'ajout, l'effacement ou les modificatons dans les aires suivantes de votre  [organisation de projet][dirs] :

* `/static/*`
* `/content/*`
* `/data/*`
* `/i18n/*`
* `/layouts/*`
* `/themes/<CURRENT-THEME>/*`
* `config`

Chaque fois que vous faites des modifications, Hugo reconstruira le site en même temps et continuera à diffuser du contenu. Dès que la construction est terminée, LiveReload indique au navigateur de recharger silencieusement la page.

La plupart des builds de Hugo sont si rapides que vous ne remarquez peut-être pas le changement à moins de regarder directement le site dans votre navigateur. Cela signifie que garder le site ouvert sur un deuxième moniteur (ou une autre moitié de votre moniteur actuel) vous permet de voir la version la plus à jour de votre site sans avoir à quitter votre éditeur de texte.

{{% note "Fermer la balise `</body>` "%}}
Hugo injecte le `<script>` LiveReload avant la `</body>` de fermeture dans vos modèles et ne fonctionnera donc pas si cette balise n'est pas présente..
{{% /note %}}

### Désactiver le LiveReload

LiveReload fonctionne en injectant JavaScript dans les pages générées par génère. Le script crée une connexion entre le client de socket Web du navigateur et le serveur de socket web Hugo.

LiveReload est génial pour le développement. Cependant, certains utilisateurs Hugo peuvent utiliser `hugo server` en production pour afficher instantanément le contenu mis à jour. Les méthodes suivantes permettent de désactiver LiveReload :

```bash
hugo server --watch=false
```

Ou...

```bash
hugo server --disableLiveReload
```

Ce dernier marqueur peut être omis en ajoutant la valeur-clé suivante à votre fichier `config.toml` ou` config.yml`, respectivement :

```toml
disableLiveReload = true
```

```yaml
disableLiveReload: true
```

## Déployer votre site web 

Après avoir lancé `hugo server` pour du développement web en local, vous devez lancer une commande finale  `hugo` *sans la partie `server` de la commande* pour reconstruire le site. Vous pouvez alors déployer votre site en copiant le répertoire `public/` vers votre serveur de production web.

Étant donné que Hugo génère un site Web statique, votre site peut être hébergé *n'importe où* en utilisant n'importe quel serveur web. Voir  [Hébergement et déploiement][hosting] pour des méthodes d'hébergement et d'automatisation des déploiements utilisées par la communauté Hugo. 

{{% warning "Les Fichiers Générés ne sont **PAS** Retirés sur le  Build" %}}
Lancer `hugo` *ne retire pas* les fichiers générés avant la construction. Ceci veut dire que vous devriez effacer votre dossiers `public/` (ou le dossier de publication que vous avez spécifié par le flag ou le fichier de configuration) avant de lancer la commande `hugo`. Si vous ne retirer pas ces fichiers, vous courez le risque d'avoir de mauvais fichiers (par ex. des brouillons ou posts à venir) ayant été laissé dans le site généré.
{{% /warning %}}

### Destinations Dev vs Déploiement

Hugo ne supprime pas les fichiers générés avant de construire. Une solution facile consiste à utiliser différents répertoires pour le développement et la production.

Pour démarrer un serveur qui crée un projet de contenu (utile pour l'édition), vous pouvez spécifier une destination différente; Par exemple, un répertoire `dev/` :

```bash
hugo server -wDs ~/Code/hugo/docs -d dev
```

Lorsque le contenu est prêt à être publié, utilisez par défaut le répertoire `public/`  :

```bash
hugo -s ~/Code/hugo/docs
```

Ceci évite que du contenu à l'état d'ébauche ne devienne accidentellement disponible.

[commandes]: /commandes/
[config]: /demarrage/configuration/
[dirs]: /demarrage/structure-dossier/
[front matter]: /gestion-contenu/front-matter/
[hosting]: /hebergement-et-deploiement/
[install]: /demarrage/installer/
