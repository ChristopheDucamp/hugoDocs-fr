---
title: Installer et Utiliser des Thèmes
linktitle: Installer et Utiliser des Thèmes
description: Installer et utiliser facilement un thème à partir de la galerie des thèmes Hugo en utilisant l'interface de ligne de commande.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [thèmes]
#tags: [install, themes, source, organization, organisation, directories,usage]
menu:
  docs:
    parent: "Themes"
    weight: 10
weight: 10
sections_weight: 10
draft: false
aliases: [/themes/usage/,/themes/installing/]
toc: true
wip: true
---

{{% note "Pas de thème par défaut" %}}
Hugo ne fournit pas actuellement un thème "par défaut". Cette décision est intentionnelle. Nous vous laissons décider quel thème convient le mieux à votre projet Hugo.
{{% /note %}}

## Hypothèses

1. Vous avez déjà [installé Hugo sur votre machine de développement][install].
2. Vous avez installé git sur votre machine et vous êtes à l'aise avec un usage basique de git.

## Installer des Thèmes

Les thèmes apportés par la communauté sur [themes.gohugo.io](//themes.gohugo.io/) sont hébergés dans un [dépôt centralisé GitHub][themesrepo]. Le dépôt "Hugo Themes" sur <https://github.com/gohugoio/hugoThemes> est vraiment un méta-référentiel qui contient des indications sur un ensemble de thèmes abordés.

{{% warning "télécharger d'abord `git` "%}}
Sans [Git](https://git-scm.com/) installé sur votre ordinateur, aucune des instructions suivantes du thème ne fonctionnera. Les tutoriels Git dépassent la portée des documents Hugo, mais [GitHub](https://try.github.io/) et [codecademy](https://www.codecademy.com/learn/learn-git) offrent gratuitement des cours interactifs pour débutants.
{{% /warning %}}

### Installer Tous les Thèmes

Vous pouvez installer *tous* les thèmes Hugo disponibles en clonant tout le [dépôt Hugo Theme sur GitHub][themesrepo] à partir de votre répertoire de travail. Selon votre connexion internet, le téléchargement de tous les thèmes peut prendre un certain temps.

```bash
git clone --depth 1 --recursive https://github.com/gohugoio/hugoThemes.git themes
```

Avant d'utiliser un thème, retirez le dossier .git dans ce dossier racine de theme. Autrement, cela provoquera des problèmes si vous déployez en utilisant Git.

### Installer un Thème Unique

Déplacez-vous dans le répertoire `themes` et téléchargez un thème en remplaçant `URL_TO_THEME` par l'URL du référentiel de thèmes :

```bash
cd themes
git clone URL_TO_THEME
```

L'exemple suivant montre comment utiliser le thème "Hyde", qui a sa source hébergée sur <https://github.com/spf13/hyde> :

{{% code file="clone-theme.sh" %}}
```bash
cd themes
git clone https://github.com/spf13/hyde
```
{{% /code %}}

Alternativement, vous pouvez télécharger le thème en tant que fichier `.zip`, décompressez le contenu du thème, puis déplacez la source décompressée dans votre répertoire` themes`.

{{% note "Read the `README`" %}}
Toujours examiner le fichier `README.md` qui est livré avec un thème. Souvent, ces fichiers contiennent d'autres instructions requises pour la configuration du thème ; par exemple, la copie de valeurs à partir d'un exemple de fichier de configuration.
{{% /note %}}

## Placement du Thème

Assurez-vous que vous avez installé les thèmes que vous souhaitez utiliser dans le dossier `/ themes`. C'est le répertoire par défaut utilisé par Hugo. Hugo est capable de modifier le répertoire des thèmes via la variable [`themesDir` dans la configuration de votre site][config], mais cela n'est pas recommandé.

## Utiliser les Thèmes

Hugo applique d'abord le thème décidé et applique tout ce qui se trouve dans le répertoire local. Cela permet une personnalisation plus facile tout en conservant la compatibilité avec la version en amont du thème. Pour en savoir plus, allez sur [personnaliser les thèmes][customizethemes].

### Ligne de Commande

Il existe deux approches différentes pour utiliser un thème avec votre site Web Hugo : via la CLI Hugo ou dans le fichier de configuration.

Pour changer un thème via la CLI Hugo, vous pouvez passer le [flag][] `-t` lors de la construction de votre site :

```bash
hugo -t themename
```

Vous voudrez sans doute ajouter le thème lors de l'exécution du serveur local Hugo, surtout si vous comptez [personnaliser le thème][customizethemes] :

```bash
hugo server -t themename
```

### Fichier `config`

Si vous avez déjà décidé sur le thème de votre site et que vous ne voulez pas jouer avec la ligne de commande, vous pouvez ajouter le thème directement à votre [fichier de configuration du site][config] :

```yaml
theme: nomtheme
```

{{% note "Une note sur le `nomtheme`" %}}
Le `nomtheme` dans les exemples au-dessus doit correspondre au nom du dossier spécifique du thème dans `/themes` ; par ex., le nom du dossier (probabelemnt en bas de casse et urlisé ) plutôt que le nom du thème affiché dans le [Site de Présentation des Thèmes](http://themes.gohugo.io).
{{% /note %}}

[customizethemes]: /themes/personnaliser/
[flag]: /demarrage/usage/ "Regardez la liste complète des flags dans l'usage basique d'Hugo."
[install]: /demarrage/installer/
[config]: /demarrage/configuration/  "Learn how to customize your Hugo website configuration file in yaml, toml, or json."
[themesrepo]: https://github.com/gohugoio/hugoThemes