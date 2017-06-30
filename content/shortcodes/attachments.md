+++
title = "attachments"
description = "Le raccourci-code `attachments` affiche une liste de fichiers attachés à une page."
+++

Le raccourci-code `attachments` affiche une liste de fichiers joints à une page.

Exemple
{{%alert success%}}{{%attachments  /%}}{{%/alert%}}

## Usage

Le raccouric-code liste les fichiers trouvés dans un **dossier spécifique**.
Actuellement, il supporte deux implémentations pour les pages

1. Si votre page est un fichier markdown, les pièces-jointes doivent être placées dans un **dossier** appelé comme votre page et finissant par **.files**.

    > * content
    >   * _index.md
    >   * page.files
    >      * piece-jointe.pdf
    >   * page.md

2. Si votre page est un **dossier**, les pièces jointes doivent être placée dans un dossier **'files'** imbriqué.

    > * content
    >   * _index.md
    >   * page
    >      * index.md
    >      * files
    >          * piece-jointe.pdf

C'est tout !

{{%alert info%}}**Truc** : Regardez le code source de  documentation sur github{{%/alert%}}

### paramètres

| Paramètre | Par défaut | Description |
|:--|:--|:--|
| title | "Attachments" | Liste des title  |
| pattern | ".*" | Une expression régulirèe, utilisée pour filtrer les pièces jointes par nom de fichier. <br/><br/>{{%alert warning%}}La valeur du paramètre **pattern** doit être une [expression régulière](https://fr.wikipedia.org/wiki/Expression_régulière).

Par exemple :

* Pour faire correspondre un suffixe de fichier de 'jpg', utilisez **.*jpg** (pas *.jpg).
* Pour faire correspondre des noms de fichiers finissant par 'jpg' ou 'png', utilisez **.*(jpg|png)**

{{%/alert%}}|


## Démo
### Liste de pièces jointes finissant par pdf ou mp4

    {{%/*attachments title="Fichiers en rapport" pattern=".*(pdf|mp4)"/*/%}}

restitue : 

{{%attachments title="Fichiers en rapport" pattern=".*(pdf|mp4)"/%}}

