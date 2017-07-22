---
title: Surbrillance de Syntaxe
linktitle:
description: Hugo fournit la mise en surbrillance de la syntaxe côté serveur via Pygments et, comme la plupart des générateurs de sites statiques, il fonctionne aussi très bien avec les bibliothèques de mise en surbrillance de la syntaxe côté client (JavaScript).
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
#tags: [highlighting,pygments,code blocks,syntax, syntaxe, surbrillance]
categories: [outils du développeur]
draft: false
aliases: [/extras/highlighting/,/extras/highlight/]
toc: true
---
Hugo peut mettre en surbrillance le code source de _deux manières différentes_&mdash;soit du côté du serveur à partir de votre contenu, soit en différant le traitement côté client, en utilisant une bibliothèque JavaScript.

## Côté-serveur

Pour l'approche prétraitée, la mise en surbrillance est effectuée par un programme externe basé sur Python appelé [Pygments](http://pygments.org/) et déclenchée via un shortcode intégré Hugo (voir [exemple](#exemple-input-shortcode-highlight) ci-dessous). Si Pygments est absent du chemin, il passera silencieusement le contenu sans souligner.

### Avantages côté-serveur

Les avantages de la syntaxe de mise en surbrillance côté serveur sont de ne pas dépednre d'une bibliothèque JavaScript et, par conséquent, cela fonctionne très bien lorsqu'elle est lue à partir d'un flux RSS.

### Pygments

Si vous n'avez jamais travaillé avec Pygments avant, voici une brève introduction:

