---
title: Netlify
linktitle: Héberger chez Netlify
description: Netlify peut héberger votre site Hugo avec CDN, déploiement continu, HTTPS-en-1-clic, une GUI d'admin et sa propre CLI.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
categories: [hébergement et déploiement]
#tags: [netlify,hébergement, déploiement]
authors: [Ryan Watters, Seth MacLeod, Christophe Ducamp]
menu:
  docs:
    parent: "hebergement-et-deploiement"
    weight: 10
weight: 10
sections_weight: 10
draft: false
aliases: [/hebergement-et-deploiement/hosting-on-netlify/]
toc: true
---

[Netlify][netlify] fournit des services de déploiement continu, un CDN global, un DNS ultra-rapide, des déploiements atomiques, une invalidation de cache instantané, un SSL en un clic, une interface basée dans le navigateur, une CLI et de nombreuses autres fonctionnalités pour la gestion de votre site web Hugo.

## Hypothèses

* Vous avez un compte chez GitHub, GitLab, ou Bitbucket.
* Vous avez terminé le [Quick Start][] ou vous avez un site web Hugo que vous êtes prêt à déployer et partager avec le monde.
* Vous n'avez pas encore de compte Netlify.

## Créez un compte Netlify

Allez sur [app.netlify.com][] et sélectionnez votre méthode d'inscription préférée. Ce sera probablement un fournisseur Git hébergé, bien que vous ayez également la possibilité de vous inscrire avec une adresse e-mail.

Les exemples suivants utilisent GitHub, mais d'autres fournisseurs de GIT suivront un processus similaire.

