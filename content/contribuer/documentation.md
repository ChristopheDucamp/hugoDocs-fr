---
title: Contribuer à la Documentation Hugo
linktitle: Documentation
description: La documentation fait partie intégrante de tout projet open source. La documentation d'Hugo est plus qu'un chantier en cours du fait de la source qu'elle essaye de couvrir.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [contribute, contribuer]
#tags: [docs,documentation,community, contribute, contribuer]
menu:
  docs:
    parent: "contribute"
    weight: 20
weight: 20
sections_weight: 20
draft: false
aliases: [/contribute/docs/]
toc: true
---

## Créez votre Fork

Il est préférable d'apporter des modifications aux documents Hugo sur votre machine locale pour vérifier la cohérence du style visuel. Assurez-vous que vous avez créé une bifurcation de [hugoDocs](https://github.com/gohugoio/hugoDocs) sur GitHub et cloné le dépôt localement sur votre machine. Pour plus d'informations, vous pouvez voir [la documentation de GitHub sur "forking"][ghforking] ou suivre avec [le guide de contribution au développement de Hugo][hugodev].

Vous pouvez ensuite créer une branche distincte pour vos ajouts. Assurez-vous de choisir un nom de branche descriptif qui correspond le mieux au type de contenu. Voici un exemple de nom de branche que vous pourriez utiliser pour ajouter un nouveau site Web à la vitrine : 

```git
git checkout -b jean-dupont-showcase-addition
```

## Ajouter du Nouveau Contenu

La documentation Hugo fait un usage intense de la fonctionnalité [archétypes][archetypes] d'Hugo. Toutes les sections de contenu de la documentation de Hugo ont un archétype attribué.

L'ajout de nouveaux contenus aux documents Hugo suit le même modèle, quelle que soit la section de contenu :

```
hugo new <DOCS-SECTION>/<nouveau-contenu-basdecasse>.md
```

{{% panel theme="success" header="`title:`, `date:`, et Ordre des Champs" %}}
Les champs `title` et `date` sont ajoutés automatiquement lors de l'utilisation d'archétypes via `hugo new`. Ne vous inquiétez pas si l'ordre des champs d'entrée du nouveau fichier sur votre machine locale est différent de celui des exemples fournis dans les documents Hugo.
C'est un problème connu [(#452)](https://github.com/gohugoio/hugo/issues/452).
{{% /panel %}}

### Ajouter une Nouvelle Fonction

Une fois que vous avez cloné le dépôt Hugo, vous pouvez créer une nouvelle fonction via la commande suivante. Gardez le nom du fichier en minuscule.

```
hugo new functions/nouvellefonction.md
```

L'archetype pour `functions` selon le thème Hugo est comme suit : 

{{% code file="archetypes/functions.md" %}}
```yaml
{{< readfile file="/archetypes/functions.md">}}
```
{{% /code %}}

#### Nouveaux Champs Obligatoires de Fonction 

Voici une analyse des champs de front matter générés automatiquement pour vous en utilisant `hugo new functions/*` :

***`title`***
: ceci sera pré-rempli en bas de casse quand vous utilisez le générateur `hugo new`.

***`linktitle`***
: la casse réelle de la fonction (par exemple, `replaceRE` plutôt que` replacere`).

***`description`***
: Une brève description utilisée pour remplir la [Référence rapide des fonctions](/functions/).

`categories`
: actuellement auto-remplie avec `functions` pour des raisons d'avenir et de portabilité seulement ; ignorez ce champ.

`tags`
: seulement si vous pensez que cela aidera les utilisateurs finaux à trouver d'autres fonctions connexes

`signature`
: this is a signature/syntax definition for calling the function (e.g., `apply SEQUENCE FUNCTION [PARAM...]`).

`workson`
: acceptable values include `lists`,`taxonomies`, `terms`, `groups`, and `files`.

`hugoversion`
: the version of Hugo that will ship with this new function.

`relatedfuncs`
: other [templating functions][] you feel are related to your new function to help fellow Hugo users.

`{{.Content}}`
: an extended description of the new function; examples are not only welcomed but encouraged.

Dans le corps de votre fonction, développez la courte description utilisée dans le front matter. Incluez le plus grand nombre d'exemples possibles et tirez parti de Hugo docs [`code` shortcode](#adding-code-blocks). Si vous ne parvenez pas à ajouter des exemples, mais souhaitez solliciter l'aide de la communauté Hugo, ajoutez `needsexample: true` à votre front matter.

### Ajouter un Nouveau Tutoriel

Une fois que vous avez cloné le dépôt Hugo, vous pouvez créer un nouveau tutoriel via la commande suivante. Nommez le fichier de réduction en conséquence :

```
hugo new tutorials/mon-nouveau-tutoriel.md
```

L'archetype pour le type de contenu `tutorials` est comme suit :

{{% code file="archetypes/tutorials.md" %}}
```yaml
{{< readfile file="/archetypes/tutorials.md">}}
```
{{% /code %}}

## Ajouter des Blocs de Code

