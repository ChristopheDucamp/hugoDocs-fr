---
title: Table des Matières
linktitle:
description: Hugo sait automatiquement analyser le contenu Markdown et créer une Table des Matières que vous pouvez utiliser dans vos modèles.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [gestion de contenu]
#tags: [table des matières, table of contents, toc]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 130
weight: 130	#rem
draft: false
aliases: []
toc: true
---

{{% note %}}
Actuellement, la [variable de page](/variables/page/) `{{.TableOfContents}}` ne vous permet pas de spécifier quels niveaux de titres vous voulez afficher dans la TDM. [Voir la discussion en rapport sur GitHub (#1778)](https://github.com/gohugoio/hugo/issues/1778). En tant que telle, la `<nav id="TableOfContents"><ul></ul></nav>` commencera sur `<h1>` au moment d'extraire à partir de `{{.Content}}`.
{{% /note %}}

## Usage

Créez votre markdown comme vous le feriez normalement avec les titres appropriés. Voici un exemple de contenu :


```md
<!-- Votre front matter en place ici -->

## Introduction

One morning, when Gregor Samsa woke from troubled dreams, he found himself transformed in his bed into a horrible vermin.

## Mon Titre

He lay on his armour-like back, and if he lifted his head a little he could see his brown belly, slightly domed and divided by arches into stiff sections. The bedding was hardly able to cover it and seemed ready to slide off any moment.

### Mon Sous-Titre

A collection of textile samples lay spread out on the table - Samsa was a travelling salesman - and above it there hung a picture that he had recently cut out of an illustrated magazine and housed in a nice, gilded frame. It showed a lady fitted out with a fur hat and fur boa who sat upright, raising a heavy fur muff that covered the whole of her lower arm towards the viewer. Gregor then turned to look out the window at the dull weather. Drops
```

Hugo prendra ce Markdown et créera une table des matières à partir de `## Introduction`,` ## Mon Titre` et `### Mon Sous-Titre`, puis le stockera dans [la variable de page](/variables/page/)` .TableOfContents`.

Les outputs des variables intégrées `.TableOfContents` produisent un élément `<nav id="TableOfContents">` avec un enfant `<ul>`, dont les éléments `<li>` de l'enfant commencent par n'importe quel `<h1>`s (c'est-à-dire en markdown `#`) dans votre contenu.

## Exemple de Modèle : TDM Basique

Voici un exemple d'un modèle très basique de [modèle de page unique][single page template] :

{{% code file="layout/_default/single.html" download="single.html" %}}
```html
{{ define "main" }}
<main>
    <article>
    <header>
        <h1>{{ .Title }}</h1>
    </header>
        {{ .Content }}
    </article>
    <aside>
        {{ .TableOfContents }}
    </aside>
</main>
{{ end }}
```
{{% /code %}}

## Exemple de Modèle : TDM Partielle

Voici un [modèle partiel][partiels] qui ajoute un peu plus de logique pour le contrôle au niveau de la page sur votre table des matières. Il suppose que vous utilisez un champ `toc` dans le [front matter][] de votre contenu qui, à moins que ce ne soit  spécifiquement configuré sur `false`, ajoute une TOC à n'importe quelle page avec un `.WordCount` (voir [Variables de page](variables/page/) supérieur à 400. Cet exemple montre également comment utiliser [les conditionnels][conditionals] dans votre modèle :

{{% code file="layouts/partials/toc.html" download="toc.html" %}}
```html
{{ if and (gt .WordCount 400 ) (ne .Params.toc "false") }}
<aside>
    <header>
    <h2>{{.Title}}</h2>
    </header>
    {{.TableOfContents}}
</aside>
{{ end }}
```
{{% /code %}}

{{% note %}}
Avec l'exemple précédent, même les pages avec > 400 mots *et* `toc` non réglées sur` false` ne rendront pas une table des matières s'il n'y a pas de titre dans la page pour la variable `{{.TableOfContents}}` à extraire{{% /note %}}

[conditionals]: /templates/introduction/#conditionnels
[front matter]: /gestion-contenu/table-des-matieres/
[partiels]: /templates/partiels/
[single page template]: /templates/single-page-templates/

