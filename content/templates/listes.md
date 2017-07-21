---
title: Listes de Contenu dans Hugo
linktitle: Modèles de Pages Liste
description: Les listes ont un sens et un usage spécifique dans Hugo quand elles parviennent à produire votre page d'accueil,  site, une section de page, une liste taxononomique ou une liste  taxonomique de termes.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
categories: [templates, modèles, à relire]
#tags: [lists,sections,rss,taxonomies,terms, termes, listes]
menu:
  docs:
    parent: "templates"
    weight: 22
weight: 22
sections_weight: 22
draft: false
aliases: [/templates/lists, /template/lists/,/templates/list/,/layout/indexes/]
toc: true
---

## Qu'est-ce qu'un Modèle de Page de Liste ?

Un modèle de page de liste est un modèle utilisé pour rendre plusieurs éléments de contenu dans une seule page HTML. L'exception à cette règle est la page d'accueil, qui est toujours une liste, mais dispose de son propre [modèle dédié][homepage].

Hugo utilise le terme *list* dans son vrai sens ; c'est-à-dire une disposition séquentielle du contenu, en particulier dans l'ordre alphabétique ou numérique. Hugo utilise des modèles de liste sur n'importe quelle page HTML de sortie où le contenu est traditionnellement répertorié :

* [Pages de termes de taxonomie][taxterms]
* [Pages de liste de taxonomie][taxlists]
* [Pages de liste de sections][sectiontemps]
* [RSS][rss]

L'idée d'une page de liste provient du  [modèle mental hiérarchique du web][mentalmodel] et il est mieux démontré visuellement :

