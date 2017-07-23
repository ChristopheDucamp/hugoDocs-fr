---
title: Introduction à la Modélisation Hugo
linktitle: Introduction
description: Hugo utilise les bibliothèques `html/template` et `text/template` de Go comme base pour la modélisation.
godocref: https://golang.org/pkg/html/template/
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
categories: [fondamentaux, modèles, fundamentals]
#tags: [go]
menu:
  docs:
    parent: "templates"
    weight: 10
weight: 10
sections_weight: 10
draft: false
aliases: [/templates/introduction/,/layouts/introduction/,/layout/introduction/, /templates/go-templates/]
toc: true
---

{{% note %}}
Ce qui suit n'est qu'une version simplifiée des modèles Go. Pour un examen approfondi des modèles Go, consultez la documentation  officielle [Go docs](http://golang.org/pkg/html/template/).
{{% /note %}}

Les modèles Go fournissent un langage de modèle extrêmement simple respectant la conviction que seule la logique la plus élémentaire appartient au modèle ou à la couche vue.

## Syntaxe Basique

Les modèles Golang sont des fichiers HTML avec l'ajout de [variables][variables] et de [fonctions][]. Les variables et les fonctions du modèle Golang sont accessibles dans `{{ }}`.

### Accéder à une Variable Prédéfinie

```golang
{{ foo }}
```

Les paramètres pour les fonctions sont séparés en utilisant des espaces. L'exemple qui suit appelle la fonction `add` avec des  inputs de `1` et `2` :

```golang
{{ add 1 2 }}
```

#### Les Méthodes et Champs sont Accessibles via la Notation Point

Accédez au paramètre de Page `bar` défini dans un élément de contenu du [front matter][].

```golang
{{ .Params.bar }}
```

#### Les Parenthèses Peuvent être utilisées pour Grouper des Items

```golang
{{ if or (isset .Params "alt") (isset .Params "caption") }} Caption {{ end }}
```

## Variables

Chaque modèle Go reçoit un objet data. Dans Hugo, chaque modèle est passé comme `Page`. Voir [variables][] pour plus d'informations.

Voici comment accéder à une variable `Page` à partir d'un modèle :

```golang
<title>{{ .Title }}</title>
```

Les valeurs peuvent être aussi stockées dans des variables personnalisées et référencées plus tard : 

```golang
{{ $address := "123 rue Principale."}}
{{ $address }}
```

{{% note %}}
Les variables définies dans les conditionnels `if` et similaires ne sont pas visibles de l'extérieur. Voir [https://github.com/golang/go/issues/10608](https://github.com/golang/go/issues/10608).

Hugo a créé un contournement pour ce problème dans [Scratch](/functions/scratch).

{{% /note %}}

## Fonctions

Les modèles Go ne sont livrés qu'avec quelques fonctions de base, mais fournissent également un mécanisme pour les applications afin d'étendre le jeu d'origine.

Les [fonctions de modèle Hugo][fonctions] fournissent des fonctionnalités supplémentaires spécifiques à la création de sites Web. Les fonctions sont appelées en utilisant leur nom suivi des paramètres requis séparés par des espaces. Les fonctions de modèle ne peuvent pas être ajoutées sans recompiler Hugo.

### Exemple 1 : Ajouter des Nombres

```golang
{{ add 1 2 }}
=> 3
```

### Exemple 2 : Comparer des Nombres

```golang
{{ lt 1 2 }}
=> true (i.e., since 1 is less than 2)
```

Notez que les deux exemples nous permettent d'utiliser [les fonctions mathématiques][math functions] du modèle Go.

{{% note "Opérateurs booléens supplémentaires" %}}
Il y a plus d'opérateurs booléens que ceux répertoriés dans les documents Hugo dans la [documentation du modèle Golang](http://golang.org/pkg/text/template/#hdr-Functions).
{{% /note %}}

## Inclusions

Lorsque vous incluez un autre modèle, vous y passerez les données auxquelles il pourra accéder. Pour transmettre le contexte actuel, n'oubliez pas d'inclure un point final. L'emplacement des modèles commencera toujours sur le répertoire `/layout/` dans Hugo.

### Exemples de Modèles de Partiels

```golang
{{ template "partials/header.html" . }}
```

À partir de la version Hugo v0.12, vous pouvez aussi utiliser l'appel `partial`  pour les [modèles de partiels][partials] :

```golang
{{ partial "header.html" . }}
```

## Logique

Les modèles Go fournissent l'itération la plus basique et la logique conditionnelle.

### Itération

Tout comme dans Go, les modèles Go utilisent fortement `range` pour itérer sur une "map", une "array" ou une "slice". Voici des exemples différents d'utilisation de range.

#### Exemple 1 : Utiliser le Contexte

```golang
{{ range array }}
    {{ . }}
{{ end }}
```

#### Exemple 2 : Déclarer Valeur => nom de Variable

```golang
{{range $element := array}}
    {{ $element }}
{{ end }}
```

#### Exemple 3 : Déclarer un Nom de Variable Valeur-Clé

```golang
{{range $index, $element := array}}
   {{ $index }}
   {{ $element }}
{{ end }}
```

### Conditionnels

`if`, `else`, `with`, `or`, et `and` fournissent le cadre pour gérer la logique conditionnelle dans les modèles Go. Tout comme `range`, chaque déclaration est fermée avec un `{{end}}`.

Les modèles Go traitent les valeurs qui suivent comme false :

* false
* 0
* toute array, slice, map ou chaîne de longueur-zero

#### Exemple 1 : `if`

```golang
{{ if isset .Params "title" }}<h4>{{ index .Params "title" }}</h4>{{ end }}
```

#### Exemple 2 : `if` … `else`

```golang
{{ if isset .Params "alt" }}
    {{ index .Params "alt" }}
{{else}}
    {{ index .Params "caption" }}
{{ end }}
```

#### Exemple 3 : `and` & `or`

```golang
{{ if and (or (isset .Params "title") (isset .Params "caption")) (isset .Params "attr")}}
```

#### Exemple 4 : `with`

Un moyen alternatif d'écrire "`if`" et de référencer ensuite la même valeur est d'utiliser à la place "`with`". 
`with` renvoie le contexte `.` dans sa portée et ignore le block si la variable est absente.

Le premier exemple au-dessus pourrait être ainsi simplifié : 

```golang
{{ with .Params.title }}<h4>{{ . }}</h4>{{ end }}
```

#### Exemple 5 : `if` … `else if`

```golang
{{ if isset .Params "alt" }}
    {{ index .Params "alt" }}
{{ else if isset .Params "caption" }}
    {{ index .Params "caption" }}
{{ end }}
```

## Pipes

L'un des composants les plus puissants des modèles Go est la capacité de piloter les actions l'une après l'autre. Cela se fait en utilisant des pipes. Emprunté aux pipes d'Unix, le concept est simple : la sortie de chaque pipeline devient l'entrée du pipe suivant.

En raison de la syntaxe très simple des modèles Go, le pipe est essentiel pour pouvoir chaîner les appels de fonction. Une limitation des pipes est qu'ils ne peuvent fonctionner qu'avec une seule valeur et que cette valeur devient le dernier paramètre du pipeline suivant.

Quelques exemples simples devraient aider à transmettre comment utiliser le pipe.

### Exemple 1 : `shuffle`

Les deux exemples suivants sont fonctionnellement les mêmes :

```golang
{{ shuffle (seq 1 5) }}
```


```golang
{{ (seq 1 5) | shuffle }}
```

### Exemple 2 : `index`

L'exemple qui suit accède au paramètre de la page appelé  "disqus_url" et échappe le HTML. Cet exemple utilise aussi la  [fonction `index`][index], qui est native dans les modèles Go : 

```golang
{{ index .Params "disqus_url" | html }}
```

### Exemple 3 : `or` avec `isset`

```golang
{{ if or (or (isset .Params "title") (isset .Params "caption")) (isset .Params "attr") }}
Stuff Here
{{ end }}
```

Pourrait être récrit comme : 

```golang
{{ if isset .Params "caption" | or isset .Params "title" | or isset .Params "attr" }}
Stuff Here
{{ end }}
```

### Exemple 4 : Commentaires Conditionnels Internet Explorer 

Par défaut, les Modèles Go Templates suppriment les commentaires HTML de l'output. Cela a un effet secondaire malheureux de supprimer les commentaires conditionnels d'Internet Explorer. En tant que solution de contournement, utilisez quelque chose comme ceci :

```golang
{{ "<!--[if lt IE 9]>" | safeHTML }}
  <script src="html5shiv.js"></script>
{{ "<![endif]-->" | safeHTML }}
```

Alternativement, vous pouvez utiliser le backtick (`` ` ``) pour citer les commentaires conditionnels IE, évitant la tâche d'échapper chaque double guillemet de citation (`"`) à l'intérieur, comme démontré dans les [examples](http://golang.org/pkg/text/template/#hdr-Examples) dans la documentation Go text/template :

```
{{ `<!--[if lt IE 7]><html class="no-js lt-ie9 lt-ie8 lt-ie7"><![endif]-->` | safeHTML }}
```

## Contexte (aussi appelé "le point")

Le concept le plus facilement négligé pour comprendre les modèles Go est que `{{ . }}` fait toujours référence au contexte actuel. Dans le niveau supérieur de votre modèle, ce sera le jeu de données mis à sa disposition. À l'intérieur d'une itération, cependant, il aura la valeur de l'élément actuel dans la boucle ; c'est-à-dire que `{{ . }}` ne se référera plus aux données disponibles sur la page entière. Si vous devez accéder aux données au niveau de la page (par exemple, les paramètres de page définis en avant) à partir de la boucle, vous voudrez probablement effectuer l'une des opérations suivantes :

### 1. Definir une Variable Indépendante du Contexte

L'exemple suivant montre comment défiir une variable indépendante du contexe.

{{% code file="tags-range-with-page-variable.html" %}}
```html
{{ $title := .Site.Title }}
<ul>
{{ range .Params.tags }}
    <li>
        <a href="/tags/{{ . | urlize }}">{{ . }}</a>
        - {{ $title }}
    </li>
{{ end }}
</ul>
```
{{% /code %}}

{{% note %}}
Notez comment une fois que nous sommes entrés dans la boucle (c'est-à-dire `range`), la valeur de `{{ . }}` a changé. Nous avons défini une variable en dehors de la boucle (`{{ $title }`) à laquelle nous avons attribué une valeur afin que nous ayons également accès à la valeur dans la boucle.
{{% /note %}}

### 2. Utiliser `$.` pour Accéder au Contexte Global

`$` a une signification particulière dans vos modèles. `$` est défini par défaut à la valeur de départ de `.` ("le point").  Ceci est une [caractéristique documentée de Go text/template][dotdoc]. Cela signifie que vous avez accès au contexte global à partir de n'importe où. Voici un exemple équivalent du bloc de code précédent mais utilisant maintenant  `$` pour saisir `.Site.Title` du contexte global :

{{% code file="range-through-tags-w-global.html" %}}
```hbs
<ul>
{{ range .Params.tags }}
  <li>
    <a href="/tags/{{ . | urlize }}">{{ . }}</a>
            - {{ $.Site.Title }}
  </li>
{{ end }}
</ul>
```
{{% /code %}}

{{% warning "ne redéfinissez pas le Point" %}}
La magie intégrée de `$` cesserait de fonctionner si quelqu'un devait malicieusement redéfinir le caractère spécial ; par ex `{{$:=.Site}}`. *Ne faites pas ça.* Vous pouvez bien sûr, vous recouvrer de ce mal en utilisant `{{$:=.}}` dans un contexte global pour réinitialiser `$` à sa valeur par défaut.
{{% /warning %}}

## Espace blanc

Go 1.6 inclut la possibilité de couper l'espace blanc de chaque côté d'une étiquette Go en incluant un trait d'union (`-`) et un espace immédiatement à côté du délimiteur correspondant `{{` or `}}` correspondant.

Par exemple, le modèle Go suivant inclura les nouvelles lignes et l'onglet horizontal dans sa sortie HTML :

```html
<div>
  {{ .Title }}
</div>
```

ce qui donnera :

```html
<div>
  Hello, World!
</div>
```

Utiliser le  `-` dans l'exemple suivant supprime l'espace blanc supplémentaire entourant la variable` .Title` et supprime la nouvelle ligne :

```html
<div>
  {{- .Title -}}
</div>
```

qui donnera alors : 

```html
<div>Hello, World!</div>
```

Go considère les caractères suivants en espace-blanc :

* e<kbd>space</kbd>
* onglet horizontal <kbd>tab</kbd>
* retour chariot <kbd>return</kbd>
* nouvelle ligne

## Paramètres Hugo

Hugo offre la possibilité de transmettre des valeurs à votre couche de modèle via votre [configuration de site][config] (c'est-à-dire pour les valeurs du site) ou à travers les métadonnées de chaque élément de contenu spécifique (c'est-à-dire [front matter][]). Vous pouvez définir toutes les valeurs de n'importe quel type et les utiliser comme vous le souhaitez dans vos modèles, pourvu que les valeurs soient prises en charge par le format front matter spécifié via `metaDataFormat` dans votre fichier de configuration.

## Utiliser les Paramètres de Contenu (`Page`)

Vous pouvez fournir des variables à utiliser par des modèles dans le [front matter][] individuel du contenu.

Un exemple de ceci est utilisé dans la documentation Hugo. La plupart des pages bénéficient de la présentation de la table des matières, mais parfois la table des matières n'a pas beaucoup de sens. Nous avons défini une variable `notoc` dans notre front matter qui empêche le rendu d'une table des matières lorsque spécifiquement définie sur` true`.

Voici l'exemple du front matter :

```yaml
---
title: Roadmap
lastmod: 2017-07-05
date: 2013-11-18
notoc: true
---
```

Voici un exemple de code correspondant qui pourrait être utilisé dasn un [modèle partiel][partials]  `toc.html` :

{{% code file="layouts/partials/toc.html" download="toc.html" %}}
```html
{{ if not .Params.notoc }}
<aside>
  <header>
    <a href="#{{.Title | urlize}}">
    <h3>{{.Title}}</h3>
    </a>
  </header>
  {{.TableOfContents}}
</aside>
<a href="#" id="toc-toggle"></a>
{{end}}
```
{{% /code %}}

Nous voulons que le comportement *par défaut* pour les pages soit d'inclure une table des matières, sauf indication contraire. Ce modèle vérifie que le champ `notoc:` dans le front matter de cette page n'est pas `true`.

## Utiliser les Paramètres de Configuration du Site

Vous pouvez définir arbitrairement autant de paramètres de niveau de site que vous le souhaitez dans le fichier de configuration [de votre site][config]. Ces paramètres sont globalement disponibles dans vos modèles.

Par exemple, vous pouvez déclarer ce qui suit :

{{% code file="config.yaml" %}}
```yaml
params:
  copyrighthtml: "Copyright &#xA9; 2017 John Doe. All Rights Reserved."
  twitteruser: "spf13"
  sidebarrecentlimit: 5
```
{{% /code %}}

Dans un layout de bas de page, vous pouvez déclarer un `<footer>` qui n'est rendu que si le paramètre `copyrighthtml` est fourni. S'il *est* fourni, vous devrez alors déclarer que la chaîne est sûre à utiliser via la fonction [`safeHTML`][safehtml] afin que l'entité HTML ne soit pas échappée de  nouveau. Cela vous permettra de mettre à jour tout simplement votre fichier de configuration de premier niveau chaque 1er janvier, au lieu de partir à la chasse dans vos modèles.

```html
{{if .Site.Params.copyrighthtml}}<footer>
<div class="text-center">{{.Site.Params.CopyrightHTML | safeHTML}}</div>
</footer>{{end}}
```

Une autre façon d'écrire le "`if`", puis de faire référence à la même valeur est d'utiliser à la place le [`with`][with]. `with` renvoie le contexte (`.`) dans sa portée et ignore le bloc si la variable est absente :

{{% code file="layouts/partials/twitter.html" %}}
```html
{{with .Site.Params.twitteruser}}
<div>
  <a href="https://twitter.com/{{.}}" rel="author">
  <img src="/images/twitter.png" width="48" height="48" title="Twitter: {{.}}" alt="Twitter"></a>
</div>
{{end}}
```
{{% /code %}}

Enfin, vous pouvez également extraire les "constantes magiques" de vos mises en page. Ce qui suit utilise la fonction [`first`][first], ainsi que la variable de la page [`.RelPermalink`][relpermalink] et la variable du site [`.Site.Pages`][sitevars].

```html
<nav>
  <h1>Billets Récents</h1>
  <ul>
  {{- range first .Site.Params.SidebarRecentLimit .Site.Pages -}}
    <li><a href="{{.RelPermalink}}">{{.Title}}</a></li>
  {{- end -}}
  </ul>
</nav>
```

## Exemple : n'Afficher que les Événements à Venir

Go vous permet de faire plus que ce qui est montré ici. 
En utilisant la fonction [`where` de Hugo][where] et Go built-ins, nous pouvons énumérer uniquement les éléments provenant de `content/events/` dont la date (définie dans le fichier [front matter][] du contenu est à venir. 
Voici un exemple de [modèle partiel][partials] :

{{% code file="layouts/partials/upcoming-events.html" download="upcoming-events.html" %}}
```html
<h4>Événements à venir</h4>
<ul class="upcoming-events">
{{ range where .Data.Pages.ByDate "Section" "events" }}
  {{ if ge .Date.Unix .Now.Unix }}
    <li>
    <!-- add span for event type -->
      <span>{{ .Type | title }} —</span>
      {{ .Title }} on
    <!-- add span for event date -->
      <span>{{ .Date.Format "2 January at 3:04pm" }}</span>
      at {{ .Params.place }}
    </li>
  {{ end }}
{{ end }}
</ul>
```
{{% /code %}}


[`where` function]: /fonctions/where/
[config]: /demarrage/configuration/
[dotdoc]: http://golang.org/pkg/text/template/#hdr-Variables
[first]: /fonctions/first/
[front matter]: /gestion-contenu/front-matter/
[fonctions]: /fonctions/ "Voir la liste complète des fonctions de modélisation d'Hugo avec un guide de référence rapide et des exemples basiques et avancés."
[Go html/template]: http://golang.org/pkg/html/template/ "références Godocs pour la modélisation html de Golang"
[gohtmltemplate]: http://golang.org/pkg/html/template/ "références Godocs pour la modélisation html en Golang"
[index]: /fonctions/index/
[math functions]: /fonctions/math/
[partials]: /templates/partials/ "Lien vers la page de modèles de partiel dans la section de modélisation de la docs Hugo"
[relpermalink]: /variables/page/
[safehtml]: /fonctions/safehtml/
[sitevars]: /variables/site/
[variables]: /variables/ "See the full extent of page-, site-, and other variables that Hugo make available to you in your templates."
[where]: /fonctions/where/
[with]: /fonctions/with/
[godocsindex]: http://golang.org/pkg/text/template/ "page Godocs  pour la fonction index"
