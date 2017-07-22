---
title: Taxonomies
linktitle:
description: Hugo prend en charge les taxonomies définies par l'utilisateur pour vous aider à démontrer des relations logiques entre les contenus pour les utilisateurs finaux de votre site.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-20
#tags: [taxonomies,metadata,front matter,terms, termes, métadonnées]
categories: [content management, gestion de contenu]
draft: false
aliases: [/taxonomies/overview/,/taxonomies/usage/,/indexes/overview/,/doc/indexes/,/extras/indexes]
toc: true
---

## Qu'est-ce Qu'une Taxonomie ?

Hugo prend en charge les groupages de contenu définis par l'utilisateur appelés **taxonomies**. Les taxonomies sont les classifications des relations logiques entre les contenus.

### Définitions

**Taxonomie**
: une catégorisation qui peut être utilisée pour classifier du contenu

**Terme**
: une clé dans la taxonomie

**Valeur**
: un morceau de contenu assigné à un terme

## Exemple de Taxonomie : Site Web Cinéma

Supposons que nous produisons un site web sur le cinéma. Vous pourriez vouloir inclure les taxonomies suivantes : 

* Acteurs
* Réalisateurs
* Studios
* Genre
* Années
* Prix

Puis, pour chacun des films, vous devriez spécifier les termes pour chacune de ces taxonomies (par ex., dans le [front matter][] de chacun de vos fichiers de contenu de film). À partir de ces termes, Hugo créerait automatiquement les pages pour chaque  Acteur, Réalisateur, Studio, Genre, Année, et Prix, avec chacun d'eux listant tous les Films qui correpondent à ces Acteur, Réalisateur, Studio, Genre, Année et Prix spécifiques.

### Organisation de la Taxonomie Cinéma

Pour continuer avec l'exemple d'un site de cinéma, ce qui suit démontre les relations de contenu en partant de la perspective de la taxonomie : 

```
Acteur                    <- Taxonomie
    Bruce Willis         <- Terme
        The Six Sense    <- Contenu
        Unbreakable      <- Contenu
        Moonrise Kingdom <- Contenu
    Samuel L. Jackson    <- Terme
        Unbreakable      <- Contenu
        The Avengers     <- Contenu
        xXx              <- Contenu
```

De la peerspective du contenu, les relations apparaissent différemment, même si les données et étiquettes utilisées sont les mêmes :

```
Unbreakable                 <- Contenu
    Acteurs                 <- Taxonomie
        Bruce Willis        <- Terme
        Samuel L. Jackson   <- Terme
    Réalisateur             <- Taxonomie
        M. Night Shyamalan  <- Terme
    ...
Moonrise Kingdom            <- Contenu
    Acteurs                 <- Taxonomie
        Bruce Willis        <- Terme
        Bill Murray         <- Terme
    Réalisateur             <- Taxonomie
        Wes Anderson        <- Terme
    ...
```

## Valeurs par Défaut de la Taxonomie Hugo

Hugo supporte nativement les taxonomies. 

Sans ajouter une seule ligne à votre fichier de configuration du site, Hugo créera automatiquement les  taxonomies pour les  `tags` et `categories`. Si vous ne voulez pas que Hugo crée quelque taxonomie, régler `disableKinds` dans la configuration de votre suite comme suit : 

```toml
disableKinds = ["taxonomy","taxonomyTerm"]
```

### Destinations par Défaut

Lorsque les taxonomies sont utilisées ---et les [modèles de taxonomie][taxonomy templates] sont fournis--- Hugo créera automatiquement une page répertoriant tous les termes de la taxonomie et les pages individuelles avec des listes de contenu associées à chaque terme. Par exemple, une taxonomie `categories` déclarée dans votre configuration et utilisée dans votre front matter de contenu créera les pages suivantes :

* Une seule page à `votresite.com/categories/` qui répertorie tous les [termes de la taxonomie][terms within the taxonomy]
* [Pages de liste de taxonomie individuelle][taxonomy templates] (par exemple, `/categories/development/`) pour chacun des termes qui montre une liste de toutes les pages marquées comme faisant partie de cette taxonomie dans n'importe quel fichier [front matter][] de contenu.

## Configurer les Taxonomies

Les taxonomies doivent être définies dans la [configurationd de votre site web][config] avant de pouvoir être utilisées sur l'ensemble du site. Vous devez fournir à la fois les étiquettes au singulier et au pluriel des étiquettes pour chaque taxonomie. Par exemple, `singular key = "plural value"`  pour TOML et `singular key: "plural value"` pour YAML.

### Exemple : Configuration Taxonomie TOML

```toml
[taxonomies]
  tag = "tags"
  category = "categories"
  series = "series"
```

### Exemple : Configuration Taxonomie YAML

```yaml
taxonomies:
  tag: "tags"
  category: "categories"
  series: "series"
```

### Préserver les Valeurs de Taxonomie

Par défaut, les noms de taxonomie sont normalisés.

