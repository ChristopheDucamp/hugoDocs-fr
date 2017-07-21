---
title: Taxonomy
linktitle: Taxonomy Variables
description: Les pages de taxonomie sont de type `Page` et disposent de toutes les variables de page-, de site- et de liste-. Cependant, les modèles de termes de taxonomie ont des variables supplémentaires disponibles pour leurs modèles.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [variables and params, variables et params]
#tags: [taxonomies,terms, termes]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 30
weight: 30
sections_weight: 30
aliases: []
toc: true
---

## Variables de Page de Termes de Taxonomie

Les [pages de termes de taxonomie][taxonomytemplates] sont du type `Page` et ont les variables supplémentaires qui suivent.

Par exemple, les champs suivants seraient disponibles dans `layouts/_defaults/terms.html`, selon la façon dont vous organisez vos [modèles de taxonomie][taxonomytemplates] :

`.Data.Singular`
: Le nom au singulier de la taxonomie (par ex., `tags => `tag`)

`.Data.Plural`
: Le nom au pluriel de la taxonomie (par ex., `tags => tags`)

`.Data.Pages`
: The list of pages in the taxonomy

`.Data.Terms`
: The taxonomy itself

`.Data.Terms.Alphabetical`
: The taxonomy terms alphabetized

`.Data.Terms.ByCount`
: The Terms ordered by popularity

Note that `.Data.Terms.Alphabetical` and `.Data.Terms.ByCount` can also be reversed:

* `.Data.Terms.Alphabetical.Reverse`
* `.Data.Terms.ByCount.Reverse`

## Utiliser `.Site.Taxonomies` en dehors des Modèles de Taxonomie

The `.Site.Taxonomies` variable holds all the taxonomies defined site-wide. `.Site.Taxonomies` is a map of the taxonomy name to a list of its values (e.g., `"tags" -> ["tag1", "tag2", "tag3"]``). Each value, though, is not a string but rather a *Taxonomy variable*.

## La Variable `.Taxonomy`

The `.Taxonomy` variable, available, for example, as `.Site.Taxonomies.tags`, contains the list of tags (values) and, for each tag, their corresponding content pages.

### Exemple d'Usage de `.Site.Taxonomies`

The following [partial template][partials] will list all your site's taxonomies, each of their keys, and all the content assigned to each of the keys. For more examples of how to order and render your taxonomies, see  [Taxonomy Templates][taxonomytemplates].

{{% code file="all-taxonomies-keys-and-pages.html" download="all-taxonomies-keys-and-pages.html" %}}
```html
<section>
  <ul>
    {{ range $taxonomynom, $taxonomy := .Site.Taxonomies }}
      <li><a href="{{ "/" | relLangURL}}{{ $taxonomynom | urlize }}">{{ $taxonomynom }}</a>
        <ul>
          {{ range $key, $value := $taxonomy }}
          <li> {{ $key }} </li>
                <ul>
                {{ range $value.Pages }}
                    <li><a href="{{ .Permalink}}"> {{ .LinkTitle }} </a> </li>
                {{ end }}
                </ul>
          {{ end }}
        </ul>
      </li>
    {{ end }}
  </ul>
</section>
```
{{% /code %}}

[partials]: /templates/partiels/
[taxonomytemplates]: /templates/taxonomy-templates/