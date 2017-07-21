---
title: Modèles de Page de Section
linktitle: Modèles de Section 
description: Les modèles utilisés pour les pages de section sont des **listes** et ils ont donc toutes les variables et méthodes disponibles pour les pages de listes.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-20
categories: [templates, modèles]
#tags: [lists,sections]
menu:
  docs:
    parent: "templates"
    weight: 40
weight: 40
sections_weight: 40
draft: false
aliases: [/templates/sections/]
toc: true
---

## Ajouter du Contenu et un Front Matter aux Modèles de Section

Pour tirer parti efficacement des modèles de page de section, vous devez d'abord comprendre l'[organisation de contenu](/gestion-contenu/organisation/) et en particulier, le but de `_index.md` pour ajouter du contenu et un front matter à la section et aux autres pages de la liste.

## Odre de Recherche du Modèle de Section

Voici l'[ordre de recherche][lookup] pour les modèles de section 

1. `/layouts/section/<SECTION>.html`
2. `/layouts/<SECTION>/list.html`
3. `/layouts/_default/section.html`
4. `/layouts/_default/list.html`
5. `/themes/<THEME>/layouts/section/<SECTION>.html`
6. `/themes/<THEME>/layouts/<SECTION>/list.html`
7. `/themes/<THEME>/layouts/_default/section.html`
8. `/themes/<THEME>/layouts/_default/list.html`

## `.Site.GetPage` avec Sections

Every `Page` in Hugo has a `.Kind` attribute. `Kind` can easily be combined with the [`where` function][where] in your templates to create kind-specific lists of content. This method is ideal for creating lists, but there are times where you may want to fetch just the index page of a single section via the section's path.

The [`.GetPage` function][getpage] looks up an index page of a given `Kind` and `path`.

{{% note %}}
`.GetPage` is not currently supported to grab single content files but *may* be supported in the future.
{{% /note %}}

You can call `.Site.GetPage` with two arguments: `kind` and `kind value`.

These are the valid values for 'kind':

1. `home`
2. `section`
3. `taxonomy`
4. `taxonomyTerm`


## Exemple : Créer un Modèle de Section par Défaut

{{% code file="layouts/_default/section.html" download="section.html" %}}
```html
{{ define "main" }}
  <main>
      {{ .Content }}
          <ul class="contents">
          {{ range .Paginator.Pages }}
              <li>{{.Title}}
                  <div>
                    {{ partial "summary.html" . }}
                  </div>
              </li>
          {{ end }}
          </ul>
      {{ partial "pagination.html" . }}
  </main>
{{ end }}
```
{{% /code %}}

### Exemple : Utiliser `.Site.GetPage`

The `.Site.GetPage` example that follows assumes the following project directory structure:

```bash
.
└── content
    ├── blog
    │   ├── _index.md # "title: My Hugo Blog" in the front matter
    │   ├── post-1.md
    │   ├── post-2.md
    │   └── post-3.md
    └── events #Note there is no _index.md file in "events"
        ├── event-1.md
        └── event-2.md
```

`.Site.GetPage` will return `nil` if no `_index.md` page is found. Therefore, if `content/blog/_index.md` does not exist, the template will output the section name:

```html
<h1>{{ with .Site.GetPage "section" "blog" }}{{ .Title }}{{ end }}</h1>
```

Since `blog` has a section index page with front matter at `content/blog/_index.md`, the above code will return the following result:

```html
<h1>My Hugo Blog</h1>
```

If we try the same code with the `events` section, however, Hugo will default to the section title because there is no `content/events/_index.md` from which to pull content and front matter:

```html
<h1>{{ with .Site.GetPage "section" "events" }}{{ .Title }}{{ end }}</h1>
```

Which then returns the following:

```html
<h1>Events</h1>
```


[contentorg]: /gestion-contenu/organisation/
[getpage]: /fonctions/getpage/
[lists]: /templates/lists/
[lookup]: /templates/lookup-order/
[where]: /fonctions/where/
