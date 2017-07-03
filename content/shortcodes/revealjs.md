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


{{%warning title="Important" %}}Même si le contenu joint est du markdown, utilisez le raccourci-code `<` au lieu de la notation `%`{{%/warning %}}

### Mise en forme du contenu et délimiteurs de slides

[cliquez ici pour en savoir plus ici]({{% relref "page-slide.md"%}})

## Démo

## Demo

{{<revealjs theme="moon" progress="true">}}

# In the morning

___


## Getting up

- Turn off alarm
- Get out of bed

___

## Breakfast

- Eat eggs
- Drink coffee

---

# In the evening

___

## Dinner

- Eat spaghetti
- Drink wine

___

## Going to sleep

- Get in bed
- Count sheep

{{</revealjs>}}

## Source :

* [{{%icon "sunglasses" %}} clliquez ici pour visualiser le contenu brut](https://github.com/ChristopheDucamp/Doc-DocDock-Hugo/edit/master/content/shortcodes/revealjs.md)
editURL