Les blocs de code sont essentiels pour fournir des exemples de nouvelles fonctionnalités de Hugo aux utilisateurs finaux de la documentation Hugo. Dans la mesure du possible, créez des exemples que vous pensez que les utilisateurs Hugo pourront mettre en œuvre dans leurs propres projets.

### Syntaxe Standard

Dans toutes les pages des docs Hugo, on utilise la syntaxe typique markdown du "triple-back-tick". Si vous ne souhaitez pas prendre plus de temps pour implémenter les codes courts du code suivant, utilisez le markdown standard enrichi par GitHub. Les Hugo docs utilisent une version de [highlight.js](https://highlightjs.org/) avec un ensemble spécifique de langages.

Vos options pour les langages sont `xml`/`html`, `go`/`golang`, `md`/`markdown`/`mkd`, `handlebars`, `apache`, `toml`, `yaml`, `json`, `css`, `asciidoc`, `ruby`, `powershell`/`ps`, `scss`, `sh`/`zsh`/`bash`/`git`, `http`/`https`, et `javascript`/`js`.

````html
```html
<h1>Salut le monde !</h1>
```
````

### Shortcode de Bloc de Code

La documentation Hugo contient un shortcode très robuste pour l'ajout de blocs de code interactifs.

{{% note %}}
Avec les shortcodes `code`, *vous devez inclure des tiques triples et une déclaration de langage*. Cela a été fait en conception afin que les enveloppes de shortcode soient facilement ajoutées à la documentation existante et seront beaucoup plus faciles à supprimer si nécessaire dans les futures versions des documents Hugo.
{{% /note %}}

### `code`

`code` est le shortcode de la documentation Hugo que vous utiliserez le plus souvent. `code` ne requiert qu'un paramètre nommé : `file`. Voici le modèle :

````markdown
{{%/* code file="smart/file/name/with/path.html" download="download.html" copy="true" */%}}
```langage
Un bon paquet de code peut aller ici !
```
{{%/* /code */%}}
````

Ce qui suit sont les arguments passés à l'intérieur de `code`:

***`file`***
: Le seul argument * requis *. Le `file` est nécessaire pour le style, mais joue également un rôle important pour aider les utilisateurs à créer un modèle mental autour de la structure de répertoire de Hugo. Visuellement, cela sera affiché en tant que texte en haut à gauche du bloc de code.

`download`
: if omitted, this will have no effect on the rendered shortcode. When a value is added to `download`, it's used as the filename for a downloadable version of the code block.

`copy`
: Un bouton de copie est ajouté automatiquement à tous les shortcodes `code`. Si vous souhaitez conserver le nom de fichier et le style de `code`, mais ne souhaitez pas encourager les lecteurs à copier le code (par exemple, un extrait "Ne faites pas" dans un didacticiel), utilisez `copy="false"`.

#### Exemple Input `code`

Cet exemple de bloc de code HTML indique aux utilisateurs de Hugo ce qui suit :

1. Ce fichier *pourrait* vivre dans `layouts/_default`, comme démontré par `layouts/_default/single.html` en tant que valeur pour `file`.
2. Cet extrait est suffisamment complet pour être téléchargé et mis en œuvre dans un projet Hugo, comme démontré par `download="single.html"`.

````md
{{%/* code file="layouts/_default/single.html" download="single.html" */%}}
```html
{{ define "main" }}
<main>
    <article>
        <header>
            <h1>{{.Title}}</h1>
            {{with .Params.subtitle}}
            <span>{{.}}</span>
        </header>
        <div>
            {{.Content}}
        </div>
        <aside>
            {{.TableOfContents}}
        </aside>
    </article>
</main>
{{ end }}
```
{{%/* /code */%}}
````

##### Exemple Affichage 'code'

L'output de cet exemple sera rendu dans la doc Hugo comme suit : 

{{% code file="layouts/_default/single.html" download="single.html" %}}
```html
{{ define "main" }}
<main>
    <article>
        <header>
            <h1>{{.Title}}</h1>
            {{with .Params.subtitle}}
            <span>{{.}}</span>
        </header>
        <div>
            {{.Content}}
        </div>
        <aside>
            {{.TableOfContents}}
        </aside>
    </article>
</main>
{{ end }}
```
{{% /code %}}

<!-- #### Output Code Block

The `output` shortcode is almost identical to the `code` shortcode but only takes and requires `file`. The purpose of `output` is to show *rendered* HTML and therefore almost always follows another basic code block *or* and instance of the `code` shortcode:

````html
{{%/* output file="post/my-first-post/index.html" */%}}
```html
<h1>This is my First Hugo Blog Post</h1>
<p>I am excited to be using Hugo.</p>
```
{{%/* /output */%}}
````

The preceding `output` example will render as follows to the Hugo docs:

{{% output file="post/my-first-post/index.html" %}}
```html
<h1>This is my First Hugo Blog Post</h1>
<p>I am excited to be using Hugo.</p>
```
{{% /output %}} -->

## Citations

Les blocs de citation peuvent être ajoutés à la documentation de Hugo en utilisant [la syntaxe typique de blockquote de Markdown][bqsyntax] :

```markdown
> Without the threat of punishment, there is no joy in flight.
```

La citation précédente sera rendue comme suit dans la documentation Hugo :

> Without the threat of punishment, there is no joy in flight.

Cependant, vous pouvez ajouter un élément «<cite>` simple et rapide (ajouté sur le client via JavaScript) en séparant votre citation principale et la citation avec un trait d'union avec un seul espace de chaque côté :

```markdown
> Without the threat of punishment, there is no joy in flight. - [Kobo Abe](https://en.wikipedia.org/wiki/Kobo_Abe)
```

Ce qui sortira comme suit dans la doc Hugo : 

> Without the threat of punishment, there is no joy in flight. - [Kobo Abe][abe]

{{% note "Blockquotes `!=` Admonitions" %}}
Les versions précédentes de la documentation de Hugo ont utilisé les blocs de citation pour attirer l'attention sur le texte. Ceci n'est *pas* l'[utilisation sémantique voulue de `<blockquote>`](http://html5doctor.com/cite-and-blockquote-reloaded/). Utilisez des blockquotes pour citer. Pour indiquer ou avertir votre utilisateur d'informations spécifiques, utilisez les codes courts d'avertissement qui suivent.
{{% /note %}}

## Admonitions

**Admonitions** are common in technical documentation. The most popular is that seen in [reStructuredText Directives][sourceforge]. From the SourceForge documentation:

> Admonitions are specially marked "topics" that can appear anywhere an ordinary body element can. They contain arbitrary body elements. Typically, an admonition is rendered as an offset block in a document, sometimes outlined or shaded, with a title matching the admonition type. - [SourceForge][sourceforge]

La documentation Hugo contient trois admonitions : `note`, `tip`, et `warning`.

### `note` Admonition

Utilisez le shortcode `note` quand vous voulez attirer l'attention subtilement vers l'information. `note` est conçu pour être moins une interruption dans le contenu que ne l'est le `warning`.

#### Exemple Input `note`

{{% code file="note-avec-titre.md" %}}
```markdown
{{%/* note */%}}
Voici un élément d'information sur lequel je souhaiterais attirer votre **attention**.
{{%/* /note */%}}
```
{{% /code %}}

#### Exemple `note` Output

{{% output file="note-with-heading.html" %}}
```html
{{% note %}}
Here is a piece of information I would like to draw your **attention** to.
{{% /note %}}
```
{{% /output %}}

#### Exemple `note` Display

{{% note %}}
Here is a piece of information I would like to draw your **attention** to.
{{% /note %}}

### `tip` Admonition

Use the `tip` shortcode when you want to give the reader advice. `tip`, like `note`, is intended to be less of an interruption in content than is `warning`.

#### Exemple `tip` Input

{{% code file="using-tip.md" %}}
```markdown
{{%/* tip */%}}
Here's a bit of advice to improve your productivity with Hugo.
{{%/* /tip */%}}
```
{{% /code %}}

#### Exemple `tip` Output

{{% output file="tip-output.html" %}}
```html
{{% tip %}}
Here's a bit of advice to improve your productivity with Hugo.
{{% /tip %}}
```
{{% /output %}}

#### Exemple `tip` Display

{{% tip %}}
Here's a bit of advice to improve your productivity with Hugo.
{{% /tip %}}

### `warning` Admonition

Use the `warning` shortcode when you want to draw the user's attention to something important. A good usage example is for articulating breaking changes in Hugo versions, known bugs, or templating "gotchas."

#### Exemple `warning` Input

{{% code file="warning-admonition-input.md" %}}
```markdown
{{%/* warning */%}}
This is a warning, which should be reserved for *important* information like breaking changes.
{{%/* /warning */%}}
```
{{% /code %}}

#### Exemple Output `warning`

{{% output file="warning-admonition-output.html" %}}
```html
{{% warning %}}
This is a warning, which should be reserved for *important* information like breaking changes.
{{% /warning %}}
```
{{% /output %}}

#### Exemple d'Affichage `warning` 

{{% notice warning %}}
Ceci est un warning, qui devrait être réservé, pour de l'information *importante* comme des modifications de rupture.
{{% /notice %}}

{{% panel header="Pull Requests et Branches" %}}
Tout comme les principes de [contributions au développement d'Hugo](/contribuer/developpement/), l'équipe Hugo s'attend à ce que vous créiez une branche ou un fork séparé quand vous produisez vos contributions sur la documentation Hugo.
{{% /note %}}

[abe]: https://en.wikipedia.org/wiki/Kobo_Abe
[archetypes]: /gestion-contenu/archetypes/
[bqsyntax]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#blockquotes
[charcount]: http://www.lettercount.com/
[`docs/static/images/showcase/`]: https://github.com/gohugoio/hugo/tree/master/docs/static/images/showcase/
[ghforking]: https://help.github.com/articles/fork-a-repo/
[hugodev]: /contribuer/development/
[shortcodeparams]: gestion-contenu/shortcodes/#shortcodes-sans-markdown
[sourceforge]: http://docutils.sourceforge.net/docs/ref/rst/directives.html#admonitions
[templating function]: /fonctions/
