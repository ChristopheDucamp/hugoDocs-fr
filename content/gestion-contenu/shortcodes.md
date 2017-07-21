---
title: Shortcodes
linktitle:
description: Les shortcodes sont de simples fragments de code dans vos fichiers de contenu appelant des modèles intégrés ou personnalisés
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
menu:
  docs:
    parent: "gestion-contenu"
    weight: 35
weight: 35	#rem
categories: [gestion de contenu]
#tags: [markdown,shortcodes, contenu]
draft: false
aliases: [/extras/shortcodes/]
toc: true
---

## C'est Quoi un Shortcode

Hugo adore le Markdown en raison de son format de contenu simple, mais il arrive parfois que Markdown échoue. Souvent, les auteurs de contenu sont forcés d'ajouter du HTML brut (par exemple, la vidéo `<iframes>`) au contenu Markdown. Nous pensons que cela va à l'encontre de la belle promesse de simplicité de la syntaxe de Markdown.

Hugo a créé les **shortcodes** pour contourner ces limitations.

Un shortcode est un extrait simple dans un fichier de contenu que Hugo rendra à l'aide d'un modèle prédéfini. Notez que les codes courts ne fonctionneront pas dans les fichiers de modèle. Si vous avez besoin du type de fonctionnalité déroulante fournie par les shortcodes, mais dans un modèle, vous ferez probablement à la place un [modèle partiel][partials].

En plus d'un Markdown plus propre, ces codes courts peuvent être mis à jour à tout moment pour renvoyer de nouvelles classes, techniques ou standards. Au stade de génération du site, les codes courts de Hugo se fusionneront facilement dans vos modifications. Vous évitez une opération de rechercher/ remplacer éventuellement compliquée.

## Utiliser les Shortcodes

Dans vos fichiers de contenu, un shortcode peut être appelé en appelant `{{%/* nomshortcode parametres */%}}`. Les paramètres de shortcode sont délimités par un espace et les paramètres avec des espaces internes peuvent être cités.

Le premier mot dans la déclaration shortcode est toujours le nom du shortcode. Les paramètres suivent le nom. Selon la façon dont le code court est défini, les paramètres peuvent être nommés, positionnels ou les deux, bien que vous ne puissiez pas mélanger les types de paramètres en un seul appel. Le format pour les modèles de paramètres nommés est celui de HTML avec le format `nom="valeur"`.

Certains codes courts utilisent ou nécessitent la fermeture de codes courts. Encore une fois comme en HTML, les codes abrégés d'ouverture et de fermeture correspondent (nom uniquement) à la déclaration de clôture, qui est précédée d'une barre oblique.

Voici deux exemples de codes courts couplés :

```md
{{%/* mdshortcode */%}}Stuff to `process` in the *center*.{{%/* /mdshortcode */%}}
```

```md
{{</* highlight go */>}} A bunch of code here {{</* /highlight */>}}
```

Les exemples ci-dessus utilisent deux délimiteurs différents, la différence étant le caractère `%' dans le premier et les caractères `<>` dans le second.

### Shortcodes avec Markdown

Le caractère `%` indique que le contenu interne du shortcode --- appelé dans le [modèle shortcode][sctemps] avec la [variable `.Inner`][scvars]--- nécessite un traitement ultérieur par le processeur de rendu de la page (c.-à-d. via Blackfriday). Dans l'exemple suivant, Blackfriday convertirait `**World**` en `<strong>World</ strong>` :

```md
{{%/* myshortcode */%}}Hello **World!**{{%/* /myshortcode */%}}
```

### Shortcodes Sans Markdown

Le caractère `<` indique que le contenu interne du shortcode ne nécessite *pas* plus de rendu. Souvent, les codes courts sans markdown incluent du HTML interne :

```md
{{</* myshortcode */>}}<p>Hello <strong>World!</strong></p>{{</* /myshortcode */>}}
```

### Shortcodes Imbriqués

Vous pouvez appeler des codes courts dans d'autres shortcodes en créant vos propres modèles qui utilisent la variable `.Parent`. `.Parent` vous permet de vérifier le contexte dans lequel le code court est appelé. Voir [Modèles de shortcode][sctemps].

## Utiliser les Shortcodes Intégrés de Hugo

Hugo est livré avec un ensemble de codes courts prédéfinis qui représentent un usage très courant. Ces codes courts sont fournis pour la commodité de l'auteur et pour maintenir votre contenu markdown propre.

### `figure`

`figure` est une extension de la syntaxe image en markdown, qui ne fournit pas de raccourci pour l'élément plus sémantique  [`<figure>` du HTML5][figureelement].

Le shortcode `figure` peut utiliser les paramètres nommés suivants :

* `src`
* `link`
* `title`
* `caption`
* `class`
* `attr` (i.e., attribution)
* `attrlink`
* `alt`

#### Exemple Input `figure`

{{% code file="figure-input-example.md" %}}
```markdown
{{</* figure src="/media/spf13.jpg" title="Steve Francia" */>}}
```
{{% /code %}}

#### Exemple Output `figure`

{{% output file="figure-output-example.html" %}}
```html
<figure>
  <img src="/media/spf13.jpg"  />
  <figcaption>
      <h4>Steve Francia</h4>
  </figcaption>
