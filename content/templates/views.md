---
title: Modèles de Vues de Contenu
# linktitle: Vues de Contenu
description: Hugo peut afficher d'autres vues de votre contenu, ce qui est particulièrement utile dans les vues de liste et de résumé.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
categories: [templates, modèles]
#tags: [views]
menu:
  docs:
    parent: "Templates"
    weight: 70
weight: 70
sections_weight: 70
draft: false
aliases: []
toc: true
---

Ces alternatives de **vues de contenu** sont particulièrement utiles dans les [modèles de liste][lists].

Voici les cas d'utilisation courants pour les vues de contenu :

* Vous souhaitez que le contenu de chaque type soit affiché sur la page d'accueil, mais uniquement avec des [vues de résumés] [summaries].
* Vous voulez seulement une liste à puces de votre contenu sur une [page de liste de taxonomie][taxonomylists]. Les vues font que cela est très simple en déléguant le rendu de chaque type de contenu différent au contenu lui-même.

## Créer une Vue de Contenu

Pour créer une nouvelle vue, créez un modèle dans chacun de vos différents répertoires de type de contenu avec le nom de la vue. L'exemple suivant contient une vue "li" et une vue "résumé"  pour les types de contenu `post` et `projet`. Comme vous pouvez le voir, ceux-ci sont assis aux côtés du modèle de [vue de contenu unique][single], `single.html`. Vous pouvez même fournir une vue spécifique pour un type donné et continuer à utiliser `_default/single.html` pour la vue principale.

```bash
  ▾ layouts/
    ▾ post/
        li.html
        single.html
        summary.html
    ▾ project/
        li.html
        single.html
        summary.html
```

Hugo prend également en charge un modèle de contenu par défaut à utiliser dans le cas où un modèle de vue de contenu spécifique n'a pas été fourni pour ce type. Les vues de contenu peuvent également être définies dans le répertoire `_default` et fonctionneront de la même manière que les modèles de listes et les modèles individuels qui finissent par se répercuter dans le dossier `_default` pour la question de l'ordre de recherche.

```bash
▾ layouts/
  ▾ _default/
      li.html
      single.html
      summary.html
```

## Quel Modèle sera Rendu ?

Voici l'[ordre de recherche][lookup] pour les vues de contenu :

1. `/layouts/<TYPE>/<VIEW>.html`
2. `/layouts/_default/<VIEW>.html`
3. `/themes/<THEME>/layouts/<TYPE>/<VIEW>.html`
4. `/themes/<THEME>/layouts/_default/<VIEW>.html`

## Exemple : Vue de Contenu Dans une Liste

L'exemple suivant démontre comment utiliser les vues de contenu dans vos [modèles de liste][lists].

### `list.html`

Dans cet exemple, `.Render` est transmis au modèle pour appeler la [fonction de rendu][render]. `.Render` est une fonction spéciale qui indique au contenu de se transmettre avec le modèle de vue fourni comme premier argument. Dans ce cas, le modèle va rendre la vue `summary.html` suivante :

{{% code file="layouts/_default/list.html" download="list.html" %}}
```
<main id="main">
  <div>
  <h1 id="title">{{ .Title }}</h1>
  {{ range .Data.Pages }}
    {{ .Render "summary"}}
  {{ end }}
  </div>
</main>
```
{{% /code %}}

### `summary.html`

Hugo passera l'objet entier de la page au modèle de vue `summary.html` suivant. (Voir [Variables de page][pagevars] pour une liste complète.)

{{% code file="layouts/_default/summary.html" download="summary.html" %}}
```html
<article class="post">
  <header>
    <h2><a href='{{ .Permalink }}'> {{ .Title }}</a> </h2>
    <div class="post-meta">{{ .Date.Format "Mon, Jan 2, 2006" }} - {{ .FuzzyWordCount }} Words </div>
  </header>
  {{ .Summary }}
  <footer>
  <a href='{{ .Permalink }}'><nobr>Read more →</nobr></a>
  </footer>
</article>
```
{{% /code %}}

### `li.html`

Suite à l'exemple précédent, nous pouvons modifier notre fonction de rendu pour utiliser une vue `li.html` plus petite en modifiant l'argument dans l'appel à la fonction `.Render` (c'est-à-dire, `{{ .Render "li" }}`).

{{% code file="layouts/_default/li.html" download="li.html" %}}
```html
<li>
  <a href="{{ .Permalink }}">{{ .Title }}</a>
  <div class="meta">{{ .Date.Format "Mon, Jan 2, 2006" }}</div>
</li>
```
{{% /code %}}

[lists]: /templates/listes/
[lookup]: /templates/ordre-recherche/
[pagevars]: /variables/page/
[render]: /fonctions/render/
[single]: /templates/single-page-templates/
[spf]: http://spf13.com
[spfsourceli]: https://github.com/spf13/spf13.com/blob/master/layouts/_default/li.html
[spfsourcesection]: https://github.com/spf13/spf13.com/blob/master/layouts/_default/section.html
[spfsourcesummary]: https://github.com/spf13/spf13.com/blob/master/layouts/_default/summary.html
[summaries]: /gestion-contenu/summaries/
[taxonomylists]: /templates/taxonomy-templates/