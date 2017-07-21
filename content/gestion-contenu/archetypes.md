---
title: Archétypes
linktitle: Archétypes
description: Les archétypes vous permettent de créer de nouvelles instances de types de contenu et de définir les paramètres par défaut à partir de la ligne de commande.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-20
#tags: [archetypes,generators,metadata,front matter]
categories: ["content management", gestion de contenu]
menu:
  docs:
    parent: "content-management"
    weight: 70
  quicklinks:
weight: 70	#rem
draft: false
aliases: [/content/archetypes/]
toc: true
---

{{% notice warning %}}
Cette section est dépréciée, voir https://github.com/gohugoio/hugoDocs/issues/11
{{% /notice %}}
{{% todo %}}
Voir au-dessus
{{% /todo %}}

## C'est quoi les Archétypes ?

**Les archétypes** sont des fichiers de contenu dans le [dossier archetypes][archetypes directory] de votre projet qui contiennent des [front matter][] préconfigurés pour les [types de contenu][content types] de votre site web. Les archétypes facilitent le maintient de métadonnées cohérentes sur le contenu de votre site Web et permettent aux auteurs de contenu de générer rapidement des instances d'un type de contenu via la commande `hugo new`.

Le générateur `hugo new` pour les archétypes suppose que votre répertoire de travail est le dossier de contenu à la racine de votre projet. Hugo est capable d'inférer l'archétype approprié en supposant le type de contenu à partir de la section de contenu passée à la commande CLI :

```bash
hugo new <section-contenu>/<nom-fichier.md>
```

Nous pouvons utiliser ce modèle pour créer un nouveau fichier  `.md` dans la section `posts` :

{{% code file="exemple-archetype.sh" %}}
```bash
hugo new posts/mon-premier-post.md
```
{{% /code %}}

{{% note "Annuler le Type de Contenu dans un Nouveau Fichier" %}}
Pour annuler le type de contenu Hugo infère à partir de la  `[content-section]`, il ajoute le marqueur `--kind` à la fin de la commande `hugo new`.
{{% /note %}}

Lancer cette commande dans un nouveau site qui n'a pas d'archetypes par défaut ou d'archetypes personnalisés créera le fichier suivant : 

{{% output file="content/posts/my-first-post.md" %}}
```toml
+++
date = "2017-02-01T19:20:04-07:00"
title = "mon premier post"
draft = true
+++
```
{{% /output %}}

{{% note %}}
Dans cet exemple, si vous n'avez pas déjà un dossier `content/posts`, Hugo créera à la fois pour vous `content/posts/` et `content/posts/mon-premier-post.md`.
{{% /note %}}

Les champs auto-remplis valent la peine d'être examinés : 

* `title` est généré à partir du nouveau nom de fichier du contenu (par ex. dans ce cas, `mon-premier-post`devient `"mon premier post"`)
* `date` et `title` sont les variables qui sont livrées avec Hugo et sont donc incluses dans **tous** les fichiers de contenu créés avec la CLI Hugo. `Date` est générée dans le [format RFC 3339][RFC 3339 format] à l'aide de la fonction [`now()`][] de Go, qui retourne l'heure actuelle.
* La troisième variable, `draft = true`, n'est *pas* hérité par vos archétypes par défaut ou personnalisés mais elle est incluse dans l'archetype `default.md` automatiquement construit par Hugo.

Trois variables par fichier de contenu ne suffisent souvent pas pour une gestion efficace du contenu de sites Web plus importants. Heureusement, Hugo fournit un mécanisme simple pour augmenter le nombre de variables à travers des archétypes personnalisés, ainsi que des archétypes par défaut pour conserver la création de contenu DRY.

## Ordre de Recherche pour les Archétypes

