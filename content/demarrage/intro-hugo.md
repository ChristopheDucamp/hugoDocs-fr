+++

title = "C'est quoi Hugo ?"
description = "Une rapide introduction à Hugo par son auteur"
weight = 1
+++
{{% note %}}
[Source "Introduction to Hugo" par Steve Francia (auteur d'Hugo)](https://gohugo.io/overview/introduction/) - traduction en cours ouverte à toutes vos améliorations.
{{% /note %}}

## C’est Quoi Hugo ?

Hugo est un framework de site Web généraliste. Techniquement parlant, Hugo est un générateur de site statique. Contrairement à d'autres systèmes qui créent dynamiquement une page chaque fois qu'un visiteur en fait la demande, Hugo lance la construction lorsque vous créez votre contenu. Étant donné que les sites Web sont affichés beaucoup plus souvent qu'ils ne sont édités, Hugo est optimisé pour l'affichage du site tout en offrant une excellente expérience d'écriture.

Les sites construits avec Hugo sont extrêmement rapides et très sécurisés. Les sites Hugo peuvent être hébergés n'importe où, y compris chez [Heroku][1], [GoDaddy][2], [DreamHost][3], [GitHub Pages][4], [Netlify][5], [Surge][6] , [Aerobatic][7], [Firebase Hosting][8], [Google Cloud Storage][9], [Amazon S3][10] et [CloudFront][11], et fonctionnent bien avec les CDN. Les sites Hugo s'exécutent sans dépendances aux runtimes coûteuses comme Ruby, Python ou PHP et sans dépendances aux bases de données.

Nous pensons que Hugo est l'outil de création de site idéal. Avec des temps de construction presque instantanés et la possibilité de reconstruire à chaque fois qu'un changement est effectué, Hugo fournit une boucle de rétroaction très rapide. Ceci est essentiel lorsque vous concevez des sites Web, mais c'est aussi très utile lors de la création de contenu.

## Qu'est-ce qui fait que Hugo est si différent ?

Les générateurs de sites Web génèrent du contenu dans des fichiers HTML. La plupart sont des «générateurs de sites dynamiques». Cela signifie que le serveur HTTP (le programme exécuté sur votre site Web à qui parle le navigateur de l'utilisateur) lance le générateur pour créer un nouveau fichier HTML à chaque fois qu'un utilisateur souhaite afficher une page.

Créer la page dynamiquement signifie que l'ordinateur hébergeant le serveur HTTP doit disposer d'une mémoire et d'une CPU suffisantes pour exécuter efficacement le générateur 24 heures sur 24. Sinon, l'utilisateur doit attendre dans la file  pour générer la page.

Personne ne veut que les utilisateurs attendent plus longtemps que nécessaire, de sorte que les générateurs de sites dynamiques ont programmé leurs systèmes pour mettre en cache les fichiers HTML. Lorsqu'un fichier est mis en cache, une copie est stockée temporairement sur l'ordinateur. Pour le serveur HTTP c’est beaucoup plus rapide d’envoyer cette copie la prochaine fois que la page sera demandée plutôt que de la générer à partir de rien.

Hugo emmène cette  notion de cache à un niveau plus haut. 
Tous les fichiers HTML sont restitués sur votre ordinateur. Vous pouvez consulter les fichiers avant de les copier sur l'ordinateur hébergeant le serveur HTTP.  Étant donné que les fichiers HTML ne sont pas générés dynamiquement, nous disons que Hugo est un «générateur de site statique».

Il y a de nombreux avantages à ne pas exécuter de générateur de site Web sur votre serveur HTTP.  Le premier avantage et le plus remarquable, c’est la performance - les serveurs HTTP sont très bons pour envoyer des fichiers. Si bien que vous pouvez effectivement servir le même nombre de pages avec une fraction de la mémoire et de la  CPU nécessaires pour un site dynamique.

Hugo a deux composants pour vous aider à construire et à tester votre site web. Celui que vous utiliserez probablement le plus souvent, c’est le serveur HTTP intégré. Lorsque vous lancez la commande `hugo server`, Hugo restitue tout votre contenu sous forme de fichiers HTML, puis exécute un serveur HTTP sur votre ordinateur afin que vous puissiez voir à quoi ressemblent les pages.

Le deuxième composant est utilisé lorsque vous êtes prêt à publier votre site Web sur l'ordinateur qui exécute votre site Web. Exécuter Hugo sans aucune action reconstruira tout votre site Web en utilisant le paramètre `baseURL` réglé dans le fichier de configuration de votre site. Ceci est nécessaire afin que les liens de votre page fonctionnent correctement avec la plupart des hébergeurs.



## La rapidité d’Hugo ?

Une vidéo benchmark qui démontre la vélocité moteur 

<iframe width="560" height="315" src="https://www.youtube.com/embed/CdiDYZ51a2o" frameborder="0" allowfullscreen></iframe>

## Que fait Hugo ?

En termes techniques, Hugo prend un dossier source de fichiers et de modèles, puis les utilise comme input à créer pour générer un site web complet.

Hugo a les caractéristiques suivantes :

### Général

* Temps de construction extrêmement rapide (~1 ms par page)
* Ouvert sur toutes les plates-formes : fonctionne sur macOS, Linux, Windows, et plus encore !
* [Installation facile ][12]
* Rendu des modification [à la volée][13] avec [LiveReload][14] pendant que vous développez
* Support complet des thèmes 
* Héberge votre site n’importe où

### Organisation

* [Organisation du contenu](https://gohugo.io/content/organization/) immédiate
* Support pour les [sections de sites web](https://gohugo.io/content/sections/)
* [URLs](https://gohugo.io/extras/urls/) complètement personnalisables
* Support pour [taxonomies](https://gohugo.io/taxonomies/overview/) configurables qui comprennent les catégories et tags. Créez votre propre organisation de contenu.
* Capacité à [trier le contenu](https://gohugo.io/content/ordering/) comme vous le désirez
* Génération de [tables des matières](https://gohugo.io/extras/toc/) automatique 
* Création dynamique des menus
* Support pour de [Jolies URLs](https://gohugo.io/extras/urls/) 
* [Permalien](https://gohugo.io/extras/permalinks/) pattern support
* [Alias](https://gohugo.io/extras/aliases/) (redirectios)

### Contenu

* Support natif du contenu écrit en [Markdown](https://gohugo.io/content/example/)
* Support pour d'autres langages à travers des _external helpers_, voir [formats supportés](https://gohugo.io/content/supported-formats)
* Support pour métadonnées TOML, YAML et JSON metadata dans le  [frontmatter](https://gohugo.io/content/front-matter/)
* [Page d'accueil complètement personnalisable](https://gohugo.io/layout/homepage/)
* Support pour plusieurs [types de contenus](https://gohugo.io/content/types/)
* [Résumés](https://gohugo.io/content/summaries/) automatiques et définies par l'utilisateur
* [Shortcodes](https://gohugo.io/extras/shortcodes/) pour permettre le contenu riche dans Markdown
* Fonctionnalité [“Minutes to Read”](https://gohugo.io/layout/variables/) 
* [“Compteur de mots”](https://gohugo.io/layout/variables/) functionality


### Fonctionnalités supplémentaires 

* Support commentaires [Disqus](https://disqus.com/) intégré
* Support intégré des [Google Analytics](https://google-analytics.com/)
* Création automatique de [RSS](https://gohugo.io/layout/rss/) creation
* Support pour les modèles HTML [Go](http://golang.org/pkg/html/template/), [Amber](https://github.com/eknkc/amber) et [Ace](https://github.com/yosssi/ace) 
* [Enluminure de Syntaxe](https://gohugo.io/extras/highlighting/) motorisée par [Pygments](http://pygments.org/)

Regardez ce qui arrive bientôt dans la [roadmap][15].

## Qui devrait utiliser Hugo ?

Hugo est conçu pour les personnes qui préfèrent écrire dans un éditeur de texte plutôt qu’un navigateur. 

Hugo est conçu pour les personnes qui veulent colder à la main leur propre site web sans se soucier de runtimes, dépendances et bases de données compliquées.

Hugo est conçu pour les personnes qui veulent construire un blog, un portfolio, un tumblog, une documentation, un site avec une page unique ou un site avec des milliers de pages.

## Pourquoi avoir écrit Hugo ?

J'ai écrit Hugo en fin de compte pour plusieurs raisons. Tout d'abord, j'ai été déçu par WordPress, ma solution de site Web d’alors. Avec WordPress, je ne pouvais pas créer de contenu aussi efficace que je le voulais. Il était trop lent en production. Il m’obligeait à être en ligne pour écrire des messages : en outre, ses mises à jour de sécurité constantes et les histoires horribles de blogs piratés  !  Je détestais comment le contenu pour WordPress n’était écrit qu'en HTML, au lieu du Markdown beaucoup plus simple. Dans l'ensemble, j'avais l'impression que WordPress me barrait plus le chemin qu’il ne m’aidait. Il m'a empêché d'écrire du contenu formidable.

J'ai regardé les générateurs de sites statiques existants comme [Jekyll][16], [Middleman][17] et [Nanoc][18]. Tous avaient des dépendances d'installation compliquées et prenaient bien plus de temps pour produire mon blog avec ses centaines de messages que ce que je sentais comme acceptable. Je voulais un framework  capable de me donner des feedbacks rapides tout en produisant des modifications aux modèles, et les temps de rendu de 5 minutes et + étaient tout simplement beaucoup trop lents. En général, WordPress était très orienté blog et n’avait pas la capacité de fournir d'autres types de contenu et des URL flexibles.

Je voulais développer un framework de site Web rapide et complet sans aucune dépendance.  Le [langage Go ][19] semblait disposait de toutes les fonctionnalités dont j'avais besoin dans un langage. J'ai commencé à développer Hugo dans Go et suis tombé amoureux du langage. J'espère que vous tirerez autant de plaisir  de pouvoir utiliser Hugo (et y contribuer) autant que je n'en ai eu en l'ayant écrit.

—Steve Francia (@spf13)

## Prochaines étapes 

* [Installer Hugo](/installer/)
* [Démarrage rapide](/quickstart/) si vous êtes perdu.e
* [Rejoignez la liste de discussion](https://gohugo.io/community/mailing-list/)
* [Star us on GitHub](https://github.com/gohugoio/hugo)
* [Forum de discussion](https://discourse.gohugo.io/)



[1]: https://www.heroku.com/
[2]: https://www.godaddy.com/
[3]: http://www.dreamhost.com/
[4]: https://pages.github.com/
[5]: https://www.netlify.com
[6]: https://surge.sh
[7]: https://www.aerobatic.com/
[8]: https://firebase.google.com/docs/hosting/
[9]: http://cloud.google.com/storage/
[10]: http://aws.amazon.com/s3/
[11]: http://aws.amazon.com/cloudfront/ "Amazon CloudFront"
[12]: https://gohugo.io/overview/installing/
[13]: https://gohugo.io/overview/usage/
[14]: https://gohugo.io/extras/livereload/
[15]: https://gohugo.io/meta/roadmap/
[16]: http://jekyllrb.com/
[17]: https://middlemanapp.com/
[18]: http://nanoc.ws/
[19]: http://golang.org/ "The Go Programming Language"

