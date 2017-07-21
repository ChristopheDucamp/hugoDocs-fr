---
title: Formats de Sortie Personnalisés
linktitle: Formats Output Personnalisés
description: Hugo peut afficher du contenu dans plusieurs formats, y compris les événements de calendrier, les formats de livre électronique, Google AMP et les index de recherche JSON, ou tout format de texte personnalisé.
date: 2017-03-22
publishdate: 2017-03-22
lastmod: 2017-07-20
categories: [templates, modèles]
#tags: ["amp","outputs","rss"]
menu:
  docs:
    parent: "templates"
    weight: 18
weight: 18
sections_weight: 18
draft: false
aliases: [/templates/outputs/,/templates/output-formats/,/content-management/custom-outputs/]
toc: true
---

Cette page décrit comment configurer correctement votre site avec les types de médias et les formats de sortie, ainsi que l'endroit où créer vos modèles pour vos sorties personnalisées.


## Types de Média

Un [media type][] (aussi connu comme le *MIME type* et le  *content type*) est un identifiant en deux-parties pour les formats de fichier et les formats de contenus transmis sur internet.

Il s'agit de l'ensemble complet des types de médias intégrés dans Hugo :

{{< datatable "media" "types" "Type" "Suffix" >}}

**Note:**

* Il est possible d'ajouter des types de media personnalisés ou de changer les valeurs par défaut ; par ex., si vous voulez modifier le suffixe pour `text/html` en `asp`.
* Le `Suffix` est la valeur qui sera utilisée pour les URLs et noms de fichiers pour ce type de média dans Hugo.
* Le `Type` est l'identifiant qui doit être utilisé au moment de définir de nouveau/personnaliser les `Output Formats` (voir en-dessous).
* L'ensemble complet des types de media sera enregistré dans un serveur de développement intégré dans Hugo pour s'assurer qu'ils sont reconnus par le navigateur.

Pour ajouter ou modifier un type de média, définissez-le dans une section `mediaTypes` à l'intérieur de votre [configuration de site][config], soit pour tous les sites ou pour un langage donné.

Exemple dans `config.toml` :

```toml
[mediaTypes]
  [mediaTypes."text/enriched"]
  suffix = "enr"
  [mediaTypes."text/html"]
  suffix = "asp"
```

L'exemple ci-dessus ajoute un nouveau media type, `text/enriched`, et change le suffixe pour le media type `text/html` intégré.

## Formats de Sortie

Compte tenu d'un type de média et d'une configuration supplémentaire, vous obtenez un `Output Format` (« Format de sortie ») :

Voici l'ensemble complet des formats de sortie intégrés dans Hugo :

{{< datatable "output" "formats" "Name" "MediaType" "Path" "BaseName" "Rel" "Protocol" "IsPlainText" "IsHTML" "NoUgly">}}

* Une page peut être sortie dans autant de formats de sortie que vous voulez, et vous pouvez avoir une quantité infinie de formats de sortie définis **aussi longtemps qu'ils résolvent un chemin unique sur le système de fichiers**. Dans le tableau ci-dessus, le meilleur exemple est `AMP` vs `HTML`. `AMP` a la valeur `amp` pour `Path` afin qu'il n'écrase pas la version `HTML` ; par exemple, nous pouvons maintenant avoir à la fois `/index.html` et `/amp/index.html`.
* Le `MediaType` doit correspondre au `Type` d'un type de média déjà défini.
* Vous pouvez définir de nouveaux formats de sortie ou redéfinir les formats de sortie intégrés ; par exemple, si vous souhaitez placer les pages `AMP` dans un chemin différent.

Pour ajouter ou modifier un format de sortie, définissez-le dans une section `outputFormats` dans le [fichier de configuration](/templates/configuration), soit pour tous les sites, soit pour un langage donné.

```toml
[outputFormats.MyEnrichedFormat]
mediaType = "text/enriched"
baseName = "myindex"
isPlainText = true
protocol = "bep://"
```

L'exemple ci-dessus est fictif, mais s'il est utilisé pour la page d'accueil sur un site avec `baseURL` `http://exemple.org`, il produira une page d'accueil en texte brut avec l'URL `bep://exemple.org/myindex.enr`.

### Configurer des Formats de Sortie

Voici la liste complète des options de configuration pour les formats de sortie et leurs valeurs par défaut :

`Name`
: l'ouput de l'identifiant du format. Ceci est utilisé pour définir quel(s) format(s) d'output vous volez pour vos pages.

`MediaType`
: ceci doit correspondre au `Type` d'un media type défini.

`Path`
: sous-chemin pour sauvegarder les fichiers output.

`BaseName`
: le nom de fichier de la base pour les noms de fichiers de la liste (homepage, etc.). **Par défaut:** `index`.

`Rel`
: peut être utilisé pour créer des valeurs `rel` dans les tags  `link`. **Par défaut :** `alternate`.

`Protocol`
: remplacera le "http://" ou "https://" dans votre `baseURL` pour ce format d'output.

