---
title: Créer un Thème
linktitle: Créer un Thème
description: La commande `hugo new theme` échafaudera les débuts d'un nouveau thème pour que vous puissiez vous mettre sur votre chemin.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
categories: [themes, thèmes]
#tags: [themes, source, organization, directories, dossiers, organisation]
menu:
  docs:
    parent: "themes"
    weight: 30
weight: 30
sections_weight: 30
draft: false
aliases: [/themes/creation/,/tutorials/creating-a-new-theme/]
toc: true
wip: true
---

{{% warning "Utiliser des Liens Relatifs" %}}
Si vous créez un thème avec des plans pour le partager avec la communauté, utilisez des URL relatives puisque les utilisateurs de votre thème ne peuvent pas publier à partir de la racine de leur site. Voir [relURL](/fonctions/relurl) et [absURL](/fonctions/absurl).
{{% /warning %}}

Hugo peut initialiser un nouveau dossier de thème blanc dans votre dossier existant `themes` en utilisant la commande `hugo new` :

```bash
hugo new theme [nom]
```

## Composant du Thème

Un thème se compose de modèles et d'éléments statiques tels que les fichiers javascript et css. 
Les thèmes peuvent également fournir des [archetypes][], qui sont des types de contenu archétypes utilisés par la commande `hugo new` pour construire de nouveaux fichiers de contenu avec un front matter préconfiguré.

{{% note "Utilisez le tag Hugo Generator" %}}
La balise [`.Hugo.Generator`](/variables/hugo/) est incluse dans tous les thèmes présentés dans [Hugo Themes Showcase](http://themes.gohugo.io). Nous vous demandons d'inclure le tag du générateur dans tous les sites et thèmes que vous créez avec Hugo pour aider l'équipe principale à suivre l'utilisation et la popularité de Hugo.
{{% /note %}}

## Layouts

Hugo est construit autour du concept que les choses devraient être aussi simples que possible. Fondamentalement, le contenu du site Web est affiché de deux manières différentes, un seul
élément de contenu et une liste d'éléments de contenu. 
Avec Hugo, une mise en page de thème démarre avec les valeurs par défaut. Au fur et à mesure que des configurations supplémentaires sont définies, elles sont utilisées pour
le type de contenu ou la section à laquelle elles s'appliquent. Cela permet de simplifier les mises en page, mais permet une grande flexibilité.

## Contenu Unique

Le fichier de mise en page par défaut pour un fichier unique est situé sur `layouts/_default/single.html`.

## Liste de Contenus

Le fichier de layout par défaut pour les listes est situé sur  `layouts/_default/list.html`.

## Modèles de Partiel

Les créateurs de thème devraient utiliser les [modèles partiels](/templates/partials/) dans leurs fichiers de thème. Non seulement c'est une bonne pratique DRY d'inclure du code partagé, mais les partiels sont un type de modèle spéciale qui permet à l'utilisateur final du thème de remplacer simplement un petit élément d'un fichier ou d'injecter du code à l'intérieur du thème à partir de ses `/layouts` locaux. Ces modèles partiels sont parfaits pour une injection facile à l'intérieur du thème avec une maintenance minimale pour garantir une future compatibilité.

## Statique

Tout ce qui est dans le dossier `static` sera copié directement à l'intérieur du site final au moment du rendu. Aucune structure n'est fournie ici pour permettre une totale liberté. Il est commun d'oganiser le contenu statique en :

```
/css
/js
/img
```

La structure actuelle dépend entièrement de vous, le créateur du thème, sur la façon dont vous souhaitez organiser vos fichiers.

## Archétypes

Si votre thème utilise des clés spécifiques dans le front matter, c'est une bonne idée que de fournir un archétype pour chaque type de contenu que vous avez. [En savoir plus sur les archétypes][archetypes].

[archetypes]: /gestion-contenu/archetypes/
