---
title: Shortcode
linktitle: Variables Shortcode
description: Les shortcodes peuvent accéder aux variables de page et ont aussi leurs propres variables spécifiques intégrées.
date: 2017-03-12
publishdate: 2017-03-12
lastmod: 2017-03-24
categories: [variables and params, variables et params]
#tags: [shortcodes]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 20
weight: 20
sections_weight: 20
aliases: []
toc: false
---

Les [shortcodes][shortcodes] ont accès aux paramètres délimités  dans la déclaration shortcode via [`.Get`][getfunction] page- et aux variables de niveau-site, et aussi aux champs spécifiques suivants :

`.Parent`
: fournit un accès au contexte parent du shortcode dans les shortcodes imbriqués. Ce peut être très utile pour l'héritage de paramètres communs shortcode provenant de la racine.

`.IsNamedParams`
: booléen qui renvoie `true` quand le shortcode en question utilise des [paramètres nommés plutôt que positionnels][shortcodes]

`.Inner`
: represente le contenu entre les balises d'ouverture et de fermeture quand un [shortcode fermant][markdownshortcode] est utilisé.

[getfunction]: /fonctions/get/
[markdownshortcode]: /gestion-contenu/shortcodes/#shortcodes-avec-markdown
[shortcodes]: /templates/shortcode-templates/


