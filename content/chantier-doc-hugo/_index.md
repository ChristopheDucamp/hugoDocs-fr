+++
title = "Chantier Doc Hugo : Organisation"
description = "organiser, organiser"
weight = 200
+++

Avec **Hugo**, les pages sont le coeur de votre site. Organisez votre site comme tout autre projet Hugo. **La magie opère avec l'implémentation des sections réalisée dans la v0.22 de Hugo (bravo @bep)**.

Avec docDock, **chaque page de contenu compose le menu**. Les pages de contenus façonnent la structure de votre site web.

Pour relier les pages les unes aux autres, placez-les dans une hiérarchie de dossiers. 

```
content
├── niveau-un
│   ├── niveau-deux
│   │   ├── niveau-trois
│   │   │   ├── niveau-quatre
│   │   │   │   ├── _index.md
│   │   │   │   ├── page-4-a.md
│   │   │   │   ├── page-4-b.md
│   │   │   │   └── page-4-c.md
│   │   │   ├── _index.md
│   │   │   ├── page-3-a.md
│   │   │   ├── page-3-b.md
│   │   │   └── page-3-c.md
│   │   ├── _index.md
│   │   ├── page-2-a.md
│   │   ├── page-2-b.md
│   │   └── page-2-c.md
│   ├── _index.md
│   ├── page-1-a.md
│   ├── page-1-b.md
│   └── page-1-c.md
├── _index.md
└── page-top.md
```


{{%note %}} **_index.md** est requis dans chaque dossier, c'est votre "page d'accueil de dossier"
{{%/note%}}


### Ajoutez une icône à une entrée de menu

Dans le front matter de la page, ajoutez un paramètre `pre` pour insérer tout code HTML avant l'étiquette du menu : 

exemple pour afficher une icône github :

	+++
	title = "repo Github"
	pre ="<i class='fa fa-github'></i> "
	+++

![dsf](https://monosnap.com/file/5QFj1mxo5R4N8bkGX6BTsgoGhsx0H7.png)

<!-- ### Customize menu entry label

Add a `name` param next to `[menu.main]`

	+++
	[menu.main]
	parent = ""
	identifier = "repo"
	pre ="<i class='fa fa-github'></i> "
	name = "Github repo"
	+++ -->

<!-- ### Créer une redirection de page
Ajoutez un paramètre `url` à côté de `[menu.main]`

	+++
	[menu.main]
	parent = "page"
	identifier = "page-images"
	weight = 23
	url = "/shortcode/image/"
	+++

{{%note%}}Look at the menu "Create Page/About images" which redirects to "Shortcodes/image{{%/note%}}
 -->
### Ordre des entrées groupées de menu/page

dans votre frontmatter ajoutez le param `weight` avec un nombre pour trier.

	+++
	title="Ma page"
	weight = 4
	+++


### Cacher une entrée de menu

dans votre frontmatter ajoutez le parma `hidden=true`.

	+++
	title="Ma page"
	hidden = true
	+++


### Menu déplié par défaut

Une ou plusieurs entrées de menu peuvent être affichées dépliées par défaut. (Comme l'entrée du menu "Démarrer" sur ce site web.)

dans votre frontmatter ajoutez le param `alwaysopen=true`.
exemple :

```
title = "Démarrage"
description = ""
weight = 1
alwaysopen = true
```

### Structure de dossier et nom de fichier

Organisation de Contenu **est** votre structure de dossier  `content`.

### Page d'accueil

Pour indiquer au thème Hugo docDock de considérer une page comme un contenu de page d’accueil, créez simplement un fichier de contenu appelé `_index.md` dans le dossier `content`.






