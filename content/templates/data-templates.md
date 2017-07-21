---
title: Modèles de Data 
linktitle:
description: En plus des variables intégrées de Hugo, vous pouvez spécifier vos propres données personnalisées dans des modèles ou shortcodes qui extraient des sources locales et dynamiques.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-19
categories: [templates]
#tags: [data,dynamic,csv,json,toml,yaml]
menu:
  docs:
    parent: "templates"
    weight: 80
weight: 80
sections_weight: 80
draft: false
aliases: [/extras/datafiles/,/extras/datadrivencontent/,/doc/datafiles/]
toc: true
---

<!-- begin data files -->

Hugo prend en charge le chargement des données des fichiers YAML, JSON et TOML situés dans le dossier `data` placé à la racine de votre projet Hugo.

## Le Dossier Data

Le dossier `data` est l'endroit où vous pouvez stocker des données supplémentaires à utiliser par Hugo lors de la génération de votre site. Les fichiers de données ne sont pas utilisés pour générer des pages autonomes ; ils sont destinés à être complémentaires aux fichiers de contenu. Cette fonctionnalité peut augmenter le contenu dans le cas où vos champs de front matter ne seraient plus contrôlés. Ou peut-être souhaitez-vous montrer un ensemble de données plus important dans un modèle (voir l'exemple ci-dessous). Dans les deux cas, il est judicieux d'externaliser les données dans leurs propres fichiers.

