+++
title = "alert"
description = "Le raccourci-code alert vous permet de surligner l'information dans votre page."
+++

Le raccourci-code `alert` vous permet de surligner l'information dans votre page. Il crée une boîte coloré entourant votre texte, comme ceci : 

{{%alert%}}**Ceci est une** alerte !{{%/alert%}}
## Usage 

| Paramètre | Par défaut | Description |
|:--|:--|:--|
| theme | `info` | `success`, `info`,`warning`,`danger` |

{{%alert info%}}
**Trucs :** régler uniquement le thème comme argument fonctionne aussi : 
`{{%/*alert warning*/%}}`  au lieu de `{{%/*alert theme="warning"*/%}}`
{{%/alert%}}

## Exemples basiques

	{{%/* alert theme="info" */%}}**ceci** est une info texte{{%/* /alert */%}}
	{{%/* alert theme="success" */%}}**Yeahhh !** est un  texte{{%/* /alert */%}}
	{{%/* alert theme="warning" */%}}**Soyez prudents** est un texte{{%/* /alert */%}}
	{{%/* alert theme="danger" */%}}**Attention !** est un texte{{%/* /alert */%}}

{{% alert theme="info"%}}**ceci** est une info{{% /alert %}}
{{% alert theme="success" %}}**Yeahhh !** est un success{{% /alert %}}
{{% alert theme="warning" %}}**Soyez prudent** est un warning{{% /alert %}}
{{% alert theme="danger" %}}**Attention !** est un danger{{% /alert %}}