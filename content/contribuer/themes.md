---
title: Ajoutez votre Thème Hugo à la Galerie
linktitle: Thèmes
description: Vous avez construit un thème Hugo et vous voulez contribuer en retour dans la communauté. Ajoutez votre thème à la Galerie Hugo.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [contribuer]
#tags: [contribuer,themes,design]
authors: [digitalcraftsman]
menu:
  docs:
    parent: "contribuer"
    weight: 30
weight: 30
sections_weight: 30
draft: false
aliases: [/contribute/theme/]
wip: true
toc: true
---

Une collection de tous les thèmes créés par la communauté Hugo, y compris des captures d'écran et des démos, se trouve à l'adresse <https://themes.gohugo.io>. Chaque thème de cette liste sera automatiquement ajouté au site des thèmes. Les mises à jour de thèmes ne sont pas programmées, mais elles se produisent généralement au moins une fois par semaine.

## tl;dr

1. Créez votre thème en utilisant `hugo new theme <NOMTHEME>` ;
2. Testez votre thème contre <https://github.com/spf13/HugoBasicExample> \*
3. Ajoutez un fichier `theme.toml` à la racine de votre thème avec toutes métadonnées requises
4. Ajoutez un `README.md` descriptif à la racine du thème source
5. Ajoutez `/images/screenshot.png` et `/images/tn.png`

\* Si votre thème ne correspond pas au site `Hugo Basic Example`, nous encourageons les auteurs de thème à fournit un site Hugo auto-contenu dans `/exampleSite`.

{{% note %}}

Le nom du dossier ici ---`exampleSite`--- est important, car ce dossier sera repris et utilisé par le script qui génère le site de Thèmes Hugo. Il reflète le répertoire racine d'un site Web Hugo et vous permet d'y ajouter du contenu personnalisé, des assets et un fichier `config` avec des valeurs présélectionnées.
{{% /note %}}

Regardez l'[exampleSite du thème Hugo Artist][artistexample] pour un bon exemple.

{{% note %}}
SVP faites en sorte que le contenu dans l'exemple de votre site soit aussi neutre que possible. Nous espérons que cela va sans dire.
{{% /note %}}

## Exigences du Thème

Afin d'ajouter votre thème à la Galerie (Showcase), les exigences suivantes doivent être satisfaites : 

1. `theme.toml` avec tous les champs requis
2. Images miniature et capture-écran
3. Un bon fichier README d'instructions pour les utilisateurs
4. Ajout au repo GitHub hugoThemes

### Ajoutez Votre Thème au Repo

Le moyen le plus facile d'ajouter votre thème est d'[ouvrir un nouvel "issue" dans le repo du thème][themeissuenew] avec un lien vers le repo de votre thème sur GitHub.

### Créez un fichier `theme.toml`

`theme.toml` contient des métadonnées sur le thème et son créateur et devrait être créée automatiquement lors du lancement   de la commande `hugo new theme`. Le fichier généré automatiquement est fourni ici aussi pour un téléchargement facile :

{{% code file="theme.toml" download="theme.toml" %}}
```toml
name = ""
license = "MIT"
licenselink = "https://github.com/<VOTRENOM>/<VOTRETHEME>/blob/master/LICENSE.md"
description = ""
homepage = "http://votresite.com/"
tags = []
features = []
min_version = 0.19

[author]
  name = ""
  homepage = ""

# Si portage d'un thème existant
[original]
  name = ""
  homepage = ""
  repo = ""
```
{{% /code %}}

Les champs suivant sont obligatoires :

```toml
name = "Hyde"
license = "MIT"
licenselink = "https://github.com/spf13/hyde/blob/master/LICENSE.md"
description = "An elegant open source and mobile first theme"
homepage = "http://siteforthistheme.com/"
tags = ["blog", "company"]
features = ["blog"]
min_version = 0.13

[author]
    name = "spf13"
    homepage = "http://spf13.com/"

# Si portage d'un thème existant
[original]
    author = "mdo"
    homepage = "http://hyde.getpoole.com/"
    repo = "https://www.github.com/mdo/hyde"
```

{{% note %}}
1. Ceci est différent du fichier `theme.toml` créé par `hugo new theme` dans les versions d'Hugo avant la v0.14.
2. Seul `theme.toml` est accepté ; c'est à dire pas de `theme.yaml` et pas de `theme.json`.
{{% /note %}}

### Images

Les captures d'écran sont utilisées pour des aperçus dans la galerie de thème Hugo. Assurez-vous qu'elles aient les bonnes dimensions :

* La miniature devrait être de 900px × 600px
* La capture d'écran devrait être de 1500px × 1000px
* Les médias doivent être posés dans 
     * <THEMEDIR>/images/screenshot.png</ code>
     * <THEMEDIR>/images/tn.png</ code>

Des médias supplémentaires peuvent être fournis dans le même répertoire.


### Créer un fichier README 

Le fichier README de votre thème doit être écrit en markdown et sauvegardé à la racine de la structure de répertoire de votre thème. Votre `README.md` sert de

1. Contenu pour la page de détails de votre thème sur <https://themes.gohugo.io>
2. Informations générales sur le thème dans votre dépôt GitHub


#### Exemple `README.md`

Vous pouvez télécharger le `README.md` suivant comme un aperçu :

{{% code file="README.md" download="README.md" %}}
```markdown

# Theme Title

**Need input from @digitalcraftsman on what could be added to this file.**




```
{{% /code %}}

{{% note "Captures-écran dans votre `README.md`"%}}

Si vous ajoutez des captures d'écran au README, utilisez les chemins de fichiers absolus au lieu des images relatives `/images/screenshot.png`. Les chemins relatifs fonctionnent bien sur GitHub mais ils ne correspondent pas à la structure de répertoire de [themes.gohugo.io](http://themes.gohugo.io/). Par conséquent, les navigateurs ne pourront pas afficher les captures d'écran sur le site thématique sous le chemin donné (relatif).
{{% /note %}}

[artistexample]: https://github.com/digitalcraftsman/hugo-artists-theme/tree/master/exampleSite
[themeissuenew]: https://github.com/gohugoio/hugoThemes/issues/new