---
title: Organisation du Contenu
linktitle: Organisation
description: Hugo suppose que la même structure qui fonctionne pour organiser votre contenu source est utilisée pour organiser le site rendu.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
categories: [fondamentaux, gestion de contenu,fundamentals]
#tags: [sections,contenu, organisation]
menu:
  docs:
    parent: "Gestion de Contenu"
    weight: 10
weight: 10	#rem
draft: false
aliases: []
toc: true
---

{{% note %}}
Cette section n'est pas mise à jour avec le support de nouvelles sections imbriquées dans Hugo 0.24, voir https://github.com/gohugoio/hugoDocs/issues/36
{{% /note %}}
{{% todo %}}
See above
{{% /todo %}}

## Organisation du Contenu Source

Dans Hugo, votre contenu doit être organisé d'une manière qui reflète le site Web rendu.

Alors que Hugo prend en charge le contenu imbriqué à n'importe quel niveau, les niveaux supérieurs (c'est-à-dire `content/<DOSSIERS>`) sont spéciaux dans Hugo et sont considérés comme le contenu [sections][]. Sans aucune configuration supplémentaire, les éléments suivants vont simplement fonctionner :

```
.
└── content
    └── about
    |   └── _index.md  // <- http://votresite.com/about/
    ├── post
    |   ├── firstpost.md   // <- http://votresite.com/post/premierpost/
    |   ├── happy
    |   |   └── ness.md  // <- http://votresite.com/post/happy/ness/
    |   └── secondpost.md  // <- http://votresite.com/post/secondpost/
    └── citation
        ├── premier.md       // <- http://votresite.com/quote/first/
        └── second.md      // <- http://votresite.com/quote/second/
```

## Répartition de Chemins dans Hugo

Ce qui suit illustre les relations entre votre organisation de contenu et la structure d'URL de sortie pour votre site Web Hugo lorsqu'il est rendu. Ces exemples supposent que vous utilisez [l'utilisation de belles URL][pretty], ce qui est le comportement par défaut de Hugo. Les exemples prennent également une valeur-clé de `baseurl = "http://votresite.com"` dans le  [fichier de configuration de votre site][config].

### Pages Index : `_index.md`

`_index.md` a un rôle spécial dans Hugo. Il vous permet d'ajouter le front matter et le contenu à vos [modèles de liste][listes] à partir de v0.18. Ces modèles incluent ceux pour les  [modèles de section][section templates], les [modèles de taxonomie][taxononomy templates], les [modèles de termes de taxonomie][taxonomy terms templates], et votre [modèle de page d'accueil][homepage template]. Dans vos modèles, vous pouvez saisir des informations de `_index.md` à l'aide de la fonction [`.Site.GetPage`][getpage].

Vous pouvez conserver un `_index.md` pour votre page d'accueil et un dans chacune de vos sections de contenu, taxonomies et termes de taxonomie. Ce qui suit montre le placement typique d'un `_index.md` qui contiendrait du contenu et un front matter pour une page de liste des sections `posts`  sur un site web Hugo :


```bash
.         url
.       ⊢--^-⊣
.        path    slug
.       ⊢--^-⊣⊢---^---⊣
.           filepath
.       ⊢------^------⊣
content/posts/_index.md
```

Lors de la compilation, cela générera la destination suivante avec les valeurs associées :

```bash

                     url ("/posts/")
                    ⊢-^-⊣
       baseurl      section ("posts")
⊢--------^---------⊣⊢-^-⊣
        permalink
⊢----------^-------------⊣
http://votresite.com/posts/index.html
```

### Pages Uniques dans les Sections

Les fichiers de contenu unique dans chacune de vos sections vont être rendus comme [modèles de page unique][singles]. Voici un exemple d'un `post`  unique dans `posts` :

```bash
                   path ("posts/mon-premier-hugo-post.md")
.       ⊢-----------^------------⊣
.      section        slug
.       ⊢-^-⊣⊢--------^----------⊣
content/posts/mon-premier-hugo-post.md
```

Au moment où Hugo construit votre site, le contenu sera envoyé à la destination suivante :

```bash

                               url ("/posts/mon-premier-hugo-post/")
                   ⊢------------^----------⊣
       baseurl     section     slug
⊢--------^--------⊣⊢-^--⊣⊢-------^---------⊣
                 permalink
⊢--------------------^---------------------⊣
http://votresite.com/posts/mon-premier-post-hugovotresite/index.html
```

### Section avec Répertoires Imbriqués

Pour continuer l'exemple, les éléments suivants montrent les chemins de destination d'un fichier situé dans `content/events/chicago/lollapalooza.md` dans le même site :


```bash
                    section
                    ⊢--^--⊣
                               url
                    ⊢-------------^------------⊣

      baseURL             path        slug
⊢--------^--------⊣ ⊢------^-----⊣⊢----^------⊣
                  permalink
⊢----------------------^-----------------------⊣
http://votresite.com/events/chicago/lollapalooza/
```

