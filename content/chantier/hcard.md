---
title: Créer un Partiel h-card
linktitle: Poser une h-card
description: Penser à poser une h-card dans le footer.
date: 2017-07-21
publishdate: 2017-07-21
lastmod: 2017-07-21
categories: [indieweb]
#tags: [indieweb, h-card]
menu:
  docs:
    parent: "chantier"
    weight: 200
weight: 200
sections_weight: 200
draft: false
aliases: [hcard]
toc: true
wip: true
---

Inspiré par l'indieweb et le thème de Kevin Marks pour le blog de Christopher Allen (aka [@ChristopherA](https://github.com/ChristopherA), réfléchir à un partiel [h-card sur ce modèle](https://github.com/ChristopherA/LifeWithAlacrityBlog/blob/master/blog/layouts/partials/hcard.html)  

```html
<div class="h-card">
<h2><a class="u-url u-uid p-name" href="{{ .Site.Params.authorurl }}" >{{ .Site.Params.author }}</a></h2>
<img class="u-photo" src="{{ .Site.Params.authorphoto }}" />
<p class="abstract p-note p-summary">Principal Architect at Blockstream<br>Internet Cryptography Pioneer<br>Co-author TLS Security Standard<br>Collaborative Tools & Patterns<br>Decentralized Identity</p>
<ul>
<li><a rel="me" class="u-url" href="https://twitter.com/ChristopherA">@ChristopherA</a>
<li><a rel="me" class="u-url" href="https://github.com/ChristopherA">github</a>
<li><a rel="me" class="u-url" href="http://christophera.livejournal.com/">LiveJournal</a>
</ul>
</div>
```

Puis le déposer quelque part dans le footer.

