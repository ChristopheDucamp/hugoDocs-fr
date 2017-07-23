---
title: emojify
description: Lance une chaîne dans le processeur d'émoticônes Emoji.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-18
categories: [functions]
menu:
  docs:
    parent: "Fonctions"
#tags: [strings,emojis]
signature: ["emojify INPUT"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
---
`emoji` exécute une chaîne passée dans le processeur d'émoticônes Emoji.

Voir l'[anti-sèche Emoji][emojis] pour les émoticônes disponibles.

La fonction `emojify` peut être appelée dans vos modèles, mais pas directement dans vos fichiers de contenu par défaut. Pour les emojis dans les fichiers de contenu, réglez `enableEmoji` sur `true` dans la [configuration][config] de votre site. Ensuite, vous pouvez écrire directement sur vos fichiers de contenu ; par exemple <code>I :</code><code>heart</code><code>: Hugo !</code>  :

I :heart: Hugo !

 :fr:



[config]: /demarrage/configuration/
[emojis]: http://www.emoji-cheat-sheet.com/
[sc]: /templates/shortcode-templates/
[scsource]: https://github.com/gohugoio/hugo/tree/master/docs/layouts/shortcodes
