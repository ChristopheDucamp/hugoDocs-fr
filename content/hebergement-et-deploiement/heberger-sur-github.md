---
title: GitHub
linktitle: Héberger sur GitHub
description: Déployer Hugo en tant que projet GitHub Pages ou site personnel/organisation et automatiser tout le processus avec un simple script shell.
date: 2014-03-21
publishdate: 2014-03-21
lastmod: 2017-07-21
categories: [hébergement et déploiement]
#tags: [hosting, hébergement, déploiement, git]
authors: [Spencer Lyon, Gunnar Morling, Christophe Ducamp]
draft: false
toc: true
aliases: [/hebergement-et-deploiement/hosting-on-github/,/tutorials/github-pages-blog/]
---

GitHub fournit un hébergement statique gratuit et rapide sur SSL pour les personnes, organisations ou pages de projet directement à partir d'un repo GitHub via son [service GitHub Pages][].

## Hypothèses

1. Vous avez Git 2.5 ou +  [installé sur votre machine][installgit].
2. Vous avez un compte GitHub. [S'enregistrer][ghsignup] sur GitHub est gratuit.
3. Vous avez un site web Hugo prêt-à-publier ou avez au moins terminé le [Quick Start][].

Si vous travaillez dans un compte Organisation ou si vous voulez régler un site web d'utilisateur sur GitHub et souhaiteriez plus d'informations, visitez la [documentation GitHub Pages][ghorgs].

{{% note %}}
Assurez-vous que votre valeur-clé `baseURL` dans votre [fichier de configuration de site](/demarrage/configuration/) soit l'URL complète de votre repository GitHub Page si vous utilisez l'URL par défaut GH Pages (par ex. `votrenomutilisateur.github.io/monnomprojet/`) et non un domaine personnalisé.
{{% /note %}}

## Déploiement via le dossier `/docs` sur la Branche Master

[Comme décrit dans la documentation GitHub Pages][ghpfromdocs], vous pouvez déployer à partir d'un dossier appelé `docs/` sur votre branche master. Pour utiliser efficacement cette fonctionnalité avec Hugo, vous devrez modifier le répertoire de publication de Hugo dans le fichier de [configuration de votre site][config] `config.toml` et `config.yaml`, respectivement :

```yaml
publishDir: docs
```

```toml
publishDir = "docs"
```

Après avoir lancé `hugo`, poussez votre branche master vers le repo distant et choisissez le dossier `docs/` comme le site web source de votre repo. Faites ce qui suit à partir de l'intérieur  de votre projet GitHub :

1. Allez sur **Settings** &rarr; **GitHub Pages**
2. À partir de **Source**,  sélectionnez "master branch /docs folder". Si l'option n'est pas activée, vous n'avez probablement pas de dossier `docs/` à la racine de votre projet.

{{% note %}}
L'option `docs/` est l'approche la plus simple mais requiert que vous réglez un répertoire de publication dans votre configuration de site. Vous ne pouvez actuellement pas configurer GitHub pages pour publier à partir d'un autre répertoire sur master, et tout le monde et tout le monde n'apprécie pas d'avoir le site de sortie en même temps que les fichiers source dans le contrôle de la version.
{{% /note %}}

## Déploiement à partir de votre Branche `gh-pages` 

Vous pouvez également indiquer à GitHub Pages de traiter votre branche `master` comme le site publié ou pointer vers une branche `gh-pages` séparée. Cette dernière approche est un peu plus complexe mais présente des avantages :

* Elle conserve votre site source et généré dans différentes branches et maintient donc l'historique de contrôle de version pour les deux.
* Contrairement à l'option `docs/` précédente, elle utilise le dossier `public` par défaut.

### Préparations pour la branche `gh-pages`

Ces étapes ne doivent être effectuées qu'une seule fois. Remplacez `upstream` par le nom de votre remote ; par exemple, `origin` :

#### Ajoutez le dossier public

Tout d'abord, ajoutez le dossier `public` à votre fichier `.gitignore` à la racine du projet afin que le répertoire soit ignoré sur la branche principale :

```bash
echo "public" >> .gitignore
```

#### Initialisez votre branche `gh-pages`

Vous pouvez maintenant initialiser votre branche `gh-pages` comme une [branche orpheline][] vide :

```bash
git checkout --orphan gh-pages
git reset --hard
git commit --allow-empty -m "Initializing gh-pages branch"
git push upstream gh-pages
git checkout master
```

### Construction et Déploiement

Maintenant, vérifiez la branche `gh-pages` dans votre dossier `public` à l'aide de [la fonction Worktree][] de git. En fait, le worktree vous permet d'avoir plusieurs branches du même repo  local à vérifier dans différents répertoires :

```sh
rm -rf public
git worktree add -B gh-pages public upstream/gh-pages
```

Régénérez le site en utilisant la commande `hugo` et commitez  les fichiers générés sur la branche `gh-pages` :

{{% code file="commit-gh-pages-files.sh"%}}
```bash
hugo
cd public && git add --all && git commit -m "Publier sur gh-pages" && cd ..
```
{{% /code %}}

Si les modifications apportées à votre branche locale `gh-pages` semblent bien, poussez-les sur le repo distant :

```bash
git push upstream gh-pages
```

#### Réglez `gh-pages` comme votre Branche Publique

Pour utiliser votre branche `gh-pages` en tant que branche de publication, vous devrez configurer le dépôt dans l'IU GitHub. Cela se produira probablement automatiquement une fois que GitHub réalisera que vous avez créé cette branche. Vous pouvez également configurer la branche manuellement à partir de votre projet GitHub :

1. Accédez sur **Settings** &rarr; **Github Pages**
2. À partir de **Source**, sélectionnez "gh-pages branch", puis **Save**. Si l'option n'est pas activée, vous n'avez probablement pas encore créé la branche OU vous n'avez pas poussé la branche de votre machine locale vers le dépôt hébergé sur GitHub.

Après un court moment, vous verrez les contenus actualisés sur votre site GitHub Pages.

### Placez-le dans un Script

Pour automatiser ces étapes, vous pouvez créer un script avec les contenus suivants :

{{% code file="publish_to_ghpages.sh" %}}
```sh
#!/bin/sh

DIR=$(dirname "$0")

cd $DIR/..

if [[ $(git status -s) ]]
then
    echo "The working directory is dirty. Please commit any pending changes."
    exit 1;
fi

echo "Deleting old publication"
rm -rf public
mkdir public
git worktree prune
rm -rf .git/worktrees/public/

echo "Checking out gh-pages branch into public"
git worktree add -B gh-pages public upstream/gh-pages

echo "Removing existing files"
rm -rf public/*

echo "Generating site"
hugo

echo "Updating gh-pages branch"
cd public && git add --all && git commit -m "Publishing to gh-pages (publish.sh)"
```
{{% /code %}}

Cela annulera s'il y a des modifications en attente dans le répertoire de travail et assurera également que tous les fichiers output précédemment existants soient supprimés. Ajustez le script à votre goût, par ex. pour inclure le push final vers le repo distant si vous n'avez pas besoin de jeter un coup d'œil à la branche gh-pages avant de pousser. Ou ajouter `echo votrenomdomaine.com >> CNAME` si vous configurez vos "gh-pages" pour utiliser le domaine personnalisé.

## Déploiement à partir de Votre Branche `master`

Pour utiliser `master` comme votre branche de publicaiton, vous aurez besoin que votre site Web rendu vive à la racine du dépôt GitHub. Les étapes doivent être similaires à celles de la branche `gh-pages`, à l'exception que vous allez créer votre repo GitHub avec le répertoire `public` comme racine. Notez que cela ne fournit pas les mêmes avantages que la branche `gh-pages` pour maintenir votre source et votre sortie séparément, mais contrôlées par version, dans le même compte.

Vous devrez également définir `master` comme votre branche publiable à partir de l'interface utilisateur GitHub :

1. Allez sur **Settings** &rarr; **GitHub Pages**
2. À partir de **Source**, sélectionnez "master branch" et puis **Save**.

## Héberger des Pages Utilisateur GitHub ou des Pages Organisation 

Comme mentionné [dans cet article GitHub Help](https://help.github.com/articles/user-organization-and-project-pages/), vous pouvez héberger une page utilisateur/organisation en plus de vos pages projet. Voici les différences-clés dans les sites web GitHub Pages pour les Utilisateurs et Organisations :

1. Vous devez utiliser le schéma de nommage `<USERNAME>.github.io` pour votre repo GitHub.
2. Le contenu provenant de la branche `master` sera utilisé pour publier votre site GitHub Pages.

Cela devient beaucoup plus simple dans ce cas: nous allons créer deux repos distincts, l'un pour le contenu de Hugo et un sous-module git avec le contenu du dossier `public`.

### Instructions étapes par étapes

1. Créez un repository git `<VOTRE-PROJET>` sur GitHub. Ce  repository contiendra le contenu d'Hugo et d'autres fichiers source.
2. Créez un repository GitHub `<NOMUTILISATEUR>.github.io`. Ceci est le repository qui contiendra la version complètement rendue de votre site web Hugo.
3. `git clone <VOTRE-PROJET-URL> && cd <YOUR-PROJECT>`
4.  Faites fonctionner votre site web localement (`hugo server` ou `hugo server -t <VOTRETHEME>`) et ouvrez votre navigateur sur  <http://localhost:1313>.
5. Une fois que vous êtes satisfait des résultats : 
    * Pressez <kbd>Ctrl</kbd>+<kbd>C</kbd> pour éteindre le serveur
    * `rm -rf public` pour retirer complètement le dossier `public` s'il y en a un
6. `git submodule add -b master git@github.com:<NOMUTILISATEUR>/<NOMUTILISATEUR>.github.io.git public`. Ceci crée un [submodule][] git. Maintenant quand vous lancez la commande `hugo` pour construire votre site vers `public`, le dossier `public` créé aura un "remote origin" différent (c'est-à-dire un repository hébergé GitHub). Vous pouvez automatiser certaines de ces étapes avec le script suivant.

#### Placez ça dans un Script

Vous avez presque fini. Vous pouvez maintenant ajouter un script  `deploy.sh` pour automatiser les étapes qui précédent. Vous pouvez aussi faire un exécutable avec `chmod +x deploy.sh`.

Ce qui suit sont les contenus du script `deploy.sh` :

```sh
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..
```


Vous pouvez alors lancer la commande `./deploy.sh "Votre message de commit facultatif"` pour envoyer les modifications à  `<NOMUTILISATEUR>.github.io`. Notez que vous voudrez probablement commiter aussi les modifications vers votre repository  `<VOTRE_PROJET>`.

C'est tout ! Votre page personnelle devrait être en train de tourner sur `https://votrenomutilisateur.github.io` d'ici quelques minutes.

## Utiliser un Domaine Personnalisé

Si vous souhaitez utiliser un domaine personnalisé pour votre site GitHub Pages, créez un fichier `static/CNAME`. Votre nom de domaine personnalisé devrait être le seul contenu à l'intérieur de `CNAME`. Étant donné qu'il est à l'intérieur de `static`, le site publié contiendra le fichier CNAME à la racine du site publié, ce qui est une exigence de GitHub Pages.

Pour plus d'informations, reportez-vous à la [documentation officielle pour les domaines personnalisés][domaines].

[config]: /demarrage/configuration/
[domains]: https://help.github.com/articles/using-a-custom-domain-with-github-pages/
[ghorgs]: https://help.github.com/articles/user-organization-and-project-pages/#user--organization-pages
[ghpfromdocs]: https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/#publishing-your-github-pages-site-from-a-docs-folder-on-your-master-branch
[ghsignup]: https://github.com/join
[service GitHub Pages]: https://help.github.com/articles/what-is-github-pages/
[installgit]: https://git-scm.com/downloads
[orphan branch]: https://git-scm.com/docs/git-checkout/#git-checkout---orphanltnewbranchgt
[Quick Start]: /getting-started/quick-start/
[submodule]: https://github.com/blog/2104-working-with-submodules
[worktree feature]: https://git-scm.com/docs/git-worktree