![Image démontrant une carte de site hiérarchique d'un site web.](/images/site-hierarchy.svg)

## List : les Paramètres par Défaut

### Modèles par Défaut

Puisque les listes de sections et les listes de taxonomie (N.B. *pas* les [listes de termes de taxonomie][taxterms]) sont à la fois des *listes* en ce qui concerne leurs modèles, les deux ont la même terminaison par défaut `_default/list.html` ou `themes/<THEME>/layouts/_default/list.html` dans leur ordre de recherche. En outre, tant les [listes de sections][sectiontemps]  et les [listes de taxonomie][taxlists] disposent de leurs propres modèles de liste par défaut dans `_default` :

#### Modèles de Section par Défaut

1. `layouts/_default/section.html`
2. `layouts/_default/list.html`

#### Modèles de Liste de Taxonomie par Défaut

1. `layouts/_default/taxonomy.html`
2. `themes/<THEME>/layouts/_default/taxonomy.html`

## Ajouter du Contenu et un Front Matter aux Pages de Liste

Depuis la v0.18, [tout dans Hugo est une `Page`][bepsays]. Cela signifie que les pages de liste et la page d'accueil peuvent contenir des fichiers de contenu associés (c'est-à-dire `_index.md`) qui contiennent des métadonnées de page (c'est-à-dire le front matter) et le contenu.

Ce nouveau modèle vous permet d'inclure des informations frontales spécifiques à la liste via `.Params` et signifie également que les modèles de liste (par exemple,` layouts / _default / list.html`) ont accès à toutes [variables de page] [pagevars].

{{% note %}}
Il est important de noter que tous les fichiers de contenu `_index.md` seront rendus en fonction d'un modèle *list* et non selon un [modèle de page unique](/templates/single-page-templates/).
{{% /note %}}

### Exemple de Dossier Projet

Ce qui suit est un exemple d'un contenu de dossier typique de projet Hugo : 

```bash
.
...
├── content
|   ├── post
|   |   ├── _index.md
|   |   ├── post-01.md
|   |   └── post-02.md
|   └── quote
|   |   ├── quote-01.md
|   |   └── quote-02.md
...
```

En utilisant l'exemple au-dessus, supposons que nous ayons ce qui suit dans `content/post/_index.md`:

{{% code file="content/post/_index.md" %}}
```yaml
---
title: Mon Voyage Golang
date: 2017-03-23
publishdate: 2017-03-24
---

J'ai décidé de commencer à apprendre Golang en Juillet 2017.

Suivez mon voyage sur ce nouveau blog.
```
{{% /code %}}

Vous pouvez désormais accéder à ce contenu des `_index.md` dans votre modèle de liste :

{{% code file="layouts/_default/list.html" download="list.html" %}}
```html
{{ define "main" }}
<main>
    <article>
        <header>
            <h1>{{.Title}}</h1>
        </header>
        <!-- "{{.Content}}" pulls from the markdown content of the corresponding _index.md -->
        {{.Content}}
    </article>
    <ul>
    <!-- Ranges through content/post/*.md -->
    {{ range .Data.Pages }}
        <li>
            <a href="{{.Permalink}}">{{.Date.Format "2006-01-02"}} | {{.Title}}</a
        </li>
    {{ end }}
    </ul>
</main>
{{ end }}
```
{{% /code %}}

Ceci au-dessus sortira le HTML qui suit : 

{{% code file="yoursite.com/post/index.html" copy="false" %}}
```html
<!--top of your baseof code-->
<main>
    <article>
        <header>
            <h1>Mon Voyage Golang</h1>
        </header>
        <p>J'ai décidé de commencer à apprendre Golang en Juillet 2017.</p>
        <p>Suivez mon voyage sur ce nouveau blog.</p>
    </article>
    <ul>
        <li><a href="/post/post-01/">Post 1</a></li>
        <li><a href="/post/post-02/">Post 2</a></li>
    </ul>
</main>
<!--bottom of your baseof-->
```
{{% /code %}}

### Liste de Pages Sans `_index.md`

Vous ne devez *pas* créer un fichier `_index.md` pour chaque liste de pages (c-a-d. section, taxonomie, termes de taxonomie, etc) ou la page d'accueil. Si Hugo ne trouve pas un `_index.md` dans la section de contenu respective au moment de produire un modèle de liste, la page sera créée sans le `{{.Content}}` et seulemetn avec les valeurs par défaut pour le `.Title` etc.

L'utilisation de ce même modèle `layouts/_default/list.html` et l'application à la section `quotes` ci-dessus rendra la sortie suivante. Notez que `quotes` n'a pas de fichier` _index.md` à extraire de :

{{% code file="yoursite.com/quote/index.html" copy="false" %}}
```html
<!--baseof-->
<main>
    <article>
        <header>
        <!-- Hugo assumes that .Title is the name of the section since there is no _index.md content file from which to pull a "title:" field -->
            <h1>Quotes</h1>
        </header>
    </article>
    <ul>
        <li><a href="https://yoursite.com/quote/quotes-01/">Quote 1</a></li>
        <li><a href="https://yoursite.com/quote/quotes-02/">Quote 2</a></li>
    </ul>
</main>
<!--baseof-->
```
{{% /code %}}

{{% note %}}
Le comportement par défaut de Hugo est de plurieliser les titres de liste ; d'où l'inflexion de la section `quote` vers "Quotes" lorsqu'elle est appelée avec `.Title` [variable de page](/variables/page/). Vous pouvez changer cela via la directive `pluralizeListTitles` dans votre [configuration de site](/demarrage/configuration/).
{{% /note %}}

## Exemple de Modèles de Liste

### Modèle Section

Ce modèle de liste a été légèrement modifié à partir d'un modèle utilisé à l'origine dans [spf13.com](http://spf13.com/). Il utilise les [modèles partiels][partials] pour le chrome de la page rendue plutôt que d'utiliser un [modèle de base][base]. Les exemples qui suivent utilisent également les [modèles de vue de contenu][views] `li.html` ou `summary.html`.

{{% code file="layouts/section/post.html" %}}
```html
{{ partial "header.html" . }}
{{ partial "subheader.html" . }}
<main>
  <div>
   <h1>{{ .Title }}</h1>
        <ul>
        <!-- Renders the li.html content view for each content/post/*.md -->
            {{ range .Data.Pages }}
                {{ .Render "li"}}
            {{ end }}
        </ul>
  </div>
</main>
{{ partial "footer.html" . }}
```
{{% /code %}}

### Modèle de Taxonomie

{{% code file="layouts/_default/taxonomies.html" download="taxonomies.html" %}}
```html
{{ define "main" }}
<main>
  <div>
   <h1>{{ .Title }}</h1>
   <!-- ranges through each of the content files associated with a particular taxonomy term and renders the summary.html content view -->
    {{ range .Data.Pages }}
        {{ .Render "summary"}}
    {{ end }}
  </div>
</main>
{{ end }}
```
{{% /code %}}

## Ordre du Contenu

Les listes Hugo rendent le contenu en fonction des métadonnées que vous fournissez dans [front matter][]. En plus des valeurs par défaut correctes, Hugo est également livré avec de multiples méthodes pour faire un travail rapide de tri du contenu dans les modèles de liste :

### Liste Ordonnée par Défaut : Weight > Date

{{% code file="layouts/partials/default-order.html" %}}
```html
<ul>
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
<ul>
    {{ range .Data.Pages.ByWeight }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Date

{{% code file="layouts/partials/by-date.html" %}}
```html
<ul>
    <!-- ordonne le contenu selon le champ "date" dans le front matter -->
    {{ range .Data.Pages.ByDate }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Date de Publication

{{% code file="layouts/partials/by-publish-date.html" %}}
```html
<ul>
    <!-- orders content according to the "publishdate" field in front matter -->
    {{ range .Data.Pages.ByPublishDate }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Date d'Expiration

{{% code file="layouts/partials/by-expiry-date.html" %}}
```html
<ul>
    {{ range .Data.Pages.ByExpiryDate }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Date de Dernière Modification

{{% code file="layouts/partials/by-last-mod.html" %}}
```html
<ul>
    <!-- orders content according to the "lastmod" field in front matter -->
    {{ range .Data.Pages.ByLastmod }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Longueur

{{% code file="layouts/partials/by-length.html" %}}
```html
<ul>
    <!-- orders content according to content length in ascending order (i.e., the shortest content will be listed first) -->
    {{ range .Data.Pages.ByLength }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Titre

{{% code file="layouts/partials/by-title.html" %}}
```html
<ul>
    <!-- ranges through content in ascending order according to the "title" field set in front matter -->
    {{ range .Data.Pages.ByTitle }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Titre du Lien

{{% code file="layouts/partials/by-link-title.html" %}}
```html
<ul>
    <!-- ranges through content in ascending order according to the "linktitle" field in front matter. If a "linktitle" field is not set, the range will start with content that only has a "title" field and use that value for .LinkTitle -->
    {{ range .Data.Pages.ByLinkTitle }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .LinkTitle }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

### Par Paramètre

Ordre basé sur le paramètre front matter spécifié. Le contenu qui n'a pas le champ de front matter spécifié utilisera les paramètres `.Site.Params` du site par défaut. Si le paramètre n'est pas trouvé dans certaines entrées, ces entrées apparaîtront ensemble à la fin du tri.

{{% code file="layouts/partials/by-rating.html" %}}
```html
<!-- Ranges through content according to the "rating" field set in front matter -->
{{ range (.Data.Pages.ByParam "rating") }}
  <!-- ... -->
{{ end }}
```
{{% /code %}}

Si le champ ciblé du front matter est embarqué dans un autre champ, vous pouvez accéder au chang en utilisant la notation point.

{{% code file="layouts/partials/by-nested-param.html" %}}
```html
{{ range (.Data.Pages.ByParam "author.last_name") }}
  <!-- ... -->
{{ end }}
```
{{% /code %}}

### Ordre Inversé

L'ordre inversé peut s'appliquer à n'importe laquelle des méthodes au-dessus. Voici des exemples d'utilisation de `ByDate` :

{{% code file="layouts/partials/by-date-reverse.html" %}}
```html
<ul>
    {{ range .Data.Pages.ByDate.Reverse }}
        <li>
            <h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>
            <time>{{ .Date.Format "Mon, Jan 2, 2006" }}</time>
        </li>
    {{ end }}
</ul>
```
{{% /code %}}

## Groupement de Contenu

Hugo fournit quelques fonctions pour grouper les pages par  Section, Type, Date, etc.

### Par Champ Page

{{% code file="layouts/partials/by-page-field.html" %}}
```html
<!-- Groups content according to content section. The ".Key" in this instance will be the section's title. -->
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

Dans l'exemple ci-dessus, vous pouvez vouloir `{{.Title}}` pour indiquer le champ `title` que vous avez ajouté à votre fichier `_index.md` à la place. Vous pouvez accéder à cette valeur à l'aide de la fonction [`.GetPage`][getpage] :

{{% code file="layouts/partials/by-page-field.html" %}}
```html
<!-- Groups content according to content section.-->
{{ range .Data.Pages.GroupBy "Section" }}
<!-- Checks for existence of _index.md for a section; if available, pulls from "title" in front matter -->
{{ with $.Site.GetPage "section" .Key }}
<h3>{{.Title}}</h3>
{{ else }}
<!-- If no _index.md is available, ".Key" defaults to the section title and filters to title casing -->
<h3>{{ .Key | title }}</h3>
{{ end }}
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

### Par Date

{{% code file="layouts/partials/by-page-date.html" %}}
```html
<!-- Groups content by month according to the "date" field in front matter -->
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

### Par Date de Publication

{{% code file="layouts/partials/by-page-publish-date.html" %}}
```html
<!-- Groups content by month according to the "publishdate" field in front matter -->
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

### Par Paramètre de Page

{{% code file="layouts/partials/by-page-param.html" %}}
```html
<!-- Groups content according to the "param_key" field in front matter -->
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

### Par Paramètre Page dans le Format de Date

Le modèle suivant pousse un peu plus loin le groupement par `date` et utilise la chaîne de mise en page de Golang. Voir la fonction [`Format`][`Format` function] pour plus d'exemples d'utilisation de la chaîne de mise en page de Golang pour formater les dates dans Hugo.

{{% code file="layouts/partials/by-page-param-as-date.html" %}}
```html
<!-- Groups content by month according to the "param_key" field in front matter -->
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

### Ordre Clé Inversé

L'ordre des groupes est effectué par des clés dans un ordre alphanumérique (A-Z, 1-100) et dans un ordre chronologique inverse pour les dates (c'est-à-dire avec la plus récente en premier).

Bien qu'il s'agisse de valeurs par défaut logiques, elles ne sont pas toujours l'ordre souhaité. Il existe deux syntaxes différentes pour modifier les commandes par défaut de tri pour les groupes, qui fonctionnent toutes les deux de la même manière.

#### 1. Ajouter la Méthode Reverse

```html
{{ range (.Data.Pages.GroupBy "Section").Reverse }}
```

```html
{{ range (.Data.Pages.GroupByDate "2006-01").Reverse }}
```

#### 2. Fournir la Direction Alternative

```html
{{ range .Data.Pages.GroupByDate "2006-01" "asc" }}
```

```html
{{ range .Data.Pages.GroupBy "Section" "desc" }}
```

### Ordonner Dans les Groupes

Étant donné que le groupage renvoie une `{{.Key}}` et une tranche de pages, toutes les méthodes de tri listées ci-dessus sont disponibles.

Voici la commande pour l'exemple qui suit :

1. Le contenu est regroupé par mois selon le champ `date` dans le front matter.
2. Les groupes sont classés par ordre croissant (c'est-à-dire les groupes les plus anciens d'abord)
3. Les pages dans chaque groupe respectif sont classées par ordre alphabétique selon le `title`.

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

## Filtre et Limite des Listes

Parfois, vous souhaitez seulement lister un sous-ensemble du contenu disponible. Un commun est d'afficher seulement "Posts" sur la page d'accueil du blog. Vous pouvez l'accomplir avec la fonction `where`.

### `where`

`where` fonctionne de la même manière que le mot-clé [`where` dans SQL][wherekeyword]. Il sélectionne tous les éléments de la liste ou de la tranche qui correspondent au champ et à la valeur fournis. `where` prend trois arguments :

1. `array` *ou* `slice of maps or structs`
2. `key` *ou* `field name`
3. `match value`

{{% code file="layouts/_default/.html" %}}
```html
{{ range where .Data.Pages "Section" "post" }}
   {{ .Content }}
{{ end }}
```
{{% /code %}}

Vous pouvez voir plus d'exemples dans la [documentation des fonctions pour `where`][wherefunction].

### `first`

`first` fonctionne de la même manière que le mot clé [`limit` dans SQL][limitedkeyword]. Il réduit le tableau uniquement aux éléments `first N`. Il prend le tableau et le nombre d'éléments comme entrée. `first` prend deux arguments :
  
1. `array` *ou* `slice of maps or structs`
2. `nombre d'éléments`

{{% code file="layout/_default/section.html" %}}
```html
{{ range first 10 .Data.Pages }}
  {{ .Render "summary" }}
{{ end }}
```
{{% /code %}}

### `first` et `where` Ensemble

Utilsier `first` et `where` ensemble peut être très puissant :

{{% code file="first-and-where-together.html" %}}
```html
<!-- Classe le contenu dans la section "posts" par le champ  "title" et puis ne l'étend que pour les 5 premiers posts -->
{{ range first 5 (where .Data.Pages "Section" "post").ByTitle }}
   {{ .Content }}
{{ end }}
```
{{% /code %}}

[base]: /templates/base/
[bepsays]: http://bepsays.com/en/2016/12/19/hugo-018/
[directorystructure]: /demarrage/directory-structure/
[`Format` function]: /fonctions/format/
[front matter]: /gestion-contenu/front-matter/
[getpage]: /fonctions/getpage/
[homepage]: /templates/homepage/
[homepage]: /templates/homepage/
[limitkeyword]: https://www.techonthenet.com/sql/select_limit.php
[mentalmodel]: http://webstyleguide.com/wsg3/3-information-architecture/3-site-structure.html
[pagevars]: /variables/page/
[partials]: /templates/partials/
[RSS 2.0]: http://cyber.law.harvard.edu/rss/rss.html "RSS 2.0 Specification"
[rss]: /templates/rss/
[sections]: /gestion-contenu/sections/
[sectiontemps]: /templates/section-templates/
[sitevars]: /variables/site/
[taxlists]: /templates/taxonomy-templates/#taxonomy-list-templates/
[taxterms]: /templates/taxonomy-templates/#taxonomy-terms-templates/
[taxvars]: /variables/taxonomy/
[views]: /templates/views/
[wherefunction]: /gestion-contenu/where/
[wherekeyword]: https://www.techonthenet.com/sql/where.php