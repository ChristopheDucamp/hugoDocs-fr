---
title: Modèles Partiels
linktitle: Modèles Partiels
description: Les partiels sont des plus petits composants, conscients du contexte dans vos modèles de listes et de page qui peuvent être utilisés économiquement pour maintenir votre modélisation DRY.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
categories: [modèles]
#tags: [lists,sections,partials, partiels, listes]
menu:
  docs:
    parent: "Templates"
    weight: 90
weight: 90
sections_weight: 90
draft: false
aliases: [/templates/partiels/,/templates/partial/,/layout/chrome/,/extras/analytics/]
toc: true
---

## Ordre de Recherche dans le Modèle Partiel

Les modèles partiels---comme les [modèles de page unique][singletemps] et les [modèles de page liste][listtemps]---ont un   [ordre de recherche][lookup order] spécifique. Néanmoins, les partiels sont plus simples dans le fait que Hugo ne vérifiera que deux endroits : 

1. `layouts/partials/*<NOMPARTIEL>.html`
2. `themes/<THEME>/layouts/partials/*<NOMPARTIEL>.html`

Ce qui permet à un utilisateur final de thème de copier un contenu de partiel à l'intérieur d'un fichier du même nom pour une [personnalisation][customize].

## Utilisez les Partiels dans vos Modèles

Tous les partiels de votre projet Hugo sont situés dans un unique dossier `layouts/partials`. Pour une meilleure organisation, vous pouvez tout aussi bien créer plusieurs sous-répertoires dans `partials` :

```
.
└── layouts
    └── partials
        ├── footer
        │   ├── scripts.html
        │   └── site-footer.html
        ├── head
        │   ├── favicons.html
        │   ├── metadata.html
        │   ├── prerender.html
        │   └── twitter.html
        └── header
            ├── site-header.html
            └── site-nav.html
```

Tous les partiels sont appelés dans vos modèles en utilisant le modèle suivant : 

```
{{ partial "<PATH>/<PARTIEL>.html" . }}
```

{{% note %}}
L'une des erreurs les plus fréquentes avec les nouveaux utilisateurs de Hugo est de ne pas transmettre un contexte à l'appel du partiel. Dans le modèle ci-dessus, notez comment "le point" (`.`) est requis comme second argument pour donner le contexte partiel. Vous pouvez en savoir plus sur «le point» dans [introduction de modèle Hugo](/templates/introduction/).
{{% /note %}}

Comme le montre l'exemple de structure de dossiers ci-dessus, vous pouvez imbriquer vos répertoires dans les «partials» pour une meilleure organisation source. Il suffit d'appeler le chemin imbriqué du partiel par rapport au répertoire `partials` :

```golang
{{ partial "header/site-header.html" . }}
{{ partial "footer/scripts.html" . }}
```

{{% note %}}
Avant la v0.12, Hugo utilisait l'appel de `template` pour inclure des modèles partiels. Lorsque vous utilisez Hugo v0.12 et les versions plus récentes, assurez-vous d'utiliser la syntaxe `{{ partial "<PATH>/<PARTIEL>.html" . }}``. L'ancienne approche fonctionnera encore mais a moins d'avantages.
{{% /note %}}

### Portée de Variable

Le second argument dans un appel à un partiel est la variable transmise. Les exemples ci-dessus passent le `.`, qui indique au modèle de recevoir le partiel pour appliquer le [contexte][context] actuel.

Cela signifie que le partiel ne pourra *seulement* accéder à ces variables. Le partiel est isolé et *n'a pas accès à la portée extérieure*. Dans le partiel, `$.Var` équivaut à `.Var`.

### Partiels Cachés

La [fonction de modèle `partialCached`][partialcached] peut offrir une performance significative pour les modèles complexes qui n'ont pas besoin d'être re-produits à chaque invocation. L'usage le plus simple se fait comme suit :

```
{{ partialCached "footer.html" . }}
```

Vous pouvez aussi passer des paramètres supplémentaires à `partialCached` pour créer des *variantes* du partiel caché.

Par exemple, vous pouvez dire à Hugo de produire uniquement le partiel `footer.html` une fois par section :

```
{{ partialCached "footer.html" . .Section }}
```

Si vous devez passer des paramètres supplémentaires pour créer des variantes uniques, vous pouvez passer autant de paramètres variants que vous avez besoin :

```
{{ partialCached "footer.html" . .Params.country .Params.province }}
```

Notez que les paramètres de variantes ne sont pas mis à la disposition du modèle partiel sous-jacent. Ils ne sont utilisés que pour créer une clé de cache unique.

### Exemple `header.html`

Le modèle de partiel `header.html` qui suit est utilisé pour  [spf13.com](http://spf13.com/) :

{{% code file="layouts/partials/header.html" download="header.html" %}}
```html
<!DOCTYPE html>
<html class="no-js" lang="en-US" prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb#">
<head>
    <meta charset="utf-8">

    {{ partial "meta.html" . }}

    <base href="{{ .Site.BaseURL }}">
    <title> {{ .Title }} : spf13.com </title>
    <link rel="canonical" href="{{ .Permalink }}">
    {{ if .RSSLink }}<link href="{{ .RSSLink }}" rel="alternate" type="application/rss+xml" title="{{ .Title }}" />{{ end }}

    {{ partial "head_includes.html" . }}
</head>
<body lang="en">
```
{{% /code %}}

{{% note %}}
L'exemple partiel de `header.html` a été construit avant l'introduction des modèles de blocs à Hugo. En savoir plus sur les [modèles et blocs de base](/templates/base/) pour définir le chrome externe ou la coque de vos modèles maîtres (c'est-à-dire la tête, l'en-tête et le pied de page de votre site). Vous pouvez même combiner des blocs et des partiels pour une flexibilité accrue.
{{% /note %}}

### Exemple `footer.html`

Le modèle de partiel `footer.html` qui suit est utilisé pour  [spf13.com](http://spf13.com/) :

{{% code file="layouts/partials/footer.html" download="footer.html" %}}
```html
<footer>
  <div>
    <p>
    &copy; 2013-14 Steve Francia.
    <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons Attribution">Some rights reserved</a>;
    please attribute properly and link back. Hosted by <a href="http://servergrove.com">ServerGrove</a>.
    </p>
  </div>
</footer>
<script type="text/javascript">

  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-XYSYXYSY-X']);
  _gaq.push(['_trackPageview']);

  (function() {
    var ga = document.createElement('script');
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' :
        'http://www') + '.google-analytics.com/ga.js';
    ga.setAttribute('async', 'true');
    document.documentElement.firstChild.appendChild(ga);
  })();

</script>
</body>
</html>
```
{{% /code %}}

[context]: /templates/introduction/ "The most easily overlooked concept to understand about Go templating is how the dot always refers to the current context."
[customize]: /themes/personnaliser/ "Hugo fournit des moyens faciles pour personnaliser le thèmes tant que les utilisateurs sont à l'aise avec l'ordre de recherche des modèles Hugo."
[listtemps]: /templates/listes/ "To effectively leverage Hugo's system, see how Hugo handles list pages, where content for sections, taxonomies, and the homepage are listed and ordered."
[lookup order]: /templates/ordre-recherche/ "To keep your templating dry, read the documentation on Hugo's lookup order."
[partialcached]: /fonctions/partialcached/ "Use the partial cached function to improve build times in cases where Hugo can cache partials that don't need to be rendered with every page."
[singletemps]: /templates/single-page-templates/ "The most common form of template in Hugo is the single content template. Read the docs on how to create templates for individual pages."
[themes]: /themes/