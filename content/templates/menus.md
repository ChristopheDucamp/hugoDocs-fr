---
title: Modèles de Menu
linktitle: Modèles de Menu
description: Les menus sont une fonctionnalité puissante mais simple pour la gestion de contenu mais ils peuvent être aisément manipulés dans vos modèles pour servir vos exigences de design.
date: 2017-02-01
publishdate: 2017-07-21
lastmod: 2017-07-19
categories: [templates, modèles]
#tags: [lists,sections,menus, listes]
menu:
  docs:
    parent: "Templates"
    weight: 130
weight: 130
sections_weight: 130
draft: false
aliases: [/templates/menu-templates, /templates/menus-templates, /templates/menu]
toc: false
---
Hugo ne fait aucune hypothèse sur la façon dont votre rendu HTML sera structuré. Au lieu de cela, il fournit toutes les fonctions dont vous avez besoin pour créer votre menu comme vous le souhaitez.

Voici un exemple : 

{{% code file="layouts/partials/sidebar.html" download="sidebar.html" %}}
```html
<!-- sidebar start -->
<aside>
    <div id="sidebar" class="nav-collapse">
        <!-- sidebar menu start-->
        <ul class="sidebar-menu">
          {{ $currentPage := . }}
          {{ range .Site.Menus.main }}
              {{ if .HasChildren }}

            <li class="sub-menu{{if $currentPage.HasMenuCurrent "main" . }} active{{end}}">
            <a href="javascript:;" class="">
                {{ .Pre }}
                <span>{{ .Name }}</span>
                <span class="menu-arrow arrow_carrot-right"></span>
            </a>
            <ul class="sub">
                {{ range .Children }}
                <li{{if $currentPage.IsMenuCurrent "main" . }} class="active"{{end}}><a href="{{.URL}}"> {{ .Name }} </a> </li>
                {{ end }}
            </ul>
          {{else}}
            <li>
            <a href="{{.URL}}">
                {{ .Pre }}
                <span>{{ .Name }}</span>
            </a>
          {{end}}
          </li>
          {{end}}
            <li> <a href="https://github.com/gohugoio/hugo/issues" target="blank">Questions and Issues</a> </li>
            <li> <a href="#" target="blank">Améliorez cette Page</a> </li>
        </ul>
        <!-- sidebar menu end-->
    </div>
</aside>
<!--sidebar end-->
```
{{% /code %}}

{{% note "`absLangURL` et `relLangURL`" %}}
Utilisez les fonctions [`absLangUrl`](/fonctions/abslangurl) ou [`relLangUrl`](/fonctions/rellangurl) si votre thème utilise la [fonctionnalité multilingue](/gestion-contenu/multilingue/). À la différence de `absURL` et `relURL`, ces deux fonctions ajoutent le préfixe correct de langue à l'url.
{{% /note %}}

## Section Menu pour Blogueurs Paresseux

Pour activer ce menu, ajoutez ce qui suit à votre fichier `config` de site :

```toml
SectionPagesMenu = "main"
```

Le nom de menu peut être tout ce que vous voulez, mais prenez note de son nom.

Ceci créera un menu avec toutes les sections sous forme d'items de menu et toutes les pages des sections sous forme de "shadow-members". Le _shadow_ sous-entend que les pages ne sont pas représentées par un item-menu en elles-même, mais ceci vous permet de créer un menu de plus haut niveau comme ceci : 

```html
<nav class="sidebar-nav">
    {{ $currentPage := . }}
    {{ range .Site.Menus.main }}
    <a class="sidebar-nav-item{{if or ($currentPage.IsMenuCurrent "main" .) ($currentPage.HasMenuCurrent "main" .) }} active{{end}}" href="{{.URL}}">{{ .Name }}</a>
    {{ end }}
</nav>
```

Dans l'exemple au-dessus, l'item menu est marqué comme actif s'il est sur la page de liste de la section actuelle ou surune page dans cette section.

Ce qui précède est tout ce qu'il faut. Mais si vous voulez des éléments de menu personnalisés, par ex. en changeant le `weight` ou le nom, vous pouvez les définir manuellement dans la configuration du site, c'est-à-dire `config.toml` :

```toml
[[menu.main]]
    name = "Voici ma section de blog"
    weight = -110
    identifier = "blog"
    url = "/blog/"
```

{{% note %}}
L'`identifier` *doit* correspondre au nom de la section.
{{% /note %}}