Tout comme pour [l'ordre de recherche pour les modèles][lookup] dans votre dossier `layouts`, Hugo recherche un archétype de section ou un archétype spécifique-au-type, puis un archétype par défaut et enfin un archétype interne livré avec Hugo. Par exemple, Hugo recherchera un archétype pour `content/posts/mon-premier-post.md` dans l'ordre suivant :

1. `archetypes/posts.md`
2. `archetypes/default.md`
3. `themes/<THEME>/archetypes/posts.md`
4. `themes/<THEME>/archetypes/default.md` (Auto-généré avec `hugo new site`)

{{% note "Utililser un Archétype de Thème" %}}
Si vous souhaitez utiliser des archétype livrés avec un thème, le champ `theme` doit être spécifié dans votre [fichier de configuration](/getting-started/configuration/).
{{% /note %}}

## Choisissez votre Format Front Matter d'Archetype

Par défaut, les fichiers de contenu `hugo new` incluent le front matter au format TOML quel que soit le format utilisé dans `archétypes/*.md`.

Vous pouvez spécifier un format par défaut différent dans votre [fichier de configuration][configuration file] de site en utilisant la directive `metaDataFormat`. Les valeurs possibles sont `toml`,` yaml` et `json`.

## Archétypes par Défaut

Les archétypes par défaut sont pratiques si votre front matter de contenu reste cohérent à travers plusieurs [sections de contenu][sections].

### Créer l'Archétype par Défaut

Lorsque vous créez un nouveau projet Hugo en utilisant `hugo new site`, vous remarquerez que Hugo a déjà échafaudé un fichier sur `archetypes/default.md`.

Les exemples suivants proviennent d'un site utilisant les `tags` et `categories` comme [taxonomies][]. Si nous supposons que tous les fichiers de contenu nécessiteront ces deux valeurs-clés, nous pouvons créer un archétype `default.md` qui *étend*  l'archétype de base de Hugo. Dans cet exemple, nous incluons "golang" et "hugo" comme tags et "développement web" en tant que catégorie.

{{% code file="archetypes/default.md" %}}
```toml
+++
tags = ["golang", "hugo"]
categories = ["dévelopopement web"]
+++
```
{{% /code %}}

{{% warning "caractères EOL dans les éditeurs de texte"%}}
Si vous obtenez une `EOF error` lors de l'utilisation de `hugo new`, ajoutez un retour de chariot dans votre front matter TOML ou YAML après la fermeture du `+++` ou `---` , respectivement. (Voir l'[article de dépannage sur les erreurs EOF](/troubleshooting/eof-error/) pour plus d'informations.)
{{% /warning %}}

### Utiliser l'Archétype par Défaut

Avec un `archetypes/default.md` en place, nous pouvons utiliser la CLI pour créer un nouveau post dans la section de contenu `posts` :

{{% code file="new-post-from-default.sh" %}}
```bash
$ hugo new posts/mon-nouveau-post.md
```
{{% /code %}}

Hugo crée alors un nouveau fichier markdown file avec le front matter suivant :

{{% output file="content/posts/my-new-post.md" %}}
```toml
+++
categories = ["développement web"]
date = "2017-02-01T19:20:04-07:00"
tags = ["golang", "hugo"]
title = "mon nouveau post"
+++
```
{{% /output %}}

Nous voyons que les valeurs-clés `title` et `date` ont été ajoutées en plus des valeurs-clés `tags` et `categories` provenant de `archetypes/default.md`.

{{% note "Ordre du Front Matter" %}}
Vous pouvez remarquer que les fichiers de contenu créés avec  `hugo new` ne respectent pas l'orde des valeurs-clés spécifiées dans vos fichiers archétype. Ceci est un [problème connu](https://github.com/gohugoio/hugo/issues/452).
{{% /note %}}

## Personnaliser les Archétypes

Supposons que la section `posts` de votre site requiert un front matter plus sophistiqué que ce qui a été spécifié dans `archetypes/default.md`. Vous pouvez créer un archétype personnalisé pour vos posts sur `archetypes/posts.md` qui comprend l'ensemble complet du front matter à ajouter aux deux champs d'archétypes par défaut.

### Créer un Archétype Personnalisé

{{% code file="archetypes/posts.md"%}}
```toml
+++
description = ""
tags = ""
categories = ""
+++
```
{{% /code %}}

### Utiliser un Archétype Personnalisé

Avec un `archetypes/posts.md` en place, vous pouvez utiliser la CLI Hugo pour créer une nouvelle publication avec votre front matter préconfiguré dans la section de contenu `posts` :

{{% code file="new-post-from-custom.sh" %}}
```bash
$ hugo new posts/post-from-custom.md
```
{{% /code %}}

Cette fois, Hugo reconnaît notre archétype `archetypes/posts.md` personnalisé et l'utilise à la place de `archetypes/default.md`. Le fichier généré comprend maintenant la liste complète des paramètres du front matter, ainsi que les `title` et `date` de l'archétype de base :

{{% output file="content/posts/post-from-custom-archetype.md" %}}
```toml
+++
categories = ""
date = 2017-02-13T17:24:43-08:00
description = ""
tags = ""
title = "post from custom archetype"
+++
```
{{% /output %}}

### Docs Hugo sur l'Archétype Personnalisé

Pour un exemple d'archétypes en pratique, ce qui suit est l'archétype `functions` provenant de la documentation Hugo :

{{% code file="archetypes/functions.md" %}}
```yaml
{{< readfile file="/archetypes/functions.md" >}}
```
{{% /code %}}

{{% note %}}
L'archétype précédent est maintenu à jour à chaque fois que Hugo construit en utilisant la [fonction `readFile`](/fonctions/readfile/) d'Hugo. Pour des exemples similaires, regardez les [Modèles de Fichier Local](/templates/files/).
{{% /note %}}

[archetypes directory]: /demarrage/structure-dossier/
[`now()`]: http://golang.org/pkg/time/#Now
[configuration file]: /demarrage/configuration/
[sections]: /gestion-contenu/sections/
[content types]: /gestion-contenu/types/
[front matter]: /gestion-contenu/front-matter/
[RFC 3339 format]: https://www.ietf.org/rfc/rfc3339.txt
[taxonomies]: /gestion-contenu/taxonomies/
[lookup]: /templates/lookup/
[templates]: /templates/
