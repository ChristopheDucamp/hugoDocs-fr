---
title: Ordre de Recherche Hugo
linktitle: Ordre de Recherche de Modèle
description: L'ordre de recherche est une liste prioritaire utilisée par Hugo car elle traverse vos fichiers à la recherche du fichier approprié correspondant pour produire votre contenu.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [modèles,fondamentaux]
#tags: [lookup]
menu:
  docs:
    parent: "Templates"
    weight: 15
  quicklinks:
weight: 15
sections_weight: 15
draft: false
aliases: [templates/lookup-order,/templates/lookup/]
toc: true
---

Avant de créer vos modèles, il est important de savoir comment Hugo recherche des fichiers dans la [structure de répertoire][structure-dossier] de votre projet.

Hugo utilise une liste prioritaire appelée **ordre de recherche** car elle traverse votre dossier `layouts` dans votre projet Hugo *en cherchant* le modèle approprié pour rendre votre contenu.

L'ordre de recherche de modèle est une cascade inversée : si le modèle A n'est pas présent ou spécifié, Hugo se tournera vers le modèle B. Si le modèle B n'est pas présent ou spécifié, Hugo recherchera le modèle C ... et ainsi de suite jusqu'à ce qu'il atteigne le dossier `_default/` pour votre projet ou votre thème. À bien des égards, l'ordre de recherche est similaire au concept de programmation d'une [instruction de commutation sans décalage][switch].

La puissance de l'ordre de recherche est de vous permettre de concevoir des mises en page spécifiques et de garder votre modélisation [DRY][].

{{% note %}}
La plupart des sites web Hugo n'auront besoin que de  fichiers de modèles par défaut à la fin de l'ordre de recherche (à savoir `_default/*.html`).
{{% /note %}}

## Ordres de Recherche

L'odre de recherche respectif pour chacun des modèles d'Hugo a été défini dans la documentation d'Hugo :

* [Modèle de Page d'Accueil][home]
* [Modèles Base][base]
* [Modèles de Page Section][sectionlookup]
* [Modèles de Liste de Taxonomie][taxonomylookup]
* [Modèles de Termes de Taxonomie][termslookup]
* [Modèles de Page Unique][singlelookup]
* [Modèles RSS][rsslookup]
* [Modèles Shortcode][sclookup]

## Exemples de Recherche de Modèle

L'ordre de recherche est mieux illustré par des exemples. Ce qui suit vous montre le processus utilisé par Hugo pour trouver le modèle approprié pour rendre vos [modèles de page unique][single page templates], mais le concept est vrai pour tous les modèles de Hugo.

1. Le projet utilise le thème `montheme` (spécifié dans la [configuration][config] du projet).
2. Les layouts et les dossiers de contenu du projet sont les suivants :

```bash
.
├── content
│   ├── events
│   │   ├── _index.md
│   │   └── my-first-event.md
│   └── posts
│       ├── my-first-post.md
│       └── my-second-post.md
├── layouts
│   ├── _default
│   │   └── single.html
│   ├── posts
│   │   └── single.html
│   └── reviews
│       └── reviewarticle.html
└── themes
    └── montheme
        └── layouts
            ├── _default
            │   ├── list.html
            │   └── single.html
            └── posts
                ├── list.html
                └── single.html
```


Maintenant nous pouvons regarder le front matter pour les trois fichiers de contenu (à savoir `.md`).

{{% note  %}}
Seuls trois des quatre fichiers markdown dans le projet ci-dessus sont soumis à l'ordre de recherche de page *unique*. `_index.md` est un type `kind` spécifique à Hugo. Alors que `my-first-post.md`, `my-second-post.md` et `my-first-event.md` sont tous les trois de type `page`, tous les fichiers `_index.md` dans un projet Hugo sont utilisés pour ajouter du contenu et un front matter pour des [listes de pages](/templates/lists/). Dans cet exemple, `events/_index.md` produira en fonction de son [modèle de section](/templates/section-templates/) et de l'ordre de recherche respectif.
{{% /note %}}

### Exemple : `mon-premier-post.md`

{{% code file="content/posts/mon-premier-post.md" copy="false" %}}
```yaml
---
title: Mon Premier Post
date: 2017-02-19
description: Ceci est mon premier post.
---
```
{{% /code %}}

Au moment de construire votre site, Hugo passera l'ordre de recherche jusqu'à ce qu'il trouve ce dont il a besoin pour `my-first-post.md` :

1. ~~`/layouts/UNSPECIFIED/UNSPECIFIED.html`~~
2. ~~`/layouts/posts/UNSPECIFIED.html`~~
3. ~~`/layouts/UNSPECIFIED/single.html`~~
4. <span class="yes">`/layouts/posts/single.html`</span>
  <br><span class="break">BREAK</span>
5. <span class="na">`/layouts/_default/single.html`</span>
6. <span class="na">`/themes/<THEME>/layouts/UNSPECIFIED/UNSPECIFIED.html`</span>
7. <span class="na">`/themes/<THEME>/layouts/posts/UNSPECIFIED.html`</span>
8. <span class="na">`/themes/<THEME>/layouts/UNSPECIFIED/single.html`</span>
9. <span class="na">`/themes/<THEME>/layouts/posts/single.html`</span>
10. <span class="na">`/themes/<THEME>/layouts/_default/single.html`</span>

Notez le terme `UNSPECIFIED` plutôt que `UNDEFINED`. Si vous n'indiquez pas à Hugo le type et le layout spécifiques, il fera des hypothèses basées sur des valeurs par défaut saines. `Mon-premier-post.md` ne spécifie pas un `type` de contenu dans son front matter. Par conséquent, Hugo suppose que le contenu `type` et `section` (c'est-à-dire `posts`, qui est défini par l'emplacement du fichier) sont un dans le même. ([Plus d'infos ici sur les sections][sections].)

