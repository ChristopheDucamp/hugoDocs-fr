---
title: Installer Hugo
linktitle: Installer Hugo
description: Installer Hugo sur macOS, Windows, Linux, FreeBSD et sur toute machine où peut tourner l'outil de compilation Go.
date: 2016-11-01
publishdate: 2016-11-01
lastmod: 2017-07-22
categories: [démarrage, fondamentaux,fundamentals]
authors: [Michael Henderson]
#tags: [installer,pc,windows,linux,macos,binary,tarball,installation]
weight: 30
sections_weight: 30
draft: false
aliases: [/demarrage/installer-hugo/]
toc: true
---

{{% note %}}
Il y a eu beaucoup de discussions à propos d'Hugo étant écrit en Go, mais vous n'avez pas besoin d'installer Go pour apprécier Hugo. Piquez juste une binaire précompilée !
{{% /note %}}

Hugo est écrit en [Go][1] avec le support de nombreuses plates-formes. La dernière version peut être trouvée sur [Hugo Releases][2].

Hugo fournit actuellement des binaires pré-construites pour : 

* <i class="icon-apple"></i> macOS (Darwin) for x64, i386, et les architectures ARM
* <i class="icon-windows"></i> Windows
* <i class="icon-linux"></i> Linux
* <i class="icon-freebsd"></i> FreeBSD

Hugo peut également être compilé à partir de la source partout où la chaîne d'outils du compilateur Go peut s'exécuter; par ex. pour d'autres systèmes d'exploitation comme DragonFly BSD, OpenBSD, Plan 9, Solaris et d'autres. Regardez <http://golang.org/doc/install/source> pour accéder ) l'ensemble complet des combinaisons prises en charge des systèmes d'exploitation cibles et des architectures de compilation.

## Installation rapide

### Binaire (Inter-plateformes)

Téléchargez la version appropriée pour votre plate-forme à partir de [Hugo Releases][2]. Une fois téléchargée, la binaire peut être exécutée à partir de n'importe où. Vous n'avez pas besoin de l'installer dans un emplacement global. Cela fonctionne bien pour les hôtes partagés et d'autres systèmes où vous n'avez pas de compte privilégié.

Idéalement, vous devriez l'installer quelque part dans votre `PATH` pour une utilisation facile. `/usr/local/bin` est l'emplacement le plus probable.


### Homebrew (macOS)

Si vous êtes sur MacOS et si vous utilisez [Homebrew][3],  vous pouvez installer Hugo avec la commande qui suit :
```bash
`brew install hugo`.
```
Pour des explications plus détaillées, suivez les guides d'installation en-dessous pour installer sur macOS et Windows.

### Chocolatey (Windows)

