---
title: Modèles de Taxonomie
# linktitle:
description: La modélisation taxonomique liste les pages, les pages de termes taxonomiques et l'utilisation de taxonomies dans vos modèles de page unique.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
categories: [templates, modèles, à relire]
#tags: [taxonomies,metadata,front matter,terms, termes, métadonnées]
menu:
  docs:
    parent: "Templates"
    weight: 50
weight: 50
sections_weight: 50
draft: false
aliases: [templates/taxonomy-templates/,/taxonomies/displaying/,/templates/terms/,/indexes/displaying/,/taxonomies/templates/,/indexes/ordering/, /templates/taxonomies/, /templates/taxonomy/]
toc: true
wip: true
---

<!-- NOTE! Regardez https://github.com/gohugoio/hugo/issues/2826 pour la migration des pages de termes vers .Data.Pages ET 
https://discourse.gohugo.io/t/how-to-specify-category-slug/4856/15 pour la discussion originale.-->

Hugo supporte les groupes de contenu définis par l'utilisateur appelés **taxonomies**. Les taxonomies sont des classifications qui démontrent des relations logiques entre le contenu. Voir [Taxonomies sous Gestion de contenu](/gestion-contenu/taxonomies) si vous n'êtes pas familier avec la façon dont Hugo exploite cette puissante fonctionnalité.

Hugo offre de multiples façons d'utiliser des taxonomies tout au long de vos modèles de projet :