</figure>
```
{{% /output %}}

### `gist`

Les blogueurs veulent souvent inclure des gists GitHub au moment d'écrire des posts. Supposons que nous voulions utiliser le [gist à l'url qui suit][examplegist] :

```html
https://gist.github.com/spf13/7896402
```

Nous pouvons intégrer le gist dans notre contenu via le nom d'utilisateur et l'ID gist extraite de l'URL :

```md
{{</* gist spf13 7896402 */>}}
```

#### Exemple Input `gist`

Si le gist contient plusieurs fichiers et que vous souhaitez citer un seul d'entre eux, vous pouvez passer le nom de fichier (cité) en tant que troisième argument facultatif :

{{% code file="gist-input.md" %}}
```md
{{</* gist spf13 7896402 "img.html" */>}}
```
{{% /code %}}

#### Exemple Output `gist`

{{% output file="gist-output.html" %}}
```html
{{< gist spf13 7896402 >}}
```
{{% /output %}}

#### Exemple Affichage `gist` 

Pour démontrer l'efficacité remarquable de la fonctionnalité shortcode de Hugo, nous avons intégré l'exemple `gist` `spf13` dans cette page. Ce qui suit simule l'expérience pour les visiteurs de votre site. Naturellement, l'affichage final dépend de vos feuilles de style et des balises environnantes.

{{< gist spf13 7896402 >}}

### `highlight`

Ce code court convertira le code source fourni en HTML mettant  la syntaxe en surbrillance. Pour en savoir plus, regardez [mise en surbrillance](/tools/syntax-highlighting/). `highlight` prend exactement un paramètre `language` requis et nécessite un shortcode de fermeture.

#### Exemple Input `highlight` 

{{% code file="content/tutorials/learn-html.md" %}}
```html
{{</* highlight html */>}}
<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Data.Pages }}
        {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{</* /highlight */>}}
```
{{% /code %}}

#### Exemple Output `highlight` 

Cet exemple de shortcode `highlight` au-dessus produirait le HTML suivant au moment où le site est produit :

{{% output file="tutorials/learn-html/index.html" %}}
```html
<span style="color: #f92672">&lt;section</span> <span style="color: #a6e22e">id=</span><span style="color: #e6db74">&quot;main&quot;</span><span style="color: #f92672">&gt;</span>
  <span style="color: #f92672">&lt;div&gt;</span>
   <span style="color: #f92672">&lt;h1</span> <span style="color: #a6e22e">id=</span><span style="color: #e6db74">&quot;title&quot;</span><span style="color: #f92672">&gt;</span>{{ .Title }}<span style="color: #f92672">&lt;/h1&gt;</span>
    {{ range .Data.Pages }}
        {{ .Render &quot;summary&quot;}}
    {{ end }}
  <span style="color: #f92672">&lt;/div&gt;</span>
