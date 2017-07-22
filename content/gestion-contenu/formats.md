---
title: Formats de Contenus Supportés
linktitle: Formats de Contenus Supportés
description: Markdown et Emacs Mode-Org ont un support natif, et des formats supplémentaires (par ex.Asciidoc) proviennent d'aides externes.
date: 2017-01-10
publishdate: 2017-01-10
lastmod: 2017-07-21
categories: [gestion de contenu]
#tags: [markdown,asciidoc,mmark,content format,contenu, format de contenu]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 20
weight: 20	#rem
draft: false
aliases: []
toc: true
---

**Markdown est le principal format de contenu** et il est livré avec deux saveurs : l'excellent [projet Blackfriday][blackfriday](nommez vos fichiers `*.md` ou réglez `markup = "markdown"` dans le front matter) ou son fork [Mmark][mmark] (nommez vos fichiers `*.mmark` ou réglez `markup = "mmark"` dans le front matter), tous les deux étant deux moteurs rapides markdown écrits en Go.

Pour les utilisateurs d'Emacs, [goorgeous](https://github.com/chaseadamsio/goorgeous) fournit un support natif intégré pour Org-mode (nommez vos fichiers `*.org` ou définissez `markup = "org"` dans le front matter).

{{% note "Listes profondément imbriquées" %}}
Avant de commencer l'écriture de votre contenu dans le marquage, Blackfriday a un problème connu [(# 329)] (https://github.com/russross/blackfriday/issues/329) avec la gestion de listes profondément imbriquées. Heureusement, il y a une solution facile. Utilisez 4 espaces (c.-à-d., <kbd>tab</kbd>) plutôt que des indentations à 2 espaces.
{{% /note %}}

## Configurer un Rendu Markdown BlackFriday

Vous pouvez configurer plusieurs aspects de Blackfriday comme indiqué dans la liste suivante. Voir la documentation sur [Configuration][config] pour la liste complète des instructions explicites que vous pouvez donner à Hugo lors du rendu de votre site.

{{< readfile file="/content/readfiles/bfconfig.md" markdown="true" >}}

## Étendre le Markdown

Hugo fournit des méthodes pratiques pour étendre le markdown.

### Listes de tâches

Hugo prend en charge [les listes de tâches de style GitHub (c.-à-d. Listes TODO)][gfmtasks] pour le rendu markdown Blackfriday. Si vous ne souhaitez pas utiliser cette fonctionnalité, vous pouvez la désactiver dans votre configuration.

#### Exemple Input de Liste de Tâches

{{% code file="content/my-to-do-list.md" %}}
```markdown
- [ ] un item de liste de tâche
- [ ] syntaxe de liste exigée
- [ ] incomplète
- [x] complète
```
{{% /code %}}


#### Exemple Output de Liste de Tâches

Le markdown précédent produit le HTML suivant dans votre site web produit : 

```html
<ul class="task-list">
    <li><input type="checkbox" disabled="" class="task-list-item"> a task list item</li>
    <li><input type="checkbox" disabled="" class="task-list-item"> list syntax required</li>
    <li><input type="checkbox" disabled="" class="task-list-item"> incomplete</li>
    <li><input type="checkbox" checked="" disabled="" class="task-list-item"> completed</li>
</ul>
```

#### Exemple d'Affichage d'une Liste de Tâches

Ce qui suis présente comment l'exemple de liste de tâches s'affichera pour les utilisateurs finaux de votre site web. Notez que l'apparence visuelle des listes ne dépend que de vous. Cette liste a été stylisée selon [la feuille de style Hugo Docs][hugocss].

- [ ] un item de liste de tâche
- [ ] syntaxe de liste exigée
- [ ] incomplet
- [x] achevé

### Emojis

Pour ajouter des emojis directement au contenu, réglez  `enableEmoji` sur `true` dans votre [configuration de site][config]. Pour utiliser les emojis dans des modèles ou des codes courts, voir la [fonction `emojify`][`emojify` function].

Pour une liste complète d'emojis, consultez l'[anti-sèche Emoji][emojis].

### Shortcodes