`IsPlainText`
: use Go's plain text templates parser for the templates. **Default:** `false`.

`IsHTML`
: used in situations only relevant for `HTML`-type formats; e.g., page aliases.

`NoUgly`
: used to turn off ugly URLs If `uglyURLs` is set to `true` in your site. **Default:** `false`.

`NotAlternative`
: enable if it doesn't make sense to include this format in an `AlternativeOutputFormats` format listing on `Page` (e.g., with `CSS`). Note that we use the term *alternative* and not *alternate* here, as it does not necessarily replace the other format. **Default:** `false`.

## Formats de Sortie pour les Pages

Une `Page` dans Hugo peut être rendue vers plusieurs représentations sur le système de fichiers. Par défaut, toutes les pages se traduiront en `HTML` avec certaines d'entre elles également en tant que `RSS` (page d'accueil, sections, etc.).

Cela peut être modifié en définissant une liste `outputs` des formats de sortie soit dans le front matter de la `Page` ou dans la configuration du site (pour tous les sites ou par langage).

Exemple du site `config.toml` :

```toml
[outputs]
  home = ["HTML", "AMP", "RSS"]
  page = ["HTML"]
```

Exemple du site `config.yml` :

```yml
outputs:
  home: ["HTML", "AMP", "RSS"]
  page: ["HTML"]
```


* La définition de sortie se fait par  `Page` `Kind` (par ex., `page`, `home`, `section`, `taxonomy`, ou `taxonomyTerm`).
* Les noms utilisés doivent correspondre au `Name` d'un `Output Format` défini.
* Tout `Kind` sans une définition aura la valeur par défaut  `HTML`.
* Ceci peut être annulé par `Page` dans le front matter des fichiers de contenu.
* Les formats output sont insensibles à la casse.

Voici un exemple de front matter `YAML` dans un fichier de contenu qui définit les formats de sortie pour la `Page` rendue :

```yaml
---
date: "2016-03-19"
outputs:
- html
- amp
- json
---
```

## Lien vers les Formats de Sortie

Chaque `Page` a à la fois un `.OutputFormats` (tous les formats, y compris celui en cours) et une variable `.AlternativeOutputFormats`, la dernière étant utile pour créer une liste `link rel` dans le `<head>` de votre site :

```
{{ range .AlternativeOutputFormats -}}
<link rel="{{ .Rel }}" type="{{ .MediaType.Type }}" href="{{ .Permalink | safeURL }}">
{{ end -}}
```

Notez que `.Permalink` et `.RelPermalink` sur `Page` renverront le premier format de sortie défini pour cette page (généralement `HTML` si rien d'autre n'est défini).

Voici comment vous liez vers un format de sortie donné : 

```
{{ with  .OutputFormats.Get "json" -}}
<a href="{{ .Permalink }}">{{ .Name }}</a>
{{- end }}
```

À partir des fichiers de contenu, vous pouvez utiliser les codes courts [`ref` ou `relref`](/content-management/shortcodes/#ref-and-relref) :

```
[Neat]({{</* ref "blog/neat.md" "amp" */>}})
[Who]({{</* relref "about.md#who" "amp" */>}})
```

## Modèles pour vos Formats de Sortie

Un nouveau format de sortie nécessite un modèle correspondant afin de rendre tout utile.

{{% note %}}
La distinction clé pour les versions Hugo 0.20 et plus récentes est que Hugo cherche un `Name` d'un format de sortie et le `Suffix` du MediaType lors du choix du modèle utilisé pour rendre une `Page` donnée.
{{% /note %}}

Le tableau suivant présente des exemples de différents formats de sortie, le suffixe utilisé et le modèle respectif [ordre de recherche][lookup order] de Hugo. Tous les exemples du tableau peuvent :

* Utiliser un [modèle de base][base].
* Inclure des [modèles partiels][partials]

{{< datatable "output" "layouts" "Example" "OutputFormat" "Suffix" "Template Lookup Order" >}}

Hugo détecte maintenant le type de média et le format de sortie des partiels, si possible, et utilisera ces informations pour décider si le partiel doit être analysé comme un modèle de plein-texte  ou non.

Hugo cherchera le nom donné, afin que vous puissiez le nommer comme vous voulez. Mais si vous voulez qu'il soit traité comme un texte brut, vous devez utiliser le suffixe du fichier et, le cas échéant, le nom du format de sortie. Le modèle est le suivant :

```
[partial name].[OutputFormat].[suffix]
```

Le partiel ci-dessous est un modèle de texte brut (le format de sortie est `CSV`, et comme c'est le seul format de sortie avec le suffixe `csv`, nous n'avons pas besoin d'inclure le format de sortie `Name`) :

```
{{ partial "mytextpartial.csv" . }}
```

[base]: /templates/base/
[config]: /demarrage/configuration/
[lookup order]: /templates/ordre-recherche/
[media type]: https://en.wikipedia.org/wiki/Media_type
[partials]: /templates/partiels/
