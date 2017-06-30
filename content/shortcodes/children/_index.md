+++
title = "children"
description = "Liste les pages parents d'une page"
+++

Utilisez le raccourci-code `children` pour lister les pages enfants d'une page et des autres descendants (enfants). Par défaut, le raccourci-code affiche les liens vers les pages enfants.

## Usage

| Paramètres | Défaut | Description |
|:--|:--|:--|
| style | "li" | Choisir le style utilisé pour afficher les descendants. Ce pourrait être n'importe quel nom de balise HTML |
| showhidden | "false" | Si `true`, les pages enfants cachées par le menu seront affichées |
| description  | "false" | Vous permet d'inclure un petit texte sous chaque page dans la liste.<br/>Si aucune description n'existe pour la page, le raccourci-code prend les 70 premiers mots de votre contenu. [lire plus d'info sur les résués sur gohugo.io](https://gohugo.io/content/summaries/)  |
| depth | 1 | Entrez un nombre pour spécifier la profondeur des descendants à afficher. Par exemple, si la valeur est 2, le raccourci-code affichera 2 niveaux de pages enfants. {{%alert success%}}**Trucs :** réglez le à 999 pour obtenir tous les  descendants{{%/alert%}}|
| sort | none | Triez les enfants par <br><li><strong>Weight</strong> - pour trier sur l'ordre du menu</li><li><strong>Name</strong> - pour trier alphabétiquement par étiquette du menu </li><li><strong>Identifier</strong> - pour trier alphabétiquement sur l'identifiant réglé dans le frontmatter</li><li><strong>URL</strong> - URL</li> |



## Démo

	{{%/* children  */%}}

{{%children %}}

	{{%/* children description="true"   */%}}

{{%children description="true"   %}}

	{{%/* children showhidden="true" */%}}

{{% children showhidden="true" %}}

	{{%/* children style="h3" depth="3" description="true" */%}}

{{% children style="h3" depth="3" description="true" %}}

	{{%/* children style="div" depth="999" */%}}

{{% children style="div" depth="999" %}}






