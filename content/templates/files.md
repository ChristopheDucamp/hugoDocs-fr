---
title: Fichier Local
linktitle: Modèles de Fichier Local
description: Les fonctions `readerDir` et `readFile` de Hugo permettent de parcourir la structure du répertoire de votre projet et d'écrire le contenu du fichier dans vos modèles.
godocref: https://golang.org/pkg/os/#FileInfo
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
categories: [Templates]
#tags: [files,directories,ébauche]
menu:
  docs:
    parent: "Templates"
    weight: 110
weight: 110
sections_weight: 110
draft: false
aliases: [/extras/localfiles/,/templates/local-files/]
toc: true
---

## Traverser les Fichiers Locaux

Avec les [fonctions de template `readDir` et `readFile`][reads] d'Hugo, vous pouvez traverser vos fichiers de site web sur votr serveru.

## Utilisez `readDir`

La [fonction `readDir`][reads] renvoie une liste de  [`os.FileInfo`][osfileinfo]. Cela prend le `path` du fichier comme un argument de chaîne unique. Ce chemin peut être vers n'importe quel dossier de votre site web (par ex, comme trouvé sur votre système de fichier du serveur).

Que le chemin soit absolu ou relatif n'importe pas parce que ---au moins pour `readDir`---la racine de votre site web (typiquement `./public/`) devient à la fois :

1. La racine du système de fichier
2. Le dossier de travail en court

### Exemple `readDir` : Lister les Fichiers d'un Dossier

Ce shortcode crée un lien vers chacun des fichiers dans un répertoire ---affiché sous le nom de base du fichier---accompagné de la taille du fichier en bits.

{{% code file="layouts/shortcodes/directoryindex.html" download="directoryindex.html" %}}
```html
{{< readfile file="/themes/gohugoioTheme/layouts/shortcodes/directoryindex.html" >}}
```
{{% /code %}}

Vous pouvez alors appeler le shortcode comme suit dans le marquage de votre contenu :

```html
{{</* directoryindex path="/static/css" pathURL="/css" */>}}
```

Le shortcode au-dessus [fait partie du code pour les docs Hugo][dirindex]. Ici il liste les fichiers CSS de ce site : 

{{< directoryindex path="/themes/gohugoioTheme/static/dist" pathURL="/css" >}}

**Attention :**

{{% note "Les Slashes sont Importants" %}}
Le slash initial `/` dans `pathURL` est important dans le shortcode `directoryindex`. Autrement, `pathURL` devient relatif à la page web en cours.
{{% /note %}}

## Utilisez `readFile`

La [fonction `readfile`][reads] lit un fichier à partir du disque et le convertit dans une chaîne à manipuler par d'autres fonctions Hugo ou ajoutée comme telle. `readFile` prend le fichier, y compris le chemin, comme un argument passé à la fonction.

Pour utiliser la fonction `readFile` dans vos modèles, assurez-vous que le chemin est relatif à votre *répertoire racine de projet Hugo* :

```html
{{ readFile "/content/templates/local-file-templates" }}
```

### `readFile` Exemple : Ajouter un Fichier Projet au Contenu

Comme `readFile` est une fonction, il n'est disponible que dans vos modèles et non sur votre contenu. Cependant, nous pouvons créer un [modèle de code court][sct] qui appelle `readFile`, passe le premier argument à travers la fonction, puis permet à un second argument optionnel d'envoyer le fichier via le processeur Blackfriday. Le modèle d'ajout de ce shortcode à votre contenu sera le suivant :

```
{{</* readfile file="/path/to/local/file.txt" markdown="true" */>}}
```

{{% note %}}
Si vous comptez créer des [shortcodes personnalisés](/templates/shortcode-templates/) avec `readFile` pour un thème, notez que l'usage du shortcode fra référence à la racine du projet et *non* votre répertoire `themes`.
{{% /note %}}

Voici la modélisation pour notre nouveau shortcode `readfile` :

{{% code file="layouts/shortcodes/readfile.html" download="readfile.html" %}}
```
{{< readfile file="/themes/gohugoioTheme/layouts/shortcodes/readfile.html">}}
```
{{% /code %}}

Ce shortcode `readfile` fait [aussi partie de la doc Hugo][readfilesource]. Aussi en est-il de [`testing.txt`][testfile], qui appellera dans cet exemple en le passant notre nouveau shortcode `readfile` comme suit :

```
{{</* readfile file="/content/readfiles/testing.txt" */>}}
```

L'output "string" pour cette déclaration de shortcode sera le suivant : 

```markdown
{{< readfile file="/content/readfiles/testing.txt" >}}
```

Néanmoins, si nous voulons que Hugo passe la chaîne dans Blackfiday, nous ajouterions le paramètre optionnel  `markdown="true"` :

```html
{{</* readfile file="/content/readfiles/testing.txt" markdown="true" */>}}
```

Et voici le résultat tel qu'[appelé directement dans les docs Hugo][] et rendu pour affichage :


{{< readfile file="/content/readfiles/testing.txt" markdown="true">}}

[appelé directement dans les docs Hugo]: https://github.com/gohugoio/hugo/blob/master/docs/content/templates/files.md
[dirindex]: https://github.com/gohugoio/hugo/blob/master/docs/layouts/shortcodes/directoryindex.html
[osfileinfo]: https://golang.org/pkg/os/#FileInfo
[reads]: /fonctions/readfile/
[sc]: /gestion-contenu/shortcodes/
[sct]: /templates/shortcode-templates/
[readfilesource]: https://github.com/gohugoio/hugo/blob/master/
[testfile]: https://github.com/gohugoio/hugo/blob/master/docs/testfile
