---
title: .AddDate
description: Renvoie la date/horaire correspondant à l'ajout du nombre données des années, mois, et jours passés dans la fonction.
godocref: https://golang.org/pkg/time/#Time.AddDate
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
categories: [Fonctions]
menu:
  docs:
    parent: "Fonctions"
#tags: [dates,time]
signature: [".AddDate YEARS MONTHS DAYS"]
workson: [times]
hugoversion:
relatedfuncs: [now]
deprecated: false
aliases: []
---


La fonction `AddDate` prend trois arguments dans l'ordre logique des `years`, `months`, et `days`.

## Exemple : Tweets au Hasard des 2 Dernières Années.

Supposons que vous ayez un fichier sur `data/tweets.toml` qui contient une liste de Tweets à afficher sur votre page d'accueil de site. Le fichier est rempli avec des blocs `[[tweet]]` ; par ex.

```toml
[[tweet]]
name = "Steve Francia"
twitter_handle = "@spf13"
quote = "I'm creator of Hugo. #metadocreference"
link = "https://twitter.com/spf13"
date = "2017-01-07T00:00:00Z"
```

Supposons que vous voulez exhumer des Tweets des deux dernières années et les présenter dans un ordre aléatoire. En conjonction avec les fonctions [`where`](/fonctions/where/) et [`now`](/fonctions/now/), vous pouvez limiter votre portée aux deux dernières années via `now.AddDate -2 0 0 `, qui représente un point dans le temps 2 ans, 0 jours et 0 heures avant l'heure de votre dernière construction du site.

{{% code file="partials/templates/random-tweets.html" download="tweets.html" %}}
```html
{{ range where $.Site.Data.tweets.tweet "date" "ge" (now.AddDate -2 0 0) | shuffle }}
    <div class="item">
        <blockquote>
            <p>
            {{ .quote | safeHTML }}
            </p>
            &mdash; {{ .name }} ({{ .twitter_handle }}) <a href="{{ .link }}">
                {{ dateFormat "January 2, 2006" .date }}
            </a>
        </blockquote>
    </div>
{{ end }}
```
{{% /code %}}
