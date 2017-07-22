---
title: Résumés de Contenu
linktitle: Résumés
description: Hugo génère des résumés de votre contenu. 
date: 2017-01-10
publishdate: 2017-01-10
lastmod: 2017-07-21
categories: [gestion de contenu]
#tags: [résumés,abstracts,read more, en savoir plus]
menu:
  docs:
    parent: "gestion-contenu"
    weight: 90
weight: 90	#rem
draft: false
aliases: [/gestion-contenu/summaries, /content/summaries/,/content-management/content-summaries/]
toc: true
---

Avec l'usage de la [variable de page][pagevariables] `.Summary`, Hugo génère des résumés de contenu à utiliser comme version courte dans les vues résumées.

## Options de Fractionnement du Résumé

* Fractionnement de Résumé défini-par-Hugo
* Fractionnement de Résumé défini par l'utilisateur

Il est naturel d'accompagner le résumé avec des liens vers le contenu d'origine, et un modèle de conception commun est de voir ce lien sous la forme d'un bouton "Lire la suite ...". Voir les [variables de page][pages variables] `.RelPermalink`, `.Permalink` et `.Truncated`.

### Défini-par-Hugo : Le Fractionnement de Résumé Automatique

Par défaut, Hugo prend automatiquement les 70 premiers mots de votre contenu en tant que résumé et le stocke dans la variable de page `.Summary` à utiliser dans vos modèles. Prendre l'approche définie par Hugo pour les résumés peut faire gagner du temps, mais il y a des avantages et des inconvénients :

* **Avantages :** Automatique, aucun travail supplémentaire à faire de votre côté.
* **Inconvénients :** Tous les tags HTML sont retirés du résumé, et les 70 premiers mots, qu'ils appartiennent à un titre ou à des paragraphes différents, sont tous mis en un seul paragraphe.

{{% note %}}
Les résumés définis par Hugo sont configurés pour utiliser le nombre de mots calculé en divisant le texte par un ou plusieurs caractères blancs consécutifs. Si vous créez du contenu dans un langage `CJK` et que vous souhaitez utiliser le fractionnement automatique de résumé de Hugo, configurez `hasCJKLanguage` sur  `true` dans votre [configuration de site][config].
{{% /note %}}

### Défini-par-l'utilisateur : Fractionnement de Résumé Manuel

Sinon, vous pouvez ajouter le diviseur de résumé <code>&#60;&#33;&#45;&#45;more&#45;&#45;&#62;</code> où vous souhaitez diviser l'article. Pour l'[organisation de contenu][org], utilisez `# more` à l'endroit où vous voulez diviser l'article. Le contenu qui vient avant le diviseur de résumé sera utilisé comme résumé de ce contenu et stocké dans la variable de page `.Summary` avec toute la mise en forme HTML intacte.

{{% note "Diviseur de résumé" %}}
Le concept d'un *diviseur de résumé* n'est pas unique à Hugo. Elle est aussi également appelée "more tag" ou "excerpt separator" (séparateur d'extraits) dans d'autres publications.
{{% /note %}}

* Avantages : Liberté, précision, et rendu amélioré. Toutes les balises HTML et la mise en page sont préservées.
* Inconvénients : Travail en plus pour les auteurs de contenu, parce qu'ils ont beson de taper <code>&#60;&#33;&#45;&#45;more&#45;&#45;&#62;</code> (ou `# more` pour l'[organisation de contentu][org]) dans chaque fichier de contenu. Cela peut s'automatiser en ajoutant le diviseur de résumé en dessous du front matter d'un [archetype](/content-management/archetypes/).

{{% warning "Soyez Précis avec le Diviseur de Résumé" %}}
Prenez soin de saisir exactement <code>&#60;&#33;&#45;&#45;more&#45;&#45;&#62;</code> ; c'est à dire, tout en bas de casse et sans espace blanc.
{{% /warning %}}

## Exemple : Les 10 Premiers Articles avec Résumés

Vous pouvez afficher les résumés de contenu avec le code suivant. Vous pouvez utiliser l'extrait suivant, par exemple, dans un [modèle de section][section template].

{{% code file="page-list-with-summaries.html" %}}
```html
{{ range first 10 .Data.Pages }}
    <article>
      <!-- this <div> includes the title summary -->
      <div>
        <h2><a href="{{ .RelPermalink }}">{{ .Title }}</a></h2>
        {{ .Summary }}
      </div>
      {{ if .Truncated }}
      <!-- This <div> includes a read more link, but only if the summary is truncated... -->
      <div>
        <a href="{{ .RelPermalink }}">Lire la suite…</a>
      </div>
      {{ end }}
    </article>
{{ end }}
```
{{% /code %}}

Notez comment la valeur booléenne `.Truncated` peut être utilisée pour cacher le lien "Lire la suite..." lorsque le contenu n'est pas tronqué ; c'est-à-dire lorsque le résumé contient l'article entier.

[config]: /demarrage/configuration/
[org]: /gestion-contenu/formats/
[pages variables]: /variables/page/
[section template]: /templates/section-templates/