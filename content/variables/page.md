---
title: Page
linktitle: Variables Page
description: Les variables au-niveau page sont définies dans un front matter du fichier de contenu, dérivées à partir de l'emplacement où se situe le fichier de contenu, ou extraites à partir du corps du contenu en lui-même.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [variables et params]
#tags: [pages, todo]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 20
weight: 20
sections_weight: 20
aliases: [/variables/page/]
toc: true
---

Voici une liste des variables au niveau de la page. Beaucoup d'entre elles seront définies dans le front matter, dérivées à partir de l'emplacement du fichier ou extraites du contenu lui-même.

{{% notice note "`.Scratch`" %}}
Voir [`.Scratch`](/fonctions/scratch/) pour des variables inscriptibles à l'échelle de la page.
{{% /notice %}}

## Variables Page

`.AlternativeOutputFormats`
: contient tous les formats alternatifs pour une page donnée ; cette variable est une liste `link rel` particulièrement utile  dans vos `<head>` de site. (Voir [Formats Output](/templates/output-formats/).)

`.Content`
: le contenu lui-même, défini dans le front matter.

`.Data`
: la data spécifique à ce type de page.

`.Date`
: la date associée à la page ; `.Date` extrait du champ `date` dans un front matter de contenu. Voir aussi `.ExpiryDate`, `.PublishDate`, et `.Lastmod`.

`.Description`
: la description pour la page.

`.Draft`
: une valeur booléenne, `true` si le contenu est marqué comme une ébauche dans le front matter.

`.ExpiryDate`
: la date à laquelle le contenu est programmé pour expirer ; `.ExpiryDate` s'extrait du champ `expirydate` dans un front matter de contenu. Voir aussi `.PublishDate`, `.Date`, et `.Lastmod`.

`.FuzzyWordCount`
: le nombre approximatif de mots dans le contenu.

`.Hugo`
: voir [Variables Hugo](/variables/hugo/).

