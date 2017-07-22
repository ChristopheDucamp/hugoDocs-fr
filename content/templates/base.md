---
title: Modèles de Base et Blocs
linktitle:
description: Les blocs de construction base et block vous permettent de définir l'enveloppe externe de vos modèles maîtres. (c'est-à dire le chrome de la page).
godocref: https://golang.org/pkg/text/template/#example_Template_block
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
categories: [fondamentaux, modèles]
#tags: [blocks,base, blocs]
menu:
  docs:
    parent: "Templates"
    weight: 20
weight: 20
sections_weight: 20
draft: false
aliases: [/templates/blocks/,/templates/base-templates-and-blocks/]
toc: true
---
Le mot-clé `block` vous permet de définir l'enveloppe externe de vos pages, d'un ou plusieurs modèles maîtres et ensuite de les remplir ou d'écraser des portions si nécessaire.

## Ordre de Recherche du Modèle de Base


L'[ordre de recherche][lookup] pour les modèles de base se fait comme suit :

1. `/layouts/section/<TYPE>-baseof.html`
2. `/themes/<THEME>/layouts/section/<TYPE>-baseof.html`
3. `/layouts/<TYPE>/baseof.html`
4. `/themes/<THEME>/layouts/<TYPE>/baseof.html`
5. `/layouts/section/baseof.html`
6. `/themes/<THEME>/layouts/section/baseof.html`
7. `/layouts/_default/post-baseof.html`
8. `/themes/<THEME>/layouts/_default/post-baseof.html`
9. `/layouts/_default/baseof.html`
10. `/themes/<THEME>/layouts/_default/baseof.html`

Les variables sont indiquées par un texte en majuscules défini dans `<>`. Notez que le comportement par défaut d'Hugo pour le `type` est d'hériter de la `section` sauf indication contraire.

### Exemple d'Ordre de Recherche du Modèle de Base

À titre d'exemple, supposons que votre site utilise un thème appelé "montheme" lors du rendu de la liste de sections pour une section `post`. Hugo prendra pour modèle  `layout/section/post.html` pour [restituer la section][section]. Le bloc `{{define}}` dans ce modèle indique à Hugo que le modèle est une extension d'un modèle de base.

Voici l'ordre de recherche pour le modèle de base `post` :

1. `/layouts/section/post-baseof.html`
2. `/themes/montheme/layouts/section/post-baseof.html`
3. `/layouts/post/baseof.html`
4. `/themes/montheme/layouts/post/baseof.html`
5. `/layouts/section/baseof.html`
6. `/themes/montheme/layouts/section/baseof.html`
7. `/layouts/_default/post-baseof.html`
8. `/themes/montheme/layouts/_default/post-baseof.html`
9. `/layouts/_default/baseof.html`
10. `/themes/montheme/layouts/_default/baseof.html`

## Définir le Modèle de Base

Ce qui suit définit un modèle de base simple sur `_default/baseof.html`. Parce que c'est le modèle par défaut, c'est l'enveloppe à partir de laquelle vos pages seront produites à moins que vous ne spécifiez une autre `*baseof.html` plus proche du début de l'ordre de recherche.

{{% code file='layouts/_default/baseof.html' download="baseof.html" %}}
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ block "title" . }}
      <!-- les blocks peuvent inclure le contenu par defaut. -->
      {{ .Site.Title }}
    {{ end }}</title>
  </head>
  <body>
    <!-- Code que partagent tous vos templates, comme un header -->
    {{ block "main" . }}
      <!-- la partie de la page qui commence a differer entre les modeles -->
    {{ end }}
    {{ block "footer" . }}
    <!-- plus de code partage ici, peut-etre un pied de page mais qui peut etre annule si besoin  -->
    {{ end }}
  </body>
</html>
```
{{% /code %}}

## Écraser le Modèle de Base

À partir du modèle de base ci-dessus, vous pouvez définir un [modèle de liste par défaut][hugolists]. Le modèle de liste par défaut héritera de tout le code défini ci-dessus et pourra ensuite implémenter son propre bloc `"main"` provenant de :

{{% code file="layouts/_default/list.html" download="list.html" %}}
```html
{{ define "main" }}
  <h1>Posts</h1>
  {{ range .Data.Pages }}
    <article>
      <h2>{{ .Title }}</h2>
      {{ .Content }}
    </article>
  {{ end }}
{{ end }}
```
{{% /code %}}

Ceci remplace les contenus de notre bloc "main" (vide à la base) avec quelque chose d'utile pour le modèle liste. Dans ce cas,  nous n'avons pas défini un bloc `"title"`, par conséquent les contenus de notre modèle de base demeurent inchangés dans les listes.

{{% warning %}}
Le code que vous posez en dehors des définitions du bloc peut briser votre layout. Ceci concerne même les commentaires HTML. Par exemple :


```html
<!-- un commentaire HTML apparemment inoffensif ... qui va briser votre mise en page lors de la construction -->
{{ define "main" }}
...votre code ici
{{ end }}
```
[Voir cette discussion extraite des forums de discussion Hugo.](https://discourse.gohugo.io/t/baseof-html-block-templates-and-list-types-results-in-empty-pages/5612/6)
{{% /warning %}}

Voici un exemple pour vous montrer comment vous pouvez remplacer à la fois les zones de bloc `"main"` et `"title"` à partir du modèle de base avec un code unique vers votre [modèle de page unique par défaut][singletemplate] :

{{% code file="layouts/_default/single.html" download="single.html" %}}
```html
{{ define "title" }}
  <!-- Ceci annulera l'ensemble des valeurs par defaut reglees dans baseof.html; i.e., "{{.Site.Title}}" dans l'exemple original -->
  {{ .Title }} &ndash; {{ .Site.Title }}
{{ end }}
{{ define "main" }}
  <h1>{{ .Title }}</h1>
  {{ .Content }}
{{ end }}
```
{{% /code %}}

[hugolists]: /templates/listes
[lookup]: /templates/ordre-recherche/
[section]: /templates/section-templates/
[singletemplate]: /templates/single-page-templates/