Si vous écrivez en Markdown et que vous vous trouverez souvent en train d'intégrer votre contenu avec du HTML brut, Hugo fournit des fonctionnalités inégrées de raccourcis-code. C'est l'une des fonctionnalités les plus puissantes d'Hugo et elle vous permet de créer rapidement vos propres extensions Markdown.

Voir [Shortcodes][sc] pour l'utilisation, en particulier pour les codes courts intégrés qui sont livrés avec Hugo, et [Modélisation code court][sct] pour apprendre à construire les vôtres.

### Blocs de Code

Hugo supporte l'usage du markdown enrichi de GitHub des trois  tiques inversées tout comme un [raccourci-code imbriqué `highlight`][hlsc] pour rendre une syntaxe colorée via via [Pygments][]. Pour des exemples d'usage et une explication complète, regardez la [documentation éclairage de syntaxe][hl] dans les [outils du développeur][developer tools].

## Mmark

Mmark est une [bifurcation de BlackFriday][mmark] et un super-ensemble de markdown qui convient parfaitement à l'écriture pour la [documentation IETF][ietf]. Vous pouvez voir des exemples de la syntaxe dans [le référentiel Mmark GitHub][mmarkgh] ou la syntaxe complète sur [le site Web de Miek Gieben][Miek Gieben's website].

### Utiliser Mmark

Comme Hugo est livré avec Mmark, l'utilisation de la syntaxe est aussi simple que de changer l'extension de vos fichiers de contenu de `.md` à `.mmark`.

Dans le cas où vous souhaitez utiliser uniquement Mmark dans des fichiers spécifiques, vous pouvez également définir la syntaxe Mmark dans le front matter de votre contenu :

```yaml
---
title: Mon Super Post
date: 2017-07-18
markdown: mmark
---
```

{{% warning %}}
Voici quelques fonctionnalités non disponibles dans Mmark ; un exemple étant que les codes courts ne sont pas traduits lorsqu'ils sont utilisés dans un fichier `.mmark` inclus ([#3131](https://github.com/gohugoio/hugo/issues/3137)), et `EXTENSION_ABBREVIATION` ([#1970](https://github.com/gohugoio/hugo/issues/1970)) et les todo-listes spécifiques mentionnées au-dessus ([#2270](https://github.com/gohugoio/hugo/issues/2270)) ne sont pas pleinement supportées. Les contributions sont les bienvenues.
{{% /warning %}}

## MathJax avec Hugo

