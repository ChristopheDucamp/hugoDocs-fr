+++
title = "excerpt-include"
description = "le raccourci-code Excerpt est utilisé pour afficher un extrait de contenu (un segment) provenant d'une page dans une autre."
+++

Le raccourci-code Excerpt Include s'utilise pour afficher une extraction de contenu (ce qui veut dire un segment de) provenant d'une page dans une autre.
Avant de pouvoir utiliser ce raccourci-code, l'extrait doit avoir été défini en utilisant le raccouric-code Excerpt. {{%alert info%}}Notez que vous pouvez avoir plus d'un raccourci-code Excerpt Include sur une page (même si vous ne pouvez avoir qu'un seul raccourci-code Excerpt sur une page).{{%/alert%}}


## Usage

| Paramètre | valeur par défaut | Description |
|:--|:--|:--|
| filename | **requis** | Tapez le nom de fichier de la page qui contient l'extrait à afficher.<br/>Le chemin est relatif au dossier `content`|
| panel | none | Détermine si docDock affichera un panel autour du contenu extrait. Le panel comprend la valeur donnée du panel et la bordure du panel. Par défaut, le panel et le titre ne sont pas affichés.|

## Démo
Le paragraphe du dessous montre un exemple d'un raccourci-code Excerpt Include, contenant le contenu d'un extrait que nous avons défini sur la page de raccourci-code Excerpt. Sur le raccourci-code Excerpt Include en-dessous, nous avons réglé les options pour afficher à la fois le titre et le panel entourant le contenu.

	{{%/*excerpt-include filename="shortcodes/excerpt.md" panel="Extrait de la page excerpt" /*/%}}

{{%excerpt-include filename="shortcodes/excerpt.md" panel="Extrait de la page excerpt" /%}}
