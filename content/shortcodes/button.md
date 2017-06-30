+++
title = "button"
description = "Affiche un bouton actionnable dans votre page."
+++

Affiche un bouton actionnable dans votre page.

{{<button align="center" href="#" theme="warning" >}} Ceci est un bouton d'avertissement {{< /button >}}

## Usage 

| Paramètre | Par défaut | Description |
|:--|:--|:--|
| href | "" | L'endroit où href pointe |
| align | "center" | aligement horizontal du bouton sur la page |
| theme | `primary` | `default`, `primary` , `success`, `info`, `warning`, `danger` |

Le texte à l'intérieur du texte que vous placez en raccourci-code sera affiché comme _texte de bouton_.

## Démo

	{{</* button href="https://google.com" */>}} allez chez google {{</* /button */>}}
	{{</* button href="https://google.com" theme="success" */>}} Succès {{</* /button */>}}
	{{</* button href="https://google.com" theme="info" */>}} Info {{</* /button */>}}
	{{</* button href="https://google.com" theme="warning" */>}} Avertissement {{</* /button */>}}
	{{</* button href="https://google.com" theme="danger" */>}} Danger ! {{</* /button */>}}
	{{</* button href="https://google.com" theme="default" */>}} Danger ! {{</* /button */>}}
    
{{<button href="https://google.com" >}} allez chez google {{< /button >}}
{{<button href="https://google.com" theme="success">}} Succès {{< /button >}}
{{<button href="https://google.com" theme="info">}} Info {{< /button >}}
{{<button href="https://google.com" theme="warning">}} Avertissement {{< /button >}}
{{<button href="https://google.com" theme="danger">}} Danger ! {{< /button >}}
{{<button href="https://google.com" theme="default">}} Danger ! {{< /button >}}



