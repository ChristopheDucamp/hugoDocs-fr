---
title: Commentaires
linktitle: Commentaires
description: Hugo est livré avec un module interne Disqus, mais ce n'est pas le seul système de commentaire qui fonctionnera avec votre nouveau site web Hugo.
date: 2017-02-01
publishdate: 2017-02-22
lastmod: 2017-07-23
#tags: [sections,contenu,organisation]
categories: [organisation de projet, fondamentaux, fundamentals]
menu:
  docs:
    parent: "Gestion de Contenu"
    weight: 140
weight: 140	#rem
draft: false
aliases: [/gestion-contenu/comments,/extras/comments/]
toc: true
---

Hugo est livré avec le support pour [Disqus](https://disqus.com/), un service tiers qui fournit des fonctionnalités de commentaires et de communauté aux sites via JavaScript.

Votre thème peut déjà supporter Disqus, mais sinon, il est facile de l'ajouter à vos modèles via le [partiel Disqus intégré dans Hugo][disquspartial].

## Ajouter Disqus

Hugo est livré avec tout le code dont vous avez besoin pour charger Disqus dans vos modèles. Avant d'ajouter Disqus à votre site, vous devrez [configurer un compte][disqussetup].

### Configurer Disqus

Les commentaires de Disqus exigent que vous définissiez une seule valeur dans le [fichier de configuration de votre site][configuration]. Les éléments suivants montrent la variable de configuration dans un `config.toml` et` config.yml`, respectivement :

```toml
disqusShortname = "votrepseudodisqus"
```

```yaml
disqusShortname: "votrepseudodisqus"
```

Pour de nombreux sites Web, il s'agit d'une configuration suffisante. Cependant, vous avez également la possibilité de définir ce qui suit dans le [front matter][] d'un fichier unique de contenu :

* `disqus_identifier`
* `disqus_title`
* `disqus_url`

### Produire le Modèle de Partiel Disqus Intégré dans Hugo

Voir [Modèles de Partiel][partials] pour apprendre comment ajouter un partiel Disqus à vos modèles de site web Hugo.

## Alternatives pour les Commentaires

Il existe quelques alternatives pour commenter sur des sites statiques pour ceux qui ne veulent pas utiliser Disqus :

* [Static Man](https://staticman.net/)
* [txtpen](https://txtpen.com)
* [IntenseDebate](http://intensedebate.com/)
* [Graph Comment][]
* [Muut](http://muut.com/)
* [isso](http://posativ.org/isso/) (Auto-hébergé, Python)
    * [Tutoriel pour implémenter Isso avec Hugo][issotutorial]


<!-- I don't think this is worth including in the documentation since it seems that Steve is no longer supporting or developing this project. rdwatters - 2017-02-29.-->
<!-- * [Kaiju](https://github.com/spf13/kaiju) -->

<!-- ## Kaiju

[Kaiju](https://github.com/spf13/kaiju) is an open-source project started by [spf13](http://spf13.com/) (Hugo’s author) to bring easy and fast real time discussions to the web.

Written using Go, Socket.io, and [MongoDB][], Kaiju is very fast and easy to deploy.

It is in early development but shows promise. If you have interest, please help by contributing via pull request, [opening an issue in the Kaiju GitHub repository][kaijuissue], or [Tweeting about it][tweet]. Every bit helps. -->

[configuration]: /demarrage/configuration/
[disquspartial]: /templates/partials/#disqus
[disqussetup]: https://disqus.com/profile/signup/
[forum]: https://discourse.gohugo.io
[front matter]: /gestion-contenu/front-matter/
[Graph Comment]: https://graphcomment.com/
[kaijuissue]: https://github.com/spf13/kaiju/issues/new
[issotutorial]: https://stiobhart.net/2017-02-24-isso-comments/
[partials]: /templates/partials/
[MongoDB]: https://www.mongodb.com/
[tweet]: https://twitter.com/spf13
