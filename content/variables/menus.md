---
title: Menu 
linktitle: Variables Menu
description: Une entrée de menu dans un modèle de menu a des variables et des fonctions spécifiques pour faciliter la production de menus.
date: 2017-03-12
publishdate: 2017-03-12
lastmod: 2017-07-21
categories: [variables and params, variables et params]
#tags: [menus]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 50
weight: 50
sections_weight: 50
aliases: [/variables/menu/]
toc: false
---

Le [modèle menu][menu template] a les propriétés suivantes :

`.URL`
: string

`.Name`
: string

`.Menu`
: string

`.Identifier`
: string

`.Pre`
: template.HTML

`.Post`
: template.HTML

`.Weight`
: int

`.Parent`
: string

`.Children`
: Menu

[menu template]: /templates/menus/