Ces fichiers doivent être des fichiers YAML, JSON ou TOML (en utilisant l'extension `.yml`, `.yaml`, `.json` ou `toml`). Les données seront accessibles sous une `map` dans la variable `.Site.Data`.

## Fichiers de Données dans les Thèmes

Les fichiers de données peuvent également être utilisés dans les [thèmes Hugo][themes], mais notez que les fichiers de données de thème suivent la même logique que les autres fichiers de modèle dans [l'ordre de recherche Hugo][lookup] (c.-à-d., deux fichiers avec le même nom et le même chemin relatif, le fichier dans le dossier racine du projet `data` remplacera le fichier dans le dossier `themes/<THEME>/data`).

Par conséquent, les auteurs de thème devraient prendre soin de ne pas inclure de fichiers de données qui pourraient être facilement écrasés par un utilisateur qui décide de [personnaliser un thème][customize]. Pour les éléments de données spécifiques au thème qui ne doivent pas être annulés, il est judicieux de préfixer la structure du dossier avec un espace de noms ; par exemple. `Montheme/data/<THEME>/somekey/...`. Pour vérifier si un tel duplicata existe, lancez hugo avec le marqueur `-v`.

Les clés dans la map créées avec des modèles de données à partir des fichiers de données seront un ensemble en forme de chaîne-point de `path`, `nomfichier` et `key` dans le fichier (le cas échéant).

Ceci est mieux expliqué à l'aide d'un exemple :

## Exemple : Discographie Solo de Jaco Pastorius

[Jaco Pastorius](http://en.wikipedia.org/wiki/Jaco_Pastorius_discography) était un grand bassiste, mais sa discographie solo est assez courte pour servir d'exemple. [John Patitucci](http://en.wikipedia.org/wiki/John_Patitucci) est un autre géant de la basse.

L'exemple ci-dessous est un peu imaginé, mais il illustre la flexibilité des fichiers de données. Cet exemple utilise TOML comme son format de fichier avec les deux fichiers de données suivants :

* `data/jazz/bass/jacopastorius.toml`
* `data/jazz/bass/johnpatitucci.toml`

`jacopastorius.toml` contient le contenu en-dessous. `johnpatitucci.toml` contient une liste similaire :

```
discography = [
"1974 – Modern American Music … Period! The Criteria Sessions",
"1974 – Jaco",
"1976 - Jaco Pastorius",
"1981 - Word of Mouth",
"1981 - The Birthday Concert (released in 1995)",
"1982 - Twins I & II (released in 1999)",
"1983 - Invitation",
"1986 - Broadway Blues (released in 1998)",
"1986 - Honestly Solo Live (released in 1990)",
"1986 - Live In Italy (released in 1991)",
"1986 - Heavy'n Jazz (released in 1992)",
"1991 - Live In New York City, Volumes 1-7.",
"1999 - Rare Collection (compilation)",
"2003 - Punk Jazz: The Jaco Pastorius Anthology (compilation)",
"2007 - The Essential Jaco Pastorius (compilation)"
]
```

La liste des bassistes peut être accédée via  `.Site.Data.jazz.bass`, un bassiste solo en ajoutant le nom de fichier sans le suffixe, par ex. `.Site.Data.jazz.bass.jacopastorius`.

Vous pouvez maintenant sortir la liste des enregistrements de tous les bassistes dans un modèle : 

```html
{{ range $.Site.Data.jazz.bass }}
   {{ partial "artist.html" . }}
{{ end }}
```

Et ensuite dans le `partial/artist.html` :

```
<ul>
{{ range .discography }}
  <li>{{ . }}</li>
{{ end }}
</ul>
```

Vous découvrez un nouveau bassiste génial ? Ajoutez simplement un autre fichier `.toml` dans le même dossier.

## Exemple : Accéder à des Valeurs Nommées dans un Fichier Data

Supposez que vous ayez la structure YAML suivante dans votre fichier data `User0123.yml` situé directement dans `data/` :

```
Name: User0123
"Short Description": "He is a **jolly good** fellow."
Achievements:
  - "Can create a Key, Value list from Data File"
  - "Learns Hugo"
  - "Reads documentation"
```

Vous pouvez utiliser le code suivant pour rendre la `Short Description` dans votre layout :

```
<div>Short Description of {{.Site.Data.User0123.Name}}: <p>{{ index .Site.Data.User0123 "Short Description" | markdownify }}</p></div>
```

Notez l'usage de la [fonction modèle `markdownify`][markdownify]. Ceci renverra la description à travers le moteur de rendu Markdown Blackfriday.

<!-- begin "Data-drive Content" page -->

## Contenu Data-Driven

En plus de la fonctionnalité de [fichiers data](/extras/datafiles/), Hugo a aussi une fonctionnalité de "data-driven content" qui vous permet de charger n'importe quel fichier [JSON](http://www.json.org/) ou [CSV](http://en.wikipedia.org/wiki/Comma-separated_values) à partir de presque n'importe quelle ressource.

Le contenu "Data-driven" repose actuellement sur deux fonctions, `getJSON` et `getCSV`, qui sont disponibles dans tous les fichiers de modèles.

## Détails d'Implémentation

### Appel de Fonctions avec une URL

Dans votre modèle, appelez les fonctions comme ceci :

```golang
{{ $dataJ := getJSON "url" }}
{{ $dataC := getCSV "separator" "url" }}
```

Si vous utilisez un préfixe ou un postfix pour l'URL, les fonctions acceptent les [arguments variadiques][variadique] :

```
{{ $dataJ := getJSON "url prefix" "arg1" "arg2" "arg n" }}
{{ $dataC := getCSV  "separator" "url prefix" "arg1" "arg2" "arg n" }}
```

Le séparateur pour `getCSV` doit être placé dans la première position et ne peut comporter qu'un seul caractère.

Tous les arguments passés seront joints à l'URL finale :

```html
{{ $urlPre := "https://api.github.com" }}
{{ $gistJ := getJSON $urlPre "/users/GITHUB_USERNAME/gists" }}
```

Cela se résoudra en interne aux éléments suivants :

```html
{{ $gistJ := getJSON "https://api.github.com/users/GITHUB_USERNAME/gists" }}
```

Enfin, vous pouvez varier sur une liste (array). Cet exemple affichera les 5 premiers 5 gists d'un utilisateur GitHub :

```html
<ul>
  {{ $urlPre := "https://api.github.com" }}
  {{ $gistJ := getJSON $urlPre "/users/GITHUB_USERNAME/gists" }}
  {{ range first 5 $gistJ }}
    {{ if .public }}
      <li><a href="{{ .html_url }}" target="_blank">{{ .description }}</a></li>
    {{ end }}
  {{ end }}
</ul>
```


### Exemple pour fichiers CSV 

Pour `getCSV`, le séparateur d'un caractère doit être placé dans la première position suivi de l'URL. Voici un exemple de création d'une table HTML dans un [modèle partiel][partials] à partir d'un CSV publié :

{{% code file="layouts/partials/get-csv.html" %}}
```html
  <table>
    <thead>
      <tr>
      <th>Name</th>
      <th>Position</th>
      <th>Salary</th>
      </tr>
    </thead>
    <tbody>
    {{ $url := "http://a-big-corp.com/finance/employee-salaries.csv" }}
    {{ $sep := "," }}
    {{ range $i, $r := getCSV $sep $url }}
      <tr>
        <td>{{ index $r 0 }}</td>
        <td>{{ index $r 1 }}</td>
        <td>{{ index $r 2 }}</td>
      </tr>
    {{ end }}
    </tbody>
  </table>
```
{{% /code %}}

L'expression `{{index $r number}}` doit être utilisée pour sortir la nième-colonne à partir de la ligne en cours.

### URLs en Cache

Chaque URL téléchargée sera mise en cache dans le dossier par défaut `$TMPDIR/hugo_cache/`. La variable `$TMPDIR` sera résolue dans votre répertoire temporaire dépendant du système.

Avec l'indicateur de ligne de commande `--cacheDir`, vous pouvez spécifier n'importe quel dossier de votre système en tant que répertoire de mise en cache.

Vous pouvez également configurer `cacheDir` dans le [fichier de configuration principal][config].

Si vous n'aimez pas du tout la mise en cache, vous pouvez désactiver complètement la mise en cache avec l'indicateur de ligne de commande `--ignoreCache`.

### Authentification pour Utilisation d'URLs REST

À l'heure actuelle, vous ne pouvez utiliser que les méthodes d'authentification qui peuvent être utilisées dans une URL. [OAuth][] et d'autres méthodes d'authentification ne sont pas implémentées.

### Charger des Fichiers Locaux

Pour charger des fichiers locaux avec `getJSON` et `getCSV`, les fichiers sources doivent résider dans le répertoire de travail de Hugo. L'extension de fichier n'a pas d'importance, mais le contenu oui.

Cela applique la même logique de sortie que ci-dessus dans l'[appel des Fonctions avec une URL](#détails-d-implémentation).

## LiveReload avec Fichiers de Data

Il n'y a aucune chance de déclencher un [LiveReload][] lorsque le contenu d'une URL change. Cependant, lorsqu'un fichier *local* change (c'est-à-dire `data/*` et `themes/<THEME>/data/*`), un LiveReload sera déclenché. Les Symlinks ne sont pas pris en charge. Notez également que, parce que le téléchargement de données prend un certain temps, Hugo arrête de traiter vos fichiers Markdown jusqu'à ce que le téléchargement des données soit terminé.

{{% warning "URLs Data et LiveReload"%}}
Si vous modifiez un fichier local et que LiveReload est déclenché, Hugo lira le contenu basé sur les données (URL) du cache. Si vous avez désactivé le cache (c'est-à-dire en exécutant le serveur avec `hugo server --ignoreCache`), Hugo va re-télécharger le contenu à chaque fois que LiveReload se déclenche. Cela peut créer un trafic *énorme*. Vous pouvez atteindre rapidement les limites de l'API.
{{% /warning %}}

## Exemples de Contenu Data-driven

- Galerie de Photos motorisée par JSON : [https://github.com/pcdummy/hugo-lightslider-example](https://github.com/pcdummy/hugo-lightslider-example)
- Dépôts étoilées sur GitHub [dans un post](https://github.com/SchumacherFM/blog-cs/blob/master/content%2Fposts%2Fgithub-starred.md) utilisant un contenu data-driven dans un [shortcode personnalisé](https://github.com/SchumacherFM/blog-cs/blob/master/layouts%2Fshortcodes%2FghStarred.html).

## Specs pour Formats de Data

* [TOML Spec][toml]
* [YAML Spec][yaml]
* [JSON Spec][json]
* [CSV Spec][csv]

[config]: /getting-started/configuration/
[csv]: https://tools.ietf.org/html/rfc4180
[customize]: /themes/customizing/
[json]: /documents/ecma-404-json-spec.pdf
[LiveReload]: /getting-started/usage/#livereload
[lookup]: /templates/lookup-order/
[markdownify]: /functions/markdownify/
[OAuth]: http://en.wikipedia.org/wiki/OAuth
[partials]: /templates/partials/
[themes]: /themes/
[toml]: https://github.com/toml-lang/toml
[variadique]: https://fr.wikipedia.org/wiki/Fonction_variadique
[vars]: /variables/
[yaml]: http://yaml.org/spec/