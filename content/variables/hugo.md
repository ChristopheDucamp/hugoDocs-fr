---
title: Variables Hugo
linktitle: Variables Spécifiques à Hugo
description: La variable `.Hugo` fournit un accès facile aux données en-rapport-avec Hugo.
date: 2017-03-12
publishdate: 2017-03-12
lastmod: 2017-07-21
categories: [variables and params, variables et params]
#tags: [hugo,generator]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 60
weight: 60
sections_weight: 60
aliases: []
toc: false
wip: false
---

Elle contient les champs suivants :

`.Hugo.Generator`
: le tag `<meta>` pour la version d'Hugo qui a généré le site. `.Hugo.Generator` sort une balise HTML *complète* ; par ex. `<meta name="generator" content="Hugo 0.18" />`

`.Hugo.Version`
: la version actuelle de la binaire Hugo que vous utilisez par ex. `0.13-DEV`<br>

`.Hugo.CommitHash`
: le hash de commit git de la binaire d'Hugo par ex.`0e8bed9ccffba0df554728b46c5bbf6d78ae5247`

`.Hugo.BuildDate`
: la date de compilation de la binaire actuellle Hugo formaté aec la RFC 3339 par ex. `2002-10-02T10:00:00-05:00`<br>

{{% panel header="Utilisation du Tag Hugo Generator" %}}
Nous recommandons fortement d'utiliser `.Hugo.Generator` dans le `<head>` de votre site web. `.Hugo.Generator` est inclus par défaut dans tous les thèmes hébergés sur [themes.gohugo.io](http://themes.gohugo.io). La balise generator permet à l'équipe Hugo de suivre l'usage et la popularité d'Hugo.
{{% /panel %}}

