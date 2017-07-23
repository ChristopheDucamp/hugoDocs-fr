---
title: isset
linktitle: isset
description: Renvoie true si le paramètre est défini.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
categories: [functions]
menu:
  docs:
    parent: "Fonctions"
#tags: []
signature: ["isset COLLECTION INDEX", "isset COLLECTION KEY"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
aliases: []
---

Prend soit une "slice", "array", ou "channel" et un "index" ou une "map" et une "key" comme input.

```
{{ if isset .Params "project_url" }} {{ index .Params "project_url" }}{{ end }}
```

{{% warning %}}
Toutes les clés de configuration au niveau du site sont stockées en bas de casse. Par conséquent, une valeur-clé `myParam` définie dans votre [fichier de configuration du site](/demarrage/configuration/) doit être consultée avec `{{if isset .Site.Params "myparam"}}` et *non* pas avec `{{if isset .Site.Params "myParam"}}`. Notez que vous pouvez encore accéder à la même clé de config avec `.Site.Params.myParam` *ou* `.Site.Params.myparam`, par exemple au moment d'utiliser [`with`](/fonctions/with).
{{% /warning %}}

