+++
title = "Thème DocDock pour Hugo"
description = ""
date = "2017-06-30T10:21:43+02:00"

+++

# Thème docDock pour Hugo

[Hugo-theme-docdock](https://github.com/vjeantet/hugo-theme-docdock) est un thème pour Hugo, un moteur de site web rapide et moderne écrit en Go. Hugo est souvent utilisé pour les blogs, mais ce thème a été **entièrement conçu pour la documentation**.

Ce thème est une adaptation partielle du [thème Learn de matcornic](https://github.com/matcornic/hugo-theme-learn).

{{%panel%}}docDock fonctionne avec une "structure de page en arbre" pour organiser le contenu : Tous les contenus sont des pages, qui appartiennent à d'autres pages. 
[Cliquez ici pour en savoir plus sur l'organisation du contenu de docDock.]({{%relref "content-organisation/_index.md"%}}) {{%/panel%}}


## Principales Fonctionnalités

* [Recherche]({{%relref "search/_index.md" %}})
* **Pas de limites pour les niveaux de menu**
* [Génération de présentations slides RevealJS]({{%relref "page-slide.md"%}}) à partir du markdown (page embarquée ou plein-écran)
* Boutons suivant/précédent automatiques pour naviguer dans les entrées de menu
* [Retaillage d'images, ombre...]({{%relref "shortcodes/image.md" %}})
* [Fichiers attachés]({{%relref "shortcodes/attachments.md" %}})
* [Liste de pages enfants]({{%relref "shortcodes/children/_index.md" %}})
* [Extraction]({{%relref "shortcodes/excerpt.md"%}}) ! Inclusion de segment de contenu d'une page dans une autre
* [Diagramme Mermaid]({{%relref "shortcodes/mermaid.md" %}}) (flowchart, sequence, gantt)
* [Icônes]({{%relref "shortcodes/icon.md" %}}), [Boutons]({{%relref "shortcodes/button.md" %}}), [Alertes]({{%relref "shortcodes/alert.md" %}}), [Panels]({{%relref "shortcodes/panel.md" %}}), [Truc/Note/Info/Warning boxes]({{%relref "shortcodes/notice.md" %}}), [Expansion]({{%relref "shortcodes/expand.md" %}})
* [Look and feel personnalisable]({{%relref "content-organisation/customize-style/_index.md"%}}), [variantes de thèmes]({{%relref "content-organisation/customize-style/theme-variants.md"%}})




![](https://raw.githubusercontent.com/vjeantet/hugo-theme-docdock/master/images/tn.png?width=33pc&classes=border,shadow)

## Contribuez à cette documentation
Aidez à mettre à jour ce contenu, cliquez simplement sur le lien  **Modifier cette page** affiché en haut et à droite de chaque page, et envoyez une pull-request 
{{%alert%}}Votre modification sera déployée automatiquemnet une fois fusionnée.{{%/alert%}}


## Documentation
Cette documentation a été générée statiquement avec Hugo à l'aide d'une simple : `hugo -t docdock` -- le code source est  [disponible ici sur GitHub {{%icon fa-github%}}](https://github.com/vjeantet/hugo-theme-docDock)

{{% panel theme="success" header="Déploiements Automatiques" footer="Netlify construit, déploie, et héberge les  frontends." %}}
Publié automatiquement et hébergé chez [Netlify](https://www.netlify.com/).

Pour en savoir plus sur les [déploiements automatisés d'HUGO avec Netlify](https://www.netlify.com/blog/2015/07/30/hosting-hugo-on-netlifyinsanely-fast-deploys/)
{{% /panel %}}



