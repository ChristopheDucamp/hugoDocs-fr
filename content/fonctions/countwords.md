---
title: countwords
description: Compte le nombre de mots dans une chaîne.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
categories: [fonctions]
menu:
  docs:
    parent: "Fonctions"
#tags: [comptage, compteur de mot]
signature: ["countwords INPUT"]
workson: []
hugoversion:
relatedfuncs: [countrunes]
deprecated: false
aliases: [/functions/countrunes/,/functions/countwords/]
---

La fonction pour le modèle fonctionne de manière similaire à la  [variable de page .WordCount][pagevars].

```html
{{ "Hugo est un générateur de site statique." | countwords }}
<!-- sort une longueur de contenu de 6 mots.  -->
```


[pagevars]: /variables/page/
