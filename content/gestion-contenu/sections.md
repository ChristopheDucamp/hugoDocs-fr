---
title: Sections de Contenu
linktitle: Sections
description: Hugo supporte les sections de contenus, qui selon le comportement par défaut d'Hugo, reflètent la structure du site web rendu.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-20
categories: [gestion de contenu]
#tags: [listes,sections, types de contenus, organisation]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 50
weight: 50	#rem
draft: false
aliases: [/content/sections/, /gestion-de-contenu/section/]
toc: true
---

{{% note %}}
Cette section n'est pas mise à jour avec le support des sections imbriquées dans Hugo 0.24, voir https://github.com/gohugoio/hugoDocs/issues/36
{{% /note %}}
{{% todo %}}
Voir au-dessus
{{% /todo %}}

Hugo croit que vous organisez votre contenu avec un but. La même structure qui fonctionne pour organiser votre contenu source est utilisée pour organiser le site rendu (voir [structure des dossiers][directory structure]).

Suivant ce modèle, Hugo utilise le niveau supérieur de votre organisation de contenu comme la **section** de contenu.

L'exemple suivant montre une structure de répertoire de contenu pour un site Web qui comporte trois sections : "auteurs", "evenements" et "articles" :

```bash
.
└── content
    ├── auteurs
    |   ├── _index.md     // <- votresite.com/auteurs/
    |   ├── john-doe.md   // <- votresite.com/auteurs/john-doe/
    |   └── jane-doe.md   // <- votresite.com/auteurs/jane-doe/
    └── evenements
    |   ├── _index.md     // <- votresite.com/evenements/
    |   ├── event-1.md    // <- votresite.com/evenements/event-1/
    |   ├── event-2.md    // <- votresite.com/evenements/event-2/
    |   └── event-3.md    // <- votresite.com/evenements/event-3/
    └── articles
    |   ├── _index.md     // <- votresite.com/articles/
    |   ├── event-1.md    // <- votresite.com/articles/event-1/
    |   ├── event-2.md    // <- votresite.com/articles/event-2/
    |   ├── event-3.md    // <- votresite.com/articles/event-3/
    |   ├── event-4.md    // <- votresite.com/articles/event-4/
    |   └── event-5.md    // <- votresite.com/articles/event-5/
```

## Section Listes de Contenus

Hugo créera automatiquement des pages pour chaque racine de section qui répertorie tout le contenu dans cette section. Consultez la documentation sur [les modèles de section][section templates] pour plus de détails sur la personnalisation du rendu de ces pages.

À partir de Hugo v0.18, les pages de section peuvent également contenir un fichier de contenu et un front matter. Ces fichiers de contenu de section doivent être placés dans leur dossier de section correspondant et doivent être nommés `_index.md` afin qu'Hugo puisse correctement afficher le front matter et le contenu.

{{% warning "`index.md` vs `_index.md`" %}}
Les thèmes Hugo développées avant la v0.18 utilisaient souvent un `index.md`(c-a-d. sans le tiret précédent [`_`]) dans une section de contenu comme un hack pour émuler le comportement `_index.md`. Le hack peut fonctionner... *parfois* ; cependant, le rendu de l'ordre des pages peut être imprévisible dans Hugo. Ce qui fonctionne maintenant peut échouer pour être rendu proprement au fur et à mesure que votre site grandit. Il est  **fortement conseillé** d'utiliser `_index.md` comme contenu pour vos page index de section.
**Note :** le layout de `_index.md`, comme représentatif d'une section est un [modèle de page liste](/templates/section-templates/) et *non pas* un [modèle de page unique](/templates/single-page-templates/). Si vous voulez enrichir le nouveau comportement par défaut pour `_index.md`, configurez  `disableKinds` en rapport dans la [configuration de votre site](/demarrage/configuration/).
{{% /warning %}}

## *Section* Contenu vs *Type* Contenu

Par défaut tout ce qui est créé dans une section utilisera le [type de contenu][content type] qui correspond au nom de section. Par exemple, Hugo supposera que `articles/post-1.md` est un type de contenu `articles`. Si vous utilisez un [archetype][] pour votre section articles, Hugo générera le front matter selon ce qu'il trouve dans `archetypes/articles.md`.

[archetype]: /gestion-contenu/archetypes/
[content type]: /gestion-contenu/types/
[directory structure]: /demarrage/structure-dossier/
[section templates]: /templates/section-templates/