[MathJax](http://www.mathjax.org/) is a JavaScript library that allows the display of mathematical expressions described via a LaTeX-style syntax in the HTML (or Markdown) source of a web page. As it is a pure a JavaScript library, getting it to work within Hugo is fairly straightforward, but does have some oddities that will be discussed here.

This is not an introduction into actually using MathJax to render typeset mathematics on your website. Instead, this page is a collection of tips and hints for one way to get MathJax working on a website built with Hugo.

[MathJax](http://www.mathjax.org/) est une bibliothèque JavaScript qui permet d'afficher des expressions mathématiques décrites par une syntaxe de type LaTeX dans la source HTML (ou Markdown) d'une page Web. Comme il s'agit d'une pure bibliothèque JavaScript, le faire fonctionner dans Hugo est assez simple, mais il y a des bizarreries qui seront discutées ici.

Ce n'est pas une introduction à l'utilisation de MathJax pour afficher les caractères mathématiques sur votre site. Au lieu de cela, cette page est une collection de conseils et d'astuces pour une façon de faire fonctionner MathJax sur un site Web construit avec Hugo.

### Activer MathJax

La première étape consiste à activer MathJax sur les pages où vous souhaitez avoir des caractères mathématiques. Il y a plusieurs façons de le faire (les lecteurs aventureux peuvent consulter la section [Chargement et Configuration](http://docs.mathjax.org/en/latest/configuration.html) de la documentation MathJax pour des méthodes supplémentaires d'inclusion de MathJax). Mais la façon la plus simple est d'utiliser le CDN sécurisé MathJax en incluant une balise `<script>` pour le CDN sécurisé officiellement recommandé ([cdn.js.com](https://cdnjs.com)) :

{{% code file="add-mathjax-to-page.html" %}}
```html
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```
{{% /code %}}

Une façon de s'assurer que ce code est inclus dans toutes les pages est de le placer dans l'un des modèles dans le répertoire `layouts/partials/`. Par exemple, je l'ai inclus dans le bas de mon modèle `footer.html` car je sais que le pied de page sera inclus dans chaque page de mon site.

### Options et Fonctionnalités

MathJax est une bibliothèque stable open-source avec de nombreuses fonctionnalités. J'encourage le lecteur intéressé à regarder la [Documentation MathJax](http://docs.mathjax.org/en/latest/index.html), en particulier les sections sur l'[Utilisation de Base](http://docs.mathjax.org/en/latest/index.html#basic-usage) et les [Options de Configuration MathJax](http://docs.mathjax.org/en/latest/index.html#mathjax-configuration-options).

### Problèmes avec Markdown

{{% note%}}

Les problèmes suivants avec Markdown supposent que vous utilisez `.md` pour le contenu et BlackFriday pour l'analyse. En utilisant [Mmark](#mmark), car votre format de contenu évitera la nécessité des solutions de contournement suivantes.

Si vous utilisez Mmark avec MathJax, utilisez `displayMath: [['$$','$$'], ['\\[','\\]']]`. Voir le [Mmark `README.md`](https://github.com/miekg/mmark/wiki/Syntax#math-blocks) pour plus d'informations. En plus de MathJax, Mmark fonctionne bien avec [KaTeX](https://github.com/Khan/KaTeX). Voir cet [article de blog d'un utilisateur Hugo](http://nosubstance.me/post/a-great-toolset-for-static-blogging/).
{{% /note %}}

Après avoir activé MathJax, toutes les entrées mathématiques  entre les marqueurs appropriés (voir la [documentation MathJax] [mathjaxdocs]) seront traitées et restranscrites dans la page Web. Un problème se pose cependant avec Markdown : le caractère de soulignement (`_`) est interprété par Markdown comme un moyen d'envelopper du texte dans des blocs `emph` tandis que LaTeX (MathJax) interprète le trait de soulignement comme un moyen de créer un sous-titre . Ce «double parler» du trait de soulignement peut entraîner des comportements inattendus et indésirables.

### Solution

Il existe plusieurs façons de remédier à ce problème. Une solution consiste à échapper à chaque trait de soulignement dans votre code mathématique en entrant `\_` au lieu de `_`. Cela peut devenir très fastidieux si les équations que vous entrez sont pleines d'indices.

Une autre option est de dire à Markdown de traiter le code MathJax comme un code textuel et de ne pas le traiter. Une façon de le faire est d'envelopper l'expression mathématique dans un bloc `<div>` `</div>`. Markdown ignorera ces sections et elles seront transmises directement à MathJax et traitées correctement. Cela fonctionne bien pour les mathématiques de style d'affichage, mais pour les expressions mathématiques en ligne, la rupture de ligne induite par `<div>` n'est pas acceptable. La syntaxe pour instruire Markdown pour traiter le texte en ligne comme textuel est en l'enveloppant dans les backticks (`` `` `). Vous avez peut-être remarqué, cependant, que le texte inclus entre les backticks est restitué différemment du texte standard (sur ce site, il s'agit d'éléments mis en surbrillance en rouge). Pour contourner ce problème, nous pourrions créer une nouvelle entrée CSS qui applique un style standard pour tout texte en ligne verbatim qui inclut le code MathJax. Ci-dessous je vais montrer la source HTML et CSS qui accomplirait cette (note cette solution a été adaptée de [ce blog](http://doswa.com/2011/07/20/mathjax-in-markdown.html) - Tous les crédits reviennent à l'auteur original).

{{% code file="mathjax-markdown-solution.html" %}}
```js
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$'], ['\[','\]']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
});
</script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Queue(function() {
    // Fix <code> tags after MathJax finishes running. This is a
    // hack to overcome a shortcoming of Markdown. Discussion at
    // https://github.com/mojombo/jekyll/issues/199
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
```
{{% /code %}}

Comme précédemment, ce contenu devrait être inclus dans la source HTML de chaque page qui utilisera MathJax. L'extrait de code suivant contient le CSS qui est utilisé pour que les blocs MathJax textuels contiennent le même style de police que le corps de la page.

{{% code file="mathjax-style.css" %}}
```css
code.has-jax {
    font: inherit;
    font-size: 100%;
    background: inherit;
    border: inherit;
    color: #515151;
}
```
{{% /code %}}

Dans l'extrait CSS, notez la ligne `color: #515151;`. `#515151` est la valeur attribuée à l'attribut `color` de la classe `body` dans ma CSS. Pour que les équations s'inscrivent dans le corps d'une page Web, cette valeur devrait être identique à la couleur du corps.

### Usage

Avec cette configuration, tout est en place pour une utilisation naturelle de MathJax sur les pages générées à l'aide d'Hugo. Pour inclure les mathématiques en ligne, il suffit de mettre le code LaTeX entre `` `$ TeX Code $` `` ou `` `\( TeX Code \)` ``. Pour inclure le style mathématiques, placez juste le code LaTeX entre `<div>$$TeX Code$$</div>`. Tous les maths seront correctement composés et affichés dans votre page web générée par Hugo !

## Formats Supplémentaires via les Aides Externes

Hugo a un nouveau concept appelé «aide extérieure». Cela signifie que vous pouvez écrire votre contenu en utilisant [Asciidoc][ascii], [reStructuredText][rest]. Si vous avez des fichiers avec des extensions associées, Hugo appellera des commandes externes pour générer le contenu. ([Voir le code source Hugo pour les assistants externes][helperssource].)

Par exemple, pour les fichiers Asciidoc, Hugo essaiera d'appeler la commande `asciidoctor` ou `asciidoc`. Cela signifie que vous devrez installer l'outil associé sur votre machine pour pouvoir utiliser ces formats. ([Voir les documents Asciidoctor pour les instructions d'installation](http://asciidoctor.org/docs/install-toolchain/)).

Pour utiliser ces formats, utilisez simplement l'extension standard et le front matter exactement comme vous le feriez avec les fichiers `.md` supportés nativement.

{{% warning "Performance des aideurs externes" %}}
Étant donné que les formats supplémentaires sont des commandes externes, les performances de génération dépendront fortement de la performance de l'outil externe que vous utilisez. Comme cette fonctionnalité en est encore à ses débuts, les commentaires sont les bienvenus.
{{% /warning %}}

## Apprendre le Markdown

La syntaxe Markdown est suffisamment simple à apprendre en une seule séance. Les ressources qui suivent sont excellentes pour vous mettre en route :

* [Daring Fireball: Markdown, John Gruber (Créateur du Markdown)][fireball]
* [Anti-sèche Markdown, Adam Pritchard][mdcheatsheet]
* [Tutoriel Markdown (Interactif), Garen Torikian][mdtutorial]

[`emojify` function]: /fonctions/emojify/
[ascii]: http://asciidoc.org/
[bfconfig]: /demarrage/configuration/#configurer-rendu-blackfriday
[blackfriday]: https://github.com/russross/blackfriday
[mmark]: https://github.com/miekg/mmark
[config]: /demarrage/configuration/
[developer tools]: /tools/
[emojis]: https://www.webpagefx.com/tools/emoji-cheat-sheet/
[fireball]: https://daringfireball.net/projects/markdown/
[gfmtasks]: https://guides.github.com/features/mastering-markdown/#syntax
[helperssource]: https://github.com/gohugoio/hugo/blob/77c60a3440806067109347d04eb5368b65ea0fe8/helpers/general.go#L65
[hl]: /outils/syntax-highlighting/
[hlsc]: /gestion-contenu/shortcodes/#highlight
[hugocss]: /css/style.css
[ietf]: https://tools.ietf.org/html/
[mathjaxdocs]: https://docs.mathjax.org/en/latest/
[mdcheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[mdtutorial]: http://www.markdowntutorial.com/
[Miek Gieben's website]: https://miek.nl/2016/March/05/mmark-syntax-document/
[mmark]: https://github.com/miekg/mmark
[mmarkgh]: https://github.com/miekg/mmark/wiki/Syntax
[org]: http://orgmode.org/
[Pygments]: http://pygments.org/
[rest]: http://docutils.sourceforge.net/rst.html
[sc]: /gestion-contenu/shortcodes/
[sct]: /templates/shortcode-templates/
