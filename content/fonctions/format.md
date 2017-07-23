---
title: .Format
description: Les formats natifs dans Hugo dates---`.Date`, `.PublishDate`, et `.LastMod`---selon la chaîne layout de Go.
godocref: https://golang.org/pkg/time/#example_Time_Format
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
categories: [fonctions]
menu:
  docs:
    parent: "Fonctions"
#tags: [dates,time]
signature: [".Format FORMAT"]
workson: [times]
hugoversion:
relatedfuncs: [dateFormat,now,Unix,time]
deprecated: false
aliases: []
toc: false
---

`.Format` formatera les valeurs de date définies dans votre front matter et peut être utilisé comme une propriété sur les [variables de page][pagevars] suivantes :

* `.PublishDate`
* `.Date`
* `.LastMod`

En supposant une valeur-clé de `date: 2017-03-03` dans un front matter de fichier de contenu, vous pouvez lancer la date à travers `.Format` suivie par une chaîne de layout pour votre output désiré au moment du build :

```golang
{{ .PublishDate.Format "January 2, 2007" }} => March 3, 2017
```

Pour mettre en forme *toutes* toutes les représentations de chaînes de dates définies dans votre front matter, regardez la  [fonction `dateFormat`][dateFormat], qui tire encore parti de la chaîne de layout Golang expliquée en-dessous mais qui utilise une syntaxe légèrement différente.

## Chaîne de Layout de Go

Les modèles Hugo [mettent en forme vos dates][time] via les chaînes de layout qui pointent vers une référence "time" spécifque :

```
Mon Jan 2 15:04:05 MST 2006
```

Bien que cela puisse sembler arbitraire, la valeur numérique de  `MST` est `07`, produisant par conséquent la chaîne de layout d'une séquence de nombres.

Voici une explication visuelle [prise directement dans la documentation Go][gdex] :

```
 Jan 2 15:04:05 2006 MST
=> 1 2  3  4  5    6  -7
```

### Hugo Date and Time Templating Reference

Les exemples suivants montrent la chaîne de mise en page suivie de la sortie rendue.

Les exemples ont été rendus et testés dans [CST][] et tous indiquent le même champ dans le front matter d'un fichier de contenu :

```
date: 2017-03-03T14:15:59-06:00
```

`.Date` (i.e. appelé via [page variable][pagevars])
: **Renvoie**: `2017-03-03 14:15:59 -0600 CST`

`"Monday, January 2, 2006"`
: **Renvoie**: `Friday, March 3, 2017`

`"Mon Jan 2 2006"`
: **Renvoie**: `Fri Mar 3 2017`

`"January 2nd"`
: **Renvoie**: `March 3rd`

`"January 2006"`
: **Renvoie**: `March 2017`

`"2006-01-02"`
: **Renvoie**: `2017-03-03`

`"Monday"`
: **Renvoie**: `Friday`

`"02 Jan 06 15:04 MST"` (RFC822)
: **Renvoie**: `03 Mar 17 14:15 CST`

`"02 Jan 06 15:04 -0700"` (RFC822Z)
: **Renvoie**: `03 Mar 17 14:15 -0600`

`"Mon, 02 Jan 2006 15:04:05 MST"` (RFC1123)
: **Renvoie**: `Fri, 03 Mar 2017 14:15:59 CST`

`"Mon, 02 Jan 2006 15:04:05 -0700"` (RFC339)
: **Renvoie**: `Fri, 03 Mar 2017 14:15:59 -0600`

### Numéros cardinaux et abréviations ordinales

Les numéros cardinaux étalés (par exemple «un», «deux» et «trois») et les abréviations ordinales (c'est-à-dire avec des suffixes raccourcis comme "1st", "2n" et "3rd") ne sont actuellement pas supportés :

```
{{.Date.Format "Jan 2nd 2006"}}
```

Hugo suppose que vous souhaitez ajouter `nd` en tant que chaîne au jour du mois et produit ce qui suit:

```
Mar 3nd 2017
```

{{% note %}} 
todo : étudier la solution de contournement posée sur <https://discourse.gohugo.io/t/formatting-a-date-with-suffix-2nd/5701> et localiser un exemple de date en français (1er janvier)
{{% /note %}}

### Utiliser `.Local` et `.UTC`

En conjonction avec la [fonction `dateFormat`][dateFormat], vous pouvez aussi convertir vos dates en `UTC` ou vers des timezones locales :

`{{ dateFormat "02 Jan 06 15:04 MST" .Date.UTC }}`
: **Renvoie**: `03 Mar 17 20:15 UTC`

`{{ dateFormat "02 Jan 06 15:04 MST" .Date.Local }}`
: **Renvoie**: `03 Mar 17 14:15 CST`

[CST]: https://fr.wikipedia.org/wiki/Heure_du_Centre
[dateFormat]: /fonctions/dateformat/
[gdex]: https://golang.org/pkg/time/#example_Time_Format
[pagevars]: /variables/page/
[time]: https://golang.org/pkg/time/
