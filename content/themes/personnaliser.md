---
title: Personnaliser un Thème
linktitle: Personnaliser un Thème
description: Personnalisez un thème en remplaçant les layouts de thème et les éléments statiques dans vos dossiers de projet de haut niveau.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [themes, thèmes]
#tags: [source, organization, dossiers, organisation, thèmes]
menu:
  docs:
    parent: "themes"
    weight: 20
weight: 20
sections_weight: 20
draft: false
aliases: [/themes/customize/]
toc: true
wip: true
---

Voici les concepts clés pour la personnalisation d'un site Hugo avec des thèmes. Hugo vous permet de compléter *ou* remplacer tout modèle de thème ou fichier statique par des fichiers dans votre répertoire de travail.

{{% note %}}
Lorsque vous utilisez un thème cloné à partir de son dépôt git, ne modifiez pas directement les fichiers du thème. Au lieu de cela, la personnalisation du thème dans Hugo est une question de *remplacer* les modèles mis à votre disposition dans un thème. Cela offre la flexibilité supplémentaire de peaufiner un thème pour répondre à vos besoins tout en restant à jour avec le thème en amont.
{{% /note %}}

## Remplacer les Fichiers Statiques
Il y a des moments où vous souhaitez inclure des actifs statiques qui diffèrent des versions du même élément livré avec un thème.

Par exemple, un thème peut utiliser jQuery 1.8 à l'emplacement suivant :

```bash
/themes/<THEME>/static/js/jquery.min.js
```

Vous souhaitez remplacer la version de jQuery qui est livrée avec le thème par le `jquery-3.1.1.js` plus récent. 
La façon la plus simple de le faire est de remplacer le fichier *par un fichier du même nom* dans le même chemin relatif à la racine de votre projet. Par conséquent, modifiez `jquery-3.1.1.js` vers `jquery.min.js` afin qu'il soit *identique* à la version du thème et placez le fichier ici :

```bash
/static/js/jquery.min.js
```

## Remplacer les Fichiers de Modèle

Chaque fois que Hugo recherche un modèle correspondant, il vérifiera d'abord le répertoire de travail avant de regarder dans le répertoire des thèmes. Si vous souhaitez modifier un modèle, créez simplement ce modèle dans votre répertoire local `layouts`.

La [commande de recherche de modèle][lookup] explique les règles que Hugo utilise pour déterminer quel modèle utiliser pour un contenu donné. Lisez et comprenez ces règles avec attention.

Ceci est particulièrement utile lorsque le créateur du thème a utilisé des [modèles partiels][partials]. Ces modèles partiels sont parfaits pour une injection facile dans le thème avec une maintenance minimale pour assurer une compatibilité future.

Par exemple:

```bash
/themes/<THEME>/layouts/_default/single.html
```

serait remplacé par 

```bash
/layouts/_default/single.html
```

{{% warning %}}
Cela ne fonctionne que pour les modèles que Hugo «connaît» (c'est-à-dire tous ceux qui suivent sa convention pour la structure des dossiers et la dénomination). Si un thème importe des fichiers de modèle dans un répertoire créativement nommé, Hugo ne saurait pas rechercher les `/layouts` locaux.
{{% /warning %}}

## Remplacer les archétypes

Si l'archétype livré avec le thème pour un type de contenu donné (ou tous les types de contenu) ne correspond pas à la façon dont vous utilisez le thème, n'hésitez pas à le copier dans votre dossier `/archetypes' et à y apporter des modifications comme bon vous semble .

{{% warning "Méfiez-vous de `layouts/_default` "%}}
Le dossier `_default` est une force très puissante dans Hugo, notamment en ce qui concerne l'écrasement de fichiers de thème. Si un fichier par défaut se trouve dans les [archétypes locaux](/gestion-contenu/archetypes/) ou dans le dossier layout (c.-à-d. `archetypes/default.md` ou `/layouts/_default/*.html`, respectivement), il remplacera le fichier du même nom dans le répertoire de thème correspondant (c.-à-d. `themes/<THEME>/archetypes/default.md` ou` themes/<THEME>/layout/_defaults/*. html`, respectivement).

Il est généralement préférable de remplacer des fichiers spécifiques plutôt que d'utiliser `layouts/_default/*.html` dans votre répertoire de travail.
{{% /warning %}}

[archetypes]: /gestion-contenu/archetypes/
[lookup]: /templates/ordre-recherche/
[partials]: /templates/partiels/