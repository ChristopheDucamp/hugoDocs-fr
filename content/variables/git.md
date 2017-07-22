---
title: Git
linktitle: Variables d'Info Git
description: Recevoir la dernière information de révision pour chaque contenu de fichier.
date: 2017-03-12
publishdate: 2017-03-12
lastmod: 2017-07-21
categories: [variables et params]
#tags: [git]
draft: false
menu:
  docs:
    parent: "variables"
    weight: 70
weight: 70
sections_weight: 70
aliases: [/extras/gitinfo/]
toc: false
wip: false
---

{{% note "Considérations de Performance `.GitInfo`"  %}}
Les intégration de Git de Hugo devraient être très performantes, mais elle peuvent accroître votre temps de build. Ceci dépendra de la taille de votre historique Git.
{{% /note %}}

## Pré-Requis `.GitInfo`

1. Le site Hugo doit être un dossier activé-Git.
2. L'exécutable Git doit être installé dans votre `PATH` de système.
3. La focntonnalité `.GitInfo` doit être activée dans votre projet Hugo en passant le flag `--enableGitInfo` à la ligne de commande ou en réglant `enableGitInfo` sur `true` dans votre [fichier de configuration de site][configuration].

## L'Objets `.GitInfo`

L'objet `GitInfo` contient les champs suivants :

`.AbbreviatedHash`
: le hash de commit abrégé (par ex., `866cbcc`)

`.AuthorName`
: le nom de l'auteur, respectant `.mailmap`

`.AuthorEmail`
: l'adresse email de l'auteur, respectant `.mailmap`

`.AuthorDate`
: la date de l'auteur

`.Hash`
: le hash de commit (par ex., `866cbccdab588b9908887ffd3b4f2667e94090c3`)

`.Subject`
: le sujet du message de commit (par ex., `tpl: Add custom index function`)

[configuration]: /demarrage/configuration/
