---
title: Trier et Grouper les Listes Hugo
linktitle: Trier et Grouper les Listes
description: Vous pouvez regrouper ou trier votre contenu à la fois dans votre modélisation et dans le front matter du contenu.
date: 2017-02-01
publishdate: 2017-07-23
lastmod: 2017-07-23
categories: [templates, modèles]
#tags: []
menu:
  docs:
    parent: "Modèles"
    weight: 27
weight: 27
sections_weight: 27
draft: true
aliases: [/templates/ordering/,/templates/grouping/]
toc: true
notes: Ceci devait être initialement une page séparée sur le nouveau site de la documentation, mais cela a plus de sens de conserver tout dans la page templates/listes. - rdwatters, 2017-03-12.
---

Dans Hugo, un modèle de liste est n'importe quel modèle qui sera utilisé pour rendre plusieurs éléments de contenu dans une page unique HTML.

## Exemple de Modèles de Liste

### Le Modèle de Section

Ce modèle de liste est utilisé pour [spf13.com](http://spf13.com/). Il fait usage des [modèles de partiel][partials]. Tous les exemples utilisent une [vue](/templates/views/) appelée soit "li" ou "summary."

{{% code file="layouts/section/post.html" %}}
```html
{{ partial "header.html" . }}
{{ partial "subheader.html" . }}

<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
        <ul id="list">
            {{ range .Data.Pages }}
                {{ .Render "li"}}
            {{ end }}
        </ul>
  </div>
</section>
{{ partial "footer.html" . }}
```
{{% /code %}}

### Le Modèle de Taxonomie

{{% code file="layouts/_default/taxonomies.html" download="taxonomies.html" %}}
```html
{{ define "main" }}
<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Data.Pages }}
        {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{ end }}
```
{{% /code %}}

## Trier le Contenu

Les listes Hugo rendent le contenu basé sur les métadonnées fournies dans le [front matter](/content-management/front-matter/)..

Voci une variété de différentes manières avec lesquelles vous pouvez trier les items de contenu dans vos modèles de listes :

### Par Défaut : Weight > Date

{{% code file="layouts/partials/order-default.html" %}}
```html
<ul class="pages">
    {{ range .Data.Pages }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Weight

{{% code file="layouts/partials/by-weight.html" %}}
```html
{{ range .Data.Pages.ByWeight }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}

### Par Date

{{% code file="layouts/partials/by-date.html" %}}
```html
{{ range .Data.Pages.ByDate }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}

### Par Date de Publication

{{% code file="layouts/partials/by-publish-date.html" %}}
```html
{{ range .Data.Pages.ByPublishDate }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .PublishDate.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}

### Par Date d'Expiration 

{{% code file="layouts/partials/by-expiry-date.html" %}}
```html
{{ range .Data.Pages.ByExpiryDate }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .ExpiryDate.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}

### Par Date de Modification

{{% code file="layouts/partials/by-last-mod.html" %}}
```html
{{ range .Data.Pages.ByLastmod }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}

### Par Longueur Length

{{% code file="layouts/partials/by-length.html" %}}
```html
{{ range .Data.Pages.ByLength }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}


### Par Titre

{{% code file="layouts/partials/by-title.html" %}}
```html
{{ range .Data.Pages.ByTitle }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}

### Par Titre de Lien

{{% code file="layouts/partials/by-link-title.html" %}}
```html
{{ range .Data.Pages.ByLinkTitle }}
    <li>
    <a href="{{ .Permalink }}">{{ .LinkTitle }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
{{ end }}
```
{{% /code %}}

### Par Paramètre

Le tri basé sur le paramètre spécifié du front matter. Le contenu qui n'a pas le champ front matter spécifié utilisera la valeur par défaut du site `.Site.Params` default.Si le paramètre n'est trouvé nulle part dans les entrées, ces entrées apparaîtront ensemble à la fin du tri.

L'exemple en-dessous trie une liste de posts par leur "rating".

{{% code file="layouts/partials/by-rating.html" %}}
```html
{{ range (.Data.Pages.ByParam "rating") }}
  <!-- ... -->
{{ end }}
```
{{% /code %}}

Si le champ front matter d'intérêt est embarqué sous un autre champ, vous pouvez aussi l'obtenir : 

{{% code file="layouts/partials/by-nested-param.html" %}}
```html
{{ range (.Data.Pages.ByParam "author.last_name") }}
  <!-- ... -->
{{ end }}
```
{{% /code %}}

### Ordre Inversé

Le tri inversé peut aussi s'appliquer à n'importe lesquelles des autres méthodes au-dessus. Voici des exemples utilisant  `ByDate` :

{{% code file="layouts/partials/by-date-reverse.html" %}}
```html
{{ range .Data.Pages.ByDate.Reverse }}
<li>
<a href="{{ .Permalink }}">{{ .Title }}</a>
<div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
</li>
{{ end }}
```
{{% /code %}}

## Groupe de Contenu

Hugo fournit quelques fonctions pour grouper des pages par Section, Section, Type, Date, etc.

### Par Champ de Page

{{% code file="layouts/partials/by-page-field.html" %}}
```html
{{ range .Data.Pages.GroupBy "Section" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```
{{% /code %}}

### Par date de Page

{{% code file="layouts/partials/by-page-date.html" %}}
```html
{{ range .Data.Pages.GroupByDate "2006-01" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```
{{% /code %}}

### Par date de publication de Page

{{% code file="layouts/partials/by-page-publish-date.html" %}}
```html
{{ range .Data.Pages.GroupByPublishDate "2006-01" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .PublishDate.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```
{{% /code %}}

### Par param de Page

{{% code file="layouts/partials/by-page-param.html" %}}
```html
{{ range .Data.Pages.GroupByParam "param_key" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```
{{% /code %}}

### Par Param de Page Param en Format Date

{{% code file="layouts/partials/by-page-param-as-date.html" %}}
```html
{{ range .Data.Pages.GroupByParamDate "param_key" "2006-01" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```
{{% /code %}}

### Clé de Tri Inversée

Le tri des groupes est exécuté par des clés en ordre alphanumérique (A–Z, 1–100) et en ordre chronologique inversé (les plus récents en premier) pour les dates.

Bien que ce soit des valeurs logiques par défaut, ce n'est pas toujours le tri désiré. Voici deux syntaxes différentes pour modifier l'ordre, les deux fonctionnant de la même façon. Vous pouvez utiliser votre syntaxe préférée.

#### Méthode Inversée

```html
{{ range (.Data.Pages.GroupBy "Section").Reverse }}
```

```html
{{ range (.Data.Pages.GroupByDate "2006-01").Reverse }}
```


#### Fournir la Direction Alternative

```html
{{ range .Data.Pages.GroupByDate "2006-01" "asc" }}
```

```html
{{ range .Data.Pages.GroupBy "Section" "desc" }}
```

### Ordre Dans les Groupes

Because Grouping returns a `{{.Key}}` and a slice of pages, all of the ordering methods listed above are available.

In the following example, groups are ordered chronologically and then content
within each group is ordered alphabetically by title.

{{% code file="layouts/partials/by-group-by-page.html" %}}
```html
{{ range .Data.Pages.GroupByDate "2006-01" "asc" }}
<h3>{{ .Key }}</h3>
<ul>
    {{ range .Pages.ByTitle }}
    <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
    </li>
    {{ end }}
</ul>
{{ end }}
```
{{% /code %}}

## Filtre et Limites des Listes

Sometimes you only want to list a subset of the available content. A common request is to only display “Posts” on the homepage. You can accomplish this with the `where` function.

### `where`

`where` works in a similar manner to the `where` keyword in SQL. It selects all elements of the array or slice that match the provided field and value. `where` takes three arguments:

1. `array` or a `slice of maps or structs`
2. `key` or `field name`
3. `match value`

{{% code file="layouts/_default/.html" %}}
```html
{{ range where .Data.Pages "Section" "post" }}
   {{ .Content }}
{{ end }}
```
{{% /code %}}

### `first`

`first` works in a similar manner to the [`limit` keyword in SQL][limitkeyword]. It reduces the array to only the `first N` elements. It takes the array and number of elements as input. `first` takes two arguments:

1. `array` or `slice of maps or structs`
2. `number of elements`

{{% code file="layout/_default/section.html" %}}
```html
{{ range first 10 .Data.Pages }}
  {{ .Render "summary" }}
{{ end }}
```
{{% /code %}}

### `first` et `where` Ensemble

Using `first` and `where` together can be very powerful:

{{% code file="first-and-where-together.html" %}}
```html
{{ range first 5 (where .Data.Pages "Section" "post") }}
   {{ .Content }}
{{ end }}
```
{{% /code %}}


[views]: /templates/views/
