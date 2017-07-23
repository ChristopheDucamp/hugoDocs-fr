---
title: dateFormat
description: Convertir la représentation textuelle du `datetime` dans le format spécifié.
godocref: https://golang.org/pkg/time/
date: 2017-02-01
publishdate: 2017-02-22
lastmod: 2017-02-01
categories: [Fonctions]
menu:
  docs:
    parent: "Fonctions"
#tags: [dates,time,strings]
signature: ["dateFormat LAYOUT INPUT"]
workson: []
hugoversion:
relatedfuncs: [Format,now,Unix,time]
deprecated: false
---

`dateFormat` convertit la représentation textuelle du `datetime` dans le format spécifié ou la renvoie sous une valeur Go type `time.Time`. Celles-ci sont mises en forme avec la chaîne du layout.

```
{{ dateFormat "Monday, Jan 2, 2006" "2015-01-21" }} → "Wednesday, Jan 21, 2015"
```

{{% warning %}}
À partir de la v0.19 de Hugo, la fonction `dateFormat` n'est pas supportée comme partie de la [fonctionnalité multilingue](/gestion-contenu/multilingue/).
{{% /warning %}}

Voir la [fonction `Format`](/fonctions/format/) pour une liste plus complète des options de mise en forme des dates dans vos modèles.