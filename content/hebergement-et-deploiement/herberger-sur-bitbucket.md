---
title: Hébergement sur Bitbucket
linktitle: Hébergement sur Bitbucket
description: Vous pouvez utiliser Bitbucket en conjonction avec Aerobatic pour construire, déployer et héberger un site web Hugo.
date: 2017-02-04
publishdate: 2017-02-04
lastmod: 2017-07-21
categories: [héberement et déploiement]
#tags: [hébergement,bitbucket,déploiement,aerobatic]
authors: [Jason Gowans]
draft: false
toc: true
aliases: [/hebergement-et-deploiement/hosting-on-bitbucket/]
---

Vous pouvez utiliser [Bitbucket](https://bitbucket.org/) et [Aerobatic](https://www.aerobatic.com) construire, déployer et héberger un site web Hugo. Aerobatic est un service d'hébergement statique qui s'intègre avec Bitbucket et fournit un hébergement gratuit.

## Hypothèses

* à l'aise avec Git pour le contrôle de version
* Un [compte Bitbucket](https://bitbucket.org/account/signup/)

## Installer l'interface de ligne de commande d'Aerobatic

Si vous n'avez pas déjà utilisé Aerobatic, vous devez d'abord installer l'interface de ligne de commande (CLI) et créer un compte. Pour obtenir la liste de toutes les commandes disponibles, consultez la [doccumentation Aerobic CLI](https://www.aerobatic.com/docs/cli/).

```bash
npm install aerobatic-cli -g
aero register
```

## Créer et Déployer un Site

```bash
hugo new site mon-nouveau-site-hugo
cd mon-nouveau-site-hugo
cd themes; git clone https://github.com/eliasson/liquorice
hugo -t liquorice
aero create                                           # create the Aerobatic site
hugo --baseURL https://my-new-hugo-site.aerobatic.io  # build the site overriding baseURL
aero deploy -d public                                 # deploy output to Aerobatic

Version v1 deployment complete.
View now at https://hugo-docs-test.aerobatic.io
```

In the rendered page response, the `https://__baseurl__` will be replaced with your actual site url (in this example, `https://my-new-hugo-site.aerobatic.io`). You can always rename your Aerobatic website with the `aero rename` command.

## Pousser le site Hugo sur Bitbucket

We will now create a git repository and then push our code to Bitbucket. In Bitbucket, create a repository.

![][1]

[1]: /images/hosting-and-deployment/hosting-on-bitbucket/bitbucket-create-repo.png


```bash
# initialize new git repository
git init

# set up our .gitignore file
echo -e "/public \n/themes \naero-deploy.tar.gz" >> .gitignore

# commit and push code to master branch
git add --all
git commit -m "Initial commit"
git remote add origin git@bitbucket.org:YourUsername/my-new-hugo-site.git
git push -u origin master
```

## Déploiement Continu avec les Pipelines Bitbucket

In the example above, we pushed the compiled assets in the `/public` folder to Aerobatic. In the following example, we use Bitbucket Pipelines to continuously create and deploy the compiled assets to Aerobatic.

### Étape 1 : Configurer les Pipelines Bitbucket 

In your Hugo website's Bitbucket repo;

1. Click the Pipelines link in the left nav menu of your Bitbucket repository.
2. Click the Enable Pipelines button.
3. On the next screen, leave the default template and click Next.
4. In the editor, paste in the yaml contents below and click Commit.

```bash
image: beevelop/nodejs-python
pipelines:
  branches:
    master:
      - step:
          script:
            - apt-get update -y && apt-get install wget
            - apt-get -y install git
            - wget https://github.com/gohugoio/hugo/releases/download/v0.18/hugo_0.18-64bit.deb
            - dpkg -i hugo*.deb
            - git clone https://github.com/eliasson/liquorice themes/liquorice
            - hugo --theme=liquorice --baseURL https://__baseurl__ --buildDrafts
            - npm install -g aerobatic-cli
            - aero deploy
```

### Étape 2 : Créer la variable d'environnement `AEROBATIC_API_KEY`

This step only needs to be done once per account. From the command line;

```bash
aero apikey
```

1. Navigate to the Bitbucket account settings for the account that the website repo belongs to.
2. Scroll down to the bottom of the left nav and click the Environment variables link in the PIPELINES section.
3. Create a new environment variable called AEROBATIC_API_KEY with the value you got by running the `aero apikey` command. Be sure to click the Secured checkbox.

### Étape 3 : Éditez et Committez le Code

```bash
hugo new post/good-to-great.md
hugo server --buildDrafts -t liquorice #Check that all looks good

# commit and push code to master branch
git add --all
git commit -m "New blog post"
git push -u origin master
```

Your code will be committed to Bitbucket, Bitbucket Pipelines will run your build, and a new version of your site will be deployed to Aerobatic.

At this point, you can now create and edit blog posts directly in the Bitbucket UI.

![][2]

[2]: /images/hosting-and-deployment/hosting-on-bitbucket/bitbucket-blog-post.png


## Prochaines étapes suggérées 

The code for this example can be found in this Bitbucket [repository](https://bitbucket.org/dundonian/hugo-docs-test). Aerobatic also provides a number of additional [plugins](https://www.aerobatic.com/docs) such as auth and redirects that you can use for your Hugo site.
