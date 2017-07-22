---
title: Modèles de Page Unique
linktitle:
description: La vue primaire du contenu dans Hugo est la vue unique. Hugo rendra chaque fichier Markdown fourni avec un modèle unique correspondant.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [templates, modèles]
#tags: [page]
menu:
  docs:
    parent: "Templates"
    weight: 60
weight: 60
sections_weight: 60
draft: false
aliases: [/layout/content/]
toc: true
---

## Ordre de Recherche de Modèle de Page Unique

Vous pouvez spécifier le [type de contenu][content type] et le `layout` dans un fichier de contenu [front matter][]. Toutefois, vous ne pouvez pas spécifier `section` car cela est déterminé en fonction de l'emplacement du fichier (voir [section contenu] [section]).

Hugo suppose que votre section de contenu et le type de contenu sont les mêmes, à moins que vous ne le dites à Hugo en fournissant un `type` directement dans le front matter d'un fichier de contenu. C'est pourquoi #1 et #3 arrivent avant #2 et #4, respectivement, dans la commande de recherche suivante. Les valeurs entre crochets (`<>`) sont variables.

1. `/layouts/<TYPE>/<LAYOUT>.html`
2. `/layouts/<SECTION>>/<LAYOUT>.html`
3. `/layouts/<TYPE>/single.html`
4. `/layouts/<SECTION>/single.html`
5. `/layouts/_default/single.html`
6. `/themes/<THEME>/layouts/<TYPE>/<LAYOUT>.html`
7. `/themes/<THEME>/layouts/<SECTION>/<LAYOUT>.html`
8. `/themes/<THEME>/layouts/<TYPE>/single.html`
9. `/themes/<THEME>/layouts/<SECTION>/single.html`
10. `/themes/<THEME>/layouts/_default/single.html`

## Exemple de Modèles de Page Unique

Les pages de contenu sont du type `page` et auront donc toutes les [variables de page][pagevars] et [variables de site][site variables] disponibles dans leurs modèles.

### `post/single.html`

Ce modèle de page unique utilise  les [modèles de base][base templates] de Hugo, la [fonction `.Format`][`.Format` function] pour les dates, la variable de page [`.WordCount`][pagevars] et varie selon les [taxonomies][pagetaxonomy] spécifiques du contenu unique. [`with`][] est également utilisé pour vérifier si les taxonomies sont définies dans le front matter.

{{% code file="layouts/post/single.html" download="single.html" %}}
```html
{{ define "main" }}
<section id="main">
  <h1 id="title">{{ .Title }}</h1>
  <div>
        <article id="content">
           {{ .Content }}
        </article>
  </div>
</section>
<aside id="meta">
    <div>
    <section>
      <h4 id="date"> {{ .Date.Format "Mon Jan 2, 2006" }} </h4>
      <h5 id="wordcount"> {{ .WordCount }} Words </h5>
    </section>
    {{ with .Params.topics }}
    <ul id="topics">
      {{ range . }}
        <li><a href="{{ "topics" | absURL}}{{ . | urlize }}">{{ . }}</a> </li>
      {{ end }}
    </ul>
    {{ end }}
    {{ with .Params.tags }}
    <ul id="tags">
      {{ range . }}
        <li> <a href="{{ "tags" | absURL }}{{ . | urlize }}">{{ . }}</a> </li>
      {{ end }}
    </ul>
    {{ end }}
    </div>
    <div>
        {{ with .PrevInSection }}
          <a class="previous" href="{{.Permalink}}"> {{.Title}}</a>
        {{ end }}
        {{ with .NextInSection }}
          <a class="next" href="{{.Permalink}}"> {{.Title}}</a>
        {{ end }}
    </div>
</aside>
{{ end }}
```
{{% /code %}}

Pour générer facilement de nouvelles instances d'un type de contenu (par exemple, les nouveaux fichiers `.md` dans une section comme `project/`) avec un front matter préconfiguré, utilisez les [archétypes de contenu][archetypes].

[archetypes]: /gestion-contenu/archetypes/
[base templates]: /templates/base/
[config]: /demarrage/configuration/
[content type]: /gestion-contenu/types/
[directory structure]: /demarrage/structure-dossier/
[dry]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[`.Format` function]: /fonctions/format/
[front matter]: /gestion-contenu/front-matter/
[pagetaxonomy]: /templates/taxonomie-templates/#displaying-a-single-piece-of-content-s-taxonomies
[pagevars]: /variables/page/
[partials]: /templates/partials/
[section]: /gestion-contenu/sections/
[site variables]: /variables/site/
[spf13]: http://spf13.com/
[`with`]: /fonctions/with/