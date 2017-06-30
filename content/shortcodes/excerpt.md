+++
title = "excerpt"
description = "Le raccourci-code Excerpt est utilisé pour marquer une partie d'un contenu de page pour réutilisation."
+++

Le raccourci-code `excerpt` est utilisé pour marquer une partie du contenu d'une page pour réutilisation. La définition d'un extrait permet à d'autres raccourcis-code, tels que le raccourci de code `excerpt-include`, d'afficher le contenu marqué ailleurs.

{{%alert warning%}}Vous ne pouvez définir qu'un seul extrait par page. En d'autres mots, vous ne pouvez ajouter qu'un seul raccourci-code Excerpt par page.{{%/alert%}}


## Usage

| Param | par défaut | Description |
|:--|:--|:--|
| hidden | "false" | Vérifie si le contenu de la page contenu dans le gardien de place du raccourci-code Excerpt est affiché sur la page.{{%alert warning%}}Notez que cette option n'affecte la page que si elle contien le raccourci-code Excerpt. Elle n'impacte pas les pages où le contenu est réutilisé..{{%/alert%}} |

## Demo

	{{%/*excerpt*/%}}
	Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
	tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
	quis nostrud exercitation **ullamco** laboris nisi ut aliquip ex ea commodo
	consequat. Duis aute irure dolor in _reprehenderit in voluptate_
	cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
	proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
	{{%/* /excerpt*/%}}

{{%excerpt%}}
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation **ullamco** laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in _reprehenderit in voluptate_
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
{{% /excerpt%}}



{{%alert info%}}Voir un exemple avec le [raccourci-code `excerpt-include`]({{%relref "shortcodes/excerpt-include.md"%}}){{%/alert%}}