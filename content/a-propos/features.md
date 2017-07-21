---
title: Les Fonctionnalités Hugo
linktitle: Les Fonctionnalités Hugo
description: Hugo bénéficie d'une vitesse hallucinante, d'une gestion de contenu robuste et d'un langage de mise en page puissant, ce qui en fait un excellent outil pour toutes sortes de sites Web statiques.

date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
menu:
  docs:
    parent: "about"
    weight: 20
weight: 20
sections_weight: 20
draft: false
aliases: [/about/features]
toc: true
---

## Général

* Temps de construction [extrêmement rapides][Extremely fast] (&lt; 1 ms par page)
* Complètement inter-plates-formes, avec [installation facile][install] sur macOS, Linux, Windows, et plus encore
* Rendus des modifications à la volée avec  [LiveReload][] pendant que vous développez
* [Générateur de thèmes puissant][Powerful theming]
* [Hébergement de votre site où vous voulez][hostanywhere]

## Organisation
* [Organisation immédiate pour vos projets][organization for your projects], y compris les sections du site Web
* [URLs][] personnalisables 
* Prise en charge de [taxonomies][] configurables, y compris les catégories et les balises
* [Tri du contenu][Sort content] comme vous le désirez à l'aide de [fonctions][functions] puissantes de modélisation 
* Génération automatique [table des matières][table of contents]
* Création de [menus dynamiques][Dynamic menu]
* Support des [Pretty URLs][]
* Suppor du modèle de [Lien permanent][Permalink]
* Redirection via [aliases][]
 

## Contenu

* Support natif du Markdown et Emacs Org-Mode, tout comme d'autres langages via des *external helpers* (voir [formats supportés][supported formats])
* Support métadonnées TOML, YAML, et JSON dans le [front matter][]
* [Page d'accueil][homepage] personnalisable
* Plusieurs [types de contenu][content types]
* [Résumés de contenu][content summaries] automatiques et définies par l'utilisateur
* [raccourcis-code][Shortcodes] pour activer le contenu riche dans le Markdown
* Fonctionnalité ["Minutes to Read"][pagevars]
* Fonctionnalité ["Wordcount"][pagevars]

## Fonctionnalités supplémentaires

* Support intégré de commentaires [Disqus][] 
* Support intégré de [Google Analytics][] 
* Création automatique de [RSS][] 
* Support pour les modèles HTML [Go][], [Amber], et [Ace][] 
* [Enlumineur de syntaxe][Syntax highlighting] motorisé par [Pygments][]

Regardez ce qui arrive bientôt dans la [roadmap Hugo][].

[Ace]: /templates/alternatives/
[aliases]: /gestion-contenu/urls/#aliases
[Amber]: https://github.com/eknkc/amber
[content summaries]: /gestion-contenu/summaries/
[content types]: /gestion-contenu/types/
[Disqus]: https://disqus.com/
[Dynamic menu]: /templates/menu-templates/
[Extremely fast]: https://github.com/bep/hugo-benchmark
[front matter]: /gestion-contenu/front-matter/
[functions]: /fonctions/
[Go]: http://golang.org/pkg/html/template/
[Google Analytics]: https://google-analytics.com/
[homepage]: /templates/homepage/
[hostanywhere]: /hebergement-et-deploiement/
[Hugo roadmap]: /a-propos/roadmap
[install]: /demarrage/installer/
[LiveReload]: /demarrage/usage/
[organization for your projects]: /demarrage/structure-dossier/
[pagevars]: /variables/page/
[Permalink]: /gestion-contenu/urls/#permalinks
[Powerful theming]: /themes/
[Pretty URLs]: /gestion-contenu/urls/
[Pygments]: http://pygments.org/
[RSS]: /templates/rss/
[Shortcodes]: /gestion-contenu/shortcodes/
[sort content]: /templates/
[supported formats]: /gestion-contenu/formats/
[Syntax highlighting]: /outils/syntax-highlighting/
[table of contents]: /gestion-contenu/toc/
[taxonomies]: /gestion-contenu/taxonomies/
[URLs]: /gestion-contenu/urls/
