---
title: Débuguer les Modèles
# linktitle: Template Debugging
description: Vous pouvez utiliser la fonction `printf` des modèles Go pour debuguer vos modèles Hugo. Ces fragments fournissent une visualisation rapoide et facile des variables disponibles dans différents contextes.
godocref: http://golang.org/pkg/fmt/
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-22
categories: [Modèles]
#tags: [debugging,troubleshooting]
menu:
  docs:
    parent: "Templates"
    weight: 180
weight: 180
sections_weight: 180
draft: false
aliases: []
toc: false
---

Voici quelques fragments que vous pouvez ajouter à votre modèle pour répondre à quelques questions communes.

Ces fragments utilisent la fonction `printf` disponible dans tous les modèles Go.  Cette fonction est un alias de la fonction Go, [fmt.Printf](http://golang.org/pkg/fmt/).

## Quelles Variables sont Disponibles dans ce Contexte ?

Vous pouvez utiliser la syntaxe de modèle, `$.`, pour récupérer le contexte top-level du modèle à partir de n'importe où dans votre modèle. Ceci imprimera toutes les valeurs sous `.Site`.

```html
{{ printf "%#v" $.Site }}
```

This will print out the value of `.Permalink`:


```html
{{ printf "%#v" .Permalink }}
```


This will print out a list of all the variables scoped to the current context
(`.`, aka ["the dot"][tempintro]).


```html
{{ printf "%#v" . }}
```


When developing a [homepage][], what does one of the pages you're looping through look like?

```html
{{ range .Data.Pages }}
    {{/* The context, ".", is now each one of the pages as it goes through the loop */}}
    {{ printf "%#v" . }}
{{ end }}
```

{{% note "`.Data.Pages` on the Homepage" %}}
`.Data.Pages` on the homepage is equivalent to `.Site.Pages`.
{{% /note %}}

## Pourquoi je ne Vois Pas de Variables Définies ? 

Why Am I Showing No Defined Variables?

Check that you are passing variables in the `partial` function:

```html
{{ partial "header" }}
```

This example will render the header partial, but the header partial will not have access to any contextual variables. You need to pass variables explicitly. For example, note the addition of ["the dot"][tempintro].

```html
{{ partial "header" . }}
```

The dot (`.`) is considered fundamental to understanding Hugo templating. For more information, see [Introduction to Hugo Templating][tempintro].

[homepage]: /templates/pageaccueil/
[tempintro]: /templates/introduction/