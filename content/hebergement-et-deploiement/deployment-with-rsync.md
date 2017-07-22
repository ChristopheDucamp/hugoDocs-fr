---
title: Déploiement avec Rysnc
linktitle: Déploiement avec Rysnc
description: Si vous avez accès à votre hébergeur web avec SSH, vous pouvez utiliser une simple commande rsync en une ligne pour déployer incrémentalement la totalité de votre site web Hugo.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
categories: [hébergement et déploiement]
#tags: [tutoriel, rysnc,déploiement]
authors: [Adrien Poupin]
draft: false
aliases: []
toc: true
notesforauthors:
---

## Hypothèses

* Accéder à votre hébergeur web avec SSH
* Un site web fonctionnel construit avec Hugo

Le spoiler est que vous pouvez déployer la totalité de votre site web avec une ligne de commande qui ressemble à ce qui suit :

```bash
hugo && rsync -avz --delete public/ www-data@ftp.topologix.fr:~/www/
```

Comme vous le verrez, nous As you will see, we put it in a shell script file, which makes building and deployment as easy as executing `./deploy`.

Comme vous le verrez, nous l'avons placé dans un fichier de script shell, ce qui rend le développement et le déploiement aussi simple que d'exécuter `./deploy`.

## Installer la Clé SSH

Si ce n'est pas encore fait, nous allons créer un moyen automatisé de SSH vers votre serveur. Si vous avez déjà installé une clé SSH, passez à la section suivante.

D'abord, installez le client ssh. Sur Debian/Ubuntu/ et dérivés, utilisez la commande suivante :

{{% code file="install-openssh.sh" %}}
```bash
sudo apt-get install openssh-client
```
{{% /code %}}

Puis générez votre clé en entrant les commandes suivantes :

```bash
~$ cd && mkdir .ssh & cd .ssh
~/.ssh/$ ssh-keygen -t rsa -q -C "For SSH" -f rsa_id
~/.ssh/$ cat >> config <<EOF
Host HOST
     Hostname HOST
     Port 22
     User USER
     IdentityFile ~/.ssh/rsa_id
EOF
```

N'oubliez pas de remplacer les valeurs `HOST` et `USER` par les vôtres. Puis copiez votre clé publique ssh sur le serveur distant : 

```bash
~/.ssh/$ ssh-copy-id -i rsa_id.pub USER@HOST.com
```

Maintenant vous pouvez facilement vous connecter vers le serveur distant :

```
~$ ssh user@host
Enter passphrase for key '/home/mylogin/.ssh/rsa_id':
```

Et vous avez terminé !

## Script Shell

Nous mettrons la première commande dans un script à la racine de votre arbre Hugo:

```bash
~/websites/topologix.fr$ editor deploy
```

Ici vous mettez le contenu suivant. Remplacez les valeurs `USER`,` HOST` et `DIR` par les vôtres :

```bash
#!/bin/sh
USER=my-user
HOST=my-server.com
DIR=my/directory/to/topologix.fr/   # might sometimes be empty!

hugo && rsync -avz --delete public/ ${USER}@${HOST}:~/${DIR}

exit 0
```

Notez que `DIR` est le chemin relatif de la home de l'utilisateur distant. Si vous devez spécifier un chemin complet (par exemple `/var/www/monsite/`), vous devez modifier `~/${DIR}` par `${DIR}` dans la ligne de commande. Dans la plupart des cas, vous ne devriez pas le faire.

Enregistrez et fermez et créez le fichier exécutable `deploy` :

```
~/websites/topologix.fr$ chmod +x deploy
```

Maintenant vous n'avez qu'à entrer la commande suivante pour déployer et mettre à jour votre site web 

```
~/websites/topologix.fr$ ./deploy
Started building sites ...
Built site for language en:
0 draft content
0 future content
0 expired content
5 pages created
0 non-page files copied
0 paginator pages created
0 tags created
0 categories created
total in 56 ms
sending incremental file list
404.html
index.html
index.xml
sitemap.xml
cours-versailles/index.html
exercices/index.html
exercices/index.xml
exercices/barycentre-et-carres-des-distances/index.html
post/
post/index.html
sujets/index.html
sujets/index.xml
sujets/2016-09_supelec-jp/index.html
tarifs-contact/index.html

sent 9,550 bytes  received 1,708 bytes  7,505.33 bytes/sec
total size is 966,557  speedup is 85.86
```
