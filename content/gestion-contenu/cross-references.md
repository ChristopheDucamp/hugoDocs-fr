---
title: Références Croisées
description: Hugo facilite le lien entre les documents.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [gestion de contenu]
#tags: [ancre, urls,références]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 100
weight: 100	#rem
aliases: []
toc: true
---

Les shortcodes `ref` et `relref` lient ensemble les documents, ceux qui sont en [raccourcis de codes intégrés dans Hugo][built-in Hugo shortcodes]. Ces shortcodes sont utilisés pour fournir des liens vers les titres à l'intérieur de votre contenu, que ce soit entre les documents ou dans un document. La seule différence entre `ref` et `relref` est respectivement si l'URL résultante est absolue (`http://1.com/a-propos/`) ou relative (`/a-propos/`).

## Utilisez `ref` et `relref`

```md
{{</* ref "document" */>}}
{{</* ref "#ancre" */>}}
{{</* ref "document#ancre" */>}}
{{</* relref "document" */>}}
{{</* relref "#ancre" */>}}
{{</* relref "document#ancre" */>}}
```

L'unique paramètre de `ref` est une chaîne avec un contenu `nomdocument` (par ex., `apropos.md`) avec ou sans ancre `anchor` dans le document (par ex `#qui`) et sans espaces.

### Noms de Document

Le `nomdocument` est le nom d'un document, comprenant son extension de format ; ceci peut être juste le nom de fichier, ou le chemin relatif à partir du dossier `content/`. Avec un document `content/blog/post.md`, les deux formats produiront le même résultat :

```md
{{</* relref "blog/post.md" */>}} => `/blog/post/`
{{</* relref "post.md" */>}} => `/blog/post/`
```

Si vous avez le même nom de fichier utilisé sur plusieurs sections, vous devriez utiliser seulement le format du chemin relatif ; autrement le comportement sera `undefined`. Ceci s'illustre mieux avec un exemple de dossier `content` :

```bash
.
└── content
    ├── evenements
    │   └── mon-anniversaire.md
    ├── galeries
    │   └── mon-anniversaire.md
    ├── meta
    │   └── mon-article.md
    └── posts
        └── mon-anniversaire.md
```

Pour être sûr d'avoir la référence correcte dans ce cas, utilisez le chemin complet :

{{% code file="content/meta/mon-article.md" copy="false" %}}
```md
{{</* relref "evenements/mon-anniversaire.md" */>}} => /evenements/mon-anniversaire/
```
{{% /code %}}

{{< todo >}}Retirer cet avertissement quand https://github.com/gohugoio/hugo/issues/3703 sera sorti.{{< /todo >}}

Un nom de document relatif *ne doit pas* commencer par un slash  (`/`).
```md
{{</* relref "/evenements/mon-anniversaire.md" */>}} => ""
```

### Avec Plusieurs Format Output 

Si la page existe dans plusieurs [formats de sortie][output formats], `ref` ou `relref` peuvent s'utiliser avec un nom de format output :

```
 [Neat]({{</* ref "blog/neat.md" "amp" */>}})
```

### Ancres

Quand une ancre `anchor` est fournie en elle-même, l'identifiant  unique de la page sera ajouté ; quand une `anchor` est fournie ajoutée au `nomdocument`, l'identifiant unique de page trouvé sera ajouté : 

```md
{{</* relref "#ancres" */>}} => #ancres:9decaf7
{{</* relref "a-propos/features.md#content" */>}} => /blog/post/#who:badcafe
```

Les exemples au-dessus restituent comme suit pour cette page très particulière tout comme une référence au titre du "Content" dans les fonctionnalités de documentation Hugo 

```md
{{</* relref "#qui" */>}} => #qui:9decaf7
{{</* relref "blog/post.md#qui" */>}} => /blog/post/#qui:badcafe
```

Plus d'informations sur les identifiants uniques de documents et les titres peuvent être trouvées [en-dessous]({{< ref "#ancres-titre-hugo" >}}).

### Exemples

* `{{</* ref "blog/post.md" */>}}` => `http://votresite.com/blog/post/`
* `{{</* ref "post.md#tldr" */>}}` => `http://votresite.com/blog/post/#tldr:caffebad`
* `{{</* relref "post.md" */>}}` => `/blog/post/`
* `{{</* relref "blog/post.md#tldr" */>}}` => `/blog/post/#tldr:caffebad`
* `{{</* ref "#tldr" */>}}` => `#tldr:badcaffe`
* `{{</* relref "#tldr" */>}}` => `#tldr:badcaffe`

## Ancres Titres Hugo

Lorsque vous utilisez des types de documents Markdown, Hugo génère automatiquement des ancres de titres. L'ancrage généré pour cette section est `ancres-titres-hugo`. Étant donné que les ancrages d'en-têtes sont générés automatiquement, Hugo s'efforce de s'assurer que les ancres de titres soient uniques à la fois dans un document et sur l'ensemble du site.

Assurer l'exclusivité du titre sur le site est accompli avec un identifiant unique pour chaque document en fonction de son chemin. À moins qu'un document ne soit renommé ou déplacé entre les sections *dans le système de fichiers*, l'identifiant unique du document ne changera pas : `blog/post.md` aura toujours un identifiant unique de `81df004c333b392d34a49fd3a91ba720`.

`ref` et `relref` ont été ajoutés afin que vous puissiez créer ces liens de référence sans avoir à connaître l'identifiant unique du document. (Les liens dans les tableaux de contenu des documents sont automatiquement mis à jour avec cette valeur.)

```md
{{</* relref "gestion-contenu/cross-references.md#ancres-titres-hugo" */>}}
/gestion-contenu/cross-references/#ancres-titres-hugo:77cd9ea530577debf4ce0f28c8dca242
```


[built-in Hugo shortcodes]: /gestion-contenu/shortcodes/#using-the-built-in-shortcodes
[lists]: /templates/listes/
[output formats]: /templates/output-formats/
[shortcode]: /gestion-contenu/shortcodes/