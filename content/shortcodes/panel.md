+++
title = "panel"
description = "Permet de mettre en évidence les informations ou de les mettre dans une boîte."

+++



{{% panel theme="success" header="Le raccourci panel" %}}Vous permet de mettre en évidence les informations ou de les mettre dans une boîte. Il crée une boîte colorée entourant votre texte.{{% /panel %}}


## Usage 

| Paramètre | Par défaut | Description |
|:--|:--|:--|
| header | aucun | Le titre du panneau. Si spécifié, ce titre sera affiché dans sa propre ligne d'en-tête. |
| footer | aucun | le pied de page du panneau. Si spécifié, ce texte sera affiché dans sa propre ligne |
| theme | `primary` | `default`,`primary`,`info`,`success`,`warning`,`danger` |

## Exemple basique

Par défaut :

	{{%/* panel */%}}ceci est un texte panel (dans un panneau){{%/* /panel */%}}

{{%panel%}}ceci est un texte panel (dans un panneau){{%/panel%}}

## Panneau avec Titre

Ajoutez facilement un conteneu de titre à votre panneau avec le paramètre `header`. Vous pouve l'appliquer sur tous les thèmes.

	{{%/* panel theme="danger" header="Titre du Panneau" */%}}ceci est un texte panel (dans un panneau){{%/* /panel */%}}

{{% panel theme="danger" header="Titre du Panneau" %}}ceci est un texte panel (dans un panneau){{% /panel %}}

	{{%/* panel theme="success" header="Titre du Panneau" */%}}ceci est un texte panel (dans un panneau){{%/* /panel */%}}

{{% panel theme="success" header="Titre du Panneau" %}}ceci est un texte panel (dans un panneau){{% /panel %}}

## Panneau avec pied de page
Emballez un texte secondaire en pied de panneau.

	{{%/* panel footer="pied de page du panneau" */%}}Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.{{%/* /panel */%}}

{{% panel footer="pied de page du panneau" %}}
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
{{% /panel %}}

## Thèmes

{{% panel theme="success" header="Thème Success" %}}ceci est un texte panel (dans un panneau){{% /panel %}}
{{% panel theme="default" header="Thème Default" %}}ceci est un texte panel (dans un panneau){{% /panel %}}
{{% panel theme="primary" header="Thème Primary" %}}ceci est un texte panel (dans un panneau){{% /panel %}}
{{% panel theme="info" header="Thème Info" %}}ceci est un texte panel (dans un panneau){{% /panel %}}
{{% panel theme="warning" header="Thème Warning" %}}ceci est un texte panel (dans un panneau){{% /panel %}}
{{% panel theme="danger" header="Thème Danger" %}}ceci est un texte panel (dans un panneau){{% /panel %}}