Par conséquent, si vous avez un terme de taxonomie avec des caractères spéciaux tels que `Gérard Depardieu` au lieu de  `Gerard Depardieu`, régler la valeur de `preserveTaxonomyNames` sur `true` dans votre [configuration de site][config]. Hugo préservera alors les caractères spéciaux dans les valeurs de taxonomie mais titrera encore les valeurs pour les titres et les normalisera dans les URLs.

Notez que si vous utilisez `preserveTaxonomyNames` et avez l'intention de construire manuellement les URLs vers la page archive, vous devrez passer les valeurs de taxonomie à travers la [fonction de modèle `urlize`][].

{{% note %}}
Vous pouvez ajouter du contenu et un front matter à votre liste de taxonomie et aux pages de termes de la taxonomie. Voir  [Organisation du Contenu](/gestion-contenu/organization/) pour plus d'informations sur la manière d'ajouter un  `_index.md` pour cet objectif.

Notez aussi que les [permaliens](/gestion-contenu/urls/) de taxonomie ne sont *pas* configurables.
{{% /note %}}

## Ajouter des Taxonomies au Contenu

Une fois qu'une taxonomie est définie au niveau du site, n'importe quel contenu peut lui être attribué, indépendamment du [type de contenu][content type] ou de la [section de contenu][content section].

L'affectation de contenu à une taxonomie se fait dans le  [front matter][]. Créez simplement une variable avec le nom *plural* de la taxonomie et attribuez tous les termes que vous souhaitez appliquer à l'instance du type de contenu.

{{% note %}}
Si vous souhaitez générer rapidement des fichiers de contenu avec des taxonomies ou des termes préconfigurés, lisez les documents sur les [archétypes Hugo](/gestion-contenu/archetypes/).
{{% /note %}}

### Exemple : Front Matter TOML avec Taxonomies

```toml
+++
title = "Hugo: A fast and flexible static site generator"
tags = [ "Development", "Go", "fast", "Blogging" ]
categories = [ "Development" ]
series = [ "Go Web Dev" ]
slug = "hugo"
project_url = "https://github.com/gohugoio/hugo"
+++
```

### Exemple : Front Matter YAML avec Taxonomies

```yaml
---
title: "Hugo: A fast and flexible static site generator"
#tags: ["Development", "Go", "fast", "Blogging"]
categories: ["Development"]
categories: ["Go Web Dev"]
slug: "hugo"
project_url: "https://github.com/gohugoio/hugo"
---
```

### Exemple : Front Matter JSON avec Taxonomies

```json
{
    "title": "Hugo: A fast and flexible static site generator",
    "tags": [
        "Development",
        "Go",
        "fast",
        "Blogging"
    ],
    "categories" : [
        "Development"
    ],
    "series" : [
        "Go Web Dev"
    ],
    "slug": "hugo",
    "project_url": "https://github.com/gohugoio/hugo"
}
```

## Ordre des Taxonomies

Un fichier de contenu peut affecter du poids pour chacune de ses taxonomies associées. Le poids taxonomique peut être utilisé pour trier ou commander du contenu dans [modèles de liste de taxonomie][taxonomy list templates] et il est déclaré dans le [front matter][] du fichier de contenu. La convention pour déclarer le poids taxonomique est `taxonomyname_weight`.

Les exemples suivants de TOML et YAML montrent un contenu qui a un poids de 22, qui peut être utilisé à des fins de tri lors du rendu des pages attribuées aux valeurs "a", "b" et "c" de la taxonomie "tags" . On lui a également attribué le poids de 44 lors du rendu de la page de catégorie «d».


### Exemple : TOML `weight` Taxonomique

```toml
+++
title = "foo"
tags = [ "a", "b", "c" ]
tags_weight = 22
categories = ["d"]
categories_weight = 44
+++
```

### Exemple : YAML `weight` Taxonomique

```yaml
---
title: foo
#tags: [ "a", "b", "c" ]
tags_weight: 22
categories: ["d"]
categories_weight: 44
---
```

En utilisant le poids taxonomique, le même contenu peut apparaître dans différentes positions dans différentes taxonomies.

{{% note "Limites dans les ordres de taxonomies" %}}
Actuellement, les taxonomies ne supportent que le [tri par défaut `weight => date` de la liste de contenu](/templates/lists/#liste-ordonnée-par-défaut-weight-date). Pour plus d'informations, consultez la documentation sur [modèles de taxonomie](/templates/taxonomy-templates/).
{{% /note %}}


[`urlize` template function]: /fonctions/urlize/
[content section]: /gestion-contenu/sections/
[content type]: /gestion-contenu/types/
[documentation on archetypes]: /gestion-contenu/archetypes/
[front matter]: /gestion-contenu/front-matter/
[taxonomy list templates]: /templates/taxonomy-templates/#taxonomy-page-templates
[taxonomy templates]: /templates/taxonomy-templates/
[terms within the taxonomy]: /templates/taxonomy-templates/#taxonomy-terms-templates "Voir comment trier les termes associés à une taxonomie"
[config]: /demarrage/configuration/