{{% note %}}
À partir de v0.20, Hugo ne reconnaît pas les sections imbriquées. Bien que vous puissiez nicher autant de *répertoires* de contenu que vous le souhaitez, tout répertoire enfant d'une section sera toujours considéré comme de la même section que celle de ses parents. Par conséquent, dans l'exemple ci-dessus, `{{.Section}}` pour `lollapalooza.md` est `events` et *non* `chicago`. Voir le [problème connexe sur GitHub](https://github.com/gohugoio/hugo/issues/465).
{{% /note %}}

## Chemins expliqués

Les concepts suivants donneront une meilleure idée de la relation entre l'organisation de votre projet et les comportements par défaut de Hugo lors de la création du site Web de sortie.

### `section`

Un type de contenu par défaut est déterminé par un élément de section du contenu. `section` est déterminé par l'emplacement dans le répertoire `content` du projet. `section` *ne peut pas* être spécifié ou remplacé dans le front matter.

### `slug`

Le `slug` d'un contenu est soit `nom.extension` ou `nom/`. La valeur de `slug` est déterminée par 

* Le nom du fichier de contenu (par exemple, `lollapalooza.md`) OU
* le remplacement du front matter

### `path`

Un `path` de contenu est déterminé par le chemin de section vers le fichier. Le `path` du fichier 

* est basé sur le chemin vers l'endroit du contenu ET
* ne comprend pas le slug

### `url`

L'`url` est l'URL relative du contenu. L'`url`

* est basé sur l'emplacement du contenu dans la structure de répertoire OU
* est défini dans le front matter et *remplace tout ce qui précède*

## Annuler les Chemins de Destination via le Front Matter

Hugo croit que vous organisez votre contenu avec un but. La même structure qui fonctionne pour organiser votre contenu source est utilisée pour organiser le site rendu. Comme indiqué ci-dessus, l'organisation du contenu source sera reflétée dans la destination.

Il arrive que vous ayez besoin de plus de contrôle sur votre contenu. Dans ces cas, il existe des champs qui peuvent être spécifiés dans le front matter pour déterminer la destination d'un contenu spécifique.

Les éléments suivants sont définis dans cet ordre pour une raison spécifique : les éléments expliqués plus bas dans la liste annuleront les éléments précédents, et tous ces éléments ne peuvent être définis dans le front matter :

### `nomfichier`

Ce n'est pas dans le front matter mais c'est le nom réel du fichier moins l'extension. Ce sera le nom du fichier dans la destination (par exemple, `content/posts/my-post.md` devient `votresite.com/posts/my-post/`).

### `slug`

Lorsqu'il est défini dans le front, le `slug` peut prendre la place du nom de fichier pour la destination.

{{% code file="content/posts/old-post.md" %}}
```yaml
---
title: Nouveau Post
slug: "nouveau-post"
---
```
{{% /code %}}

Cela rendra la destination suivante selon le comportement par défaut de Hugo :

```
votresite.com/posts/nouveau-post/
```

### `section`

`section` est déterminé par l'emplacement d'un contenu sur le disque et *ne peut pas* être spécifié dans le front matter. Voir [sections][] pour plus d'informations.

### `type`

Un `type` d'un contenu est également déterminé par son emplacement sur le disque mais, contrairement à `section`, il *peut* être spécifié dans le front matter. Voir [types][]. Cela peut être particulièrement utile lorsque vous souhaitez qu'un contenu soit rendu à l'aide d'un layout différent. Dans l'exemple suivant, vous pouvez créer une mise en page sur  `layouts/new/monlayout.html` que Hugo utilisera pour reproduire ce contenu, même au milieu de plusieurs autres publications.

{{% code file="content/posts/mon-post.md" %}}
```yaml
---
title: Mon Post
type: new
layout: monlayout
---
```
{{% /code %}}
<!-- Voir https://discourse.gohugo.io/t/path-not-works/6387 -->

### `path`

Le `path` peut être fourni dans le front matter. Ceci remplacera le chemin réel du fichier sur le disque. La destination créera la destination avec le même chemin, y compris la section.

### `url`

Une URL complète peut être fournie. Cela annulera tout ce qui précède en ce qui concerne la destination finale. Ce doit être le chemin de la baseURL (commençant par `/`). `url` sera utilisé exactement comme fourni dans le front matter et ignorera le paramètre `--uglyURLs` réglé dans la configuration de votre site :

{{% code file="content/posts/old-url.md" %}}
```yaml
---
title: Vieil URL
url: /blog/nouvel-url/
---
```
{{% /code %}}

En supposant que votre `baseURL` est [configurée][config] sur `https://votresite.com`, l'ajout de `url` dans le front matter rendra "vieil-url.md` à la destination suivante :

```
https://votresite.com/blog/nouvel-url/
```

Vous pouvez voir plus d'informations sur la façon de contrôler les chemins de sortie dans la [Gestion des URL][urls].

[config]: /demarrage/configuration/
[formats]: /gestion-contenu/formats/
[front matter]: /content-management/front-matter/
[getpage]: /functions/getpage/
[homepage template]: /templates/homepage/
[homepage]: /templates/homepage/
[lists]: /templates/lists/
[pretty]: /gestion-contenu/urls/#pretty-urls
[section templates]: /templates/section-templates/
[sections]: /gestion-contenu/sections/
[singles]: /templates/single-page-templates/
[taxonomy templates]: /templates/taxonomy-templates/
[taxonomy terms templates]: /templates/taxonomy-templates/
[types]: /gestion-contenu/types/
[urls]: /gestion-contenu/urls/
