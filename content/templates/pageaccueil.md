---
title: Modèle Page Accueil
linktitle: Modèle Page Accueil
description: La page d'accueil d'un site web est souvent mise en page différemment des autres pages. Pour cette raison, Hugo facilite la définition de votre page d'accueil de nouveau site comme un modèle unique.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [templates, modèles]
#tags: [homepage, page d'accueil]
menu:
  docs:
    parent: "Templates"
    weight: 30
weight: 30
sections_weight: 30
draft: false
aliases: [templates/homepage,/layout/homepage/,/templates/homepage-template/]
toc: true
---

La page d'accueil est une `Page` et par conséquent elle dispose de toutes les [variables de page][pagevars] et [variables de site][sitevars] disponibles pour utilisation.

{{% note "Le Seul Modèle Requis" %}}
Le modèle de la page d'accueil est le *seul* modèle requis pour la construction d'un site et donc utile lors du démarrage d'un nouveau site et d'un nouveau modèle. Il est également le seul modèle requis si vous développez un site Web à page unique.
{{% /note %}}

## Ordre de Recherche du Modèle de Page d'Accueil

L'[ordre de recherche][lookup] pour le modèle de page d'accueil est le suivant : 

1. `/layouts/index.html`
2. `/layouts/_default/list.html`
3. `/themes/<THEME>/layouts/index.html`
4. `/themes/<THEME>/layouts/_default/list.html`

## Ajouter du Contenu et un Front Matter à la Page d'Accueil

La page d'accueil, similaire à d'autres [pages de liste dans Hugo][listes], accepte le contenu et le front matter à partir d'un fichier `_index.md`. Ce fichier devrait être à la racine de votre dossier `content` (c'est-à-dire `content/_index.md`). Vous pouvez ensuite ajouter des copies de body et de métadonnées à votre page d'accueil de la façon dont vous le feriez pour tout autre fichier de contenu.

Consultez le modèle de la page d'accueil ci-dessous ou [Organisation de Contenu][contentorg] pour plus d'informations sur le rôle de `_index.md` dans l'ajout de contenu et de front matter pour lister les pages.

## `.Data.Pages` sur la Page d'Accueil

En plus des [variables de page][pagevars] standards, le modèle de page d'accueil a accès à *tout* le contenu du site via `.Data.Pages`.

## Exemple de Modèle de Page d'Accueil

Voici un exemple d'un modèle de page d'accueil utilisant des modèles [partiels][partiels], [base][] et un fichier de contenu sur `content/_index.md` pour remplir les [variables de page][pagevars] `{{.Title}}` et `{{Content}}`.

{{% code file="layouts/index.html" download="index.html" %}}
```html
{{ define "main" }}
    <main aria-role="main">
      <header class="homepage-header">
        <h1>{{.Title}}</h1>
        {{ with .Params.subtitle }}
        <span class="subtitle">{{.}}</span>
        {{ end }}
      </header>
      <div class="homepage-content">
        <!-- Note that the content for index.html, as a sort of list page, will pull from content/_index.md -->
        {{.Content}}
      </div>
      <div>
        <!-- Note that .Data.Pages is the equivalent of .Site.Pages on the homepage template. -->
        {{ range first 10 .Data.Pages }}
            {{ .Render "summary"}}
        {{ end }}
      </div>
    </main>
{{ end }}
```
{{% /code %}}

[base]: /templates/base/
[contentorg]: /gestion-contenu/organisation/
[listes]: /templates/listes/
[lookup]: /templates/ordre-recherche/
[pagevars]: /variables/page/
[partiels]: /templates/partiels/
[sitevars]: /variables/site/
