---
title: printf
linktitle: printf
description: Met en forme une chaîne utilisant la fonction standard `fmt.Sprintf`.
godocref: https://golang.org/pkg/fmt/
date: 2017-02-01
publishdate: 2017-06-28
lastmod: 2017-02-01
categories: [fonctions]
menu:
  docs:
    parent: "fonctions"
#tags: [strings]
signature: ["printf FORMAT INPUT"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
---

Voir la [doc go](https://golang.org/pkg/fmt/) pour des informations supplémentaires.

```golang
{{ i18n ( printf "combined_%s" $var ) }}
```

```
{{ printf "formatted %.2f" 3.1416 }}
```
