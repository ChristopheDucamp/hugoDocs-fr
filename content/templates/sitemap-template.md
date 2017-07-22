---
title: Sitemap
linktitle: Modèle Sitemap 
description: Hugo est livré avec un fichier modèle natif observant la v0.9 du protocole Sitemap, mais vous pouvez annuler ce modèle si besoin.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-02-21
categories: [modèles]
#tags: [sitemap, xml]
menu:
  docs:
    parent: "Templates"
    weight: 160
weight: 160
sections_weight: 160
draft: false
aliases: [/layout/sitemap/,/templates/sitemap/]
toc: false
---

Un modèle unique Sitemap est uitlisé pour générer le fichier `sitemap.xml`.
Hugo vient automatiquement avec ce fichier modèle. *Aucun travail n'est demandé de la part de l'utilisateur à moins qu'il ne veuille personnaliser `sitemap.xml`.*

Un sitemap est une `Page` et par consésquent, elle a toutes les [variables de page][pagevars] disponibles à utiliser dans ce modèle aux côté de ceux spécifiques-Sitemap :

`.Sitemap.ChangeFreq`
: The page change frequency

`.Sitemap.Priority`
: The priority of the page

`.Sitemap.Filename`
: The sitemap filename

If provided, Hugo will use `/layouts/sitemap.xml` instead of the internal `sitemap.xml` template that ships with Hugo.

## Le sitemap.xml d'Hugo

This template respects the version 0.9 of the [Sitemap Protocol](http://www.sitemaps.org/protocol.html).

```xml
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  {{ range .Data.Pages }}
  <url>
    <loc>{{ .Permalink }}</loc>{{ if not .Lastmod.IsZero }}
    <lastmod>{{ safeHTML ( .Lastmod.Format "2006-01-02T15:04:05-07:00" ) }}</lastmod>{{ end }}{{ with .Sitemap.ChangeFreq }}
    <changefreq>{{ . }}</changefreq>{{ end }}{{ if ge .Sitemap.Priority 0.0 }}
    <priority>{{ .Sitemap.Priority }}</priority>{{ end }}
  </url>
  {{ end }}
</urlset>
```

{{% note %}}
Hugo will automatically add the following header line to this file
on render. Please don't include this in the template as it's not valid HTML.

`<?xml version="1.0" encoding="utf-8" standalone="yes" ?>`
{{% /note %}}

## Configurer `sitemap.xml`

Defaults for `<changefreq>`, `<priority>` and `filename` values can be set in the site's config file, e.g.:

```toml
[sitemap]
  changefreq = "monthly"
  priority = 0.5
  filename = "sitemap.xml"
```

The same fields can be specified in an individual content file's front matter in order to override the value assigned to that piece of content at render time.

[pagevars]: /variables/page/