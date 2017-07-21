---
title: Gestion des URLs
linktitle: Gestion des URLs
description: Hugo prend en charge les permaliens, les alias, la canonisation et les options multiples pour gérer les URLs relatives par rapport aux URL absolues.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-20
#tags: [aliases,redirects,permalinks,urls]
categories: [content management, gestion de contenu]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 110
weight: 110	#rem
draft: false
aliases: [/extras/permalinks/,/extras/aliases/,/extras/urls/,/doc/redirects/,/doc/alias/,/doc/aliases/]
toc: true
---

## Permaliens

Le répertoire cible Hugo par défaut pour votre site Web construit est `public/`. Toutefois, vous pouvez modifier cette valeur en spécifiant un `publishDir` différent dans la  [configuration de votre site][config]. Les répertoires créés au moment de la construction pour une section reflètent la position du répertoire du contenu dans le dossier `content` et l'espace de noms correspondant à sa mise en page dans la hiérarchie `contentdir`.

L'option `permalinks` dans votre [configuration de site][config] vous permet d'ajuster les chemins de répertoires (c'est-à-dire les URL) en fonction de chaque section. Cela changera l'endroit où les fichiers sont écrits et changera l'emplacement "canonique" interne de la page, de sorte que les références de modèle vers `.RelPermalink` honoreront les ajustements effectués à la suite des mappages dans cette option.

{{% note "Dossiers par Défaut de Publication et Contenu" %}}
Ces exemples utilisent les valeurs par défaut pour `publishDir` et `contentDir` ; c'est-à-dire «publication» et «contenu», respectivement. Vous pouvez remplacer les valeurs par défaut dans le [fichier `config` de votre site](/start-started/configuration/).
{{% /note %}}

Par exemple, si l'une de vos [sections][] s'appelle `post` et que vous souhaitez ajuster le chemin canonique pour être hiérarchique en fonction de l'année, du mois et du titre de la publication, vous pouvez configurer respectivement les configurations suivantes dans YAML et TOML.

### Exemple YAML de Configuration des Permaliens

{{% code file="config.yml" copy="false" %}}
```yaml
permalinks:
  post: /:year/:month/:title/
```
{{% /code %}}

### Exemple TOML de Configuration des Permaliens

{{% code file="config.toml" copy="false" %}}
```toml
[permalinks]
  post = "/:year/:month/:title/"
```
{{% /code %}}

Seul le contenu sous `post/` aura la nouvelle structure d'URL. Par exemple, le fichier `content/post/entree-echantillon.md` avec  `date: 2017-02-27T19:20:00-05:00` dans son front matter sera rendu en `public/2017/02/entree-echantillon/index.html` à l'heure du build et par conséquent sera atteignable sur `http://votresite.com/2017/02/entree-echantillon/.

### Valeurs de la Configuration Permaliens

Voici une liste de valeurs pouvant être utilisées dans une définition de `permalink` dans le fichier `config` de votre site. Toutes les références au temps dépendent de la date du contenu.

`:year`
: l'année en 4 chiffres

`:month`
: le mois en 2 chiffres

`:monthname`
: le nom du mois

`:day`
: le jour en deux chiffres

`:weekday`
: le chiffre du jour de la semaine (Dimanche = 0)

`:weekdayname`
: le nom du jour de la semaine

`:yearday`
: le 1- à 3-chiffres du jour de l'année

`:section`
: la section du contenu

`:title`
: le titre du contenu

`:slug`
: le slug du contenu (ou le titre si aucun slug n'est fourni dans le front matter)

`:filename`
: le nom du fichier de contenu (sans extension)

## Alias

Pour les personnes qui migrent le contenu publié existant vers Hugo, il y a de bonnes chances que vous ayez besoin d'un mécanisme pour gérer la redirection des anciennes URL.

Heureusement, les redirections peuvent être traitées facilement avec les **alias ** dans Hugo.

### Exemple : Alias

Supposons que vous créez un nouveau contenu sur `content/posts/mon-super-billet-de-blog.md`. Le contenu est une révision de votre publication précédente sur `content/posts/mon-url-original.md`. Vous pouvez créer un champ `aliases` dans le front matter de  votre nouveau `mon-super-billet-de-blog.md`, où vous pouvez ajouter les chemins précédents. Les exemples suivants montrent comment le créer dans les front matter TOML et YAML, respectivement.

#### TOML Front Matter

{{% code file="content/posts/mon-super-post.md" copy="false" %}}
```toml
+++
aliases = [
    "/posts/mon-url-originale/",
    "/2010/01/01/url-meme-avant.html"
]
+++
```
{{% /code %}}

#### YAML Front Matter

{{% code file="content/posts/my-awesome-post.md" copy="false" %}}
```yaml
---
aliases:
    - /posts/mon-url-originale/
    - /2010/01/01/url-meme-avant.html
---
```
{{% /code %}}

Maintenant, lorsque vous visitez l'un des emplacements spécifiés dans les alias ---c'est-à-dire, *en supposant le même domaine du site*--- vous serez redirigé vers la page sur laquelle ils sont spécifiés. Par exemple, un visiteur sur `votresite.com/posts/mon-url-original/` sera immédiatement redirigé vers `votresite.com/posts/mon-super-billet-de-blog/`.

### Exemple : Aliases en Multilingue

Sur les [sites multilingues][multilingual], chaque traduction d'une publication peut avoir des alias uniques. Pour utiliser le même alias sur plusieurs langues, précédez-le avec le code de langue.

Dans `/posts/mon-nouveau-post.es.md`:

```yaml
---
aliases:
    - /es/posts/mon-post-original/
---
```

### Comment Fonctionnent les Alias Hugo

Lorsque les alias sont spécifiés, Hugo crée un répertoire correspondant à l'entrée d'alias. À l'intérieur du répertoire, Hugo crée un fichier `.html` spécifiant l'URL canonique pour la page et la nouvelle cible de redirection.

Par exemple, un fichier de contenu sur `posts/mon-url-souhaite.md` avec ce qui suit dans le front matter :

```yaml
---
title: Mon Nouveau Post
aliases: [/posts/ma-vieille-url/]
---
```

En supposant une `baseURL` de `votresite.com`, le contenu de l'alias généré automatiquement `.html` trouvé sur `https://votresite.com/posts/ma-vieille-url/` contiendra les éléments suivants :

```html
<!DOCTYPE html>
<html>
  <head>
    <title>http://votresite.com/posts/mon-url-souhaite</title>
    <link rel="canonical" href="http://votresite.com/posts/mon-url-souhaite"/>
    <meta name=\"robots\" content=\"noindex\">
    <meta http-equiv="content-type" content="text/html; charset=utf-8"/>
    <meta http-equiv="refresh" content="0; url=http://votresite.com/posts/mon-url-souhaite"/>
  </head>
</html>
```

La ligne `http-equiv="refresh"` est ce qui effectue la redirection, en 0 seconde dans ce cas. Si un utilisateur final de votre site Web va sur `https://votresite.com/posts/ma-vieille-url`, il sera automatiquement redirigé vers l'URL plus récente et correcte. L'ajout de `<meta name=\"robots\"content=\"noindex\">` permet aux robots des moteurs de recherche de savoir qu'ils ne doivent pas faire d'exploration et indexer votre nouvelle page d'alias.

### Personnaliser 

Vous pouvez personnaliser cette page d'alias en créant un modèle `alias.html` dans le dossier layouts de votre site (c.-à-d. `layouts/alias.html`). Dans ce cas, les données transmises au modèle sont : 

`Permalink`
: le lien vers la page étant aliasée

`Page`
: la data de la Page pour la page étant aliasée

### Comportements Importans des Alias

1. Hugo ne fait aucune hypothèse sur les alias. Ils ne changent pas en fonction du réglage de vos UglyURLs. Vous devez fournir des chemins absolus vers votre racine Web et le nom complet du fichier ou le répertoire.
2. Les alias sont rendus *avant* que tout contenu ne soit rendu et ils seront donc remplacés par tout contenu ayant le même emplacement.


## Pretty URLs

Le comportement par défaut de Hugo est de rendre votre contenu avec des URL "pretty" (jolies). Aucune configuration non standard du serveur n'est nécessaire pour que ces jolies URL fonctionnent.

Voici ce qui suit pour démontrer le concept : 


```bash
content/posts/_index.md
=> votresite.com/posts/index.html
content/posts/post-1.md
=> votresite.com/posts/post-1/
```

## Ugly URLs

Si vous aimeriez être souvent cité pour avoir des "URL laides" (par. ex., votresite.com/urls.html), définissez `uglyurls = true` ou `uglyurls: true` dans le `config.toml` ou le `config.yaml` de votre site, respectivement. Vous pouvez également utiliser `--uglyURLs=true` comme [marqueur à partir de la ligne de commande][usage] avec` hugo` ou `hugo server`..

Si vous souhaitez qu'un contenu spécifique ait une URL exacte, vous pouvez le spécifier dans le [front matter][] sous la clé `url`. Les exemples suivants sont des exemples du même répertoire de contenu et quelle sera la structure URL éventuelle lorsque Hugo s'exécute avec son comportement par défaut.

Voir [Organisation de contenu][contentorg] pour plus de détails sur les chemins d'accès.

```bash
.
└── content
    └── about
    |   └── _index.md  // <- http://yoursite.com/about/
    ├── post
    |   ├── firstpost.md   // <- http://yoursite.com/post/firstpost/
    |   ├── happy
    |   |   └── ness.md  // <- http://yoursite.com/post/happy/ness/
    |   └── secondpost.md  // <- http://yoursite.com/post/secondpost/
    └── quote
        ├── first.md       // <- http://yoursite.com/quote/first/
        └── second.md      // <- http://yoursite.com/quote/second/
```

Voici la même organisation qui tourne avec `hugo --uglyURLs`:

```bash
.
└── content
    └── about
    |   └── _index.md  // <- http://yoursite.com/about/index.html
    ├── post
    |   ├── firstpost.md   // <- http://yoursite.com/post/firstpost.html
    |   ├── happy
    |   |   └── ness.md    // <- http://yoursite.com/post/happy/ness.html
    |   └── secondpost.md  // <- http://yoursite.com/post/secondpost.html
    └── quote
        ├── first.md       // <- http://yoursite.com/quote/first.html
        └── second.md      // <- http://yoursite.com/quote/second.html
```


## Canonisation

Par défaut, toutes les URL relatives rencontrées dans l'input ne sont pas modifiées, par ex. `/css/foo.css` resterait comme `/css/foo.css`. Le champ `canonifyURLs` dans votre `config` de site a une valeur par défaut de `false`.

En réglant `canonifyURLs` sur `true`, toutes les URL relatives seraient *canonisés* en utilisant `baseURL`. Par exemple, en supposant que vous avez `baseURL = https://votresite.com/`, l'URL relative `/css/foo.css` serait transformée en URL absolue `http://yoursite.com/css/foo.css`.

Les avantages de la canonisation comprennent la fixation de toutes les URL pour être absolues, ce qui peut aider à certaines tâches d'analyse. Notez cependant que tous les navigateurs modernes traitent ce problème sur le client sans problème.

Les avantages de la non-canonisation comprennent la possibilité d'inclure l'inclusion de ressources relatives au schéma ; par exemple, `http` vs `https` peut être décidé selon la façon dont la page a été récupérée.

{{% note "`canonifyURLs` changement par défaut" %}}
Dans la version de Hugo v0.11 en mai 2014, la valeur par défaut de `canonifyURLs` a été basculée de` true` vers `false`, ce qui, selon nous, est le meilleur défaut et devrait continuer à être le cas dans l'avenir. Veuillez vérifier et ajuster votre site en conséquence si vous effectuez une mise à niveau à partir des versions antérieures.
{{% /note %}}

Pour connaître la valeur actuelle de `canonifyURLs` pour votre site Web, vous pouvez utiliser la commande `hugo config` ajoutée dans v0.13.

```bash
hugo config | grep -i canon
```

Ou, si vous êtes sur Windows et que `grep` n'est pas installé :

```
hugo config | FINDSTR /I canon
```

## Annuler les URL avec le Front Matter

En plus de spécifier les valeurs de permalink dans la configuration de votre site pour différentes sections de contenu, Hugo fournit un contrôle encore plus granulaire pour des contenus individuels.

Les deux `slug` et `url` peuvent être définis dans la première ligne. Pour plus d'informations sur les destinations de contenu au moment de la construction, voir [Organisation du contenu][contentorg].

## URL relatives

Par défaut, toutes les URLs relatives sont laissées inchangées par Hugo, ce qui peut être problématique lorsque vous souhaitez que votre site soit navigable à partir d'un système de fichiers local.

Régler `relativeURLs` sur ` true` dans votre [configuration de site][config] fera en sorte que Hugo réécrit toutes les URLs relatives pour être relatives au contenu actuel.

Par exemple, si votre page `/post/first/` contient un lien vers `/about/`, Hugo réécrira l'URL vers `../../about/`.

[config]: /demarrage/configuration/
[contentorg]: /gestion-contenu/organization/
[front matter]: /gestion-contenu/front-matter/
[multilingual]: /gestion-contenu/multilingual/
[sections]: /gestion-contenu/sections/
[usage]: /demarrage/usage/

