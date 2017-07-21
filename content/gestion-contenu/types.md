---
title: Types de Contenus
linktitle: Types
description: Hugo supporte les sites avec plusieurs types de contenu et suppose que votre site sera organisé en sections, où chaque section représente le type correspondant.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-20
categories: [gestion de contenu]
#tags: [listes,sections,types de contenu,types,organisation, sections, contenu]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 60
weight: 60	#rem
draft: false
aliases: [/content/types]
toc: true
---

Un **type de contenu** peut avoir un ensemble unique de métadonnées (par ex., [front matter][]) ou un [modèle][template] et peut être créé par la commande `hugo new` via les  [archetypes][].

## Qu'est-ce Qu'un Type de Contenu

[Tumblr][] est un bel exemple de site web avec plusieurs types de contenus. Un morceau de "contenu" pourrait être une photo, une citation, ou un article, chacun avec différents ensembles de métadonnées et différents rendus visuels.

## Assigner un Type de Contenu

Hugo suppose que votre site sera organisé en [sections][] et que chaque section représente un type de contenu correspondant. Il s'agit de réduire la configuration nécessaire aux nouveaux projets Hugo.

Si vous tirez profit de ce comportement par défaut, chaque nouvelle partie de contenu que vous placez dans une section héritera automatiquement du type. Par conséquent, un nouveau fichier créé sur `content/articles/nouvel-article.md` recevra automatiquement le type `articles`. Alternativement, vous pouvez définir le type de contenu dans le [front matter][] d'un fichier de contenu dans le champ "`type`".

## Créer le Nouveau Contenu d'un Type Spécifique

Vous pouvez ajouter manuellement des fichiers à vos répertoires de contenu, mais Hugo peut créer et remplir un nouveau fichier de contenu avec un front matter préconfiguré via [archétypes] [archetypes].

## Définir un Type de Contenu

Créer un nouveau type de contenu est facile. Vous définissez simplement les modèles et l'archetype unique pour votre nouveau type de contenu, ou Hugo utilisera ceux par défaut.


{{% note "Déclarer les Types de Contenu" %}}
Souvenez-vous que tout ce qui suit est *facultatif*. Si vous ne déclarez pas spécifiquemente les types de contenu dans votre front matter ou si vous développez des layouts spécifiques pour les types de contenu, Hugo est suffisamment intelligent pour supposer le type de contenu à partir du chemin de fichier et la section. (Voir [Sections de Contenu](/gestion-contenu/sections/) pour plus d'informations.)
{{% /note %}}

Les exemples suivants vous permettent de passer par étapes en créant une nouvelle mise en page de type pour un fichier de contenu contenant le front matter suivant :

{{% code file="content/events/my-first-event.md" copy="false" %}}
```toml
+++
title = My first event
date = "2016-06-24T19:20:04-07:00"
description = "Aujourd'hui, j'ai 36 ans. Comme le temps file."
type = "event"
layout = "birthday"
+++
```
{{% /code %}}

Par défaut, Hugo suppose `*.md` sous `events` est du type de contenu `events`. Néanmoins, nous avons spécifié que ce fichier particulier sur `content/events/my-first-event.md` est de type `event` et devrait s'afficher en utilisant le layout  `birthday`.

### Créer un Dossier de Layout pour le Type

Créez un dossier avec le nom du type dans `/layouts`. Pour créer ces layouts personnalisés, **type est toujours au singulier** ; par ex., `articles => article`, `events => event` et `posts => post`.

Pour cet exemple, vous devez créer `layouts/event/birthday.html`.

{{% note %}}
Si vous avez plusieurs fichiers de contenu dans votre dossier  `events` qui sont du type `special` et que vous ne vouliez pas définir spécifiquement le `layout` pour chaque élement de contenu, vous pouvez créer un layout sur `layouts/special/single.html` pour observer le [modèle d'odre de recherche d'une page unique](/templates/single-page-templates/).
{{% /note %}}

{{% warning %}}
Avec le modèle de data "tout est une page" introduit dans la v0.18 (voir [Organisation de Contenu](/gestion-contenu/organisation/)), vous pouvez utiliser `_index.md` dans les dossiers de contenu pour ajouter à la fois le contenu et le front matter pour [lister les pages](/templates/lists/). Néanmoins, `type` et `layout` déclarés dans le front matter de `_index.md` ne sont *pas* actuellement respectés au moment du build sur la v0.19. C'est un problème connu [(#3005)](https://github.com/gohugoio/hugo/issues/3005).
{{% /warning %}}

### Créer des Vues

De nombreux sites prennent en charge le rendu du contenu de plusieurs façons différentes ; Ppar exemple, une vue de page unique et une vue récapitulative à utiliser lors de l'affichage d'une [liste de contenu de section][sectiontemplates].

Hugo limite les hypothèses sur la façon dont vous souhaitez afficher votre contenu dans un ensemble intuitif par défaut et soutiendra autant de vues différentes d'un type de contenu que votre site requiert. Tout ce qui est nécessaire pour ces vues supplémentaires est qu'un modèle existe dans chaque répertoire `/layouts/<TYPE>` avec le même nom.

### Ordre de Recherche Personnalisé des Types de Contenu

L'ordre de recherche des modèles pour `content/events/my-first-event.md` serait comme suit :

* `layouts/event/birthday.html`
* `layouts/event/single.html`
* `layouts/events/single.html`
* `layouts/_default/single.html`

### Créer un Archétype Correspondant

Nous pouvons alors créer un archétype personnalisé avec un front matter préconfiguré sur `event.md` dans le répertoire `/archetypes` ; c'est-à-dire `archetypes/event.md`.

Lire [Archétypes][archetypes] pour plus d'informations sur l'utilisation de l'archétype avec `hugo new`.

[archetypes]: /gestion-contenu/archetypes/
[front matter]: /gestion-contenu/front-matter/
[sectiontemplates]: /templates/section-templates/
[sections]: /gestion-contenu/sections/
[template]: /templates/
[Tumblr]: https://www.tumblr.com/