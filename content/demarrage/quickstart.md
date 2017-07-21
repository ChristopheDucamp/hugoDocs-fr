+++

title = "Hugo QuickStart"
description = "Avant de vous lancer dans la construction d'une documentation, un guide simple pour créer une bibliothèque en ligne. Une occasion de taper dans ligne de commande Hugo, la structure du répertoire, la configuration et l'installation d'un thème."
weight = 2
+++

[Source originale](https://gohugo.io/getting-started/quick-start/)

{{% note %}} Ce guide de démarrage rapide a été initialement écrit par Shekhar Gulati dans sa série "[52 Technologies in 2016](https://github.com/shekhargulati/52-technologies-in-2016)" mais a été largement modifié pour inclure les nouvelles fonctionnalités et modifications apportées à Hugo.{{% /note %}}

## Construire une Bibliothèque

Dans ce guide de démarrage, nous allons construire une bibliothèque qui listera les livres et leurs critiques.


## Étape 1. Installez Hugo

[Installez Hugo](/installer-hugo). Si vous installez à partir des [Versions Hugo][2], vous devrez sauvegarder l'exécutable principal sous `hugo`(ou `hugo.exe` sur Windows) quelque part dans votre `PATH`. Vous aurez besoin de la commande `hugo`pour les étapes suivantes.


{{% note "Utilisateurs Windows et Git Bash" %}} Si vous êtes sous Windows, ce guide de démarrage suppose que vous utilisez [Git Bash][3] (aussi connu comme Git pour Windows). Par conséquent, toutes les commandes démarreront avec le caractère d'invitation Bash (qui est `$`).{{% /note %}}

Une fois `hugo` intallé, assurez-vous de lancer la commande `help` pour vérifier l'installation de `hugo`. Ci-dessous, vous pouvez voir une partie traduite de l'output de la commande `help`.
    
    
    $ hugo help
    
    hugo c'est la commande principale, utilisée pour construire votre site Hugo.
    
    Hugo est un Générateur de Site Statique (GSS) Rapide et Flexible construit avec amour par spf13 et ses amis en Go.
    
    Une documentation complète est disponible sur http://gohugo.io/.

Vous pouvez vérifier la version de  `hugo` en utilisant la commande en dessous.
    
    $ hugo version
    
    Hugo Static Site Generator v0.25 darwin/amd64 BuildDate: 2017-07-07T19:09:03+02:00
    

## Étape 2. Échafaudez le site de la Bibliothèque avec Hugo 

Hugo dispose de commmandes qui nous permettent d'échafauder rapidement un site web géré avec Hugo. Naviguez vers un endroit qui vous plaira sur votre système de fichiers, et créez un nouveau site `bibliotheque` en exécutant la commande qui suit : 

    $ hugo new site bibliotheque
        
Changez de répertoire vers le nouveau répertoire  `bibliotheque` 

    $ cd bibliotheque 

Lancez la commande `tree -a` pour visualiser  le contenu de votre répertoire :


    $ tree -a
    
    .
    ├── archetypes
    │   └── default.md
    ├── config.toml
    ├── content
    ├── data
    ├── layouts
    ├── static
    └── themes
    
    6 directories, 2 files    

Vous verrez le dossier `bibliotheque` qui comprend 6 sous-dossiers et 2 fichiers. Jetons un oeil à chacun d'eux.

* **archetypes** : [Archetypes][archetypes] vous permet de pré-configurer le front-matter pour les fichiers de contenu dans Hugo pour un meilleur échafaudage du contenu en utilisant la commande `hugo new`. 
* **config.toml** : Hugo utilise `.toml`pour son propre format de configuration. mais il accepte aussi bien les formats `.yml` ou `.json`. Les réglages de configuration mentionnés dans le fichier `config.toml`s'appliquent à l'ensemble du site web et comprennent des variables globales importantes telles que la `baseURL` et le `title` de votre site web. (Voir [configuration](configurer-hugo.md))
* **content** : Ce dossier unique abrite tous les contenus de votre site web. Chaque sous-répertoire dans content s'appelle une section. Si votre site web dispose de sections pour les articles, événements et tutoriels, vous pourriez créer `content/posts`, `content/events` et `content/tutoriels`.
* **data** : Ce dossier est utilisé pour stocker les fichiers de données en séries (YAML, JSON, ou TOML) qui peuvent être utilisés dans les [data templates](https://gohugo.io/templates/data-templates/) et votre [menu de site web](https://gohugo.io/content-management/menus/).
* **layouts** : C'est le carrefour pour tous vos [modèles](https://gohugo.io/templates/introduction/), incluant les [modèles de listes et sections](https://gohugo.io/templates/lists/) et [shortcodes](https://gohugo.io/templates/shortcode-templates/).
* **static** : Ce dossier accueille tout le contenu statique ; par exemple les images, JavaScript et CSS. Tout ce qui est dans `/static` est copié tel quel vers votre site web fini.
* **themes** : C'est l'endroit où vous stockerez les thèmes Hugo. Vous pouvez voir une galrie de tous les thèmes sur [http://themes.gohugo.io](https://themes.gohugo.io)

## Étape 3. Ajoutez du Contenu

Ajoutons maintenant un article à notre   `bibliotheque`. Nous utiliserons la commande `hugo new` pour ajouter un article. Ce premier post sera sur le livre [Good To Great][6]. **Assurez-vous de bien être dans le dossier `bibliotheque`.** Et lancez la commande : 


    $ hugo new post/good-to-great.md
    
    
Vous devriez voir s'afficher ce qui suit : 

    /Users/votrenomutilisateur/bibliotheque/content/post/good-to-great.md created

La commande au-dessus crée un nouveau dossier `post`  à l'intérieur du dossier `content` et crée `content/post/good-to-great.md`. Le répertoire pour votre projet Hugo ressemblera maintenant à ce qui suit : 
    
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
    


Ouvrez `good-to-great.md` dans votre éditeur de texte préféré : 


    +++
    title: "Good To Great"
    date: 2017-07-01T14:31:19+02:00
    draft: true
    +++


Le contenu encadré entre les signes `+++` est le front matter TOML pour le contenu. Le front matter vous permet de définir des méta-données embarquées qui voyage avec le fichier de contenu. Parce que nous n'avons pas configuré quelque archetype pour notre projet, Hugo a utilisé propriétés de configuration natives et présentées au-dessous :  

* **title** spécifie le titre du billet.
* **date** spécifie la date et l'horaire à laquelle le billet a été créé.
* **draft** quant il est réglé sur `true`, dit à Hugo que ce post n'est pas prêt pour la publication.

Ajoutons une petite critique pour le livre **Good to Great** :     

    +++
    title: "Good To Great"
    date: 2017-07-01T14:31:19+02:00
    draft: true
    +++


    
    J'ai lu **Good to Great en janvier 2016**. Une analyse merveilleuse décrivant avec acuité comment les grandes sociétés enchantent le monde.
    

## Étape 4. Servez le contenu

Hugo a un serveur intégré qui peut servir le contenu de votre site web afin que vous puissiez le prévisualiser et développer. Pour servir le contenu, lancez la commande suivante à l'intérieur de votre répertoire `bibliotheque` :

    $ hugo server
    
Vous devriez voir quelque chose de similaire à ce qui suit : 

    Started building sites ...
    Built site for language en:
    0 of 1 draft rendered
    0 future content
    0 expired content
    0 regular pages created
    6 other pages created
    0 non-page files copied
    0 paginator pages created
    0 tags created
    0 categories created
    total in 14 ms
    Watching for changes in /Users/xtof
    Sites/Tuto-Quickstart-Hugo/bibliotheque
    {data,content,layouts,static}
    Serving pages from memory
    Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
    Press Ctrl+C to stop

Cette commande lancera le serveur sur le port `1313`. Vous pourrez regarder votre blog à l'adresse <http://localhost:1313/>. Cependant, si vous allez sur le lien, vous ne verrez rien ! Deux raisons à cela : 

1. Comme vous pouvez le voir dans la sortie de commande `hugo server`, Hugo n'a pas produit le draft. Hugo ne produira les drafts (ébauches) que si vous passez le flag `buildDrafts` sur la commande `hugo server`.
2. Nous n'avons pas spécifié comment le contenu Markdown devrait être produit. Nous devons spécifier un thème à utiliser par Hugo. Nous ferons ça à l'étape suivante.

Pour produire les drafts (ébauches), relancez le serveur avec la commande ci-dessous : 
    
    `$ hugo server --buildDrafts

Vous devriez voir quelque chose de similaire à ce qui suit : 
    
    Started building sites ...
    Built site for language en:
    1 of 1 draft rendered
    0 future content
    0 expired content
    1 regular pages created
    8 other pages created
    0 non-page files copied
    0 paginator pages created
    0 tags created
    0 categories created
    total in 6 ms
    Watching for changes in /Users/xtof/Sites/Tuto-Quickstart-Hugo/bibliotheque/{data,content,layouts,static}
    Serving pages from memory
    Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
    Press Ctrl+C to stop

Bien, maintenant nous avons notre page unique "build", mais noue ne voyons rien dans le navigateur  à l'adresse <http://localhost:1313/>. Ceci n'était fait que pour démontrer l'utilité du flag `--buildDrafts`.

## Étape 5. Ajoutez un thème

Les [thèmes](https://gohugo.io/themes/) fournissent à Hugo la mise en page et les modèles pour produire votre site Web. Vous pouvez voir la sélection complète de thèmes open source sur <https://themes.gohugo.io/>.

> **Hugo n'est toujours pas livré à ce jour avec un thème par défaut, permettant ainsi à l'utilisateur de choisir le thème qui conviendra le mieux à son projet.**

Les thèmes doivent être ajoutés dans le dossier `themes`, l'un des dossiers échafaudés avec la commande `hugo new site`que nous avons utilisée pour démarrer notre projet Hugo. Pour installer nos thèmes, modifions tout d'abord à l'intérieur du répertoire `themes` 
    
    $ cd themes

Vous pouvez cloner un ou plusieurs thèmes à l'intérieur de votre dossier `themes`. Nous utiliserons ici le [thème `robust`](https://github.com/dim0627/hugo_theme_robust), mais avec un point d'arrêt (dans son historique) qui fonctionne pour ce guide de démarrage rapide.
  

    git clone https://github.com/dim0627/hugo_theme_robust.git && cd hugo_theme_robust && git checkout 3baae29 && cd ../..

Maintenant redémarrons le serveur Hugo mais avec l'ajout du flag `--theme` pour Robust : 
    
    
    $ hugo server --theme=hugo_theme_robust --buildDrafts
    
Vous devriez voir un output de console similaire à ce qui suit : 

    Built site for language en:
    1 of 1 draft rendered
    0 future content
    0 expired content
    1 regular pages created
    8 other pages created
    0 non-page files copied
    2 paginator pages created
    0 tags created
    0 categories created
    total in 8 ms
    Watching for changes in /Users/xtof/Sites/Tuto-Quickstart-Hugo/bibliotheque/{data,content,layouts,static,themes}
    Serving pages from memory
    Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
    Press Ctrl+C to stop    

> _Note : Si Hugo ne trouve pas le thème spécifié dans le dossier `themes`, il lancera une exception comme affiché en-dessous._

>     FATAL: 2016/02/14 Unable to find theme Directory: /Users/xtof/bibliotheque/themes/robust

Pour voir votre site web, rendez-vous maintenant sur <http://localhost:1313/>. Vous verrez ce qui s'affiche ci-dessous.

![](https://d33wubrfki0l68.cloudfront.net/e988e7a93df69093c8c0dda7c05098536b8462e8/88604/images/quickstart/bookshelf-robust-theme.png)

Similaire à ce que nous avons observé lors de l'échafaudage pour notre nouveau site web Hugo, jetons un oeil à ce que comprend un thème Hugo typique. Ce qui suit n'est qu'une sélection de ce que vous verriez si vous listiez les contenus du répertoire du thème Robust. Il y a aussi quelques-uns des fichiers par défaut créés par Hugo v0.23. (Voir [Créer un Thème](https://gohugo.io/themes/creating/))
    
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

* **theme.toml** est le fichier de configuration du thème qui vous donne l'information sur le thème comme le nom et la description du thème, les détails de l'auteur, la licence du thème, la version minimum d'Hugo qui sera par défaut votre version d'Hugo localement installée.
* **layouts** contient différentes vues (cad. templates) pour différents types de contenus. Dans ce guide de démarrage,  nous voyons que chaque type de contenu a un fichier `single.html` et un fichier  `list.html`. `single.html` s'utilise pour produire un morceau unique de contenu. `list.html` s'utilise pour visualiser `*.md*` dans la section posts. Penez à `list.html` comme `exemple.com/posts` et `single.html` comme `exemple.com/posts/mon-post-unique/`.
* **static** a le même objectif que celui du `static`dans notre échafaudage original. Ce dossier  stocke tous les actifs statiques utilisés par le thème et il est copié tel quel au moment du *build*.

## Étape 6. Utilisez plusieurs thèmes

Vous pouvez facilement tester différentes configurations en alternant entre différents thèmes. dans Hugo. Supposons que nous voulions essayer le [thème `bleak`.](http://themes.gohugo.io/bleak/) Tuez le serveur Hugo si vous êtes encore en train de le faire fonctionner à la ligne de commande. 

À partir de la racine de votre projet, vous pouvez utiliser cette commande à une ligne à changer à l'intérieur de `themes`, clonez Bleak et revenez à la racine de votre projet. 

    cd themes && git clone https://github.com/Zenithar/hugo-theme-bleak.git && cd ..


Ou en détails à la ligne de commande :
Replacez-vous dans le dossier `themes`

    cd themes
    
Et clonez le thème `bleak` :

    $ git clone https://github.com/Zenithar/hugo-theme-bleak.git
    

Redémarrez le serveur en utilisant le thème `hugo-theme-bleak` comme affiché ci-dessous 
    
    $ cd ..
    $ hugo server --theme=hugo-theme-bleak --buildDrafts
    

... Désormais, notre site web utilise le thème `bleak` sur [http://localhost:1313](http://localhost:1313) et s'affiche différemment comme ci-dessous 

![Bibliothèque avec le thème Bleak](https://monosnap.com/file/rSwnbQN1sEzIPE450E3KQ9oOH4opHl.png)

## Étape 7. Mise à jourde votre configuration

Maintenant, arrêtez si besoin (Ctrl + C) pour redémarrer le serveur avec le thème `robust`, car nous allons l'utiliser pour ce guide de démarrage rapide : 
        
    $ hugo server --theme=hugo_theme_robust --buildDrafts
    
### Mise à jour de `config.toml`

Notre site web utilise actuellement les valeurs stupides spécifiées dans le fichier de configuration `bibliotheque/config.toml`, qui a été auto-généré avec `hugo new site bibliotheque`. Mettons à jour la configuration.
        
    baseURL = "http://exemple.org/"
    languageCode = "fr-fr"
    title = "Critiques de Livres par Shekhar Gulati"
    
    [Params]
      Author = "Shekhar Gulati"
    
### Regardez votre site se recharger instantanément 

Hugo supporte nativement le rechargement en live. Ce qui veut dire que Hugo reconstruira et rechargera votre site à chaque fois que vous sauvegarderez une modification d'un contenu, template, asset statique et même votre fichier de configuration. Vous devriez voir quelque chose de similaire à l'impression-écran qui suit sur <http://localhost:1313> une fois que vous sauvegarderez les modifications ci-dessus dans votre fichier `config.toml` : 

![Fichier config.toml mis à jour. (titre du site et nom de l'auteur)](https://monosnap.com/file/UbJoG3jvblTgmwRk1fO7Ymc8dLIg7l.png)

Outre la visualisation, vous retrouverez la modification dans la console. Dès que vous avez modifié le fichier de configuration, Hugo a appliqué ces modifications aux pages concernées et reconstruit le site :     
    
    Config file changed: /Users/votrenomutilisateur/bibliotheque/config.toml
    Started building sites ...
    Built site for language en:
    1 of 1 draft rendered
    0 future content
    0 expired content
    1 regular pages created
    8 other pages created
    0 non-page files copied
    2 paginator pages created
    0 tags created
    0 categories created
    total in 24 ms    

## Étape 8. Personnalisez le thème robust

Le thème `robust` est un bon départ pour notre bibliothèque en ligne mais nous voulons le personnaliser afin de le rapprocher de nos besoins pour une bibliothèque. Hugo [facilite la personnalisation des thèmes. Vous pouvez aussi créer vos propres thèmes](https://gohugo.io/themes/). Pour ce guide nous nous concentrerons sur la personnalisation.

La première modification à produire, c'est d'utiliser une image par défaut différente de celle utilisée dans le thème. L'image par défaut du thème utilisée à la fois dans le fichier `list.html`et `single.html` se trouve à l'intérieur de `themes/hugo_theme_robust/static/images/default.jpg`. Nous pouvons facilement l'annuler en créant une structure de répertoire simple dans le répertoire `static` du dossier.

Créez un dossier `images` dans le répertoire `bibliotheque/static` et copiez dedans une image avec le nom `default.jpg`. Nous utiliserons par défaut l'image affichée en dessous.

![image `default.jpg` à copier dans votre dossier `bibliotheque/static/images`][11]

Hugo synchronisera les modifications et rechargera le site web pour utiliser cette nouvelle image 

![Nouvelle image par défaut](https://monosnap.com/file/VsZKPzYi4vydK1787jnuwRBTexV7yE.png)

Maintenant, nous devons modifier le layout de la page index afin que seules les images soient affichées au lieu du texte. Le fichier `themes/hugo-theme_robust/layouts/index.html` fait référence au partiel `li` qui produit la vue en liste ci-dessous.    

```
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

    cd layouts && mkdir _default && cd _default && touch li.html && cd ../..

Copiez le contenu affiché en dessous dans le nouveau fichier `li.html`. Si vous comparez ça avec le `li.html`livré avec le thème Robust, vous remarquerez que nous avons enlevé les détails du livre, afin que seule l'image s'affiche.


```
<article class="li">
  <a href="{{ .Permalink }}" class="clearfix">
    <div class="image" style="background-image: url({{ $.Site.BaseURL }}images/{{ with .Params.image }}{{ . }}{{ else }}default.jpg{{ end }});"></div>
  </a>
</article>
```    

Maintenant, le site web devrait ressembler à ce qui s'affiche en-dessous 

![... image sans détails.](https://monosnap.com/file/GgqLdZrcGQu87neTAWQQGN4VBxLjOl.png)

Ensuite, nous voulons retirer l'information présente en pied de page concernant le thème. Pour faire ainsi, créez un nouveau dossier sur `bibliotheque/layouts/partials`. Celui-ci détiendra notre nouveau fichier appelé `default_foot.html`

Ceci est un nouveau [template partial](https://gohugo.io/templates/partials/). Si vous êtes encore à la racine du répertoire de votre projet, vous pouvez utilisez la commande-en-une-linge qui suit pour créer le partial avant de de revenir à la racine du projet : 


    cd layouts && mkdir partials && cd partials && touch default_foot.html && cd ../..
    

Ajoutez maintenant ce qui suit à notre nouveau template partial `default_foot.html` : 

    
    <footer class="site">
      <p>{{ with .Site.Copyright | safeHTML }}{{ . }}{{ else }}&copy; {{ $.Site.LastChange.Year }} {{ if isset $.Site.Params "Author" }}{{ $.Site.Params.Author }}{{ else }}{{ .Site.Title }}{{ end }}{{ end }}</p>
      <p>Motorisé par <a href="http://gohugo.io" target="_blank">Hugo</a>,</p>
    </footer>
    

A ce stade nous utilisons l'image par défaut mais nous aimerions utiliser l'image du livre que nous pourrions rattacher au livre. Chaque critique de livre définira un réglage de configuration dans son front matter. Mettez à jour le contenu et le front matter de `good-to-great.md` comme affiché ci-dessous :  

```
+++
date = "2017-02-19T21:09:05-06:00"
draft = true
title = "Good to Great Book Review"
image = "good-to-great.jpg"
+++

I read **Good to Great in January 2016**. An awesome read sharing detailed analysis on how good companies became great. Although this book is about how companies became great but we could apply a lot of the learnings on ourselves. Concepts like level 5 leader, hedgehog concept, the stockdale paradox are equally applicable to individuals.

```


Piquez quelque part (légal SVP) une image, appelez-la `good-to-great.jpg`, et placez-la dans le dossier `bibliotheque/static/images`.

Après avoir ajouté quelques autres livres à notre étagère de bibliothèque, voic à quoi ressemble l'ensemble. Quelques livres que j'ai lus durant l'année. 

![image à refaire en français](https://d33wubrfki0l68.cloudfront.net/e03165bd6db7ba50f0bb728074b50809562fb050/ae4e7/img/quickstart/bookshelf.png)


Dernier raffinage... Nous devons aussi enlever la barre latérale à droite. Copiez le fichier `index.html` dans le dossier `layouts` du thème vers le dossier `bibliotheque/layouts`. Retirez la section en rapport avec la barre latérale du HTML :

    <div class="col-sm-3">
      {{ partial "sidebar.html" . }}
    </div>



## Étape 9. Rendez les posts publics

À ce stade, tous les posts que nous avons écrits sont en statut draft, c'est à dire `draft=true` (ébauche). Afin de faire qu'un draft soit public, vous pouvez soit lancer une commande ou modifier manuellement le statut draft dans le post en `false`. Hugo fournit une commande pratique appelée `undraft`pour faire ça :

    $ hugo undraft content/post/good-to-great.md

Si nous vérifions le front matter de `good-to-great.md` après avoir lancé cette commande, nous remarquons que Hugo a écrit la modification du statut draft au fichier : 

    +++
    date = "2017-02-19T22:42:53-06:00"
    draft = false
    title = "Good to Great Book Review"
    image = "good-to-great.jpg"
    +++
    

Maintenant, nous pouvons lancer le serveur sans l'option `buildDrafts`.

    $ hugo server --theme=hugo_theme_robust

## Étape 10. Construire votre site Web 

Pour générer la source du site web Hugo, qui peut être déployé vers GitHub Pages. nous avons besoin de modifier la ligne `baseURL` dans notre configuration comme suit :

    baseURL = "https://<votre nomutilisateur GitHub>.github.io/bibliotheque/"

Puis lancez la commande suivante à partir du répertoire racine de votre projet Hugo : 

    $ hugo --theme=hugo_theme_robust
    
    Started building sites ...
    Built site for language en:
    0 draft content
    0 future content
    0 expired content
    1 regular pages created
    8 other pages created
    0 non-page files copied
    2 paginator pages created
    0 tags created
    0 categories created
    total in 10 ms


Après avoir lancé la commande `hugo`, un répertoire  `bibliotheque/public` est créé contenant la source du site web généré.

P.S. En passant, (si vous avez essayé), le site web n'est pas accessible proprement via le protocole `file:///`.


## Étape 11. Et après ?[ ](https://gohugo.io/getting-started/quick-start/#step-11-what-next)

**Bravo !** Votre nouveau répertoire public `bibliothèque`/ est un site web Hugo entièrement généré et déployable. Du fait que tous vos fichiers sont _statiques_, vous avez d'innombrables options d'hébergement, et votre nouvelle structure de répertoire et votre format de contenu simple vont améliorer grandement votre site web.

Voic ce que vous pourriez regardez ensuite : 

  1. [Voir les options d'hébergement et de déploiement](https://gohugo.io/hosting-and-deployment/) pour partager votre nouveau site web Hugo avec le monde.
  2. [Apprenez en plus sur le templating puissant d'Hugo](https://gohugo.io/templates/introduction/) pour personnaliser votre site web Hugo à vos besoins spécifiques et pour le faire grandir.
  3. [Visitez le Forum de discussion Hugo](https://discourse.gohugo.io) pour poser des questions, répondre aux questions, et devenir un membre actif de la communauté Hugo.


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

[archetypes][/gestion-contenu/archetypes/]
[2]: https://github.com/gohugoio/hugo/releases
[3]: https://git-for-windows.github.io/
[4]: https://gohugo.io/content/archetypes/
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

