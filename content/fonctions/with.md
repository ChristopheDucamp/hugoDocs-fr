---
title: with
# linktitle: with
description: Renvoie le contexte (`.`) dans sa portée et ignore le bloc si la variable est absente.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
categories: [fonctions,fondamentaux]
menu:
  docs:
    parent: "Fonctions"
#tags: [conditionnels,conditionals,fondamentaux,fundamentals]
signature: ["with INPUT"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
---

Une autre façon d'écrire une instruction `if` et de faire référence ensuite à la même valeur est d'utiliser `with`. `with` renvoie le contexte (`.`) dans sa portée et ignore le bloc si la variable est absente ou désactivée.

L'exemple suivant vérifie une [variable de site définie par l'utilisateur](/variables/site/) appelée «twitteruser». Si la valeur-clé n'est pas définie, ce qui suit ne rendra rien :

{{% code file="layouts/partials/twitter.html" %}}
```html
{{with .Site.Params.twitteruser}}<span class="twitter">
<a href="https://twitter.com/{{.}}" rel="author">
<img src="/images/twitter.png" width="48" height="48" title="Twitter: {{.}}"
 alt="Twitter"></a>
</span>{{end}}
```
{{% /code %}}
