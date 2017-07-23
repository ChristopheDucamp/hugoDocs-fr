---
title: .Param
description: Appelle des variables de page ou site à l'intérieur de votre modèle.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-04-30
#tags: ["front matter"]
categories: [functions]
menu:
  docs:
    parent: "Fonctions"
toc:
signature: [".Param KEY"]
workson: []
hugoversion:
relatedfuncs: [default]
deprecated: false
draft: false
aliases: []
---

Dans Hugo, vous pouvez déclarer des [params valables-sur-tout-le-site][sitevars] (par ex. dans votre [configuration][]), tout comme les params pour les [pages individuelles][pagevars].

Un cas d'usage commun est d'avoir une valeur générale pour le site et une valeur plus spécifique pour quelques-unes des pages (par ex., une image).

Vous pouvez utiliser la méthode `.Param` pour appeler ces valeurs à l'intérieur de votre modèle. Ce qui suit cherchera d'abord un param `image` dans un [front matter][] spécifique de contenu. S'il n'est pas trouvé, Hugo cherchera un param `image` param dans votre configuration de site :

```
$.Param "image"
```

{{% note %}}
La méthode `Param` peut ne pas considérer des chaînes vides dans un front matter de contenu comme "non trouvées." Si vous réglez un front matter avec des champs pré-configurés vers des chaînes vides en utilisant les archétypes d'Hugo, il peut être mieux d'utiliser la [fonction `default`](/fonctions/default/) au lieu de `Param`. Voir le [problème en rapport remonté sur GitHub](https://github.com/gohugoio/hugo/issues/3366).
{{% /note %}}


[configuration]: /demarrage/configuration/
[front matter]: /gestion-contenu/front-matter/
[pagevars]: /variables/page/
[sitevars]: /variables/site/
