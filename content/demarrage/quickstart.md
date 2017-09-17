---
title: Quick Start
linktitle: Quick Start
description: Créez un site Hugo en utilisant le magnifique thème Ananke.
date: 2013-07-01
publishdate: 2013-07-24
categories: [démarrage]
#tags: [quick start,usage]
authors: [Shekhar Gulati, Ryan Watters]
menu:
  docs:
    parent: "démarrage"
    weight: 10
weight: 10
sections_weight: 10
draft: false
aliases: [/getting-started/quick-start/,/quickstart/, /overview/quickstart/]
toc: true
---

{{% note %}}
Ce guide de démarrage rapide utilise `macOS` dans les exemples. Pour les instructions d'installation d'Hugo sur d'autres systèmes d'exploitation, regardez [installer](/demarrage/installer/).

Vous aurez aussi besoin d'[avoir installé Git](https://git-scm.com/downloads) pour faire tourner ce tutoriel.
{{% /note %}}


## Étape 1. Installez Hugo

{{% note %}}
`Homebrew`, un gestionnaire de package pour `macOS`, peut être installé à partir de [brew.sh](https://brew.sh/). Voir [comment installer](/démarrage/installer) si vous tournez sur Windows, etc.
{{% /note %}}

```bash
brew install hugo
```

Pour vérifier votre nouvelle installation :

```bash
hugo version
```


{{< asciicast HDlKrUrbfT7yiWsbd6QoxzRTN >}}


## Étape 2 : Créez un nouveau site 

```bash
hugo new site quickstart
```

La commande au-dessus créera un nouveau site Hugo dans un dossier appelé `quickstart`.

{{< asciicast 1PH9A2fs14Dnyarx5v8OMYQer >}}


## Étape 3 : Ajoutez un thème

Regardez [themes.gohugo.io](https://themes.gohugo.io/) pour une liste de thèmes à envisager. Ce quickstart utilise le magnifique [thème Ananke](https://themes.gohugo.io/gohugo-theme-ananke/).

```bash
cd quickstart
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke

# Editez votre fichier de configuration  config.toml
# et ajoutez le theme Ananke.
echo 'theme = "ananke"' >> config.toml
```


{{< asciicast WJM2LEZQs8VRhNeuZ5NiGPp9I >}}

## Étape 4 : Ajoutez un peu de Contenu

```bash
hugo new post/mon-premier-post.md
```


Éditez si vous voulez le nouveau fichier de contenu créé. Maintenant, démarrez le serveur Hugo avec l'activation de [drafts](/demarrage/usage/#contenus-draft-futurs-et-expire) :

```bash
hugo server -D
```

ce qui devrait donner dans la console : 
```bash

Started building sites ...
Built site for language en:
1 of 1 draft rendered
0 future content
0 expired content
1 regular pages created
8 other pages created
0 non-page files copied
1 paginator pages created
0 categories created
0 tags created
total in 18 ms
Watching for changes in /Users/bep/sites/quickstart/{data,content,layouts,static,themes}
Serving pages from memory
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```


**Naviguez sur votre nouveau site sur [http://localhost:1313/](http://localhost:1313/).**



## Étape 5 : Personnalisez le Thème

Votre nouveau site a déjà fière allure, mais vous voudrez sans doute le tripoter un peu avant de le présenter au public.

### Configuration du Site

Ouvrez `config.toml` dans un éditeur de texte :

```toml
baseURL = "http://example.org/"
languageCode = "en-us"
title = "My New Hugo Site"
theme = "ananke"
```


Remplacez le `title` au-dessus par quelque chose de plus personnel. Aussi si vous avez déjà un domaine prêt l'emploi, paramétrez `baseURL`. Notez que cette valeur n'est pas nécessaire quand votre site tourne sur le serveur de développement local.

{{% note %}}
**Truc :** Faites les modifications de la configuration du site ou de tout autre fichier dans votre site pendant que le serveur Hugo est en train de tourner, et vous verrez les modifications directement en live dans le navigateur.
{{% /note %}}


Pour les options spécifiques de configuration de thème, voir le [site du thème](https://github.com/budparr/gohugo-theme-ananke).

**Pour de plus amples personnalisations du thème, regardez comment [Personnaliser un Thème](/themes/personnaliser/).**

## Récapitulation 

{{< asciicast pWp4uvyAkdWgQllD9RCfeBL5k >}}







