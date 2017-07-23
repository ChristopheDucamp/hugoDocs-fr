---
title: replaceRE
# linktitle: replaceRE
description: remplace toutes les occurrences d'une expression régulière avec le modèle de remplacemenet.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [functions]
menu:
  docs:
    parent: "Fonctions"
#tags: [regex]
signature: ["replaceRE PATTERN REPLACEMENT INPUT"]
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
aliases: []
---

```golang
{{ replaceRE "^https?://([^/]+).*" "$1" "http://gohugo.io/docs" }}` → "gohugo.io"
{{ "http://gohugo.io/docs" | replaceRE "^https?://([^/]+).*" "$1" }}` → "gohugo.io"
```

{{% note %}}
Hugo utilise le [Regular Expression package](https://golang.org/pkg/regexp/) de  Golang, qui est la même syntaxe générale utilise par Perl, Python, et d'autres langages mais avec quelques différences mineures pour ceux venant d'un background dans PCRE. Pour une liste complète de la syntaxe, regardez le  [wiki GitHub pour re2](https://github.com/google/re2/wiki/Syntax).

Si vous apprenez RegEx, ou au moins l'enrichissement de Golang, vous pouvez pratiquer une correspondance de pattern dans le navigateur sur <https://regex101.com/>.
{{% /note %}}
