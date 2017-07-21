---
title: Pagination
linktitle: Pagination
description: Hugo supporte la pagination pour vos pages d'accueil, pages de section et taxonomies.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-20
categories: [templates, modèles]
#tags: [lists,sections,pagination, listes]
menu:
  docs:
    parent: "templates"
    weight: 140
weight: 140
sections_weight: 140
draft: false
aliases: [/extras/pagination,/doc/pagination/]
toc: true
---

Le vrai pouvoir de la pagination Hugo brille quand elle est combinée avec la [fonction `where`][where] et ses opérateurs de type SQL : [`first`][], [`last`][], and [`after`][]. Vous pouvez même [ordonner le contenu][lists] de la façon que vous aviez l'habitude de faire avec Hugo.

## Configurer la Pagination

La pagination peut être configurée dans votre [configuration de site][configuration]:

`Paginate`
: default = `10`. Ce réglage peut être annulé dans le modèle.

`PaginatePath`
: default = `page`. Vous permet de régler un chemin différent pour vos pages de pagination.

Setting `Paginate` to a positive value will split the list pages for the homepage, sections and taxonomies into chunks of that size. But note that the generation of the pagination pages for sections, taxonomies and homepage is *lazy* --- the pages will not be created if not referenced by a `.Paginator` (see below).

`PaginatePath` is used to adapt the `URL` to the pages in the paginator (the default setting will produce URLs on the form `/page/1/`.

## List Paginator Pages

{{% notice warning %}}
`.Paginator` is provided to help you build a pager menu. This feature is currently only supported on homepage and list pages (i.e., taxonomies and section lists).
{{% /notice %}}

There are two ways to configure and use a `.Paginator`:

1. The simplest way is just to call `.Paginator.Pages` from a template. It will contain the pages for *that page*.
2. Select a subset of the pages with the available template functions and ordering options, and pass the slice to `.Paginate`, e.g. `{{ range (.Paginate ( first 50 .Data.Pages.ByTitle )).Pages }}`.

For a given **Page**, it's one of the options above. The `.Paginator` is static and cannot change once created.

The global page size setting (`Paginate`) can be overridden by providing a positive integer as the last argument. The examples below will give five items per page:

* `{{ range (.Paginator 5).Pages }}`
* `{{ $paginator := .Paginate (where .Data.Pages "Type" "post") 5 }}`

It is also possible to use the `GroupBy` functions in combination with pagination:

```
{{ range (.Paginate (.Data.Pages.GroupByDate "2006")).PageGroups  }}
```

## Construire la Navigation

The `.Paginator` contains enough information to build a paginator interface.

The easiest way to add this to your pages is to include the built-in template (with `Bootstrap`-compatible styles):

```html
{{ template "_internal/pagination.html" . }}
```

{{% note "When to Create `.Paginator`" %}}
If you use any filters or ordering functions to create your `.Paginator` *and* you want the navigation buttons to be shown before the page listing, you must create the `.Paginator` before it's used.
{{% /note %}}

The following example shows how to create `.Paginator` before its used:

```html
{{ $paginator := .Paginate (where .Data.Pages "Type" "post") }}
{{ template "_internal/pagination.html" . }}
{{ range $paginator.Pages }}
   {{ .Title }}
{{ end }}
```

Without the `where` filter, the above example is even simpler:

```html
{{ template "_internal/pagination.html" . }}
{{ range .Paginator.Pages }}
   {{ .Title }}
{{ end }}
```

If you want to build custom navigation, you can do so using the `.Paginator` object, which includes the following properties:

`PageNumber`
: The current page's number in the pager sequence

`URL`:
The relative URL to the current pager

`Pages`:
The pages in the current pager

`NumberOfElements`
: The number of elements on this page

`HasPrev`
: Whether there are page(s) before the current

`Prev`
: The pager for the previous page

`HasNext`
: Whether there are page(s) after the current

`Next`
: The pager for the next page

`First`
: The pager for the first page

`Last`
: The pager for the last page

`Pagers`
: A list of pagers that can be used to build a pagination menu

`PageSize`
: Size of each pager

`TotalPages`
: The number of pages in the paginator

`TotalNumberOfElements`
: The number of elements on all pages in this paginator

## Information Supplémentaire

The pages are built on the following form (`BLANK` means no value):

```
[SECTION/TAXONOMY/BLANK]/index.html
[SECTION/TAXONOMY/BLANK]/page/1/index.html => redirect to  [SECTION/TAXONOMY/BLANK]/index.html
[SECTION/TAXONOMY/BLANK]/page/2/index.html
....
```


[`first`]: /fonctions/first/
[`last`]: /fonctions/last/
[`after`]: /fonctions/after/
[configuration]: /demarrage/configuration/
[lists]: /templates/lists/
[where]: /fonctions/where/