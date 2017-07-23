---
title: .GetPage
description: "Reçoit une `Page` d'un `Kind` et d'un `path` donnés."
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
categories: [functions]
menu:
  docs:
    parent: "Fonctions"
#tags: [sections,lists,indexes]
signature: [".GetPage TYPE PATH"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
aliases: []
---

Chaque `Page` a un attribut `Kind` qui affiche quel type de page c'est. Bien que cet attribut puisse être utilisé pour lister des pages d'un certain `Kind` en utilisant `where`, il peut être souvent utile d'extraire une seule page par son chemin.

`.GetPage` recherche une page d'un `Kind` et d'un `path` donnés.

```
{{ with .Site.GetPage "section" "blog" }}{{ .Title }}{{ end }}
```

Cette méthode renverra `nil` quand aucune page ne pourra être trouvée, ainsi ce qui est au-dessus n'imprimera rien si la section blog n'est pas trouvée.

Pour une page régulière : 

```
{{ with .Site.GetPage "page" "blog" "mon-post.md" }}{{ .Title }}{{ end }}
```

Notez que le chemin peut aussi être fournie comme ceci : 

```
{{ with .Site.GetPage "page" "blog/mon-post.md" }}{{ .Title }}{{ end }}
```

Les types valides (`kind`) sont: *page, home, section, taxonomy et taxonomyTerm.*

## Exemple `.GetPage`

Cet extrait de code ---sous la forme d'un [modèle partiel][partials]--- vous permettra de faire ce qui suit : 


1. Prendre l'objet index de votre [taxonomie][] `tags`
2. Assigner cet objet à une variable, `$t`
3. Trier les termes associés à la taxonomie par popularité.
4. Prendre les deux termes les plus populaires dans la taxonomie (c'est-à-dire les deux balises les plus populaires attribuées au contenu.)

{{% code file="grab-top-two-tags.html" %}}
```html
<ul class="most-popular-tags">
{{ $t := $.Site.GetPage "taxonomyTerm" "tags" }}
{{ range first 2 $t.Data.Terms.ByCount }}
    <li>{{.}}</li>
{{ end }}
</ul>
```
{{% /code %}}


[partials]: /templates/partiels/
[taxonomie]: /gestion-contenu/taxonomies/
