---

title: QuickStart
linktitle: QuickStart
description: Avant de vous lancer dans la construction d'une documentation, un guide simple pour créer une bibliothèque en ligne. Une occasion de taper dans ligne de commande Hugo, la structure du répertoire, la configuration et l'installation d'un thème.
date: 2013-07-01
publishdate: 2013-07-01
lastmod: 2017-06-23
categories: [démarrage]
#tags: [quick start,usage]
authors: [Shekhar Gulati, Ryan Watters]
menu:
weight: 10
draft: false
aliases: [demarrage/quick-start,getting-started/quick-start]
toc: true
wip: true
---

{{% note %}}
Ce Guide de Démarrage Rapide a été initialement écrit par [Shekhar Gulati](https://twitter.com/shekhargulati) dans sa série de posts [52 Technologies in 2016](https://github.com/shekhargulati/52-technologies-in-2016) mais il a été considérablement modifié pour présenter les fonctionnalités supplémentaires et autres modifications dans Hugo.
{{% /note %}}

Dans ce guide de démarrage, nous allons construire une bibliothèque qui listera des livres et leurs critiques.

## Étape 1. Installez Hugo

[Installez Hugo](/installer-hugo). Si vous installez à partir des [Versions Hugo][2], vous devrez sauvegarder l'exécutable principal sous `hugo`(ou `hugo.exe` sur Windows) quelque part dans votre `PATH`. Vous aurez besoin de la commande `hugo`pour les étapes suivantes.

{{% note "Utilisateurs Windows et Git Bash" %}} Si vous êtes sous Windows, ce guide de démarrage suppose que vous utilisez [Git Bash][3] (aussi connu comme Git pour Windows). Par conséquent, toutes les commandes démarreront avec le caractère d'invitation Bash (qui est `$`).{{% /note %}}

Une fois `hugo` intallé, assurez-vous de lancer la commande `help` pour vérifier l'installation de `hugo`. Ci-dessous, vous pouvez voir une partie traduite de l'output de la commande `help`.
    
```bash
hugo help

hugo is the main command, used to build your Hugo site.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at http://gohugo.io/.
```

Vous pouvez vérifier la version de  `hugo` en utilisant la commande en dessous.

```bash    
$ hugo version
```    

```bash
Hugo Static Site Generator v0.25 darwin/amd64 BuildDate: 2017-07-07T19:09:03+02:00
```
## Étape 2. Échafaudez le site de la Bibliothèque avec Hugo 

Hugo dispose de commmandes qui nous permettent d'échafauder rapidement un site web géré avec Hugo. Naviguez vers un endroit qui vous plaira sur votre système de fichiers, et créez un nouveau site `bibliotheque` en exécutant la commande qui suit : 

```bash
$ hugo new site bibliotheque
```
        
Changez de répertoire vers le nouveau répertoire  `bibliotheque` 

    $ cd bibliotheque 

Lancez la commande `tree -a` pour visualiser  le contenu de votre répertoire :


```bash
$ tree -a
```

```bash
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes

6 directories, 1 file
```

Vous verrez le dossier `bibliotheque` qui comprend 6 sous-dossiers et 2 fichiers. Jetons un oeil à chacun d'eux.

* **archetypes** : [Archetypes][archetypes] vous permet de pré-configurer le front-matter pour les fichiers de contenu dans Hugo pour un meilleur échafaudage du contenu en utilisant la commande `hugo new`. 
* **config.toml** : Hugo utilise `.toml`pour son propre format de configuration. mais il accepte aussi bien les formats `.yml` ou `.json`. Les réglages de configuration mentionnés dans le fichier `config.toml`s'appliquent à l'ensemble du site web et comprennent des variables globales importantes telles que la `baseURL` et le `title` de votre site web. (Voir [configuration](configurer-hugo.md))
* **content** : Ce dossier unique abrite tous les contenus de votre site web. Chaque sous-répertoire dans content s'appelle une section. Si votre site web dispose de sections pour les articles, événements et tutoriels, vous pourriez créer `content/posts`, `content/events` et `content/tutoriels`.
* **data** : Ce dossier est utilisé pour stocker les fichiers de données en séries (YAML, JSON, ou TOML) qui peuvent être utilisés dans les [data templates](templates/data-templates/) et votre [menu de site web](/gestion-contenu/menus/).
* **layouts** : C'est le carrefour pour tous vos [modèles](templates/introduction/), incluant les [modèles de listes et sections](templates/lists/) et [shortcodes](/templates/shortcode-templates/).
* **static** : Ce dossier accueille tout le contenu statique ; par exemple les images, JavaScript et CSS. Tout ce qui est dans `/static` est copié tel quel vers votre site web fini.
* **themes** : C'est l'endroit où vous stockerez les thèmes Hugo. Vous pouvez voir une galrie de tous les thèmes sur [http://themes.gohugo.io](https://themes.gohugo.io)

## Étape 3. Ajoutez du Contenu

Ajoutons maintenant un article à notre   `bibliotheque`. Nous utiliserons la commande `hugo new` pour ajouter un article. Ce premier post sera sur le livre [Good To Great][6]. **Assurez-vous de bien être dans le dossier `bibliotheque`.** Et lancez la commande : 

{{% code file="create-new-book-review-post.sh" %}}
```bash
    $ hugo new post/good-to-great.md
```
{{% /code %}}    
Vous devriez voir s'afficher ce qui suit : 

```bash
/Users/votrenomutilisateur/bibliotheque/content/post/good-to-great.md created
```

La commande au-dessus créera un nouveau dossier `post`  à l'intérieur du dossier `content` et créera `content/post/good-to-great.md`. Le répertoire pour votre projet Hugo ressemblera maintenant à ce qui suit : 
  

```bash
.
├── archetypes
├── config.toml
├── content
│   └── post
│       └── good-to-great.md
├── data
├── layouts
├── static
└── themes
```


Ouvrez `good-to-great.md` dans votre éditeur de texte préféré : 

```toml
+++
date = "2017-02-19T21:09:05-06:00"
title = "good to great"
draft = true

+++
```

Le contenu encadré entre les signes `+++` est le [front matter][fm] pour le contenu. Le front matter vous permet de définir des méta-données embarquées qui voyage avec le fichier de contenu. Parce que nous n'avons pas configuré quelque [archétype][] pour notre projet, Hugo a utilisé ses propriétés de configuration natives, qui incluent les trois valeurs dans le front-matter :  

* `date` spécifie la date et l'horaire à laquelle le billet a été créé.
* `title` spécifie le titre du billet.
* `draft` quand il est réglé sur `true`, dit à Hugo que ce post n'est pas prêt pour la publication.

Ajoutons une petite critique pour le livre **Good to Great** :     

{{% code file="good-to-great-start.md" %}}
```markdown
+++
date = "2016-02-14T16:11:58+05:30"
draft = true
title = "Good to Great Book Review"
+++

I read **Good to Great in January 2016**. An awesome read sharing detailed analysis on how good companies became great. Although this book is about how companies became great but we could apply a lot of the learnings on ourselves. Concepts like level 5 leader, hedgehog concept, the stockdale paradox are equally applicable to individuals.
```
{{% /code %}}

## Étape 4. Servez le contenu

Hugo a un serveur intégré qui peut servir le contenu de votre site web afin que vous puissiez le prévisualiser facilement et développer. Pour servir le contenu, lancez la commande suivante à l'intérieur de votre répertoire `bibliotheque` :

```bash
$ hugo server
```
    
Vous devriez voir quelque chose de similaire à ce qui suit : 

```bash
Built site for language en:
0 of 1 draft rendered
0 future content
0 expired content
0 regular pages created
1 other pages created
0 non-page files copied
0 paginator pages created
0 tags created
0 categories created
total in 1 ms
Watching for changes in /Users/yourusername/bookshelf/{data,content,layouts,static}
Serving pages from memory
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Cette commande lancera le serveur sur le port `1313`. Vous pourrez regarder votre blog à l'adresse <http://localhost:1313/>. Cependant, si vous allez sur le lien, vous ne verrez rien ! Deux raisons à cela : 

1. Comme vous pouvez le voir dans la sortie de commande `hugo server`, Hugo n'a *pas* produit le draft. Hugo ne produira les drafts (ébauches) que si vous passez l'option `buildDrafts` sur la commande `hugo server`.
2. Nous n'avons pas spécifié comment le contenu Markdown devrait être produit. Nous devons spécifier un thème à utiliser par Hugo. Nous ferons ça à l'étape suivante.

Tuez le serveur en utilisant <kbd>Ctrl</kbd> + <kbd>C</kbd> et relancez le serveur avec l'option `--buildDrafts` ajoutée à la commande :

```bash
hugo server --buildDrafts
```

Vous devriez maintenant voir quelque chose de similaire à ce qui suit : 
    
```bash
Built site for language en:
1 of 1 draft rendered
0 future content
0 expired content
1 regular pages created
2 other pages created
0 non-page files copied
0 paginator pages created
0 tags created
0 categories created
total in 2 ms
Watching for changes in /Users/yourusername/bookshelf/{data,content,layouts,static}
Serving pages from memory
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Très bien. Maintenant nous avons notre page unique "build", mais nous ne voyons rien dans le navigateur  à l'adresse <http://localhost:1313/>. Ceci n'était fait que pour démontrer l'utilité de l'option `--buildDrafts`.

Pendant que nous nous approchons du but, nous devons indiquer à Hugo un thème à utiliser au moment de la construction du site.

## Étape 5. Ajoutez un thème

Les [thèmes][themesection] fournissent à Hugo la mise en page et les modèles pour rendre votre site Web. Vous pouvez voir la sélection complète de thèmes open source sur <https://themes.gohugo.io/>.

{{% note "Pas de Thèmes Hugo par Défaut" %}}
À ce jour, Hugo n'est toujours pas livré avec un thème par défaut, permettant ainsi à l'utilisateur de choisir le thème qui conviendra le mieux à son projet.
{{% /note %}}

Les thèmes doivent être ajoutés dans le dossier `themes`, l'un des dossiers échafaudés avec la commande `hugo new site` que nous avons utilisée pour démarrer notre projet Hugo. Pour installer nos thèmes, déplaçons-nous tout d'abord dans le répertoire `themes` : 

```bash    
$ cd themes
```

Vous pouvez cloner un ou plusieurs thèmes à l'intérieur de votre dossier `themes`. Nous utiliserons le [thème `robust`](https://github.com/dim0627/hugo_theme_robust), mais au commit le plus récent à la dernière mise à jour de ce guide de démarrage rapide.
  
Une fois dans le dossier `themes`, vous pouvez uitliser la commande suivante en une ligne pour cloner Robust, check out le commit spécifique, et revenir ensuite à la racine de votre dossier projet :

{{% code file="clone-robust-theme" %}}
```bash
git clone https://github.com/dim0627/hugo_theme_robust.git && cd hugo_theme_robust && git checkout 3baae29 && cd ../..
```
{{% /code %}}

Maintenant redémarrons le serveur Hugo mais avec l'ajout de l'option `--theme` pour Robust : 
    
{{% code file="hugo-server-with-theme.sh" %}}
```bash
hugo server --theme=hugo_theme_robust --buildDrafts
```
{{% /code %}}

Vous devriez voir un output de console similaire à ce qui suit : 

```bash
Built site for language en:
1 of 1 draft rendered
0 future content
0 expired content
1 regular pages created
2 other pages created
0 non-page files copied
2 paginator pages created
0 tags created
0 categories created
total in 8 ms
Watching for changes in /Users/yourusername/bookshelf/{data,content,layouts,static,themes}
Serving pages from memory
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```


Si Hugo ne trouve pas le thème spécifié dans le dossier `themes`, il lancera une exception comme affiché en-dessous._

```bash
FATAL: 2016/02/14 Unable to find theme Directory: /Users/xtof/bibliotheque/themes/robust
```

Pour voir votre site web, rendez-vous maintenant sur <http://localhost:1313/>. Vous verrez ce qui s'affiche ci-dessous.

![](https://d33wubrfki0l68.cloudfront.net/e988e7a93df69093c8c0dda7c05098536b8462e8/88604/images/quickstart/bookshelf-robust-theme.png)

Comme nous l'avions fait lors de l'échafaudage de notre nouveau site web Hugo, jetons un oeil à ce que comprend un thème typique. Ce qui suit n'est qu'une sélection de ce que vous verriez si vous listiez les contenus du répertoire du thème Robust. Il y a aussi quelques-uns des fichiers par défaut créés par Hugo v0.23. (Voir [Créer un Thème](/themes/creer/))

```bash
.
├── LICENSE.md
├── archetypes
│   └── default.md
├── layouts
│   ├── 404.html
│   ├── _default
│   │   ├── list.html
│   │   └── single.html
│   ├── index.html
│   └── partials
│       ├── footer.html
│       └── header.html
├── static
│   ├── css
│   └── js
└── theme.toml
```


* `theme.toml` est le fichier de configuration du thème qui vous donne l'information sur le thème comme le nom et la description du thème, les détails de l'auteur, la licence du thème, la version minimum d'Hugo qui sera par défaut celle de votre version d'Hugo localement installée.
* `layouts` contient différentes vues (c.a.d. des [modèles](/templates/) pour différents types de contenus. Dans ce guide de démarrage,  nous voyons que chaque type de contenu a un fichier `single.html` et un fichier  `list.html`. `single.html` est utilisé pour rendre un élement unique de contenu. `list.html` s'utilise pour visualiser `*.md*` dans la section posts. Pensez à `list.html` comme `exemple.com/posts/` et `single.html` comme `exemple.com/posts/mon-post-unique/`.
* ``static`` a le même objectif que celui du `static` dans notre échafaudage original. Ce dossier stocke tous les actifs statiques utilisés par le thème et il est copié *tel quel* au moment du build.

## Étape 6. Utilisez plusieurs thèmes

Vous pouvez facilement tester différentes configurations en alternant entre différents thèmes. dans Hugo. Supposons que nous voulions essayer le [thème `bleak`.](http://themes.gohugo.io/bleak/). Tuez le serveur Hugo si vous êtes encore en train de le faire fonctionner à la ligne de commande. 

À partir de la racine de votre projet, vous pouvez utiliser cette commande-en-une-ligne pour vous déplacer dans le dossier themes, cloner Bleak et revenir à la racine de votre projet :  

{{% code file="clone-bleak-theme.sh" %}}
```bash
cd themes && git clone https://github.com/Zenithar/hugo-theme-bleak.git && cd ..
```
{{% /code %}}

Maintenant, redémarrez le serveur avec notre option de nouveau thème :
    
{{% code file="run-server-with-bleak.sh" %}}
```bash
hugo server --theme=hugo-theme-bleak --buildDrafts
```
{{% /code %}}    

Notre site web utilise maintenant le thème `bleak` sur [http://localhost:1313](http://localhost:1313) et s'affiche différemment comme ci-dessous : 

![Bibliothèque avec le thème Bleak](https://monosnap.com/file/rSwnbQN1sEzIPE450E3KQ9oOH4opHl.png)

## Étape 7. Mise à jour de votre configuration

Arrêtez si besoin le serveur et redémarrez avec le thème `robust`, car nous allons utiliser ce thème pour ce guide de démarrage rapide : 

{{% code file="restart-with-robust-sh" %}}
```bash
hugo server --theme=hugo_theme_robust --buildDrafts
```
{{% /code %}}    

### Mise à jour de Notre `config.toml`

Notre site web utilise actuellement les valeurs stupides spécifiées dans le fichier de configuration `bibliotheque/config.toml`, qui a été auto-généré avec `hugo new site bibliotheque`. Mettons à jour la configuration.
        
{{% code file="updated-config.toml" %}}
```toml
baseURL = "http://exemple.org/"
languageCode = "fr-fr"
title = "Critiques de Livres par Shekhar Gulati"

[Params]
      Author = "Shekhar Gulati"
```
{{% /code %}}
### Regardez votre Site se Recharger Instantanément 

Hugo supporte nativement le rechargement en live. Ce qui veut dire que Hugo reconstruira et rechargera votre site à chaque fois que vous sauvegarderez une modification d'un contenu, template, asset statique et même votre fichier de configuration. Vous devriez voir quelque chose de similaire à la capture-écran en-dessous en vous rendant sur <http://localhost:1313> une fois que vous aurez sauvegardé les modifications ci-dessus dans votre fichier `config.toml` : 

![Fichier config.toml mis à jour. (titre du site et nom de l'auteur)](https://monosnap.com/file/UbJoG3jvblTgmwRk1fO7Ymc8dLIg7l.png)

Outre la visualisation, vous retrouverez la modification dans la console. Dès que vous avez modifié le fichier de configuration, Hugo a appliqué ces modifications aux pages concernées et reconstruit le site :     
```    
Config file changed: /Users/votrenomutilisateur/bibliotheque/config.toml
Started building sites ...
Built site for language en
1 of 1 draft rendered
0 future content
0 future content
0 expired content
1 regular pages created
2 other pages created
0 non-page files copied
2 paginator pages created
0 tags created
0 categories created
total in 20 ms
```

## Étape 8. Personnalisez le Thème robust

Le thème `robust` est un bon départ pour notre bibliothèque en ligne mais nous voulons le personnaliser afin de le rapprocher de nos besoins pour une bibliothèque. Hugo [facilite la personnalisation des thèmes. Vous pouvez aussi créer vos propres thèmes](https://gohugo.io/themes/). Pour ce guide nous nous concentrerons sur la personnalisation.

Le premier changement sera d'utiliser une image par défaut différente de celle utilisée dans le thème. L'image par défaut du thème utilisée à la fois dans le fichier `list.html`et `single.html` se trouve à l'intérieur de `themes/hugo_theme_robust/static/images/default.jpg`. Nous pouvons facilement l'annuler en créant une simple structure de dossier à l'intérieur de notre dossier `static`.

Créez un dossier `images` dans le répertoire `bibliotheque/static` et copiez dedans une image avec le nom `default.jpg`. Nous utiliserons par défaut l'image affichée en dessous.

![image `default.jpg` à copier dans votre dossier `bibliotheque/static/images`][11]

Hugo synchronisera les modifications et rechargera le site web pour utiliser cette nouvelle image 

![Nouvelle image par défaut](https://monosnap.com/file/VsZKPzYi4vydK1787jnuwRBTexV7yE.png)

Maintenant, nous devons modifier le layout de la page index afin que seules les images soient affichées au lieu du texte. Le fichier `themes/hugo-theme_robust/layouts/index.html` fait référence au partiel `li` qui produit la vue en liste ci-dessous.    

```html
<article class="li">
  <a href="{{ .Permalink }}" class="clearfix">
    <div class="image" style="background-image: url({{ $.Site.BaseURL }}images/{{ with .Params.image }}{{ . }}{{ else }}default.jpg{{ end }});"></div>
    <div class="detail">
      <time>{{ with .Site.Params.DateForm }}{{ $.Date.Format . }}{{ else }}{{ $.Date.Format "Mon, Jan 2, 2006" }}{{ end }}</time>
      <h2 class="title">{{ .Title }}</h2>
      <div class="summary">{{ .Summary }}</div>
    </div>
  </a>
</article>
```

Créez un nouveau fichier `li.html` à l'intérieur du dossier `bibliotheque/layouts/_default`. Si vous êtes à la racine de votre projet, vous pouvez utiliser la commande-en-une-ligne qui suit pour créer à la fois le fichier et revenir à la racine : 

{{% code file="create-new-li-html.sh" %}}
```bash
cd layouts && mkdir _default && cd _default && touch li.html && cd ../..
```
{{% /code %}}

Copiez le contenu affiché en dessous dans le nouveau fichier `li.html`. Si vous comparez ça avec le `li.html`livré avec le thème Robust, vous remarquerez que nous avons enlevé les détails du livre, afin que seule l'image s'affiche.


{{% code file="layouts/_default/li.html" %}}
```html
<article class="li">
  <a href="{{ .Permalink }}" class="clearfix">
    <div class="image" style="background-image: url({{ $.Site.BaseURL }}images/{{ with .Params.image }}{{ . }}{{ else }}default.jpg{{ end }});"></div>
  </a>
</article>
```
{{% /code %}}

Maintenant, le site web devrait ressembler à ce qui s'affiche en-dessous 

![... image sans détails.](https://monosnap.com/file/GgqLdZrcGQu87neTAWQQGN4VBxLjOl.png)

Ensuite, nous voulons retirer l'information présente en pied de page concernant le thème. Pour faire ainsi, créez un nouveau dossier sur `bibliotheque/layouts/partials`. Celui-ci détiendra notre nouveau fichier appelé `default_foot.html`

Ceci est un nouveau [modèle partiel][partials]. Si vous êtes encore à la racine du répertoire de votre projet, vous pouvez utilisez la commande-en-une-ligne qui suit pour créer le partial avant de de revenir à la racine du projet : 

{{% code file="create-new-default-foot.sh" %}}
```bash
cd layouts && mkdir partials && cd partials && touch default_foot.html && cd ../..
```
{{% /code %}}


Ajoutez maintenant ce qui suit à notre nouveau modèle partiel `default_foot.html` : 

 {{% code file="layouts/partials/default_foot.html" %}}
```html
<footer class="site">
  <p>{{ with .Site.Copyright | safeHTML }}{{ . }}{{ else }}&copy; {{ $.Site.LastChange.Year }} {{ if isset $.Site.Params "Author" }}{{ $.Site.Params.Author }}{{ else }}{{ .Site.Title }}{{ end }}{{ end }}</p>
  <p>Powered by <a href="http://gohugo.io" target="_blank">Hugo</a>,</p>
</footer>
```
{{% /code %}}
    

A ce stade nous utilisons l'image par défaut mais nous aimerions utiliser l'image du livre que nous pourrions rattacher au livre. Chaque critique de livre définira un réglage de configuration dans son front matter. Mettez à jour le contenu et le front matter de `good-to-great.md` comme affiché ci-dessous :  

{{% code file="content/post/good-to-great.md" %}}
```markdown
+++
date = "2017-02-19T21:09:05-06:00"
draft = true
title = "Good to Great Book Review"
image = "good-to-great.jpg"
+++

I read **Good to Great in January 2016**. An awesome read sharing detailed analysis on how good companies became great. Although this book is about how companies became great but we could apply a lot of the learnings on ourselves. Concepts like level 5 leader, hedgehog concept, the stockdale paradox are equally applicable to individuals.
```
{{% /code %}}


Piquez quelque part (légal SVP) une image, appelez-la `good-to-great.jpg`, et placez-la dans le dossier `bibliotheque/static/images`.

Après avoir ajouté quelques autres livres à notre bibliothèque, voici à quoi ressemble le premier rayon. 

![image à refaire en français](https://d33wubrfki0l68.cloudfront.net/e03165bd6db7ba50f0bb728074b50809562fb050/ae4e7/img/quickstart/bookshelf.png)

{{% note %}}
Dernier raffinage facultatif. Vous pouvez retirer la barre latérale à droite. Copiez le fichier `index.html` dans le dossier `layouts` du thème vers le dossier `bibliotheque/layouts`. Et tetirez la section en rapport avec la barre latérale du HTML :

```html
<div class="col-sm-3">
    {{ partial "sidebar.html" . }}
</div>
```
{{% /note %}}


## Étape 9. Rendez les posts publics

À ce stade, tous les posts que nous avons écrits sont en statut draft, c'est à dire `draft=true` (ébauche). Afin de faire qu'un draft soit public, vous pouvez soit lancer une commande ou modifier manuellement le statut draft dans le post en `false`. Hugo fournit une commande pratique appelée `undraft`pour faire ça :

```bash
hugo undraft content/post/good-to-great.md
```

Si nous vérifions le front matter de `good-to-great.md` après avoir lancé cette commande, nous remarquons que Hugo a écrit la modification du statut draft au fichier : 

```toml
+++
date = "2017-02-19T22:42:53-06:00"
draft = false
title = "Good to Great Book Review"
image = "good-to-great.jpg"
+++
```

Maintenant, nous pouvons lancer le serveur *sans* l'option `buildDrafts`.

```bash
$ hugo server --theme=hugo_theme_robust
```


<!-- ## Step 10. Integrate Disqus Comments

{{% note "Adding Disqus to Your Website" %}}
To implement Disqus comments as part of the Quick Start, you'll need to set up a Disqus account. Follow the [Disqus documentation for adding their service to websites](https://help.disqus.com/customer/portal/articles/1257441-adding-disqus-to-your-site).
{{% /note %}}

To enable Disqus on our new site, we only need to update the `disqusShortname` in the config.toml as shown below.

```toml
[Params]
  Author = "Shekhar Gulati"
  disqusShortname = <your disqus shortname>
```

Now, commenting will be enabled in your blog.

![](/images/quickstart/bookshelf-disqus.png)
 -->


## Étape 10. Construisez votre site Web 

Pour générer un site web qui puisse être déployé vers GitHub Pages. nous avons besoin de modifier la ligne `baseURL` dans notre configuration comme suit :

```toml
baseURL = "https://<votre nomutilisateur GitHub>.github.io/bibliotheque/"
```

Puis lancez la commande suivante à partir du répertoire racine de votre projet Hugo : 

```bash
hugo --theme=hugo_theme_robust
0 draft content
0 future content
5 pages created
2 paginator pages created
0 tags created
0 categories created
in 17 ms
```

Après avoir lancé la commande `hugo`, un répertoire  `bibliotheque/public` est créé contenant la source du site web généré.

P.S. En passant, (si vous avez essayé), le site web n'est pas accessible proprement via le protocole `file:///`.


## Étape 11. Et après ?

**Bravo !** Votre nouveau répertoire public `bibliothèque`/ est un site web Hugo entièrement généré et déployable. Tous vos fichiers étant  _statiques_, vous avez d'innombrables options d'hébergement. Votre nouvelle structure de répertoire et votre format de contenu simple vont améliorer grandement votre site web.

Voic ce que vous pourriez regardez ensuite : 

  1. [Voir les options d'hébergement et de déploiement](/hebergement-et-deploiement/) pour partager votre nouveau site web Hugo avec le monde.
  2. [Apprenez en plus sur la modélisation puissante d'Hugo](/templates/introduction/) pour personnaliser votre site web Hugo à vos besoins spécifiques et pour le faire grandir.
  3. [Visitez le Forum de discussion Hugo](https://discourse.gohugo.io) pour poser des questions, répondre aux questions et devenir un membre actif de la communauté Hugo.


## (Option) Étape 12. Déployez le site bibliotheque sur GitHub pages

Lançons le contôle de version de votre bibliotheque : 

    $ git init
    $ echo "/public/" >> .gitignore
    $ echo "/themes/" >> .gitignore
    $ git add --all
    $ git commit -m "Initial commit"
    

Maintenant les repos Git sous `bibliotheque/themes` ne rentreront plus en conflit avec votre repo `bibliotheque`, et c'est aussi le cas pour un repo Git dans `bibliotheque/public`.

Créez un nouveau repository sur GitHub appelé `bibliotheque` (sans  README). Une fois que c'est fait, créez un nouveau repo Git sur votre système local dans `bibliotheque/public` et ajoutez remote :

    $ cd public
    $ git init
    $ git remote add origin git@github.com:<votre-nomutilisateur-github>/bibliotheque.git

Puis créez et checkout une nouvelle branche `gh-pages`

    $ git checkout -b gh-pages
    Switched to a new branch 'gh-pages'
    

Ajoutez tous les fichiers (dans `bibliotheque/public`) à l'index, commitez-les, et poussez les modifications sur GitHub.

    $ git add --all
    $ git commit -m "bibliotheque added"
    $ git push -f origin gh-pages


Dans quelques minutes, votre site web sera vivant sur `https://<github-nomutilisateur>.github.io/bibliotheque/`.

A tout moment, vous pouvez régénérer votre site avec : 

    $ (cd ..; hugo --theme=hugo_theme_robust)
    $ git add --all
    $ git commit -m "<some change message>"
    $ git push -f origin gh-pages
    

* * *

Ce tutoriel rapide a été initialement écrit par [Shekhar Gulati][16] dans sa série de blog [52 Technologies in 2016][17].

[archétype]: /gestion-contenu/archetypes/
[fm]: /gestion-contenu/front-matter/
[themesection]: /themes/
[partials]: /templates/partials/

[2]: https://github.com/gohugoio/hugo/releases
[3]: https://git-for-windows.github.io/
[4]: /archetypes/
[5]: https://github.com/toml-lang/toml
[6]: http://www.amazon.com/Good-Great-Some-Companies-Others/dp/0066620996/
[7]: https://d1ro8r1rbfn3jf.cloudfront.net/ms_35590/CPzNqsm7sTlNQvQkjipd39Nr8Sfxap/My%2BNew%2BHugo%2BSite-theme-robust.png?Expires=1499000968&Signature=hn3OOZ4lAQcizvR-NXOnJUVuift1Lchg2RGP4zrl9XUzQFKEjGcPtW6JZOFhlZCGM1w4~A2tBJSzU2se8JiuWoEv46sMPZU9Am7UGzxXV2eyemeVFng0Nze9bq~FNDCAQt920Khpk7tM5lGCzjc3MmTckVp4qkSsxA1l-lCjelJKoRExP5dttNIp84Z7BzZUaP23shWEF40hcfSYkfbTRv4LRwJ6-eQeCqHOml4l9Cd~btaJ4oTRkOXk6YNH13lbQe~~FwwYbCMnVUhzIld2jOuFcPOpQTR16KzWgrMd0kHsC18q3nQzW1lh9CA-p8ZOSKy1FrgjeQ0wFAJo8npgLg__&Key-Pair-Id=APKAJHEJJBIZWFB73RSA
[8]: loudfront.net/e1f909506901b95bb95c7b1e59055658eadc5641/0f5ca/img/quickstart/bookshelf-bleak-theme.png
[9]: https://d33wubrfki0l68.cloudfront.net/08d0677e03a918c95c5bb5060f66165e09c1e8d3/7a5b5/img/quickstart/bibliotheque-updated-config.png
[10]: https://gohugo.io/themes/creation/
[11]: https://d33wubrfki0l68.cloudfront.net/447347fbf1133963df95f6509f7c54176431106d/8613d/img/quickstart/default.jpg
[12]: https://d33wubrfki0l68.cloudfront.net/23f0d937f891116d0838edc3567d59e9e21bf949/de922/img/quickstart/bibliotheque-new-default-image.png
[13]: https://d33wubrfki0l68.cloudfront.net/2892039ba375a68aa7797e1c41e8daebccf7a3e4/525e1/img/quickstart/bibliotheque-only-picture.png
[14]: https://d33wubrfki0l68.cloudfront.net/e03165bd6db7ba50f0bb728074b50809562fb050/ae4e7/img/quickstart/bibliotheque.png
[15]: https://d33wubrfki0l68.cloudfront.net/befcde2ffdd91d30376565731957739cf6fd615c/ce533/img/quickstart/bibliotheque-disqus.png
[16]: https://twitter.com/shekhargulati
[17]: https://github.com/shekhargulati/52-technologies-in-2016

