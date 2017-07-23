---
title: countrunes
description: Détermine le nombre de rune dans une chaîne en excluant tout espace-blanc.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [fonctions]
menu:
  docs:
    parent: "Fonctions"
#tags: [compteur, mots, comptage]
signature: ["countrunes INPUT"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
aliases: [/functions/countrunes/,/functions/countwords/]
---

Contrairement à la fonction `countwords`, qui compte chaque mot dans une chaîne, la fonction `countrunes` détermine le nombre de runes dans le contenu et exclut tout espace blanc. Cela a une utilité spécifique si vous rencontrez des langages similaires au CJK.

```html
{{ "Hello, 世界" | countrunes }}
<!-- sort une longueur de contenu de 8 runes. -->
```

[pagevars]: /variables/page/
