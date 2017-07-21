---
title: GitLab
linktitle: Héberger sur GitLab
description: GitLab fait qu'il est incroyablement facile de construire, déployer et héberger votre site web Hugo vis son service gratuit GitLab Pages, qui fournit un support natif pour Hugo.
date: 2016-06-23
publishdate: 2016-07-21
lastmod: 2016-06-23
categories: [hosting and deployment, hébergement et déploiement]
#tags: [hosting,deployment,git,gitlab]
authors: [Riku-Pekka Silvola]
menu:
  docs:
    parent: "hebergement-et-deploiement"
    weight: 40
weight: 40
sections_weight: 40
draft: false
toc: true
wip: false
aliases: [/tutorials/hosting-on-gitlab/,/hebergement-et-deploiement/hosting-on-gitlab]
---

[GitLab](https://gitlab.com/) rend incroyablement facile la construction, le déploiement et l'hébergement de votre site web Hugo via son service gratuit GitLab Pages, qui fournit un [support natif pour Hugo, ainsi que de nombreux autres générateurs de sites statiques ](https://gitlab.com/pages/hugo).

## Hypothèses

* Connaissance de travail avec Git pour le contrôle de version
* Achèvement du tutoriel Hugo [QuickStart](/demarrage/quickstart/)
* Un [compte GitLab](https://gitlab.com/users/sign_in)
* Un site Web Hugo sur votre machine locale que vous êtes prêt à publier

## Créer .gitlab-ci.yml

```bash
cd votre-site-hugo
```

À la racine du répertoire de votre site Hugo, créez un fichier  `.gitlab-ci.yml`. Le fichier `.gitlab-ci.yml` configure le CI GitLab sur la façon de construire votre page. Ajoutez-y simplement le contenu en-dessous.

{{% code file="gitlab-ci.yml" %}}
```yml
image: publysher/hugo

pages:
  script:
  - hugo
  artifacts:
    paths:
    - public
  only:
  - master
```
{{% /code %}}

## Pousser votre Site Web Hugo vers GitLab

Puis, créez un nouveau repo sur GitLab. Il n'est *pas* nécessaire de rendre le repo public. En outre, vous pourriez vouloir ajouter `/public` à votre fichier .gitignore, car il n'y a pas besoin de poussser les assets compilés vers GitLab ou de conserver votre output de site web sous contrôle de version.

```bash
# initialiser nouveau repository git
git init

# ajout dossier /public a notre ficier .gitignore
echo "/public" >> .gitignore

# committer et pousser le code sur la branche master
git add .
git commit -m "Premier commit"
git remote add origin https://gitlab.com/VotreNomUtilisateur/votre-site-hugo.git
git push -u origin master
```


## Attendre que votre page se Construise

C'est tout ! Vous pouvez désormais suivre l'agent CI construire votre page sur https://gitlab.com/<VotreNomUtilisateur>/<votre-site-hugo>/pipelines.

After the build has passed, your new website is available at `https://<YourUsername>.gitlab.io/<your-hugo-site>/`.

## Prochaines étapes

GitLab supporte l'utilisation de CNAME's et des certificats TLS personnalisés. Pour plus de détails sur GitLab Pages, regardez la [documentation de réglages GitLab Pages](https://about.gitlab.com/2016/04/07/gitlab-pages-setup/).

