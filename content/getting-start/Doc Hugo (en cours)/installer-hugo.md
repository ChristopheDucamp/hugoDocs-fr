+++

title = "Installer Hugo"
description = "Comment installer Hugo sur votre machine."
weight = 3
+++

{{% notice note %}}
[Source "Installing Hugo](https://gohugo.io/overview/installing/ "Permalink to Hugo - Installing Hugo") - documentation officielle Hugo, demeurant le seul lien de référence.
{{% /notice %}}

Hugo est écrit en [Go][1] avec le support de nombreuses plates-formes.

La dernière version peut être trouvée sur [Hugo Releases][2]. Nous proposons actuellement des binaires pré-construits pour {{<icon fa-windows>}}Windows, {{<icon fa-linux>}}Linux, FreeBSD et {{<icon fa-apple>}}OS X (Darwin) pour les architectures x64, i386 et ARM.

Hugo peut également être compilé à partir de la source partout où la chaîne d'outils du compilateur Go peut s'exécuter, par ex. pour d'autres systèmes d'exploitation comme DragonFly BSD, OpenBSD, Plan 9 et Solaris. Voir <http://golang.org/doc/install/source> pour l'ensemble complet des combinaisons prises en charge des systèmes d'exploitation cibles et des architectures de compilation.

## Installer Hugo (binaire)

L'installation est très simple. Téléchargez simplement la version appropriée pour votre plate-forme à partir de [Hugo Releases][2]. Une fois téléchargé, Hugo peut être exécuté à partir de n'importe où. Vous n'avez pas besoin de l'installer dans un emplacement global. Cela fonctionne bien pour les hôtes partagés et d'autres systèmes où vous n'avez pas de compte privilégié.

Idéalement, vous devriez l'installer quelque part dans votre `PATH` pour une utilisation facile. `/usr/local/bin` est l'emplacement le plus probable.

Sur MacOS, si vous avez [Homebrew][3], l'installation est encore plus simple : il suffit d'exécuter `brew install hugo`.

Pour une explication plus détaillée, suivez les guides d'installation correspondants :

### Installer Pygments (facultatif)

L'exécutable Hugo a une dépendance externe _facultative_ pour l'enluminure du code source (Pygments).

Si vous voulez disposer de la mise en beauté du code source en utilisant le [racccourci-code hightlight][4], vous devrez installer le programme Pygments basé sur Python. La procédure est décrite sur la [page d'accueil Pygments][5].

## Mettre à jour Hugo

Mettre à jour Hugo est aussi facile que de télécharger et remplacer l'exécutable que vous avez posé dans votre `PATH`.

Sur macOS, si vous avez [Homebrew][3], mettre à jour est encore plus facile : lancez simplement la commande `brew upgrade hugo`.

## Installer Hugo sur Linux à partir de pacakages natifs

### Arch Linux

Vous pouvez installer Hugo à partir du [repo Arch user][6] sur Arch Linux ou des dérivés tels que Manjaro.
      
    sudo pacman -S yaourt
    yaourt -S hugo
    

Soyez conscients que Hugo est construit à partir de la source. Ce qui veut dire que des outils complémentaires comme [Git][7] et [Go][8] seront tout aussi bien installés.

### Debian et Ubuntu

Hugo a été inclus dans Debian et Ubuntu depuis 2016, et par conséquent, installer Hugo est aussi simple que :

    
    sudo apt install hugo
    

Pros :

* Native Debian/Ubuntu package maintained by Debian Developers
* Pre-installed bash completion script and man pages for best interactive experience

Cons :

* Might not be the latest version, especially if you are using an older stable version (e.g., Ubuntu 16.04 LTS). Until backports and PPA are available, you may consider installing the Hugo snap package to get the latest version of Hugo, as described below.

### Fedora, CentOS et Red Hat

Voir aussi [cette discussion][9].

## Méthodes d'Installation Alternatives

### Snap Package

Dans n'importe lesquelles des [distributions Linux qui supporent snap][10]:
   
    
    snap install hugo
    

> Note : Hugo-as-a-snap can write only inside the user's `$HOME` directory—and gvfs-mounted directories owned by the user—because of Snaps' confinement and security model. More information is also available [in this related GitHub issue][11].

### Image Docker (non officiel)

[Docker Hugo][12] est une image Docker qui peut s'utiliser pour du développement local mais plus important, elle peut être utilisée aisément pour des builds d'intégration continue de votre site Hugo sur  [CircleCI][13] ou [Travis CI][14]. Source disponible sur [GitHub][15].

## Installer à partir de la source

### Outils pré-requis pour télécharger et construire le code source

### Dépendances de vendeurs 

Hugo uses [govendor][16] to vendor dependencies, but we don't commit the vendored packages themselves to the Hugo git repository. Therefore, a simple `go get` is not supported since `go get` is not vendor-aware. You **must use govendor** to fetch Hugo's dependencies.

### Récupérer à partir de GitHub
    
    
    The commands below assume that you have [Go](https://golang.org/dl/) installed with your `$GOPATH` set.
    
    go get github.com/kardianos/govendor
    govendor get github.com/gohugoio/hugo
    

`govendor get` will fetch Hugo and all its dependent libraries to `$GOPATH/src/github.com/gohugoio/hugo`, and compile everything into a final `hugo` (or `hugo.exe`) executable, which you will find sitting inside `$GOPATH/go/bin/`, all ready to go!

_Windows users: where you see the `$HOME` environment variable above, replace it with `%USERPROFILE%`._

_Note: For syntax highlighting using the [highlight shortcode][4], you need to install the Python-based [Pygments][5] program._

## Contribuer

Please see the [contributing guide][17] if you are interested in working with the Hugo source or contributing to the project in any way.

[1]: http://golang.org/
[2]: https://github.com/gohugoio/hugo/releases
[3]: http://brew.sh/
[4]: https://gohugo.io/extras/highlighting/
[5]: http://pygments.org/
[6]: https://aur.archlinux.org/
[7]: https://git-scm.com/
[8]: https://golang.org/doc/install
[9]: https://discourse.gohugo.io/t/solved-fedora-copr-repository-out-of-service/2491
[10]: http://snapcraft.io/docs/core/install
[11]: https://github.com/gohugoio/hugo/issues/3143
[12]: https://hub.docker.com/r/felicianotech/docker-hugo/
[13]: https://circleci.com/
[14]: https://travis-ci.org/
[15]: https://github.com/felicianotech/docker-hugo
[16]: https://github.com/kardianos/govendor
[17]: https://gohugo.io/doc/contributing/