`Mon-premier-post.md` ne spécifie pas non plus un `layout` dans son front matter. Par conséquent, Hugo suppose que `mon-premier-post.md`, qui est de type `page` et un *unique* élément de contenu, devrait par défaut être la prochaine occurrence d'un modèle `single.html` dans la recherche (#4).

### Exemple : `mon-second-post.md`

{{% code file="content/posts/mon-second-post.md" copy="false" %}}
```yaml
---
title: Mon Second Post
date: 2017-02-21
description: Ceci est mon second post.
type: review
layout: reviewarticle
---
```
{{% /code %}}

Voici le moyen avec lequel Hugo traverse l'odre de recherche de page-unique pour `my-second-post.md`:

1. <span class="yes">`/layouts/review/reviewarticle.html`</span>
  <br><span class="break">BREAK</span>
2. <span class="na">`/layouts/posts/reviewarticle.html`</span>
3. <span class="na">`/layouts/review/single.html`</span>
4. <span class="na">`/layouts/posts/single.html`</span>
5. <span class="na">`/layouts/_default/single.html`</span>
6. <span class="na">`/themes/<THEME>/layouts/review/reviewarticle.html`</span>
7. <span class="na">`/themes/<THEME>/layouts/posts/reviewarticle.html`</span>
8. <span class="na">`/themes/<THEME>/layouts/review/single.html`</span>
9. <span class="na">`/themes/<THEME>/layouts/posts/single.html`</span>
10. <span class="na">`/themes/<THEME>/layouts/_default/single.html`</span>

Le front matter dans `mon-second-post.md` spécifie le contenu `type` (c'est-à-dire `review`) ainsi que le `layout` (c'est-à-dire `reviewarticle`). Hugo trouve la mise en page dont il a besoin au niveau supérieur de la recherche (#1) et ne continue pas à rechercher dans les autres modèles.

{{% note "Type et pas de Types"%}}
Notez que le répertoire du modèle pour `mon-second-post.md` est `review` et non `reviews`. Ceci parce que *type est toujours singulier lorsqu'il est défini dans le front matter*.
{{% /note %}}


### Exemple : `my-first-event.md`

{{% code file="content/events/my-first-event.md" copy="false" %}}
```yaml
---
title: My First Event
date: 2018-07-06
description: Ceci est un évenement à venir..
---
```
{{% /code %}}

Voici la façon avec laquelle Hugo traverse l'ordre de recherche de page-unique pour `my-first-event.md`:

1. ~~`/layouts/UNSPECIFIED/UNSPECIFIED.html`~~
2. ~~`/layouts/events/UNSPECIFIED.html`~~
3. ~~`/layouts/UNSPECIFIED/single.html`~~
4. ~~`/layouts/events/single.html`~~
5. <span class="yes">`/layouts/_default/single.html`</span>
<br><span class="break">BREAK</span>
6. <span class="na">`/themes/<THEME>/layouts/UNSPECIFIED/UNSPECIFIED.html`</span>
7. <span class="na">`/themes/<THEME>/layouts/events/UNSPECIFIED.html`</span>
8. <span class="na">`/themes/<THEME>/layouts/UNSPECIFIED/single.html`</span>
9. <span class="na">`/themes/<THEME>/layouts/events/single.html`</span>
10. <span class="na">`/themes/<THEME>/layouts/_default/single.html`</span>


{{% note %}}
`my-first-event.md` est important car il démontre le rôle de l'ordre de recherche dans les thèmes de Hugo. Le répertoire de projet racine *et* le répertoire thèmes `mytheme` ont un fichier  sur `_default/single.html`. La compréhension de cet ordre vous permet de [personnaliser les thèmes Hugo](/themes/personnaliser/)  en créant des fichiers de modèles avec des noms identiques dans votre répertoire de projet qui se positionnent devant les fichiers de modèle de thème dans la recherche. Cela vous permet de personnaliser l'apparence de votre site Web tout en maintenant la compatibilité avec le thème en amont.
{{% /note %}}

[base]: /templates/base/#ordre-de-recherche-du-modèle-de-base
[config]: /demarrage/configuration/
[structure-dossier]: /demarrage/structure-dossier/
[DRY]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[home]: /templates/pageaccueil/#ordre-de-recherche-du-modèle-de-page-d-accueil

[rsslookup]: /templates/rss/#rss-template-lookup-order
[sclookup]: /templates/shortcode-templates/#shortcode-template-lookup-order
[sections]: /gestion-contenu/sections/
[sectionlookup]: /templates/section-templates/#section-template-lookup-order
[single page templates]: /templates/single-page-templates/
[singlelookup]: /templates/single-page-templates/#single-page-template-lookup-order
[switch]: https://en.wikipedia.org/wiki/Switch_statement#Fallthrough
[taxonomylookup]: /templates/taxonomy-templates/#taxonomy-list-template-lookup-order
[termslookup]: /templates/taxonomy-templates/#taxonomy-terms-template-lookup-order