![Capture-écran de la page d'accueil pour app.netlify.com, contenant les liens vers les emplacements de solutions git les plus populaires.](/images/hosting-and-deployment/hosting-on-netlify/netlify-signup.jpg)

La sélection de GitHub permet d'afficher un mode d'utilisation typique à travers une autre application qui utilise GitHub pour l'authentification. Sélectionnez "Autorize application".

![Capture-écran du popup d'autorisation pour Netlify et GitHub.](/images/hosting-and-deployment/hosting-on-netlify/netlify-first-authorize.jpg)

## Créez un Nouveau Site avec Déploiement Continu

Vous êtes maintenant membre de Netlify et vous devriez vous retrouver dans votre nouveau tableau de bord. Sélectionnez "Nouveau site à partir de git" (NDT "New site from git").

![Capture-écran du tableau de boc d'admin de Netlify sans sites et un bouton 'add new site'](/images/hosting-and-deployment/hosting-on-netlify/netlify-add-new-site.jpg)

Netlify commencera à marcher pour suivre les étapes nécessaires au déploiement continu. Tout d'abord, vous devrez sélectionner à nouveau votre fournisseur de git, mais cette fois, vous donnez à Netlify des autorisations supplémentaires pour accéder à vos dépôts.

![Capture écran de l'étape 1 de création d'un nouveau site sur  Netlify : sélectionner le fournisseur git](/images/hosting-and-deployment/hosting-on-netlify/netlify-create-new-site-step-1.jpg)

Et de nouveau avec le modèle d'autorisation GitHub :

![Capture écran de l'étape 1 de pour créer un nouveau site sur Netlify : sélection du fournisseur git](/images/hosting-and-deployment/hosting-on-netlify/netlify-authorize-added-permissions.jpg)

Sélectionnez le repo que vous voulez utiliser pour un déploiement continu. Si vous avez un grand nombre de dépôts, vous pouvez le filtrer en utilisant la recherche de repo en temps réel : 

![Screenshot of step 1 of create a new site for Netlify: selecting the git provider](/images/hosting-and-deployment/hosting-on-netlify/netlify-create-new-site-step-2.jpg)

Une fois sélectionné, vous serez amené à un écran pour une installation basique. De là, vous pouvez sélectionner la branche que vous voulez publier, votre [comment build][build command], et votre répertoire de publication (c'est-à-dire celui du déploiement). Le répertoire de publication devrait correspondre à celui que vous avez réglé dans votre [configuration de site][config], la valeur par défaut de celui-ci étant `public`. Les étapes suivantes supposent que vous publiez à partir de la branche `master`.

### Construire avec une Version Hugo Spécifique

Le réglage de la commande build sur `hugo` construira votre site selon la version de Hugo utilisée par défaut par Netlify. Vous pouvez voir la liste complète des [version Hugo disponibles dans le fichier Docker de Netlify][hugoversions].

Si vous voulez préciser à Netlify de construire avec une version spécifique, vous pouvez ajouter un trait souligné suivi du numéro de version à la commande build : 

```bash
hugo_0.19
```

Votre configuration simple devrait maintenant ressembler à ce qui suit :

![Capture écran de l'étape 3, installation d'un déploiement continu basique avec un nouveau site Hugo sur Netlify](/images/hosting-and-deployment/hosting-on-netlify/netlify-create-new-site-step-3.jpg)

Sélectionnez "Deploy site" vous emmènera directement vers un terminal pour votre construction : 

![gif animé du déploiement d'un site sur Netlify, comprendant la lecture du terminal pour le build.](/images/hosting-and-deployment/hosting-on-netlify/netlify-deploying-site.gif)

Une fois la construction terminée --- cela ne devrait prendre que quelques secondes - vous devriez maintenant voir une "Carte Hero" en haut de votre écran pour vous informer que le déploiement a réussi. La Carte Hero est le premier élément que vous voyez dans la plupart des pages. Elle vous permet de voir un résumé rapide de la page et donne accès aux actions et aux informations les plus courantes/pertinentes. Vous verrez que l'URL est automatiquement générée par Netlify. Vous pouvez mettre à jour l'URL dans "Settings".

![Capture-écran d'un badge de déploiement réussi en haut de l'écran deployments à partir de l'admin Netlify.](/images/hosting-and-deployment/hosting-on-netlify/netlify-deploy-published.jpg)

![Capture-écran de la page d'accueil de https://hugo-netlify-example.netlify.com, qui est essentiellemnet du faux texte](/images/hosting-and-deployment/hosting-on-netlify/netlify-live-site.jpg)

[Visitez le site en live][visit].

Maintenant à chaque fois que vous pousserez des modifications sur votre repo git hébergé, Netlify reconstruira et re-déploira votre site.

{{% note %}}

Si votre build venait à échouer, vous pouvez aussi accéder à la section avancée "Advanced build settings" et renseigner respectivement les "Key" et "Value" à `HUGO_VERSION`et `0.25`.


![capture-écran dess réglages de déploiement avancés pour spécifier une version Hugo](/images/hosting-and-deployment/hosting-on-netlify/netlify-deploying-hugo-0.25.png)

{{%/note%}}


## Utilisez les Thèmes Hugo avec Netlify

La commande [`git clone` pour installer les thèmes][installthemes] n'est pas supportée par Netlify. Si vous deviez utiliser `git clone`, il faudrait que vous supprimiez récursivement le sous-répertoire `.git` du dossier de thème ce qui empêche donc la compatibilité avec les versions futures du thème.

Une *meilleure* approche consiste à installer un thème comme un sous-module Git approprié. Pour plus d'informations, vous pouvez  [lire la documentation GitHub pour les sous-modules][ghsm] ou celle sur [le site web de Git][gitsm], mais la commande est similaire à celle de `git clone` : 

```bash
cd themes
git submodule add https://github.com/<CREATEURTHEME>/<NOMTHEME>
```

## Prochaines étapes

Vous avez maintenant un site web en live servi avec https, distribué à travers un CDN et configuré pour un déploiement continu. Plongez plus à fond dans la documentation de Netlify documentation :

1. [Utiliser un Nom de Domaine Personnalisé][]
2. [Régler le HTTPS sur les Domaines Personnalisés][httpscustom]
3. [Règles de Redirection et Rewrite][]


[app.netlify.com]: https://app.netlify.com
[build command]: /getting-started/usage/#the-hugo-command
[config]: /demarrage/configuration/
[ghsm]: https://github.com/blog/2104-working-with-submodules
[gitsm]: https://git-scm.com/book/en/v2/Git-Tools-Submodules
[httpscustom]: https://www.netlify.com/docs/ssl/
[hugoversions]: https://github.com/netlify/build-image/blob/master/Dockerfile#L166
[installthemes]: /themes/installing/
[netlify]: https://www.netlify.com/
[netlifysignup]: https://app.netlify.com/signup
[Quick Start]: /demarrage/quickstart/
[Règles de Redirection et Rewrite]: https://www.netlify.com/docs/redirects/
[Utiliser un Nom de Domaine Personnalisé]: https://www.netlify.com/docs/custom-domains/
[visit]: https://hugo-netlify-example.netlify.com