`.IsHome`
: `true` dans le contexte de la [page d'accueil](/templates/page-accueil/).

`.IsNode`
: always `false` for regular content pages.

`.IsPage`
: always `true` for regular content pages.

`.IsTranslated`
: `true` if there are translations to display.

`.Keywords`
: the meta keywords for the content.

`.Kind`
: le *type* de page. Les valeurs de retour possibles sont `page`, `home`, `section`, `taxonomy`, ou `taxonomyTerm`. Notez qu'il existe aussi les *kind*s `RSS`, `sitemap`, `robotsTXT`, et les `404`, mais celles-ci sont uniquement disponibles durant le rendu de chacuns de ces kind respectifs de page et par conséquent *non* disponibles dans n'importe lesquelles des collections de `Pages`.

`.Lang`
: la langue prise à partir de le l'extenstion de notation language.

`.Language`
: un objet langage quipointe vers la définition de langage dans le `config` du site.

`.Lastmod`
: La date à laquelle le contenu a été dernièrement modifié ; `.Lastmod` extrait du champ `lastmod` dans un front matter de contenu. Si `lastmod` n'est pas réglé, Hugo prendra par défaut le champ `date`. Voir aussi `.ExpiryDate`, `.Date`, et  `.PublishDate`.

`.LinkTitle`
: access when creating links to the content. If set, Hugo will use the `linktitle` from the front matter before `title`.

`.Next`
: pointeur vers le contenu suivant (basé sur le champ `publishdate` dans le front matter).

`.NextInSection`
: pointeur vers le contenu suivant dans la même section (basé sur le champ `publishdate` dans le front matter).

`.OutputFormats`
: contains all formats, including the current format, for a given page. Can be combined the with [`.Get` function](/functions/get/) to grab a specific format. (See [Output Formats](/templates/output-formats/).)

`.Pages`
: une collection de pages associées. Cette valeur sera `nil` pour les pages normales de contenu. `.Pages` est un alias pour  `.Data.Pages`.

`.Permalink`
: le lien permanent pour cette page ; voir [Permalinks](/gestion-contenu/urls/)

`.Plain`
: le contenu de page dénudé des balises HTML et présenté sous forme de chaîne.

`.PlainWords`
: le contenu de page dénudé du HTML sous forme d'une `[]string` utilisant les [`strings.Fields`](https://golang.org/pkg/strings/#Fields) de GO pour découper `.Plain` dans une slice.

`.Prev`
: Pointeur vers le contenu précédent (basé sur le champ `publishdate` dans le front matter).

`.PrevInSection`
: Pointeur vers le contenu précédent dans la même section (basé sur le champ `publishdate` dans le front matter). Par exemple, `{{if .PrevInSection}}{{.PrevInSection.Permalink}}{{end}}`.

`.PublishDate`
: la date à laquelle le contenu a été ou sera publié ; `.Publishdate` extrait à partir du champ `publishdate` dans le front matter d'un contenu. Voir aussi `.ExpiryDate`, `.Date`, et `.Lastmod`.

`.RSSLink`
: lien vers le lien RSS des taxonomies.

`.RawContent`
: le contenu brut markdown sans le front matter. Utile avec  [remarkjs.com](
http://remarkjs.com)

`.ReadingTime`
: le temps de lecture estimé, en minutes, que cela prend pour lire le contenu.

`.Ref`
: renvoie le permalien pour une référence donnée (par ex. `.Ref "sample.md"`).  `.Ref` ne gère *pas* correctement les fragments dans-la-page. Voir [références croisées](/gestion-contenu/cross-references/).

`.RelPermalink`
: Le lien permanent relatif pour cette page.

`.RelRef`
: renvoie le permalien relatif pour une référence donnée (par ex., `RelRef
"sample.md"`). `.RelRef` ne gère *pas* correctement les fragments dans-la-page. Voir [références croisées](/gestion-contenu/cross-references/).

`.Section`
: la [section](/gestion-contenu/sections/) à laquelle ce contenu appartient.

`.Site`
: voir les [Variables Site](/variables/site/).

`.Summary`
: un résumé généré du contenu pour afficher facilement un extrait dans une vue récapitulative. Le point d'arrêt peut être réglé manuellement en insérant <code>&lt;!&#x2d;&#x2d;more&#x2d;&#x2d;&gt;</code> à l'endroit approprié dans la page de contenu. Voir [Résumés du contenu](/gestion-contenu/resumes) pour plus de détails.

`.TableOfContents`
: La [table des matières](/gestion-contenu/toc/) pour la page.

`.Title`
: le titre pour cette page.

`.Translations`
: a list of translated versions of the current page. See [Multilingual Mode](/gestion-contenu/multilingual/) for more information.

`.Truncated`
: a boolean, `true` if the `.Summary` is truncated. Useful for showing a "Read more..." link only when necessary.  See [Summaries](/gestion-contenu/summaries/) for more information.

`.Type`
: the [content type](/gestion-contenu/types/) of the content (e.g., `post`).

`.URL`
: the URL for the page relative to the web root. Note that a `url` set directly in front matter overrides the default relative URL for the rendered page.

`.UniqueID`
: the MD5-checksum of the content file's path.

`.Weight`
: assigned weight (in the front matter) to this content, used in sorting.

`.WordCount`
: the number of words in the content.

## Params Niveau-Page

Toute autre valeur définie dans la page d'accueil d'un fichier de contenu, y compris les taxonomies, sera mise à disposition dans le cadre de la variable `.Params`.


```yaml
---
title: Mon Premier Post
date: date: 2017-02-20T15:26:23-06:00
categories: [un]
tags: [deux,trois,quatre]
```

Avec le front matter ci-dessus, les taxonomies `tags` et `categories` sont accessibles via les éléments suivants :

* `.Params.tags`
* `.Params.categories`

{{% panel theme="warning" header="Casse des Params" %}}
Les `.Params` niveau-page sont *uniquement* accessibles en bas de casse.
{{% /panel %}}

La variable `.Params` est particulièrement utile pour l'introduction de champs du front matter définis par l'utilisateur dans les fichiers de contenu. Par exemple, site web Hugo de critiques de livres pourrait avoir le front matter suivant dans `/content/review/livre01.md`:

```yaml
---
...
affiliatelink: "http://www.mon-lien-livre.ici"
recommendedby: "Ma Maman"
...
---
```

Ces champs seraient alors accessibles pour le modèle `/themes/votretheme/layouts/review/single.html` à travers `.Params.affiliatelink` et `.Params.recommendedby`, respectivement.


Deux situations communes où ce type de champ de front matter peut être introduit sont soit comme valeur d'un certain attribut comme `href=""` ou en lui-même peut être affiché en tant que texte pour les visiteurs du site.

{{% code file="/themes/yourtheme/layouts/review/single.html" %}}
```html
<h3><a href={{ printf "%s" $.Params.affiliatelink }}>Achetez ce livre</a></h3>
<p>Il a été recommandé par {{ .Params.recommendedby }}.</p>
```
{{% /code %}}

Ce modèle serait rendu comme suit, en supposant que vous ayez réglé [`uglyURLs`](/gestion-contenu/urls/) sur `false` dans votre [`config` de site](/demarrage/configuration/) :

{{% output file="votreurlbase/review/livre01/index.html" %}}
```html
<h3><a href="http://www.mon-lien-livre.ici">Achetez ce livre</a></h3>
<p>Il a été recommandé par ma Maman.</p>
```
{{% /output %}}

{{% note %}}
Voir [Archetypes](/gestion-contenu/archetypes/) pour une cohérence des `Params` sur les éléments de contenu.
{{% /note %}}

### La Méthode `.Param`

Dans Hugo, vous pouvez déclarer des params dans des pages individuelles et globalement pour tout votre site Web. Un cas d'utilisation courant est d'avoir une valeur générale pour le paramètre du site et une valeur plus spécifique pour certaines pages (c'est-à-dire une image d'en-tête) :

```golang
{{ $.Param "header_image" }}
```

La méthode `.Param` fournit un moyen de résoudre une valeur unique en fonction de sa définition dans un paramètre de page (c'est-à-dire dans le front matter du contenu) ou un paramètre de site (c'est-à-dire dans votre `config`).

### Accéder aux Champs Imbriqués dans le Front Matter

Quand le front matter contient des champs imbriqués comme suit :

```yaml
---
author:
  given_name: Jean
  family_name: Feminella
  display_name: Jean Feminella
---
```
`.Param` peut accéder à ces champs en concaténant les noms de champs ensemble avec un point :

```
{{ $.Param "author.display_name" }}
```

Si votre front matter contient une clé de niveau-supérieur qui est ambigue avec une clé imbriquée, comme dans le cas suivant : 

```
---
favorites.flavor: vanille
favorites:
  flavor: chocolat
---
```

La clé du niveau le plus haut sera préférée. Par conséquent, la méthode suivante sera appliquée à l'exemple précédent, et imprimera `vanille` et non pas `chocolat` :

```golang
{{ $.Param "favorites.flavor" }}
=> vanille
```