<span style="color: #f92672">&lt;/section&gt;</span>
```
{{% /output %}}

{{% note "More on Syntax Highlighting" %}}
Pour voir encore plus d'options pour ajouter la mise en surbrillance de blocs de code pour votre site web, regardez [Mise en Surbrillance dans les Outils du Développeur](/tools/syntax-highlighting/).
{{% /note %}}

### `instagram`

Si vous souhaitez intégrer une photo provenant d'[Instagram][], vous n'avez besoin que de l'ID de la photo. Vous pouvez retrouver l'ID de photo Instagram à partir de l'URL :

```html
https://www.instagram.com/p/BWNjjyYFxVx/
```

#### Exemple Input `instagram` 

{{% code file="instagram-input.md" %}}
```md
{{</* instagram BWNjjyYFxVx */>}}
```
{{% /code %}}

Vous avez aussi l'option de cacher la légende :

{{% code file="instagram-input-hide-caption.md" %}}
```md
{{</* instagram BWNjjyYFxVx hidecaption */>}}
```
{{% /code %}}

#### Exemple Output `instagram` 

En ajoutant l'exemple précédent `hidecaption`, le HTML suivant sera ajouté à votre marquage de rendu de site web : 

{{% output file="instagram-hide-caption-output.html" %}}
```html
{{< instagram BWNjjyYFxVx hidecaption >}}
```
{{% /output %}}

#### Exemple Affichage `instagram` 

En utilisant l'exemple précédent `instagram` avec l'exemple `hidecaption` ci-dessus, ce qui suit simule l'expérience affichée pour les visiteurs de votre site. Naturellement, l'affichage final dépend de vos feuilles de style et des balises environnantes.

{{< instagram BWikbcNFUV8 hidecaption >}}


### `ref` and `relref`

Ces shortcodes recherchent les pages par leur chemin relatif (par ex., `blog/post.md`) ou leur nom logique (`post.md`) et renvoient le permalien (`ref`) ou le permalien relatif (`relref`) pour la page trouvée.

`ref` et `relref` permettent également de créer des liens fragmentaires qui fonctionnent pour les liens d'en-tête générés par Hugo.

{{% note "More on Cross References" %}}
Lisez une description plus détaillée de `ref` et `relref` dans la documentation sur les [références croisées](/content-management/cross-references/).
{{% /note %}}

`ref` et `relref` prennent exactement un paramètre requis de  _reference_, citée et en position `0`.

#### Exemple Input `ref` and `relref`

```md
[Neat]({{</* ref "blog/neat.md" */>}})
[Who]({{</* relref "about.md#who" */>}})
```

#### Exemple Output `ref` et `relref`

En supposant que les pretty URLs standards d'Hugo soient activées :

```html
<a href="/blog/neat">Neat</a>
<a href="/about/#who:c28654c202e73453784cfd2c5ab356c0">Who</a>
```

### `speakerdeck`

Pour embarquer les slides provenant de [Speaker Deck][], cliquez sur "&lt;&#8239;/&gt;&nbsp;Embed" (sous Share tout à droite du modèle sur Speaker Deck) et copiez l'URL :

```html
<script async class="speakerdeck-embed" data-id="4e8126e72d853c0060001f97" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>
```

#### Exemple Input `speakerdeck`

Extrayez la valeur du champ `data-id` et passez-la dans le shortcode :

{{% code file="speakerdeck-example-input.md" %}}
```md
{{</* speakerdeck 4e8126e72d853c0060001f97 */>}}
```
{{% /code %}}

#### Exemple Output `speakerdeck`

{{% output file="speakerdeck-example-input.md" %}}
```html
{{< speakerdeck 4e8126e72d853c0060001f97 >}}
```
{{% /output %}}

#### Exemple Affichage `speakerdeck`

Pour l'exemple précédent `speakerdeck`, ce qui suit simule l'expérience affichée pour les visiteurs de votre site. Naturellement, l'affichage final dépend de vos feuilles de style et des balises environnantes.

{{< speakerdeck 4e8126e72d853c0060001f97 >}}

### `tweet`

Vous souhaitez inclure un tweet unique dans votre publication de blog ? Tout ce dont vous avez besoin c'est l'URL du tweet : 

```
https://twitter.com/spf13/status/877500564405444608
```

#### Exemple Input `tweet`

Passez l'ID du tweet à partir de l'URL comme paramètre pour le shortcode `tweet` :

{{% code file="example-tweet-input.md" %}}
```md
{{</* tweet 877500564405444608 */>}}
```
{{% /code %}}

#### Exemple Output `tweet`

En utilisant l'exemple du tweet précédent, le HTML suivant sera ajouté au marquage de votre site web :

{{% output file="example-tweet-output.html" %}}
```html
{{< tweet 877500564405444608 >}}
```
{{% /output %}}

#### Exemple Affichage `tweet`

En utilisant l'exemple du `tweet` précédent, ce qui suit simule l'expérience affichée pour les visiteurs de votre site web. Naturellement, l'affichage final dépend de vos feuilles de tyles et du marquage environnant.

{{< tweet 877500564405444608 >}}

### `vimeo`

Ajouter une vidéo à partir de [Vimeo][] est équivalent au shortcode YouTube vu au-dessus.

```
https://vimeo.com/channels/staffpicks/146022717
```

#### Exemple Input `vimeo`

Extrayer l'ID à partir de l'URL de la vidéo et passer la dans le shortcode `vimeo` :

{{% code file="example-vimeo-input.md" %}}
```md
{{</* vimeo 146022717 */>}}
```
{{% /code %}}

#### Exemple Output `vimeo` 

En utilisant l'exemple `vimeo` précédent, le HTML suivant sera ajouté au marquage rendu de votre site : 

{{% output file="example-vimeo-output.html" %}}
```html
{{< vimeo 146022717 >}}
```
{{% /output %}}

{{% tip %}}
Si vous voulez personnaliser plus à fond le style visuel de votre output YouTube ou Vimeo, ajoutez un paramètre nommé `class` au moment d'appeler le shortcode. Le nouveau `class` sera ajouté à la `<div>` qui emballe le `<iframe>` *et* retirera les styles dans la ligne. Notez que vous devrez appeler l'`id` comme un paramètre nommé.

```md
{{</* vimeo id="146022717" class="my-vimeo-wrapper-class" */>}}
```
{{% /tip %}}

#### Exemple Affichage `vimeo`

En utilisant l'exemple `vimeo` précédent, ce qui suit simule l'expérience affichée pour les visiteurs de votre site web. Naturellement, l'affichage final dépend de vos feuilles de tyles et du marquage environnant.

{{< vimeo 146022717 >}}

### `youtube`

Le shortcode `youtube` intègre un lecteur vidéo responsive pour  les [vidéos YouTube][YouTube videos]. Seul l'ID de la vidéo est requis, par exemple :

```
https://www.youtube.com/watch?v=w7Ft2ymGmfc
```


#### Exemple Input `youtube`

Copiez l'ID vidéo YouTube qui suit `v=` dans l'URL de la vidéo et passez la dans le shortcode `youtube` :

{{% code file="example-youtube-input.md" %}}
```md
{{</* youtube w7Ft2ymGmfc */>}}
```
{{% /code %}}

En outre, vous pouvez lancer automatiquement la lecture de la vidéo incorporée en définissant le paramètre `autoplay` sur  `true`. N'oubliez pas que vous ne pouvez pas mélanger un paramètre nommé sans nom, vous devez donc attribuer l'identifiant vidéo non nommé au paramètre `id` :


{{% code file="example-youtube-input-with-autoplay.md" %}}
```md
{{</* youtube id="w7Ft2ymGmfc" autoplay="true" */>}}
```
{{% /code %}}

#### Exemple Output `youtube`

En utilisant l'exemple `youtube` précédent, le HTML suivant sera ajouté au marquage rendu de votre site :

{{% code file="example-youtube-output.html" %}}
```html
{{< youtube id="w7Ft2ymGmfc" autoplay="true" >}}
```
{{% /code %}}

#### Exemple Affichage `youtube` 

En utilisant l'exemple `youtube` précédent (sans `autoplay="true"`), ce qui suit simule l'expérience affichée pour les visiteurs de votre site web. Naturellement, l'affichage final dépend de vos feuilles de tyles et du marquage environnant. La vidéo est aussi incluse dans le [Quick Start de la documentation Hugo][quickstart].

{{< youtube w7Ft2ymGmfc >}}

## Créer des Shortcodes Personnalisés

Pour en savoir plus sur la création de shortcodes personnalisés, regardez la [documentation du modèle de shortcode][shortcode template documentation].

[`figure` shortcode]: #figure
[contentmanagementsection]: /content-management/formats/
[examplegist]: https://gist.github.com/spf13/7896402
[figureelement]: http://html5doctor.com/the-figure-figcaption-elements/ "An article from HTML5 doctor discussing the fig and figcaption elements."
[Instagram]: https://www.instagram.com/
[pagevariables]: /variables/page/
[partials]: /templates/partials/
[Pygments]: http://pygments.org/
[quickstart]: /demarrage/quickstart/
[sctemps]: /templates/shortcode-templates/
[scvars]: /variables/shortcodes/
[shortcode template documentation]: /templates/shortcode-templates/
[Speaker Deck]: https://speakerdeck.com/
[templatessection]: /templates/
[Vimeo]: https://vimeo.com/
[YouTube Videos]: https://www.youtube.com/