Si vous êtes sur une machine Windows machine et si vous utilisez [Chocolatey](https://chocolatey.org/) pour le gestionnaire de packages, vous pouvez installez Hugo avec la commande suivante :

{{% code file="install-with-chocolatey.ps1" %}}
```powershell
choco install hugo -confirm
```
{{% /code %}}

### Source

### Outils pré-requis

  * [Git](http://git-scm.com/)
  * [Go 1.5+](https://golang.org/dl/)
  * [govendor](https://github.com/kardianos/govendor)

#### Dépendances Fournisseurs

Hugo utilise [govendor][16] pour les dépendances de fournisseurs, mais nous ne committons pas les packages des fournisseurs vers le repo git Hugo. Par conséquent, un simple `go get` n'est pas supporté. Vous **devez utiliser govendor** pour récupérer les dépendances d'Hugo.

#### Récupérer à partir de GitHub
{{% code file="from-gh.sh" %}}
```sh
go get github.com/kardianos/govendor
govendor get github.com/gohugoio/hugo
go install github.com/gohugoio/hugo
```
{{% /code %}}

`govendor get` récupéra Hugo et toutes ses bibliothèques dépendantes vers `$GOPATH/src/github.com/gohugoio/hugo`, et `go install` compile  tout à l'itnérieur d'un exécutable final `hugo` (ou `hugo.exe`) executable à l'intérieur de `$GOPATH/bin/`.

{{% note %}}
Si vous êtes utilisateur Windows, substituez la variable d'environnement `$HOME` ci-dessus par `%USERPROFILE%`.
{{% /note %}}

## <i class="icon-apple"></i>macOS

### Hypothèses

  1. Vous savez ouvrir le terminal macOS.
  2. Vous tournez sur un Mac moderne 64-bit.
  3. Vous utiliserez `~/Sites` comme point de départ pour votre. (`~/Sites` est utilisé à des fins d'exemple. Si vous êtes suffisamment à l'aise avec la ligne de commande et le système de fichiers, vous ne devriez pas avoir de problèmes à suivre les instructions.)

### Choisissez votre méthode

Il existe trois moyens d'installer Hugo sur votre Mac

  1. L'utilitaire [Homebrew](https://brew.sh/) `brew`
  2. La distribution (tarball)
  3. La construction à partir de la Source

Il n'y a pas de "meilleure" manière d'installer Hugo sur votre Mac.
Vous devriez utiliser la méthode qui correspondra le mieux à votre cas d'utilisation.

#### Pours et Contres

Il y a des pours et contres pour chacune des méthodes mentionnées au-dessus : 

  1. **Homebrew.** Homebrew est la méthode la plus simple et n'exigera qu'un minimum de travail pour la maintenance. Les inconvénients ne sont pas énormes. Le package par défaut sera la version la plus récente, par conséquent elle n'aura pas de bugs à réparer jusqu'à la prochaine version (c-a-d. qu'à moins que vous ne l'installiez avec l'option `--HEAD`). La version `brew` de Hugo peut avoir quelques jours de décalage parce qu'elle n'est pas coordonnée avec une autre équipe. Cependant, `brew` est la méthode d'installation recommandée si vous voulez travailler à partir d'une source stable et largement utilisée. Brew fonctionne bien et reste facile à mettre à jour.

  2. **Tarball.** Télécharger et installer à partir de la tarball est aussi facile, même si cela requiert un peu plus de talents en ligne de commande que sur Homebrew. Les mises à jour sont ausi faciles : vous répétez simplement le processus avec la nouvelle binaire. Ceci vous donne la flexibilité d'avoir plusieurs versions sur votre ordi. Si vous ne voulez pas utiliser `brew`, alors la tarball/binaire est un bon choix.

  3. **Construire à partir de la source.** Construire à partir de la source demande le plus de travail. L'avantage de construire à partir de la source est que vous n'avez pas à attendre une version pour ajouter des fonctionnalités ou des réparations de bugs. L'inconvénient est que vous devez passer plus de temps à gérer l'installation, ce qui est faisable mais demande plus de temps que les deux options précédentes.


{{% note %}}
Étant donné que la construction à partir de la source est attrayante pour les utilisateurs de ligne de commande plus expérimentés, ce guide se concentrera davantage sur l'installation de Hugo via Homebrew et Tarball.
{{% /note %}}

### Installer Hugo avec Brew

#### Étape 1 : Installez `brew` si vous ne l'avez pas déjà

Allez sur le site web de `brew` website, [https://brew.sh/](https://brew.sh/), et suivez les directions. L'étape la plus importante est l'installation à partir de la ligne de commande : 

{{% code file="install-brew.sh" %}}
```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
{{% /code %}}

#### Étape 2 : Lancez la commande `brew` pour installer  `hugo`

Installer Hugo en utilisant `brew` est aussi facile que ce qui suit :

{{% code file="install-brew.sh" %}}
```bash
brew install hugo
```
{{% /code %}}
Si Homebrew fonctionne bien, vous devriez voir quelque chose de similaire à ce qui suit : 

    ==> Downloading https://homebrew.bintray.com/bottles/hugo-0.21.sierra.bottle.tar.gz
    ######################################################################### 100.0%
    ==> Pouring hugo-0.21.sierra.bottle.tar.gz
    🍺  /usr/local/Cellar/hugo/0.21: 32 files, 17.4MB

{{% note "Installer la Dernière Version Hugo avec Brew" %}}
Remplacez `brew install hugo` par `brew install hugo --HEAD` si vous voulez la dernière version "in-development".
{{% /note %}}

`brew` devrait avoir mis à jour votre chemin pour inclure Hugo. Vous pouvez confirmer en ouvrant une nouvelle fenêtre de terminal et en lançant quelques commandes :

```bash
$ # show the location of the hugo executable
which hugo
/usr/local/bin/hugo

# show the installed version
ls -l $( which hugo )
lrwxr-xr-x  1 mdhender admin  30 Mar 28 22:19 /usr/local/bin/hugo -> ../Cellar/hugo/0.13_1/bin/hugo

# verify that hugo runs correctly
hugo version
Hugo Static Site Generator v0.13 BuildDate: 2015-03-09T21:34:47-05:00
```

### Installer Hugo à partir de la Tarball

#### Étape 1 : Décider de l'endroit

Lors de l'installation à partir du tarball, vous devez décider si vous installez la binaire dans `/usr/local/bin` ou dans votre répertoire personnel. Il y a trois camps à ce sujet :

  1. Installez dans `/usr/local/bin` afin que tous les utilisateurs sur votre système puissent y avoir accès. C'est une bonne idée car c'est un endroit assez standard pour les exécutables. L'inconvénient est que vous pourriez avoir besoin de privilèges élevés pour mettre le logiciel dans cet endroit. En outre, s'il y a plusieurs utilisateurs sur votre système, tous exécuteront la même version. Parfois, cela peut être un problème si vous voulez essayer une nouvelle version.

  2. Installez-le dans `~/bin` pour que vous seul vous puissiez l'exécuter. C'est une bonne idée car c'est facile à faire, facile à entretenir et ne nécessite pas de privilèges élevés. L'inconvénient est que seul vous pouvez exécuter Hugo. S'il y a d'autres utilisateurs sur votre site, ils doivent conserver leurs propres copies. Cela peut conduire à des personnes qui utilisent différentes versions. Bien sûr, cela vous permet d'expérimenter différentes versions.

  3. Installez-le dans votre répertoire `Sites`. Ce n'est pas une mauvaise idée si vous avez un seul site que vous construisez. Cela garde tout dans un seul endroit. Si vous souhaitez essayer de nouvelles versions, vous pouvez faire une copie de l'intégralité du site et mettre à jour l'exécutable Hugo.

Les trois emplacements fonctionneront pour vous. Dans l'intérêt de la brièveté, ce guide se concentre sur l'option n° 2.

#### Étape 2 : Téléchargez la Tarball

  1. Ouvrez <https://github.com/gohugoio/hugo/releases> dans votre navigateur.

  2. Trouvez la version actuelle en faisant défiler vers le bas et en recherchant la balise verte qui lit "Latest release".

   3. Téléchargez le tarball actuel pour Mac. Le nom sera quelque chose comme `hugo_X.Y_osx-64bit.tgz`, où `X.YY` est le numéro de version.

   4. Par défaut, le tarball sera enregistré dans votre répertoire `~/Downloads`. Si vous choisissez d'utiliser un emplacement différent, vous devrez changer cela dans les étapes suivantes.

#### Étape 3 : Confirmez votre téléchargement

Vérifiez que la tarball n'a pas été corrompue durant le téléchargement : 

    tar tvf ~/Downloads/hugo_X.Y_osx-64bit.tgz
    -rwxrwxrwx  0 0      0           0 Feb 22 04:02 hugo_X.Y_osx-64bit/hugo_X.Y_osx-64bit.tgz
    -rwxrwxrwx  0 0      0           0 Feb 22 03:24 hugo_X.Y_osx-64bit/README.md
    -rwxrwxrwx  0 0      0           0 Jan 30 18:48 hugo_X.Y_osx-64bit/LICENSE.md


Les fichiers `.md` sont la  documentation pour Hugo. L'autre fichier est l'exécutable.

#### Étape 4 : Installez Dans votre Répertoire `bin` 

```bash
# create the directory if needed
mkdir -p ~/bin

# make it the working directory
cd ~/bin

# extract the tarball
tar -xvzf ~/Downloads/hugo_X.Y_osx-64bit.tgz
Archive:  hugo_X.Y_osx-64bit.tgz
  x ./
  x ./hugo
  x ./LICENSE.md
  x ./README.md

# verify that it runs
./hugo version
Hugo Static Site Generator v0.13 BuildDate: 2015-02-22T04:02:30-06:00

```

Vous devrez peut-être ajouter votre répertoire bin à votre variable `PATH`. La commande `which`  vérifiera pour nous. Si elle peut trouver `hugo`, elle imprimera le chemin complet. Sinon, elle n'imprimera rien.

```bash
# check if hugo is in the path
which hugo
/Users/USERNAME/bin/hugo
```

Si `hugo` n'est pas dans votre `PATH`, ajoutez-le en mettant à jour votre fichier  `~/.bash_profile`. Démarrez un éditeur :

```bash
nano ~/.bash_profile
```

Ajoutez une ligne pour mettre à jour votre variable `PATH` :
```bash
export PATH=$PATH:$HOME/bin
```

Ensuite, enregistrez le fichier en appuyant sur Control-X, puis sur Y pour enregistrer le fichier et revenir à l'invite.

Fermez le terminal et ouvrez un nouveau terminal pour récupérer les modifications apportées à votre profil. Vérifiez votre réussite en exécutant à nouveau la commande `what hugo`.

Vous avez installé Hugo avec succès.

### Construction à partir de la Source sur Mac

Si vous souhaitez compiler Hugo vous-même, vous devrez installer Go (aka Golang). Vous pouvez [installer Go directement à partir du site Web Go] (https://golang.org/dl/) ou via Homebrew en utilisant la commande suivante:

```bash
brew install go
```

#### Étape 1 : Récupérez la Source

If you want to compile a specific version of Hugo, go to [https://github.com/gohugoio/hugo/releases](https://github.com/gohugoio/hugo/releases) and download the source code for the version of your choice. If you want to compile Hugo with all the latest changes (which might include bugs), clone the Hugo repository:

```bash
git clone https://github.com/gohugoio/hugo
```
{{% warning "Sometimes \"Latest\" = \"Bugs\""%}}
Cloning the Hugo repository directly means taking the good with the bad. By using the bleeding-edge version of Hugo, you make your development susceptible to the latest features, as well as the latest bugs. Your feedback is appreciated. If you find a bug in the latest release, [please create an issue on GitHub](https://github.com/gohugoio/hugo/issues/new).
{{% /warning %}}


#### Step 2: Compiling

Make the directory containing the source your working directory and then fetch Hugo's dependencies:

```bash
mkdir -p src/github.com/gohugoio
ln -sf $(pwd) src/github.com/gohugoio/hugo

# set the build path for Go
export GOPATH=$(pwd)

go get
```

This will fetch the absolute latest version of the dependencies. If Hugo fails to build, it may be the result of a dependency's author introducing a breaking change.

Once you have properly configured your directory, you can compile Hugo using the following command:

```bash
go build -o hugo main.go
```

Then place the `hugo` executable somewhere in your `$PATH`. You're now ready to start using Hugo.


## Windows

Ce qui suit suppose être un guide complet pour installer Hugo sur votre PC Windows.

### Hypothèses

  1. Vous utiliserez `C:\Hugo\Sites` comme point de départ pour votre nouveau projet.
  2. Vous utiliserez `C:\Hugo\bin` pour stocker les fichiers exécutables.

### Installez vos Répertoires

Vous aurez besoin d'un endroit pour stocker l'exécutable Hugo, votre  [contenu](https://gohugo.io/content-management/), et le site web généré par Hugo :

  1. Ouvrez Windows Explorer.
  2. Créez un nouveau dossier : `C:\Hugo`, en supposant que vous voulez Hugo sur votre disque C, bien que cela puisse aller ailleurs
  3. Créez un nouveau sous-dossier dans le dossier Hugo : `C:\Hugo\bin`
  4. Créez un nouveau sous-dossier dans Hugo : `C:\Hugo\Sites`

### Utilisateurs Techniques

  1. Téléchargez le dernier exécutable Hugo compressé à partir de [Hugo Releases](https://github.com/gohugoio/hugo/releases).
  2. Extrayez tous les contenus vers votre dossier  `..\Hugo\bin`.
  3. L'exécutable `hugo` sera nommé sous `hugo_hugo-version_platform_arch.exe`. Renommnez l'exécutable en  `hugo.exe` pour facilité d'utilisation.
  4. Dans PowerShell ou dans votre CLI préféré, ajoutez l'exécutable `hugo.exe` à votre  PATH en navigant vers `C:\Hugo\bin` (ou à l'endroit de votre fichier hugo.exe) et utilisez la commande `set PATH=%PATH%;C:\Hugo\bin`. Si la commande `hugo` ne fonctionne pas après un reboot, vous pourriez avoir à lancer l'invite  de commande en tant qu'administrateur.

### Utilisateurs moins-techniques

  1. Allez à la page [Hugo Releases](https://github.com/gohugoio/hugo/releases).
  2. The latest release is announced on top. Scroll to the bottom of the release announcement to see the downloads. They’re all ZIP files.
  3. Find the Windows files near the bottom (they’re in alphabetical order, so Windows is last) – download either the 32-bit or 64-bit file depending on whether you have 32-bit or 64-bit Windows. (If you don’t know, [see here](https://esupport.trendmicro.com/en-us/home/pages/technical-support/1038680.aspx).)
  4. Move the ZIP file into your `C:\Hugo\bin` folder.
  5. Double-click on the ZIP file and extract its contents. Be sure to extract the contents into the same `C:\Hugo\bin` folder – Windows will do this by default unless you tell it to extract somewhere else.
  6. You should now have three new files: hugo executable (e.g. `hugo_0.18_windows_amd64.exe`), `license.md`, and `readme.md`. (You can delete the ZIP download now.) Rename that hugo executable (`hugo_hugo-version_platform_arch.exe`) to `hugo.exe` for ease of use.

Now you need to add Hugo to your Windows PATH settings:

#### Pour utilisateurs Windows 10 :

  * Right click on the **Start** button.
  * Click on **System**.
  * Click on **Advanced System Settings** on the left.
  * Click on the **Environment Variables…** button on the bottom.
  * In the User variables section, find the row that starts with PATH (PATH will be all caps).
  * Double-click on **PATH**.
  * Click the **New…** button.
  * Type in the folder where `hugo.exe` was extracted, which is `C:\Hugo\bin` if you went by the instructions above. _The PATH entry should be the folder where Hugo lives and not the binary._ Press Enter when you’re done typing.
  * Click OK at every window to exit.

The path editor in Windows 10 was added in the large [November 2015 Update](https://blogs.windows.com/windowsexperience/2015/11/12/first-major-update-for-windows-10-available-today/). You’ll need to have that or a later update installed for the above steps to work. You can see what Windows 10 build you have by clicking on the __ Start button → Settings → System → About. See [here](https://www.howtogeek.com/236195/how-to-find-out-which-build-and-version-of-windows-10-you-have/) for more.)

#### Pour utilisateurs Windows 7 et 8.x :

Windows 7 and 8.1 do not include the easy path editor included in Windows 10, so non-technical users on those platforms are advised to install a free third-party path editor like [Windows Environment Variables Editor](http://eveditor.com/) or [Path Editor](https://patheditor2.codeplex.com/).

### Verifez l'Exécutable

Run a few commands to verify that the executable is ready to run, and then build a sample site to get started.

#### 1. Ouvrir une ligne de commande

At the prompt, type `hugo help` and press the Enter key. You should see output that starts with:

    hugo is the main command, used to build your Hugo site.

    Hugo is a Fast and Flexible Static Site Generator
    built with love by spf13 and friends in Go.

    Complete documentation is available at https://gohugo.io/.


If you do, then the installation is complete. If you don’t, double-check the path that you placed the `hugo.exe` file in and that you typed that path correctly when you added it to your `PATH` variable. If you’re still not getting the output, search the [Hugo discussion forum](https://discourse.gohugo.io) to see if others have already figured out our problem. If not, add a note—in the “Support” category—and be sure to include your command and the output.

At the prompt, change your directory to the `Sites` directory.

    C:\Program Files> cd C:\Hugo\Sites
    C:\Hugo\Sites>


#### 2. Lancez la Commande

Run the command to generate a new site. I’m using `example.com` as the name of the site.

    C:\Hugo\Sites> hugo new site example.com


You should now have a directory at `C:\Hugo\Sites\example.com`. Change into that directory and list the contents. You should get output similar to the following:

    C:\Hugo\Sites&gt;cd example.com
    C:\Hugo\Sites\example.com&gt;dir
    &nbsp;Directory of C:\hugo\sites\example.com
    &nbsp;
    04/13/2015  10:44 PM    <DIR>          .
    04/13/2015  10:44 PM    <DIR>          ..
    04/13/2015  10:44 PM    <DIR>          archetypes
    04/13/2015  10:44 PM                83 config.toml
    04/13/2015  10:44 PM    <DIR>          content
    04/13/2015  10:44 PM    <DIR>          data
    04/13/2015  10:44 PM    <DIR>          layouts
    04/13/2015  10:44 PM    <DIR>          static
                   1 File(s)             83 bytes
                   7 Dir(s)   6,273,331,200 bytes free


### Problème Installation Windows 

[@dhersam](https://github.com/dhersam) a créé une belle vidéo sur les problèmes connus : 

<div style="position:relative;height:0;padding-bottom:56.25%"><iframe src="https://www.youtube.com/embed/c8fJIRNChmU?ecver=2" width="640" height="360" frameborder="0" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></div>

## Linux

### Debian et Ubuntu

Pour toutes les [distributions Linux qui supportent  snaps](https://snapcraft.io/docs/core/install):

    sudo apt install hugo


#### Pours

  * Package natif Debian/Ubuntu maintenu par les développeurs Debian
  * Script d'achèvement bash pré-installé et pages `man`

#### Cons

  * Peut ne pas être la dernière version, surtout si vous utilisez une version plus ancienne et stable (par exemple, Ubuntu 16.04 LTS). Jusqu'à ce que les backports et les PPA soient disponibles, vous pouvez envisager d'installer le package instantané Hugo pour obtenir la dernière version de Hugo, comme décrit ci-dessous.


### Arch 

Vous pouvez aussi installer Hugo à partir du [repo Arch user][6] sur Arch Linux ou des dérivés tels que Manjaro.

Soyez conscients que Hugo est construit à partir de la source. Ce qui veut dire que des outils complémentaires comme [Git][7] et [Go][8] seront tout aussi bien installés.

    sudo pacman -S yaourt
    yaourt -S hugo


### Fedora, CentOS, and Red Hat

  * [https://copr.fedorainfracloud.org/coprs/spf13/Hugo/](https://copr.fedorainfracloud.org/coprs/spf13/Hugo/) (mis à jour vers  Hugo v0.16)
  * [https://copr.fedorainfracloud.org/coprs/daftaupe/hugo/](https://copr.fedorainfracloud.org/coprs/daftaupe/hugo/) (mis à jour vers  Hugo v0.22) ; sortie généralement quelques jours après la version Hugo officielle.

Voir la [discussion en rapport sur les forums Hugo](https://discourse.gohugo.io/t/solved-fedora-copr-repository-out-of-service/2491).


### Package Snap

Dans n'importe lesquelles des [distributions Linux qui supporent snap][10]:


    snap install hugo


> Note : Hugo-as-a-snap ne peut écrire qu'à l'intérieur du répertoire `$HOME` de l'utilisateur—et des répertoire montés-gvfs possédés par l'utilisateur—du fait du confinement de Snap et de son modèle de sécurité. Plus d'infos disponibles [dans cette issue en rapport sur GitHub][11].


## Mettre à jour Hugo

Mettre à jour Hugo est aussi facile que de télécharger et remplacer l'exécutable que vous avez posé dans votre `PATH`.

Sur macOS, si vous avez [Homebrew][3], mettre à jour est encore plus facile : lancez simplement la commande `brew upgrade hugo`.


### Installer Pygments (facultatif)

L'exécutable Hugo a une dépendance externe _facultative_ pour l'enluminure du code source ([Pygments](https://pygments.org)).

Si vous voulez disposer de la mise en beauté du code source en utilisant le [racccourci-code hightlight][4], vous devrez installer le programme Pygments basé sur Python. La procédure est décrite sur la [page d'accueil Pygments][5].


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
