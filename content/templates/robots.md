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

Pour créer votre robots.txt comme un modèle, réglez d'abord la valeur `enableRobotsTXT` sur `true` dans votre [fichier de configuration][config]. Par défaut, cette option génère un `robots.txt` avec le contenu suivant, qui indique aux moteurs de recherche qu'ils sont autorisés à tout crawler :

```http
User-agent: *
```

## Ordre de Recherche du Modèle Robots.txt

L'[ordre de recherche][lookup] pour le modèle `robots.txt` est le suivant :

* `/layouts/robots.txt`
* `/themes/<THEME>/layout/robots.txt`

{{% note %}}
Si vous ne voulez pas que Hugo crée par défaut un `robots.txt` ou utilise le modèle `robots.txt`, vous pouvez gérer le vôtre et placer le fichier dans  `static`. Souvenez-vous que tout ce qui est dans le [dossier static](/getting-started/directory-structure/) est copié tel quel quand Hugo construit votre site.
{{% /note %}}

## Exemple de Modèle Robots.txt 

Voic un exemple de layout `robots.txt` :

{{% code file="layouts/robots.txt" download="robots.txt" %}}
```http
User-agent: *

{{range .Data.Pages}}
Disallow: {{.RelPermalink}}
{{end}}
```
{{% /code %}}

Ce modèle désactive toutes les pages du site en créant une entrée `Disallow` pour chaque page.

[config]: /demarrage/configuration/
[lookup]: /templates/lookup-order/
[robots]: http://www.robotstxt.org/