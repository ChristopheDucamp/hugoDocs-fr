+++
title = "expand"
description = "Affiche une section de texte extensible / pliable dans votre page"
+++

Le raccourci-code Expand affiche une section de texte extensible ou pliable sur votre page.
Voici un exemple

{{%expand "déplie-moi" %}}Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.{{%/expand%}}


## Usage


ce raccourci-code prend exactement un paramètre facultatif pour définir le texte qui apparaît à côté de l'icône déplier/plier. (La valeur par défaut est "Expand me...")

	{{%/*expand "Ce thème docdock vous botte ?" */%}}Oui !.{{%/* /expand*/%}}

{{%expand "Ce thème docdock vous botte ?" %}}Oui !{{% /expand%}}

# Démo

	{{%/*expand "déplie-moi STP" */%}}Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
	tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
	quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
	consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
	cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
	proident, sunt in culpa qui officia deserunt mollit anim id est laborum.{{%/* /expand*/%}}


{{%expand "déplie-moi STP" %}}Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.{{% /expand%}}