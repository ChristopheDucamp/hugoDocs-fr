---
title: Fichier Robots.txt File
linktitle: Robots.txt
description: Hugo peut générer un robots.txt personnalisé de la même manière que pour tout autre modèle.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [templates]
#tags: [robots,search engines]
menu:
  docs:
    parent: "Templates"
    weight: 165
weight: 165
sections_weight: 165
draft: false
aliases: [/extras/robots-txt/]
toc: false
---

Pour créer votre robots.txt comme un modèle, réglez d'abord la valeur `enableRobotsTXT` sur `true` dans votre [configuration file][config]. Par défaut, cette option génère un robots.txt avec le contenu suivant, qui indique aux moteurs de recherche qu'ils sont autorisés à tout crawler :

```http
User-agent: *
```

## Ordre de Recherche du Modèle Robots.txt

L'[ordre de recherche][lookup] pour le modèle `robots.txt` est le suivant :

* `/layouts/robots.txt`
* `/themes/<THEME>/layout/robots.txt`

{{% note %}}
If you do not want Hugo to create a default `robots.txt` or leverage the `robots.txt` template, you can hand code your own and place the file in `static`. Remember that everything in the [static directory](/getting-started/directory-structure/) is copied over as-is when Hugo builds your site.
{{% /note %}}

## Exemple de Modèle Robots.txt 

The following is an example `robots.txt` layout:

{{% code file="layouts/robots.txt" download="robots.txt" %}}
```http
User-agent: *

{{range .Data.Pages}}
Disallow: {{.RelPermalink}}
{{end}}
```
{{% /code %}}

This template disallows all the pages of the site by creating one `Disallow` entry for each page.

[config]: /demarrage/configuration/
[lookup]: /templates/lookup-order/
[robots]: http://www.robotstxt.org/