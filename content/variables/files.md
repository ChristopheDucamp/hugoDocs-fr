---
title: File
linktitle: Variables File
description: "Vous pouvez accéder aux données relatives-au-système-de-fichier pour un fichier de contenu dans la variable `.File`."
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [variables and params,variables et params]
#tags: [files]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 40
weight: 40
sections_weight: 40
aliases: [/variables/file-variables/]
toc: false
---

{{% notice note %}}
Pour plus d'informations sur la création de shortcodes et de modèles qui utilisent le jeu de fonctionnalités liées aux fichiers de Hugo, voir [Modèles de fichiers locaux](/templates/files/).
{{% /notice %}}

L'objet `.File` contient les champs suivants :

`.File.Path`
: the original relative path of the page (e.g., `content/posts/foo.en.md`)

`.File.LogicalName`
: the name of the content file that represents a page (e.g., `foo.en.md`)

`.File.TranslationBaseName`
: the filename without extension or optional language identifier (e.g., `foo`)

`.File.BaseFileName`
: the filename without extension (e.g., `foo.en`)

`.File.Ext`
: the file extension of the content file (e.g., `md`); this can also be called using `.File.Extension` as well. Note that it is *only* the extension without `.`.

`.File.Lang`
: the language associated with the given file if Hugo's [Multilingual features][multilingual] are enabled (e.g., `en`)

`.File.Dir`
: given the path `content/posts/dir1/dir2/`, the relative directory path of the content file will be returned (e.g., `posts/dir1/dir2/`)

[Multilingual]: /content-management/multilingual/