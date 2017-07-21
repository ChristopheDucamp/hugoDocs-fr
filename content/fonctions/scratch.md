---
title: .Scratch
description: Agis comme un "scratchpad" pour autoriser les variables pouvant être écrites dans la page ou le shortcode.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-21
#tags: [iteration]
categories: [functions, fonctions]
menu:
  docs:
    parent: "fonctions"
toc:
signature: []
workson: []
hugoversion:
relatedfuncs: []
deprecated: false
draft: false
aliases: [/extras/scratch/,/doc/scratch/]
---

Dans la plupart des cas, vous pouvez bien fonctionner sans `Scratch`, mais il existe des cas d'utilisation qui ne sont pas résolus avec les modèles de Go sans l'aide de `Scratch` en raison de problèmes de portée.

`Scratch` est ajouté à la fois à `Page` et `Shortcode` -- avec les méthodes suivantes :

* `Set` and `Add` takes a `key` and the `value` to add.
* `Get` returns the `value` for the `key` given.
* `SetInMap` takes a `key`, `mapKey` and `value`
* `GetSortedMapValues` returns array of values from `key` sorted by `mapKey`

`Set` and `SetInMap` can store values of any type.

For single values, `Add` accepts values that support Go's `+` operator. If the first `Add` for a key is an array or slice, the following adds will be appended to that list.

The scope of the backing data is global for the given `Page` or `Shortcode`, and spans partial and shortcode includes.

Note that `.Scratch` from a shortcode will return the shortcode's `Scratch`, which in most cases is what you want. If you want to store it in the page scroped Scratch, then use `.Page.Scratch`.

## Usage échantillon

L'usage s'illustre mieux avec quelques échantillons

```
{{ $.Scratch.Add "a1" 12 }}
{{ $.Scratch.Get "a1" }} {{/* => 12 */}}
{{ $.Scratch.Add "a1" 1 }}
{{ $.Scratch.Get "a1" }} // {{/* => 13 */}}

{{ $.Scratch.Add "a2" "AB" }}
{{ $.Scratch.Get "a2" }} {{/* => AB */}}
{{ $.Scratch.Add "a2" "CD" }}
{{ $.Scratch.Get "a2" }} {{/* => ABCD */}}

{{ $.Scratch.Add "l1" (slice "A" "B") }}
{{ $.Scratch.Get "l1" }} {{/* => [A B]  */}}
{{ $.Scratch.Add "l1" (slice "C" "D") }}
{{ $.Scratch.Get "l1" }} {{/* => [A B C D] */}}

{{ $.Scratch.Set "v1" 123 }}
{{ $.Scratch.Get "v1" }}  {{/* => 123 */}}

{{ $.Scratch.SetInMap "a3" "b" "XX" }}
{{ $.Scratch.SetInMap "a3" "a" "AA" }}
{{ $.Scratch.SetInMap "a3" "c" "CC" }}
{{ $.Scratch.SetInMap "a3" "b" "BB" }}
{{ $.Scratch.GetSortedMapValues "a3" }} {{/* => []interface {}{"AA", "BB", "CC"} */}}
```

{{% notice note %}}

Les exemples ci-dessus utilisent la variable spéciale `$`, qui fait référence au noeud de niveau supérieur. C'est le comportement que vous voudrez le plus rapidement et aidera à supprimer une certaine confusion lors de l'utilisation des boucles de la gamme de pages `Scratch` -- et si vous commencez par appeler par inadvertance le `Scratch`. Mais il peut y avoir des cas d'utilisation pour `{{ .Scratch.Add "key" "some value" }}`.
{{% /notice %}}

[pagevars]: /variables/page/
