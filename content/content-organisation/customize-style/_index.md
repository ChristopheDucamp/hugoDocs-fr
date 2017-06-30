+++
title = "Personnaliser le look and feel de votre site web"
+++

Vous pouvez modifier le style et le comportement du thème sans y toucher.

* Injectez votre propre html, css ou js à l'intérieur de la page
* Ecrasez les css ou js existants avec vos propres fichiers


## Injecter votre HTML

### à l'intérieur de la partie \<head\> de chaque page :

Créez un fichier `custom-head.html` à l'intérieur dun dossier  `layouts/partials` aux côté du dossier `content`

> * content/
> * layouts/
>   * partials/
>      * custom-head.html

désormais, soyez à l'aise pour ajouter le code JS, CSS, HTML que vous voulez :)

### à la fin de la partie body de chaque page : 

Créez un fichier `custom-footer.html` à l'intérieur d'un dossier  `layouts/partials` à côté du dossier `content`

> * content/
> * layouts/
>   * partials/
>      * custom-footer.html

désormais, soyez à l'aise pour ajouter le code JS, CSS, HTML que vous voulez :)

## écraser les CSS ou JS existants

Créez le fichier correspondant dans votre répertoire `static`, hugo utilisera le vôtre au lieu de celui du thème.
Exemple : 

créez un theme.css et placez-le dans `static/css/` pour écraser complètement le `theme.css` de docDock
