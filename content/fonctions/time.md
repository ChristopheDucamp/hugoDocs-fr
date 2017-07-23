---
title: time
linktitle:
description: Convertit une chaîne de temps en une structure  `time.Time`.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-01
categories: [fonctions]
menu:
  docs:
    parent: "Fonctions"
#tags: [dates,time]
signature: ["time INPUT"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
aliases: []
---

`time` convertit une chaîne de temps en une structure  [`time.Time`](https://godoc.org/time#Time) afin que vous puissiez accéder à ses champs :

```
{{ time "2016-05-28" }} → "2016-05-28T00:00:00Z"
{{ (time "2016-05-28").YearDay }} → 149
{{ mul 1000 (time "2016-05-28T10:30:00.00+10:00").Unix }} → 1464395400000, ou temps Unix en millisecondes
```

## Exemple : Utiliser `time` pour récupérer l'Index du Mois

L'exemple suivant prend une chaîne de temps UNIX ---réglée sous  `utimestamp: "1489276800"` dans le front matter d'un contenu---convertit le timestamp (chaîne) dans un nombre en utilisant la  [fonction `int`][int], et puis utilise [`printf`][] pour convertir la propriété `Month` du `time` à l'intérieur d'un  index. 

L'exemple suivant peut être utile au moment de paramétrer des  [sites multilingues][multilingual] :

{{% code file="unix-to-month-integer.html" %}}
```html
{{$time := time (int .Params.addDate)}}
=> $time = 1489276800
{{$time.Month}}
=> "March"
{{$monthindex := printf "%d" $time.Month }}
=> $monthindex = 3
```
{{% /code %}}


[int]: /fonctions/int/
[multilingue]: /gestion-contenu/multilingue/
[`printf`]: /fonctions/printf/
