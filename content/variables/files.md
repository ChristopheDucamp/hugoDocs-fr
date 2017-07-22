---
title: File
linktitle: Variables File
description: "Vous pouvez accéder aux données relatives-au-système-de-fichier pour un fichier de contenu dans la variable `.File`."
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [variables et params]
#tags: [files, fichiers]
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

{{% note %}}
Pour plus d'informations sur la création de shortcodes et de modèles qui utilisent le jeu de fonctionnalités liées aux fichiers de Hugo, voir [Modèles de fichiers locaux](/templates/files/).
{{% /note %}}

L'objet `.File` contient les champs suivants :

`.File.Path`
: le chemin relatif origiinal de la page (par ex., `content/posts/foo.en.md`)

`.File.LogicalName`
: le nom du fichier de contenu qui représente une page (par ex., `foo.en.md`)

`.File.TranslationBaseName`
: le nom de fichier sans l'extenion ou l'identifiant facultatif de langue (e.g., `foo`)

`.File.BaseFileName`
: le nom de ficier sans l'extension (par ex., `foo.en`)

`.File.Ext`
: l'extension de fichier du fichier de contenu (par ex., `md`) ; ce peut être aussi appelé en utilisant `.File.Extension`. Notez que c'est *seulement* l'extension sans `.`.

`.File.Lang`
: la langue associé au fichier doné si les [Fonctionnalités Multilingues][multilingual] sont activées (par ex., `en`)

`.File.Dir`
: sur le chemin `content/posts/dir1/dir2/`, le chemin relatif du dossier du fichier de contenu sera renvoyé (par ex., `posts/dir1/dir2/`)

[Multilingual]: /gestion-contenu/multilingue/