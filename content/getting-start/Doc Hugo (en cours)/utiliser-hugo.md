+++

title = "Utiliser Hugo"
description = "Hugo run.... Lancer et déployer Hugo."
weight = 4
+++

{{% notice note %}}
[Source "Using Hugo](http://gohugo.io/overview/usage/ "Permalink vers Hugo - Using Hugo") - documentation officielle Hugo, demeurant le seul lien de référence.
{{% /notice %}}

Assurez-vous que Hugo est dans votre `PATH` (ou fournissez un chemin). Testez en lançant :

    
    $ hugo help
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
      help        Help about any commanD
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
    
    Use "hugo [command] --help" for more information about a command.
    

## Exemple Usage Commun

L'utilisation la plus commune est probablement de lancer `hugo` avec votre répertoire en cours étant le répertoire d'input :


    $ hugo
    0 draft content
    0 future content
    99 pages created
    0 paginator pages created
    16 tags created
    0 groups created
    in 120 ms
    

Ceci gnérère votre site web avers le dossier `public/`, prêt à être déployé sur votre serveur web.

## Feedback instantanée au fur et à mesure que vous développez votre site web

Si vous travaillez sur les choses et que vous souhaitez voir les modifications immédiatement, par défaut, Hugo regardera le système de fichiers pour les modifications et reconstruira votre site dès qu'un fichier est enregistré :

    $ hugo -s ~/Code/hugo/docs
    0 draft content
    0 future content
    99 pages created
    0 paginator pages created
    16 tags created
    0 groups created
    in 120 ms
    Watching for changes in /Users/spf13/Code/hugo/docs/content
    Press Ctrl+C to stop

Hugo peut même lancer un serveur et créer un aperçu du site en même temps ! Hugo met en œuvre la technologie [LiveReload](http://gohugo.io/extras/livereload/) pour recharger automatiquement toutes les pages ouvertes dans tous les navigateurs compatibles JavaScript, y compris le mobile. C'est le moyen le plus simple et le plus commun de développer un site Web Hugo :


    $ hugo server -ws ~/Code/hugo/docs
    0 draft content
    0 future content
    99 pages created
    0 paginator pages created
    16 tags created
    0 groups created
    in 120 ms
    Watching for changes in /Users/spf13/Code/hugo/docs/content
    Serving pages from /Users/spf13/Code/hugo/docs/public
    Web Server is available at http://localhost:1313/
    Press Ctrl+C to stop
    

## Déployer votre site web 

Après avoir lancé `hugo server` pour du développement web en local, vous devez lancer une commande finale  `hugo` **sans la partie `server` de la commande** pour reconstruire le site. Vous povez alors **déployer votre site** en copant le répertoire `public/` (par FTP, SFTP, WebDAV, Rsync, `git push`, etc.) vers votre serveur de production.

Étant donné que Hugo génère un site Web statique, votre site peut être hébergé n'importe où, y compris [Heroku](https://www.heroku.com/), [GoDaddy](https://www.godaddy.com/), [DreamHost](http://www.dreamhost.com/), [GitHub Pages](https://pages.github.com/), [Amazon S3](http://aws.amazon.com/s3/) with [CloudFront](http://aws.amazon.com/cloudfront/), [Firebase Hosting](https://firebase.google.com/docs/hosting/), ou tout autre service d'hébergement Web statique pas cher (ou même gratuit).

Apache, nginx, IIS ... Tout logiciel de serveur Web ferait

Since Hugo generates a static website, your site can be hosted anywhere, including [Heroku](https://www.heroku.com/), [GoDaddy](https://www.godaddy.com/), [DreamHost](http://www.dreamhost.com/), [GitHub Pages](https://pages.github.com/), [Amazon S3](http://aws.amazon.com/s3/) with [CloudFront](http://aws.amazon.com/cloudfront/), [Firebase Hosting](https://firebase.google.com/docs/hosting/), or any other cheap (or even free) static web hosting service.

[Apache](http://httpd.apache.org/), [nginx](http://nginx.org/), [IIS](http://www.iis.net/)… N'importe quel logiciel de serveur web le fera !


### Une note concernant le déploiement

Exécuter `hugo` *ne supprime pas* les fichiers générés avant la construction. Cela signifie que vous devez supprimer votre répertoire `public` / (ou le répertoire que vous avez spécifié avec `-d`/`- destination`) avant d'exécuter la commande `hugo`, ou vous risquez que des fichiers incorrects (par ex. les drafts et/ou posts futurs) soient laissés dans le site généré.

Un moyen simple de contourner cela est d'utiliser différents répertoires pour le développement et la production.

Pour démarrer un serveur qui crée un projet de contenu (utile pour l'édition), vous pouvez spécifier une destination différente : le répertoire `dev`.

    $ hugo server -wDs ~/Code/hugo/docs -d dev

Quand le contenu est prêt pour publication, utlisez le répertoire par défaut `public/` :

    $ hugo -s ~/Code/hugo/docs

Ceci évite de publier accidentellement du contenu que vous n'êtes pas encore prêt à partager.


### Alternativement, servez votre site web avec Hugo !

Oui c'est vrai! Parce que Hugo est tellement rapide tant dans la création de sites Web que dans le service Web (grâce à son design et son héritage Go), certains utilisateurs préfèrent utiliser Hugo lui-même pour servir leur site Web sur _leur serveur de production_.

Aucun autre logiciel de serveur Web (Apache, nginx, IIS ...) n'est nécessaire.

Voici la commande :
    
    $ hugo server --baseURL=http://yoursite.org/ \
                  --port=80 \
                  --appendPort=false \
                  --bind=87.245.198.50
 
 
Notez l'option `bind`, qui est l'interface à laquelle le serveur se liera (par défaut '127.0.0.1' : bien pour la plupart des cas d'utilisation en développement). Certains hôtes, comme Amazon Web Services,  lancent NAT (network address translation) ;  Parfois il peut être difficile de trouver l'adresse IP actuelle. L'utilisation de `--bind = 0.0.0.0` se liera à toutes les interfaces.

De cette façon, vous pouvez déployer uniquement les fichiers source, et Hugo sur votre serveur générera le site Web en ligne à la volée et les servira en même temps.

Vous pouvez éventuellement ajouter `--disableLiveReload=true` si vous ne souhaitez pas que le code JavaScript de LiveReload soit ajouté à vos pages Web.

Intéressé ? Voici quelques bons tutoriels fournis par les utilisateurs de Hugo :
  * [hugo, syncthing](http://fredix.xyz/2014/10/hugo-syncthing/) (French) by Frédéric Logier (@fredix)

