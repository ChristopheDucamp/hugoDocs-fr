+++
title = "revealjs"
slug = "revealjs"
description = "présente le contenu sous forme d'une slide reveal.js"
+++


{{% panel theme="danger" %}}Page en chantier - à raffiner avec [ce diaporama stratégique](/creer-page/page-slide/){{% /panel %}}

Ce raccourci-code mettra en forme le markdown entouré pour le restituer avec [reveal.js](http://lab.hakim.se/reveal-js/) sur la  runtime (côté-client)

Pour en savoir plus, regardez le [repo github revealjs](https://github.com/hakimel/reveal.js/#markdown).

## Usage

`revealjs` peut utiliser les paramètres nommés suivants : 

* theme
* transition
* controls
* progress
* history
* center


{{%warning title="Important" %}}Même si le contenu joint est du markdown, utilisez le `<` raccourci-code au lieu de la notation `%` {{%/warning %}}

### Mise en forme du contenu et délimiteurs de slides

[cliquez ici pour en savoir plus ici]({{% relref "page-slide.md"%}})

## Démo

{{<revealjs theme="moon" progress="true">}}

# Le matin

___


## Me Lever

- Désactiver le réveil
- Sortir du lit

___

## Petit-déjeuner

- Manger des oeufs
- Boire du thé

---

# Dans la soirée

___

## Dîner

- Manger des spaghettis
- Boire du Vin

___

## Aller dormir

- Aller au lit
- Compter les moutons

{{</revealjs>}}

