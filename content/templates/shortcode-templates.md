---
title: Créer vos Propres Shortcodes
linktitle: Modèles de Shortcode
description: Vous pouvez augmenter les shortcodes intégrés à Hugo en créant les vôtres en utilisant la même syntaxe de modélisation que celle utilisée pour les pages uniques et pages de listes.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [modèles]
#tags: [shortcodes]
menu:
  docs:
    parent: "Templates"
    weight: 100
weight: 100
sections_weight: 100
draft: false
aliases: []
toc: true
---
Les shortcodes sont un moyen de consolider les modèles en petits fragments réutilisables que vous pouvez intégrer directement dans votre contenu. Dans ce sens, vous pouvez considérer les codes courts comme l'intermédiaire entre des [modèles de page et de liste][templates] et des [fichiers de contenu de base][basic content files].

{{% note %}}
Hugo est également livré avec des codes courts intégrés pour les cas d'usage courant. (Voir [Gestion du contenu : Shortcodes](/gestion-contenu/shortcodes/).)
{{% /note %}}

## Créer des Shortcodes Personnalisés

Les shortcodes intégrés de Hugo couvrent beaucoup de cas communs, mais pas tous. Heureusement, Hugo offre la possibilité de créer facilement des codes courts personnalisés pour répondre aux besoins de votre site.

### Placement de Fichier

Pour créer un shortcode, placez un modèle HTML dans le dossier  `layouts/shortcodes` de votre [organisation source][source organization]. Considérez attentivement le nom du fichier car le nom du shortcode reflète celui du fichier mais sans l'extension `.html`. Par exemple, `layouts/shortcodes/monshortcode.html` sera appelé avec soit `{{</* monshortcode /*/>}}` or `{{%/* monshortcode /*/%}}` selon le type de paramètres que vous choisissez.

### Ordre de Recherche de Modèle Shortcode

Les modèles de shortcode on un [ordre de recherche][lookup order] simple :

1. `/layouts/shortcodes/<SHORTCODE>.html`
2. `/themes/<THEME>/layouts/shortcodes/<SHORTCODE>.html`

### Paramètres Positionnnels vs Nommés

Vous pouvez créer des codes courts en utilisant les types de paramètres suivants:

* Paramètres de position
* Paramètres nommés
* Paramètres de position *ou* nommé (c'est-à-dire "flexible")

Dans les codes courts avec paramètres de position, l'ordre des paramètres est important. Si un code court a une seule valeur requise (par exemple, le raccourci `youtube` ci-dessous), les paramètres positionnels fonctionnent très bien et exigent moins de saisie de la part des auteurs de contenu.

Pour des mises en page plus complexes avec des paramètres multiples ou optionnels, les paramètres nommés fonctionnent mieux. Bien qu'ayant moins de critères, les paramètres nommés nécessitent moins de mémorisation de la part de l'auteur de contenu et ils peuvent être ajoutés dans une déclaration de shortcode dans n'importe quel ordre.

Permettre les deux types de paramètres (c'est-à-dire un shortcode "flexible") est utile pour les mises en page complexes où vous souhaitez définir des valeurs par défaut qui peuvent être facilement remplacées par les utilisateurs.

### Accéder aux Paramètres

Tous les paramètres shortcode peuvent être consultés via la méthode `.Get`. Que vous passiez une clé (c'est-à-dire une chaîne) ou un numéro à la méthode `.Get` dépend de l'accès à un paramètre nommé ou positionnel, respectivement.

Pour accéder à un paramètre par nom, utilisez la méthode `.Get` suivie du paramètre nommé comme une chaîne citée :

```golang
{{ .Get "class" }}
```

Pour accéder à un paramètre par position, utilisez le `.Get` suivi d'une position numérique, en gardant à l'esprit que les paramètres positionnels sont indexés à zéro :

```golang
{{ .Get 0 }}
```

`with` est génial quand l'output dépend d'un paramètre à régler :

```golang
{{ with .Get "class"}} class="{{.}}"{{ end }}
```

`.Get` peut également être utilisé pour vérifier si un paramètre a été fourni. C'est plus utile lorsque la condition dépend de l'une ou l'autre des valeurs, ou les deux :

```golang
{{ or .Get "title" | .Get "alt" | if }} alt="{{ with .Get "alt"}}{{.}}{{else}}{{.Get "title"}}{{end}}"{{ end }}
```

#### `.Inner`

Si un shortcode de fermeture est utilisé, la variable `.Inner` sera remplie avec tout le contenu entre les shortcode d'ouverture et de fermeture. Si un shortcode de fermeture est requis, vous pouvez vérifier la longueur de `.Inner` comme un indicateur de son existence.

Un shortcode avec du contenu déclaré via la variable `.Inner` peut également être déclaré sans le contenu en ligne et sans shortcode de fermeture en utilisant la syntaxe de fermeture automatique :

```golang
{{</* innershortcode /*/>}}
```

#### `.Params`

La variable `.Params` dans shortcodes contient les paramètres de liste passés au shortcode pour des cas d'utilisation plus compliqués. Vous pouvez également accéder aux paramètres à plus haut niveau avec la logique suivante :

`$ .Params`
: Ce sont les paramètres passés directement dans la déclaration shortcode (par exemple, une ID vidéo YouTube)

`$ .Page.Params`
: Se réfère aux paramètres de la page ; la "page" dans ce cas se réfère au fichier de contenu dans lequel le code court est déclaré (par exemple, un champ `shortcode_color` dans le front matter d'un contenu pourrait être consulté via `$ .Page.Params.shortcode_color`).

`$ .Page.Site.Params`
: Se réfère à des variables globales telles que définies dans le [fichier de configuration de votre site][config].

#### `.IsNameParams`

La variable `.IsNamedParams` vérifie si la déclaration de shortcode utilise les paramètres nommés et renvoie une valeur booléenne.

Par exemple, vous pouvez créer un shortcode «image» qui peut prendre soit un paramètre nommé `src` ou le premier paramètre de position, selon la préférence de l'auteur du contenu. Supposons que le code court `image` soit appelé comme suit :

```md
{{</* image src="images/my-image.jpg"*/>}}
```

Vous pourriez alors inclure ce qui suis comme partie de votre modélisation de shortcode : 

```html
{{ if .IsNamedParams }}
<img src="{{.Get "src" alt="">
{{ else }}
<img src="{{.Get 0}}" alt="">
{{ end }}.
```

Voir l'[exemple de shortcode Vimeo][vimeoexample] en-dessous pour `.IsNamedParams` en action.

{{% warning %}}
Bien que vous puissiez créer des modèles courts qui acceptent les paramètres positionnels et nommés, vous *ne pouvez pas* déclarer des shortcode en contenus avec un mélange des types de paramètres. Par conséquent, un shortcode déclaré comme `{{</* image src="images/my-image.jpg" "This is my alt text" */>}}` renverra une erreur.
{{% /warning %}}

Vous pouvez également utiliser la variable `.Page` pour accéder à toutes les [variables de page][pagevars] normales.

Un shortcode peut également être imbriqué. Dans un shortcode imbriqué, vous pouvez accéder au contexte parent du shortcode avec la [variable `.Parent`][shortcodesvars]. Cela peut être très utile pour l'héritage de paramètres communs du shortcode à partir de la racine.

## Exemples de Personnalisation de Shortcode

Voici des exemples de différents types de shortcodes que vous pouvez créer via des fichiers de modèles de shortcode dans `/layouts/shortcodes`.

### Exemple pour un mot-unique : `year`

Supposons que vous souhaitiez tenir compte des mentions de l'année du copyright dans vos fichiers de contenu sans avoir à vérifier continuellement votre markdown. Votre objectif est de pouvoir appeler le shortcode comme suit :

```markdown
{{</* year */>}}
```

{{% code file="/layouts/shortcodes/year.html" %}}
```golang
{{ .Page.Now.Year }}
```
{{% /code %}}

### Exemple Positionnel Unique : `youtube`

L'intégration de vidéos est un ajout commun au contenu markdown qui peut devenir rapidement inégalé. Voici le code utilisé par le [shortcode YouTube intégré dans Hugo][youtubeshortcode] :

```golang
{{</* youtube 09jf3ow9jfw */>}}
```

Chargerait le modèle sur `/layouts/shortcodes/youtube.html`:

{{% code file="/layouts/shortcodes/youtube.html" %}}
```html
<div class="embed video-player">
<iframe class="youtube-player" type="text/html" width="640" height="385" src="http://www.youtube.com/embed/{{ index .Params 0 }}" allowfullscreen frameborder="0">
</iframe>
</div>
```
{{% /code %}}

{{% code file="youtube-embed.html" copy="false" %}}
```html
<div class="embed video-player">
    <iframe class="youtube-player" type="text/html"
        width="640" height="385"
        src="http://www.youtube.com/embed/09jf3ow9jfw"
        allowfullscreen frameborder="0">
    </iframe>
</div>
```
{{% /code %}}

### Exemple Nommé Unique : `image`

Disons que vous voulez créer votre propre shortcode `img` plutôt que d'utiliser le [shortcode `figure` intégré dans Hugo][figure].  Votre objectif est de pouvoir appeler le shortcode comme suit dans vos fichiers de contenu :


{{% code file="content-image.md" %}}
```golang
{{</* img src="/media/spf13.jpg" title="Steve Francia" */>}}
```
{{% /code %}}

Vous avez créé le shortcode sur `/layouts/shortcodes/img.html`, qui charge le modèle suivant de shortcode :

{{% code file="/layouts/shortcodes/img.html" %}}
```html
<!-- image -->
<figure {{ with .Get "class" }}class="{{.}}"{{ end }}>
    {{ with .Get "link"}}<a href="{{.}}">{{ end }}
        <img src="{{ .Get "src" }}" {{ if or (.Get "alt") (.Get "caption") }}alt="{{ with .Get "alt"}}{{.}}{{else}}{{ .Get "caption" }}{{ end }}"{{ end }} />
    {{ if .Get "link"}}</a>{{ end }}
    {{ if or (or (.Get "title") (.Get "caption")) (.Get "attr")}}
    <figcaption>{{ if isset .Params "title" }}
        <h4>{{ .Get "title" }}</h4>{{ end }}
        {{ if or (.Get "caption") (.Get "attr")}}<p>
        {{ .Get "caption" }}
        {{ with .Get "attrlink"}}<a href="{{.}}"> {{ end }}
            {{ .Get "attr" }}
        {{ if .Get "attrlink"}}</a> {{ end }}
        </p> {{ end }}
    </figcaption>
    {{ end }}
</figure>
<!-- image -->
```
{{% /code %}}

Et rendrait : 

{{% code file="img-output.html" copy="false" %}}
```html
<figure >
    <img src="/media/spf13.jpg"  />
    <figcaption>
        <h4>Steve Francia</h4>
    </figcaption>
</figure>
```
{{% /code %}}

### Exemple Unique Flexible : `vimeo`

```golang
{{</* vimeo 49718712 */>}}
{{</* vimeo id="49718712" class="flex-video" */>}}
```

Chargerait le modèle trouvé sur `/layouts/shortcodes/vimeo.html`:

{{% code file="/layouts/shortcodes/vimeo.html" %}}
```html
{{ if .IsNamedParams }}
  <div class="{{ if .Get "class" }}{{ .Get "class" }}{{ else }}vimeo-container{{ end }}">
    <iframe src="//player.vimeo.com/video/{{ .Get "id" }}" allowfullscreen></iframe>
  </div>
{{ else }}
  <div class="{{ if len .Params | eq 2 }}{{ .Get 1 }}{{ else }}vimeo-container{{ end }}">
    <iframe src="//player.vimeo.com/video/{{ .Get 0 }}" allowfullscreen></iframe>
  </div>
{{ end }}
```
{{% /code %}}

Et rendrait :

{{% code file="vimeo-iframes.html" copy="false" %}}
```html
<div class="vimeo-container">
  <iframe src="//player.vimeo.com/video/49718712" allowfullscreen></iframe>
</div>
<div class="flex-video">
  <iframe src="//player.vimeo.com/video/49718712" allowfullscreen></iframe>
</div>
```
{{% /code %}}

### Exemple Apparié : `highlight`

Voic un shortcode `highlight`, qui un [shortcode intégré][built-in shortcode] livré avec Hugo.

{{% code file="highlight-example.md" %}}
```markdown
{{</* highlight html */>}}
  <html>
    <body> This HTML </body>
  </html>
{{</* /highlight */>}}
```
{{% /code %}}

Le modèle pour le shortcode `highlight` utilise le code suivant, qui est déjà inclus dans Hugo :

```golang
{{ .Get 0 | highlight .Inner  }}
```

L'output rendu du bloc de code exemple HTML sera comme suit : 

{{% code file="syntax-highlighted.html" copy="false" %}}
```html
<div class="highlight" style="background: #272822"><pre style="line-height: 125%"><span style="color: #f92672">&lt;html&gt;</span>
    <span style="color: #f92672">&lt;body&gt;</span> This HTML <span style="color: #f92672">&lt;/body&gt;</span>
<span style="color: #f92672">&lt;/html&gt;</span>
</pre></div>
```
{{% /code %}}

{{% note %}}
Le shortcode précédent utilise une fonction de modèle spécifique à Hugo appelée `highlight`, qui utilise [Pygments](http://pygments.org) pour ajouter la mise en surbrillance de syntaxe sur l'exemple de bloc de code HTML. Pour plus d'informations, reportez-vous à [la page des outils du développeur sur la mise en surbrillance de la syntaxe](/tools/syntax-highlighting/).
{{% /note %}}

### Shortcode Imbriqué : Image Gallery

La variable shortcode [`.Parent`][parent] de Hugo renvoie une valeur booléenne selon que le shortcode en question est appelé dans le contexte d'un shortcode *parent*. Cela fournit un modèle d'héritage pour les paramètres de shortcode courants.

L'exemple suivant est inventé mais démontre le concept. Supposons que vous disposez d'un shortcode `gallery` qui attend un paramètre nommé `class` :

{{% code file="layouts/shortcodes/gallery.html" %}}
```html
<div class="{{.Get "class"}}">
  {{.Inner}}
</div>
```
{{% /code %}}

Vous disposez également d'un shortcode `image` avec un seul paramètre nommé `src` que vous souhaitez appeler à l'intérieur de `gallery` et d'autres shortcodes afin que le parent définisse le contexte de chaque `image` :

{{% code file="layouts/shortcodes/image.html" %}}
```html
{{- $src := .Get "src" -}}
{{- with .Parent -}}
  <img src="{{$src}}" class="{{.Get "class"}}-image">
{{- else -}}
  <img src="{{$src}}">
{{- end }}
```
{{% /code %}}

Vous pouvez alors appeler votre shortcode dans votre contenu comme suit : 

```markdown
{{</* gallery class="content-gallery" */>}}
  {{</* img src="/images/one.jpg" */>}}
  {{</* img src="/images/two.jpg" */>}}
{{</* /gallery */>}}
{{</* img src="/images/three.jpg" */>}}
```

Cela produira le HTML suivant. Notez comment les deux premiers shortcodes `image` héritent de la valeur `class` de `content-gallery` définie avec l'appel à la «galerie» parentale, alors que la troisième «image» utilise uniquement «src»:


This will output the following HTML. Note how the first two `image` shortcodes inherit the `class` value of `content-gallery` set with the call to the parent `gallery`, whereas the third `image` only uses `src`:

```html
<div class="content-gallery">
    <img src="/images/one.jpg" class="content-gallery-image">
    <img src="/images/two.jpg" class="content-gallery-image">
</div>
<img src="/images/three.jpg">
```

## Plus d'Exemples de Shortcode

Vous trouverez encore plus d'exemples dans le [dossier shortcodes de spf13.com][spfscs] et le [dossier shortcodes de la documentation Hugo][docsshortcodes].

[basic content files]: /gestion-contenu/formats/ "See how Hugo leverages markdown--and other supported formats--to create content for your website."
[built-in shortcode]: /gestion-contenu/shortcodes/
[config]: /getting-started/configuration/ "Learn more about Hugo's built-in configuration variables as well as how to us your site's configuration file to include global key-values that can be used throughout your rendered website."
[Content Management: Shortcodes]: /gestion-contenu/shortcodes/#using-hugo-s-built-in-shortcodes "Check this section if you are not familiar with the definition of what a shortcode is or if you are unfamiliar with how to use Hugo's built-in shortcodes in your content files."
[source organization]: /getting-started/directory-structure/#directory-structure-explained "Learn how Hugo scaffolds new sites and what it expects to find in each of your directories."
[docsshortcodes]: https://github.com/gohugoio/hugo/tree/master/docs/layouts/shortcodes "See the shortcode source directory for the documentation site you're currently reading."
[figure]: /gestion-contenu/shortcodes/#figure
[hugosc]: /gestion-contenu/shortcodes/#using-hugo-s-built-in-shortcodes
[lookup order]: /templates/lookup-order/ "See the order in which Hugo traverses your template files to decide where and how to render your content at build time"
[pagevars]: /variables/page/ "See which variables you can leverage in your templating for page vs list templates."
[parent]: /variables/shortcodes/
[shortcodesvars]: /variables/shortcodes/ "Certain variables are specific to shortcodes, although most .Page variables can be accessed within your shortcode template."
[spfscs]: https://github.com/spf13/spf13.com/tree/master/layouts/shortcodes "See more examples of shortcodes by visiting the shortcode directory of the source for spf13.com, the blog of Hugo's creator, Steve Francia."
[templates]: /templates/ "The templates section of the Hugo docs."
[vimeoexample]: #single-flexible-example-vimeo
[youtubeshortcode]: /gestion-contenu/shortcodes/#youtube "See how to use Hugo's built-in YouTube shortcode."