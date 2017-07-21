---
title: Firebase
linktitle: Héberger sur Firebase
description: Vous pouvez utiliser l'outil de Firebase pour héberger votre site web statique ; ceci vous donne aussi accès à l'API NOSQL de Firebase.
date: 2017-03-12
publishdate: 2017-03-12
lastmod: 2017-03-21
categories: [hébergement et déploiement]
#tags: [hébergement,firebase]
authors: [Michel Racic]
menu:
  docs:
    parent: "hebergement-et-deploiement"
    weight: 20
weight: 20
sections_weight: 20
draft: false
toc: true
aliases: [/hebergement-et-deploiement/hosting-on-firebase/]
---

## Hypothèses

1. Vous avez un compte [Firebase](https://console.firebase.google.com/). (Si vous ne le faites pas, vous pouvez vous inscrire gratuitement à l'aide de votre compte Google.)
2. Vous avez terminé le [Démarrage rapide](/demarrage/quickstart/) ou avez-vous un site web complet Hugo prêt pour le déploiement.

## Paramétrage initial

Allez sur la [console Firebase][console] et créez un nouveau projet (à moins que vous n'ayez déjà un projet). 

Vous devrez aussi installer `firebase-tools` (node.js) sur votre machine à partir de votre fenêtre de terminal, lancez la commande :

```sh
npm install -g firebase-tools
```

Connectez-vous à Firebase (réglages sur votre machine locale) en utilisant `firebase login`,qui ouvre un navigateur où vous sélectionnerez votre compte. Utilisez `firebase logout` si vous êtes déjà connecté mais avec le mauvais compte.


```sh
firebase login
```
À la racine de votre projet Hugo, initialisez le projet Firebase avec la commande `firebase init` :

```sh
firebase init
```

À partir d'ici, sélectionnez les fonctionnalités 

1. Choissez "Hosting" dans la question feature
2. Choisissez le projet que vous venez d'installer
3. Accepter la réponse par défaut pour vos "database rules file"
4. Accepter la réponse pour le dossier publication qui est `public`
5. Choisissez "No" à la question si vous déployer une app page-unique

## Déployez

Pour déployer votre site Hugo, exécutez la commande `firebase deploy`, et votre site sera live en peu de temps :

```sh
hugo && firebase deploy
```

## Paramétrages CI 

Vous pouvez générer un token de déploiement en utilisant 


```sh
firebase login:ci
```

Vous pouvez aussi paramétrer votre CI (par ex., avec [Wercker][]) et ajouter le token vers une variable privée comme  `$FIREBASE_DEPLOY_TOKEN`.

{{% notice warning %}}
Ceci est le seccret privé et ça ne devrait pas apparaître dans un repository public. Assurez)vous de bien comprendre votre CI choisi et qu'il ne soit pas visible pour les autres.
{{% /notice %}}

Vous pouvez alors ajouter une étape dans votre build pour faire le déploiemnet en utilisant le token : 

```sh
firebase deploy --token $FIREBASE_DEPLOY_TOKEN
```

## Liens de référene

* [Firebase CLI Reference](https://firebase.google.com/docs/cli/#administrative_commands)
[console]: https://console.firebase.google.com
[Quick Start]: /demarrage/quickstart/
[Wercker]: /hebergement-et-deploiement/deployment-with-wercker/

## Test 

* <https://dochugo-edf58.firebaseapp.com/hebergement-et-deploiement/> (2017-07-21)
