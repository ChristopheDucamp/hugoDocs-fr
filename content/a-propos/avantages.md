---
title: Les Avantages des Générateurs de Sites Statiques
linktitle: Les Avantages du Statique
description: Performance accrue, sécurité et facilité d'utilisation sont juste quelques-unes des raisons pour lesquelles les générateurs de site statique sont si tentants.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
#tags: [ssg,statique,performance,sécurité, statique, gss]
draft: false
aliases: []
toc: false
---
Le but des générateurs de sites Web est de transformer le contenu en fichiers HTML. La plupart sont des "générateurs de sites dynamiques". Cela signifie que le serveur HTTP ---c'est-à-dire le programme qui envoie des fichiers à afficher dans le navigateur--- exécute le générateur pour créer un nouveau fichier HTML chaque fois qu'un utilisateur final demande une page.

Au fil du temps, des générateurs de sites dynamiques ont été programmés pour mettre en cache leurs fichiers HTML afin d'éviter des retards inutiles dans la livraison de pages aux utilisateurs finaux. Une page en cache est une version statique d'une page Web.

Hugo prend la mise en cache un peu plus loin et tous les fichiers HTML sont rendus sur votre ordinateur. Vous pouvez consulter les fichiers localement avant de les copier sur l'ordinateur hébergeant le serveur HTTP. Étant donné que les fichiers HTML ne sont pas générés dynamiquement, nous disons que Hugo est un *générateur de site statique*.

Il y a de nombreux avantages à cela, le plus remarquable étant la performance. Les serveurs HTTP sont *très* bons pour envoyer des fichiers ---donc bon, en fait vous pouvez servir avec efficacité le même nombre de pages avec une fraction de la mémoire et la CPU nécessaires pour un site dynamique.

## Plus sur les Générateurs de Site Statiques
* [Passer au Statique: 5 raisons de tester la JAMstarck sur votre prochain projet, Frank Taillandier](https://jamstatic.fr/2017/03/16/5-raisons-de-tester-la-jamstack/)
* ["An Introduction to Static Site Generators", David Walsh][]
* ["Hugo vs. Wordpress page load speed comparison: Hugo leaves WordPress in its dust", GettingThingsTech][hugovwordpress]
* ["Static Site Generators", O-Reilly][]
* [StaticGen: Top Open-Source Static Site Generators (GitHub Stars)][]
* ["Top 10 Static Website Generators", Netlify blog][]
* ["The Resurgence of Static", dotCMS][dotcms]


["An Introduction to Static Site Generators", David Walsh]: https://davidwalsh.name/introduction-static-site-generators
["Static Site Generators", O-Reilly]: /documents/oreilly-static-site-generators.pdf
["Top 10 Static Website Generators", Netlify blog]: https://www.netlify.com/blog/2016/05/02/top-ten-static-website-generators/
[hugovwordpress]: https://gettingthingstech.com/hugo-vs.-wordpress-page-load-speed-comparison-hugo-leaves-wordpress-in-its-dust/
[StaticGen: Top Open-Source Static Site Generators (GitHub Stars)]: https://www.staticgen.com/
[dotcms]: https://dotcms.com/blog/post/the-resurgence-of-static
