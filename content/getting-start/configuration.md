+++
title = "Configuration"
description = ""
weight = 2
+++

Au moment de construire le site web, vous pouvez régler un thème en utilisant l'option `--theme`. Nous vous suggérons de modifier votre fichier de configuration et de régler le thème par défaut. Exemple avec le format `config.toml`.
<!--more-->
```
theme = "docdock"
```

## Génération de l'Index de Recherche

Ajoutez la ligne suivante dan le même fichier `config.toml`.

```
[outputs]
home = [ "HTML", "RSS", "JSON"]
```

Le fichier d'index de recherche LUNRJS sera généré sur les modifications récentes.

## Le Contenu de votre Site Web 

Découvrez comment [créer]({{%relref "creer-page/_index.md"%}}) et [organiser votre contenu]({{%relref "content-organisation/_index.md"%}}) rapidement et intuitivement.