+ Installez Python à partir de [python.org](https://www.python.org/downloads/). La version 2.7.x est déjà suffisante.
+ Exécuter `pip install Pigments` afin d'installer Pygments. Une fois installé, Pygments vous donne une commande `pygmentize`. Assurez-vous qu'elle soit bien dans votre PATH ; sinon, Hugo ne pourra pas le trouver et l'utiliser.

Sur les systèmes Debian et Ubuntu, vous pouvez également installer Pygments en exécutant `sudo apt-get install python3-pygments`.

Hugo vous offre deux options que vous pouvez configurer avec la variable `pygmentsuseclasses` (par défaut `false`) dans votre [configuration de site][/demarrage/configuration).

1. Les codes de couleur pour les mots clés en surbrillance sont directement insérés si `pygmentsuseclasses=false` (par défaut). Les codes de couleur dépendent de votre choix de `pygmentsstyle` (par défaut =`"monokai"`). Vous pouvez explorer les différents styles de couleurs sur [pygments.org](http://pygments.org/) après avoir inséré un exemple de code.
2. Si vous choisissez `pygmentsuseclasses=true`, Hugo inclut les noms de classe dans votre code au lieu des codes de couleurs. Pour que les noms de classe soient significatifs, vous devez inclure un fichier `.css` dans votre site Web représentant votre système de couleurs. Vous pouvez soit générer ces fichiers `.css` en fonction de [la description de la documentation Pygments](http://pygments.org/docs/cmdline/) ou télécharger l'un des nombreux modèles de couleurs pré-construits du [repo GitHub CSS de Pygments](https://github.com/richleland/pygments-css).

### Usage côté-serveur

La mise en surbrillance s'effectue via le [shortcode intégré](/gestion-contenu/shortcodes/) `highlight`. `highlight` prend exactement un paramètre requis pour que le langage de programmation soit en surbrillance et nécessite un shortcode de fermeture. Notez que `highlight` n'est pas utilisé pour la mise en surbrillance javascript côté client.

### Exemple Input Shortcode `highlight` 

{{% code file="example-highlight-shortcode-input.md" %}}
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

### Exemple Output Shortcode `highlight`

{{% output file="example-highlight-shortcode-output.html" %}}
```
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

### Options

Les options de contrôle de la mise en surbrillance peuvent être ajoutées dans le deuxième argument en tant que liste de valeurs-clés séparées par des virgules. L'exemple ci-dessous mettra en surbrillance dans `go` avec des numéros de ligne et les numéros de ligne 2 et 3 surlignés.

Options for controlling highlighting can be added in the second argument as a quoted, comma-separated key-value list. The example below will syntax highlight in `go` with inline line numbers and line numbers 2 and 3 highlighted.

```
{{</* highlight go "linenos=inline,hl_lines=2 3" */>}}
var a string
var b string
var c string
var d string
{{</* / highlight */>}}
```

Le shortcode `highlight` inclut les mots-clés supportés suivants: 

* `style`
* `encoding`
* `noclasses`
* `hl_lines`
* `linenos`

Notez que `style` et` noclasses` remplacent le paramètre similaire dans [configuration globale][config]

Les mots-clés du shortcode `highlight` reflètent ceux de Pygments à partir de la ligne de commande. Consultez la [documentation Pygments](http://pygments.org/docs/) pour plus d'informations.


### Code Fences

Il est également possible d'ajouter une mise en surbrillance de syntaxe avec des "clôtures de code enrichies de GitHub". Pour activer cela, définissez `PygmentsCodeFences` sur `true` dans votre [fichier de configuration][config] Hugo :

```html
<section id="main">
  <div>
    <h1 id="title">{{ .Title }}</h1>
    {{ range .Data.Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
```


{{% note "Disclaimers on Pygments" %}}
* Pygments est relativement lent et _provoque une baisse de  performance lors de la construction de votre site_, mais Hugo a été conçu pour mettre en cache les résultats sur le disque.
* La mise en cache peut être désactivée en réglant l'option `--ignoreCache` sur `true`.
* Les langages disponibles pour la mise en surbrillance dépendent de votre installation Pygments.
{{% /note %}}

## Côté Client

Alternativement, la mise en surbrillance de code peut être appliquée à vos blocs de code dans JavaScript côté client.

La mise en surbrillance de la syntaxe côté client est très simple à ajouter. Vous devrez choisir une bibliothèque et un thème correspondants. Certaines bibliothèques populaires sont :

- [Highlight.js]
- [Prism]
- [Rainbow]
- [Syntax Highlighter]
- [Google Prettify]

### Avantages côté client

Les avantages de la mise en surbrillance de la syntaxe côté client sont que cela ne coûte rien lors de la construction de votre site, et que certains des scripts de mise en surbrillance disponibles couvrent plus de langues que Pygments.

### Exemple Highlight.js

Cet exemple utilise la populaire bibliothèque [Highlight.js], hébergée par [Yandex], un moteur de recherche russe populaire.

Dans votre dossier `./layouts/partials /` (ou `./layouts/chrome/`), selon votre thème spécifique, il y aura un extrait qui sera inclus dans chaque page HTML générée, comme `header.html` ou `header.includes.html`. Ajoutez simplement css et js pour initialiser [Highlight.js] :

```
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/styles/default.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.6.0/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```

### Exemple Prism

Prism est une autre bibliothèque populaire de surligneur et elle est utilisée sur certains sites importants.
La section [téléchargement du site web prism.js][prismdownload] est simple à utiliser et vous offre un haut degré de personnalisation pour ne choisir que les langages que vous utiliserez sur votre site.

Similaire à Highlight.js, vous chargez simplement `prism.css` dans votre `<head>` avec n'importe quel modèle partiel de Hugo qui crée cette partie de vos pages :

```html
...
<link href="/css/prism.css" rel="stylesheet" />
...
```

Ajoutez `prism.js` près du bas de votre balise `<body>` dans tout modèle de partiel approprié pour votre site ou thème.

```html
...
<script src="/js/prism.js"></script>
</body>
```

Dans cet exemple, les chemin local, indique que votre copie téléchargée de ces fichiers a été ajoutée au site, typiquement sous `./static/css/` et `./static/js/`, respectivement.

### Usage côté-client

Pour utiliser la mise en surbrillance côté client, la plupart de ces bibliothèques javascript s'attendent à ce que votre code soit enveloppé dans des éléments `<code>` sémantiquement corrects avec des attributs de classe spécifiques au langage. Par exemple, un bloc de code pour HTML aurait `class="language-html "`.

Le script de mise en surbrillance côté client recherche donc des classes de langage de programmation selon cette convention : `language-go`,` language-html`, `language-css`,` language-bash`, etc. Si vous regardez la source de la page, vous pouvez voir quelque chose comme suit :

```html
<pre>
  <code class="language-css">
  body {
    font-family: "Noto Sans", sans-serif;
  }
  </code>
</pre>
```

Si vous utilisez le markdown, vos pages de contenu doivent utiliser la syntaxe suivante, avec le nom de langage à mettre en surbrillance directement après la première "fence". Un bloc de code clôturé peut être noté en ouvrant et en fermant trois tildes <kbd>~</ kbd> ou trois "back ticks" <kbd>`</ kbd> :


{{< nohighlight >}}
~~~css
body {
  font-family: "Noto Sans", sans-serif;
}
~~~
{{< /nohighlight >}}

Voici le même exemple avec trois backticks pour indiquer le bloc code clôturé :

{{< nohighlight >}}
```css
body {
  font-family: "Noto Sans", sans-serif;
}
```
{{< /nohighlight >}}

Passer les exemples ci-dessus à travers le script du surligneur donnerait le balisage suivant :

{{< nohighlight >}}
&lt;pre&gt;&lt;code class="language-css hljs"&gt;;&lt;span class="hljs-selector-tag"&gt;body&lt;/span&gt; {
  &lt;span class="hljs-attribute"&gt;font-family&lt;/span&gt;: &ltspan class="hljs-string"&gt;"Noto Sans"&lt;/span&gt;, sans-serif;
}
{{< /nohighlight >}}

Dans le cas du schéma de couleurs de codage utilisé par les docs Hugo, la sortie résultante ressemblerait à celle des utilisateurs finaux du site Web:

```css
body {
  font-family: "Noto Sans", sans-serif;
}
```

Consultez la documentation des bibliothèques individuelles pour savoir comment mettre en œuvre chacune des bibliothèques basées sur JavaScript.

[config]: /demarrage/configuration
[Prism]: http://prismjs.com
[prismdownload]: http://prismjs.com/download.html
[Highlight.js]: http://highlightjs.org/
[Rainbow]: http://craig.is/making/rainbows
[Syntax Highlighter]: http://alexgorbatchev.com/SyntaxHighlighter/
[Google Prettify]: https://github.com/google/code-prettify
[Yandex]: http://yandex.ru/