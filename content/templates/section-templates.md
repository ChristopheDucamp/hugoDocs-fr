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
    parent: "Templates"
    weight: 40
weight: 40
sections_weight: 40
draft: false
aliases: [/templates/sections/]
toc: true
---

## Ajouter du Contenu et un Front Matter aux Modèles de Section

Pour tirer parti efficacement des modèles de page de section, vous devez d'abord comprendre l'[organisation de contenu](/gestion-contenu/organisation/) et en particulier, le but de `_index.md` pour ajouter du contenu et un front matter à la section et aux autres pages de la liste.

## Ordre de Recherche du Modèle de Section

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

Chaque `Page` dans Hugo possède un attribut  `.Kind`. `Kind` peut facilement être combiné dans vos modèles avec la fonction [`where`][where] pour créer des listes de contenu spécifiques. Cette méthode est idéale pour créer des listes, mais il y a des fois où vous souhaitez récupérer uniquement la page d'index d'une seule section via le chemin de la section.

La fonction [`.GetPage`][getpage] recherche une page d'index d'un `Kind` et d'un `path` donnés.

{{% note %}}
`.GetPage` n'est actuellement pas supporté pour saisir les fichiers de contenu unique, mais *pourra* le devenir.
{{% /note %}}

Vous pouvez appeler `.Site.GetPage` avec deux arguments : `kind` et `kind value`.

Ce sont les valeurs valides pour 'kind' :

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

L'exemple `.Site.GetPage` qui suit suppose la structure de dossiers du projet suivante :

```bash
.
└── content
    ├── blog
    │   ├── _index.md # "title: Mon Blog Hugo" dans le  front matter
    │   ├── post-1.md
    │   ├── post-2.md
    │   └── post-3.md
    └── events #Note : pas de fichier _index.md file dans  "events"
        ├── event-1.md
        └── event-2.md
```

`.Site.GetPage` renverra `nil` si aucune page `_index.md` n'est trouvée. Par conséquent, si `content/blog/_index.md` n'existe pas, le modèle sortira le nom de section : 

```html
<h1>{{ with .Site.GetPage "section" "blog" }}{{ .Title }}{{ end }}</h1>
```

Parce que `blog` a une page index de section avec front matter sur `content/blog/_index.md`, le code au-dessus renverra le résultat suivant : 

```html
<h1>Mon Blog Hugo</h1>
```

Si nous essayons le même code avec la section `events`, Hugo ira par défaut au titre de la section parce qu'il n'y a pas de `content/events/_index.md` à partir duquel tirer du contenu et un front matter : 

```html
<h1>{{ with .Site.GetPage "section" "events" }}{{ .Title }}{{ end }}</h1>
```

qui renverra alors ce qui suit : 

```html
<h1>Events</h1>
```


[contentorg]: /gestion-contenu/organisation/
[getpage]: /fonctions/getpage/
[lists]: /templates/listes/
[lookup]: /templates/ordre-recherche/
[where]: /fonctions/where/
