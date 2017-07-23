---
title: .Scratch
description: Agit comme un "scratchpad" pour autoriser les variables pouvant être écrites dans la page ou le shortcode.
godocref:
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
#tags: [iteration, itération]
categories: [Fonctions]
menu:
  docs:
    parent: "Fonctions"
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

`Scratch` est ajoutée à la fois à `Page` et `Shortcode` -- avec les méthodes suivantes :

* `Set` et `Add` prennent une `key` et la `value` à ajouter.
* `Get` renvoie la `value` pour la `key` donnée.
* `SetInMap` prend une `key`, `mapKey` et une `value`
* `GetSortedMapValues` renvoie une array de valeurs à partir des  `key` triées par `mapKey`

`Set` et `SetInMap` peuvent stocker des valeurs de n'importe quel type.

Pour des valeurs uniques, `Add` accepte des valeurs qui supportent l'opérateur `+` de Go. Si le premier `Add` pour une clé est une "array" ou "slice", les ajouts suivants seront ajoutés à cette liste..

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

{{%note %}}
Les exemples ci-dessus utilisent la variable spéciale `$`, qui fait référence au noeud de niveau supérieur. C'est le comportement que vous voudrez le plus rapidement et aidera à supprimer une certaine confusion lors de l'utilisation des boucles de la gamme de pages `Scratch` -- et si vous commencez par appeler par inadvertance le `Scratch`. Mais il peut y avoir des cas d'utilisation pour `{{ .Scratch.Add "key" "some value" }}`.
{{% /note %}}

[pagevars]: /variables/page/