* Ordonne la manière dont les termes d'une taxonomie sont affichés dans un [modèle de termes de taxonomie](#modele-termes-taxonomie)
* Trier la manière dont le contenu associé à un terme de taxonomie est affiché dans un [modèle de liste de taxonomie](#modèles-de-liste-taxonomique)
* Liste les termes de la taxonomie d'un seul contenu dans un [modèle de page unique][]

## Modèles de Liste Taxonomique 

Les modèles de liste taxononomique sont des listes et par conséquent, ils ont toutes les variables et méthodes disponibles sur les [pages de listes][lists].

### Ordre de Recherche du Modèle de Liste Taxonomique

Une taxononomie sera produite sur /`PLURAL`/`TERM`/ (par ex., http://spf13.com/topics/golang/) selon l'ordre de recherche suivant : 

1. `/layouts/taxonomy/<SINGULAR>.html`
2. `/layouts/_default/taxonomy.html`
3. `/layouts/_default/list.html`
4. `/themes/<THEME>/layouts/taxonomy/<SINGULAR>.html`
5. `/themes/<THEME>/layouts/_default/taxonomy.html`
6. `/themes/<THEME>/layouts/_default/list.html`

## Modèle de Termes de Taxonomie

### Ordre de Recherche des Modèles de Termes de Taxonomie

Une page de termes de taxonomie sera produite sur  `votresite.com/<NOMTAXONOMIEPLURIEL>`/ par ex., http://spf13.com/topics/) selon l'ordre de recherche suivant : 

1. `/layouts/taxonomy/<SINGULAR>.terms.html`
2. `/layouts/_default/terms.html`
3. `/themes/<THEME>/layouts/taxonomy/<SINGULAR>.terms.html`
4. `/themes/<THEME>/layouts/_default/terms.html`

{{% warning "The Taxonomy Terms Template has a Unique Lookup Order" %}}
Si Hugo ne trouve pas un modèle de temes dans `layout/` ou `/themes/<THEME>/layouts/`, Hugo ne produira *pas* une page de termes de taxonomie.
{{% /warning %}}

<!-- Begin /taxonomies/methods/ -->
Hugo prend un ensemble de valeurs et méthodes sur les différentes structures de Taxononomie.

### Méthodes de Taxonomie

Une Taxononomie est une `map[string]WeightedPages`.

**.Get(term)**
: Renvoie les WeightedPages pour un terme.

**.Count(term)**
: Le nombre d'éléments de contenus assignées à ce terme.

**.Alphabetical**
: Renvoie une OrderedTaxonomy (slice) triée par terme.

**.ByCount**
: Renvoie une OrderedTaxonomy (slice) triée par nombre d'entrées.

### OrderedTaxonomy

Parce que les Maps ne sont pas ordonnées, une OrderedTaxonomy est une structure spéciale qui a un ordre défini.

```go
[]struct {
    Name          string
    WeightedPages WeightedPages
}
```

Chaque élément de la slice a : 

**.Term**
: Le terme utilisé.

**.WeightedPages**
: Une slice de Weighted Pages.

**.Count**
: Le nombre d'éléments de contenu assignées à ce terme.

**.Pages**
: Toutes les Pages assignées à ce terme. Toutes les [méthodes de liste][renderlists] sont disponibles pour ça.

## WeightedPages

WeightedPages est simplement une slice de WeightedPage.

```go
type WeightedPages []WeightedPage
```

**.Count(term)**
: Le nombre d'éléments de contenu assignées à ce terme.

.Pages
: Renvoie une slice de pages, qui peuvent être ensuite triées en utilisant n'importe laquelle des [méthodes de liste][renderlists].

<!-- Begin /taxonomies/ordering/ -->

## Ordonner les Taxonomies

Les taxonomies peuvent être classées soit par la clé alphabétique, soit par le nombre d'éléments de contenu attribuées à cette clé.

### Exemple de Classement Alphabétique

```html
<ul>
  {{ $data := .Data }}
  {{ range $key, $value := .Data.Taxonomy.Alphabetical }}
  <li><a href="{{ $.Site.LanguagePrefix }}/{{ $data.Plural }}/{{ $value.Name | urlize }}"> {{ $value.Name }} </a> {{ $value.Count }} </li>
  {{ end }}
</ul>
```

### Exemple de Classement par Popularité

```html
<ul>
  {{ $data := .Data }}
  {{ range $key, $value := .Data.Taxonomy.ByCount }}
  <li><a href="{{ $.Site.LanguagePrefix }}/{{ $data.Plural }}/{{ $value.Name | urlize }}"> {{ $value.Name }} </a> {{ $value.Count }} </li>
  {{ end }}
</ul>
```

<!-- [See Also Taxonomy Lists](/templates/list/) -->

## Ordonner le Contenu dans les Taxonomies

Hugo utilise à la fois `date` et `weight` pour ordonner le contenu dans les taxonomies.

Chaque élément de contenu dans Hugo peut éventuellement être affectée à une date. On peut également attribuer un poids pour chaque taxonomie à laquelle il est affecté.

En itérant sur le contenu dans les taxonomies, le tri par défaut est le même que celui utilisé pour les [sections pages de liste][section and list pages] d'abord par poids puis par date. Cela signifie que si les poids pour deux éléments de contenu sont identiques, le contenu le plus récent sera affiché en premier. Le poids par défaut pour tout élément de contenu est 0.


### Assigner un Poids

Le contenu peut se voir assigner un poids `weight`pour chaque taxonomie à laquelle il est affecté.

```toml
+++
tags = [ "a", "b", "c" ]
tags_weight = 22
categories = ["d"]
title = "foo"
categories_weight = 44
+++
Front Matter with weighted tags and categories
```

La convention est `nomtaxonomie_weight`.

Dans l'exemple ci-dessus, ce contenu a un poids de 22 qui s'applique au tri lors du rendu des pages assignée aux valeurs "a", "b" et "c" de la taxonomie 'tag'.

On lui a également attribué le poids de 44 lors du rendu de la catégorie 'd'.

Avec cela, le même contenu peut apparaître dans différentes positions dans différentes taxonomies.

Actuellement, les taxonomies ne supportent que la commande par défaut du contenu qui est weight -> date.

<!-- Begin /taxonomies/templates/ -->

Il existe deux modèles différents que l'utilisation des taxonomies exigera que vous fournissiez.

Les deux modèles sont détaillés dans la section des modèles.

Un [modèle de liste](/templates/list/) est n'importe quel modèle qui sera utilisé pour rendre plusieurs éléments de contenu dans une seule page html. Ce modèle sera utilisé pour générer toutes les pages de taxonomie créées automatiquement.

Un [modèle de termes de taxonomie](/templates/terms) est un modèle utilisé pour générer la liste des termes d'un modèle donné.

<!-- Begin /taxonomies/displaying/ -->

Il existe quatre façons communes d'afficher les données dans vos taxonomies en plus des pages de taxonomie automatique créées par hugo en utilisant les [modèles de liste](/templates/lists) :

1. Pour un contenu donné, vous pouvez énumérer les termes attachés
2. Pour un contenu donné, vous pouvez énumérer d'autres contenus avec le même terme
3. Vous pouvez lister tous les termes pour une taxonomie
4. Vous pouvez lister toutes les taxonomies (avec leurs termes)

## Afficher les Taxonomie d'un Élément Unique de Contenu

Dans vos modèles de contenu, vous pouvez afficher les taxonomies auxquelles cet élément de contenu est assigné.

Parce que nous exploitons le système de front matter pour définir des taxonomies pour le contenu, les taxonomies attribuées à chaque élément de contenu sont situées à l'endroit  habituel (c'est-à-dire ``.Params.<TAXONOMYPLURAL>`).

### Exemple : Liste de Tags Dans un Modèle de Page Unique

```html
<ul id="tags">
  {{ range .Params.tags }}
    <li><a href="{{ "/tags/" | relLangURL }}{{ . | urlize }}">{{ . }}</a> </li>
  {{ end }}
</ul>
```

Si vous souhaitez lister les taxonomies dans la ligne, vous devrez prendre en charge les terminaisons multiples facultatives dans le titre (si plusieurs taxonomies), ainsi que les virgules. Disons que nous avons une taxonomie "réalisateurs" telle que : `realisateurs: ["Joel Coen", "Ethan Coen"]` dans le front matter au format TOML.

Pour lister de telles taxonomies, utilisez ce qui suit : 

### Exemple : Tags délimités-par-virgule dans un Modèle de Page Unique

```html
{{ if .Params.realisateurs }}
  <strong>Réalisateur{{ if gt (len Params.realisateurs) 1 }}s{{ end }}:</strong>
  {{ range $index, $realisateur := .Params.realisateurs }}{{ if gt $index 0 }}, {{ end }}<a href="{{ "realisateurs/" | relURL }}{{ . | urlize }}">{{ . }}</a>{{ end }}
{{ end }}
```

Alternativement, vous pouvez utiliser la [fonction de modèle delimit][delimit] comme raccourci si les taxonomies devaient être simplement listées avec un séparateur. Voir {{< gh 2143 >}} sur GitHub pour discussion.

## Lister le Contenu avec le Même Terme de Taxonomie

Si vous utilisez une taxonomie pour quelque chose comme une série de publications, vous pouvez répertorier les pages individuelles associées à la même taxonomie. C'est aussi une méthode rapide et sale pour afficher le contenu connexe :

### Exemple : Afficher le Contenu dans la Même Série

```html
<ul>
  {{ range .Site.Taxonomies.series.golang }}
    <li><a href="{{ .Page.RelPermalink }}">{{ .Page.Title }}</a></li>
  {{ end }}
</ul>
```

## Lister Tous les Contenus d'une Taxonomie Donnée

Ceci serait très utile dans une barre latérale comme "contenus à la une". Vous pourriez même avoir différentes sections de "contenus à la une" en assignant différents termes au contenu.

### Exemple : Grouper le Contenu "À la Une"

```html
<section id="menu">
    <ul>
        {{ range $key, $taxonomy := .Site.Taxonomies.featured }}
        <li> {{ $key }} </li>
        <ul>
            {{ range $taxonomy.Pages }}
            <li hugo-nav="{{ .RelPermalink}}"><a href="{{ .Permalink}}"> {{ .LinkTitle }} </a> </li>
            {{ end }}
        </ul>
        {{ end }}
    </ul>
</section>
```

## Produire une Taxonomie de Site

Si vous souhaitez afficher la liste de toutes les clés pour la taxonomie de votre site, vous pouvez les récupérer à partir de la variable [`.Site`][sitevars] disponible sur chaque page.

Cela peut prendre la forme d'un nuage de mots-clés, d'un menu ou simplement d'une liste.

L'exemple suivant affiche tous les termes de la taxonomie des tags d'un site :

### Exemple : Lister Tous les Tags d'un Site

```html
<ul id="all-tags">
  {{ range $name, $taxonomy := .Site.Taxonomies.tags }}
    <li><a href="{{ "/tags/" | relLangURL }}{{ $name | urlize }}">{{ $name }}</a></li>
  {{ end }}
</ul>
```

### Exemple : Lister Toutes les Taxonomies, Termes, et Contenu Assigné

Cet exemple répertorie toutes les taxonomies et leurs termes, ainsi que tout le contenu attribué à chacun des termes.

{{% code file="layouts/partials/all-taxonomies.html" download="all-taxonomies.html" download="all-taxonomies.html" %}}
```html
<section>
  <ul id="all-taxonomies">
    {{ range $taxonomyname, $taxonomy := .Site.Taxonomies }}
      <li><a href="{{ "/" | relLangURL}}{{ $taxonomyname | urlize }}">{{ $taxonomyname }}</a>
        <ul>
          {{ range $key, $value := $taxonomy }}
          <li> {{ $key }} </li>
                <ul>
                {{ range $value.Pages }}
                    <li hugo-nav="{{ .RelPermalink}}"><a href="{{ .Permalink}}"> {{ .LinkTitle }} </a> </li>
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

## `.Site.GetPage` pour les Taxonomies

Parce que les taxonomies sont des listes, la fonction [`.GetPage`][getpage] peut être utilisée pour obtenir toutes les pages associées à un terme de taxonomie particulier en utilisant une syntaxe douteuse. Les plages suivantes sur la liste complète des tags sur votre site et les liens vers chacune des pages de taxonomie individuelles pour chaque terme sans avoir à utiliser la construction d'URL plus fragile de l'exemple "Liste de tous les tags du site" ci-dessus :

{{% code file="links-to-all-tags" %}}
```html
<ul class="tags">
  {{ range ($.Site.GetPage "taxonomyTerm" "tags").Pages }}
   <li><a href="{{ .Permalink }}">{{ .Title}}</a></li>
  {{ end }}
</ul>
```
{{% /code %}}

<!--### `.Site.GetPage` Exemple de Liste Taxonomie

### `.Site.GetPage` Taxonomy Terms Example -->


[delimit]: /fonctions/delimit/
[getpage]: /fonctions/getpage/
[lists]: /templates/lists/
[renderlists]: /templates/lists/
[modèle de page unique]: /templates/single-page-templates/
[sitevars]: /variables/site/
