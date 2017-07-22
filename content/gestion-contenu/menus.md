---
title: Menus
linktitle: Menus
description: Hugo dispose d'un système de menu vraiment puissant.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [content management, gestion de contenu]
#tags: [menus]
draft: false
aliases: []
toc: true
---

{{% note %}}
Si tout ce que vous voulez est un simple menu pour vos sections, regardez la ["Section Menu pour Blogueurs Paresseux" dans les Modèles de Menu](/templates/menu-templates/#section-menu-pour-blogueurs-paresseux).
{{% /note %}}

Vous pouvez faire ça :

* Placez le contenu dans un ou plusieurs menus
* Gérez les menus imbriqués avec une profondeur illimitée
* Créez des entrées de menu sans les rattacher à aucun contenu
* Distinguer l'élément actif (et la branche active)


## Qu'est-ce qu'un Menu dans Hugo ?

Un **menu** est une liste nommée d'entrées de menu accessible par nom via la [variable site `.Site.Menus`][sitevars]. Par exemple, vous pouvez accéder à votre menu principal de site `main` via `.Site.Menus.main`.

{{% note %}}
Si vous utilisez la [fonctionnalité multilingue](/gestion-contenu/multilingual/), vous pouvez définir des menus indépendants de la langue.
{{% /note %}}

Une entrée de menu a les propriétés suivantes (c.a.d. des variables) disponibles pour lui :

`.URL`
: string

`.Name`
: string

`.Menu`
: string

`.Identifier`
: string

`.Pre`
: template.HTML

`.Post`
: template.HTML

`.Weight`
: int

`.Parent`
: string

`.Children`
: Menu

Notez que les menus ont aussi les fonctions suivantes qui sont disponibles :

`.HasChildren`
: boolean

En outre, il existe quelques fonctions pertinentes disponibles pour les menus sur une page :

`.IsMenuCurrent`
: (menu string, menuEntry *MenuEntry ) boolean

`.HasMenuCurrent`
: (menu string, menuEntry *MenuEntry) boolean

## Ajouter du contenu aux menus

Hugo vous permet d'ajouter du contenu à un menu via le [front matter](/gestion-contenu/front-matter/) du contenu.

### Simple

Si tout ce que vous devez faire est ajouter une entrée à un menu, le formulaire simple fonctionne bien.

#### Un menu unique

```yaml
---
menu: "main"
---
```

#### Plusieurs menus

```yaml
---
menu: ["main", "footer"]
---
```

#### Avancé


```yaml
---
menu:
  docs:
    parent: 'extras'
    weight: 20
---
```

## Ajouter des Entrées de Non-contenu à un Menu

Vous pouvez également ajouter des entrées aux menus qui ne sont pas attachées à un contenu. Cela se déroule dans le [fichier `config`][config] de votre projet Hugo.

Voici un exemple de code extrait d'un fichier `config.toml` :

{{% code file="config.toml" %}}
```toml
[[menu.main]]
    name = "about hugo"
    pre = "<i class='fa fa-heart'></i>"
    weight = -110
    identifier = "about"
    url = "/about/"
[[menu.main]]
    name = "getting started"
    pre = "<i class='fa fa-road'></i>"
    weight = -100
    url = "/getting-started/"
```
{{% /code %}}

Voici l'extrait équivalent dans un `config.yaml`:

{{% code file="config.yml" %}}
```yaml
---
menu:
  docs:
      - Name: "about hugo"
        Pre: "<i class='fa fa-heart'></i>"
        Weight: -110
        Identifier: "about"
        URL: "/about/"
      - Name: "getting started"
        Pre: "<i class='fa fa-road'></i>"
        Weight: -100
        URL: "/getting-started/"
---
```
{{% /code %}}

{{% note %}}
Les URLs doivent être relatives à la racine du contexte. Si la `baseURL` est `http://exemple.com/monsite/`, alors les URLs dans le menu ne doivent pas inclure la racine du contexte `monsite`. Utiliser une URL absolue écraserea la baseURL. Si la valeur utilisée pour `URL` dans l'exemple au-dessus est `http://sousdomaine.exemple.com/`, l'output sera `http://sousdomaine.exemple.com`.
{{% /note %}}

## Imbrication

Toute l'imbrication du contenu s'effectue via le champ `parent`.

Le parent d'une entrée devrait être l'identifiant d'une autre entrée. L'identifiant doit être unique (dans un menu).

L'ordre suivant est utilisé pour déterminer un identificateur :

`.Name> .LinkTitle> .Title`

Cela signifie que `.Title` sera utilisé à moins que` .LinkTitle` soit présent, etc. En pratique, `.Name` et` .Identifier` ne servent qu'à structurer les relations et ne sont donc jamais affichés.

Dans cet exemple, le niveau supérieur du menu est défini dans votre [fichier `config` du site][config]). Toutes les entrées de contenu sont associées à l'une de ces entrées via le champ `.Parent`.

## Produire des Menus

Voir [Modèles Menu](/templates/menus/) pour vous informer sur la manière de produire des menus de sites dans vos modèles.

[config]: /demarrage/configuration/
[multilingual]: /gestion-contenu/multilingue/
[sitevars]: /variables/
