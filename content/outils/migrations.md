---
title: Migrer vers Hugo
linktitle: Migrations
description: Une liste des outils développés par la communauté pour migrer à partir de votre générateur de site statique existant ou à partir de votre système de gestion de contenu vers Hugo.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-23
#tags: [migrations,jekyll,wordpress,drupal,ghost,contentful]
draft: false
aliases: [/developer-tools/migrations/,/developer-tools/migrated/]
toc: true
---

Cette section présente quelques projets en rapport avec Hugo et développés de manière indépendante. Ces outils tentent d'étendre la fonctionnalité de notre générateur de site statique ou de vous aider à démarrer.

{{% note %}}
Connaissez-vous ou maintenez-vous un projet similaire en rapport ave Hugo ? N'hésitez pas à ouvrir une [pull request](https://github.com/gohugoio/hugo/pulls) sur GitHub si vous pensez que votre projet pourrait être ajouté.
{{% /note %}}

Jetez un oeil à cette liste d'outils de migration si vous utilisez actuellement d'autres outils de journalisation tels que Jekyll ou WordPress, mais que vous ayez l'intention de remplacer par Hugo. Ils prendront soin d'exporter votre contenu en formats amis avec Hugo.

## Jekyll

Alternativement, vous pouvez utiliser la nouvelle [commande Jekyll import](/commandes/hugo_import_jekyll/).

- [JekyllToHugo](https://github.com/SenjinDarashiva/JekyllToHugo) - Un petit script pour convertir les posts de blog de Jekyll vers un site Hugo.
- [ConvertToHugo](https://github.com/coderzh/ConvertToHugo) - Convertit votre blog de Jekyll vers Hugo.

## Ghost

- [ghostToHugo](https://github.com/jbarone/ghostToHugo) - Convertit les post de blog et les exporte vers Hugo.

## Octopress

- [octohug](https://github.com/codebrane/octohug) - migrateur de Octopress vers Hugo.

## DokuWiki

- [dokuwiki-to-hugo](https://github.com/wgroeneveld/dokuwiki-to-hugo) - Migre vos pages source de dokuwiki à partir de la  [syntaxe DokuWiki](https://www.dokuwiki.org/wiki:syntax) en syntaxe Markdown Hugo. Inclut des bonus comme le plugin TODO. Écrit avec une extensibilité à l'esprit en utilisant python 3. Génère également un en-tête TOML pour chaque page. Conçu pour copier-coller le répertoire wiki dans votre répertoire `/content`.

## WordPress

- [Wordpress-to-hugo-exporter](https://github.com/SchumacherFM/wordpress-to-hugo-exporter) - Un plugin WordPress-en-un-clic qui convertit tous les messages, pages, taxonomies, métadonnées et paramètres en Markdown et YAML qui peuvent être jetés dans Hugo. (Remarque: Si vous avez du mal à utiliser ce plugin, vous pouvez [exporter votre site pour Jekyll](https://wordpress.org/plugins/jekyll-exporter/) et utiliser le convertisseur Jekyll intégré de Hugo indiqué ci-dessus.)

## Tumblr

- [tumblr-importr](https://github.com/carlmjohnson/tumblr-importr)  - Un importateur qui utilise l'API Tumblr pour créer un site statique Hugo.
- [tumblr2hugomarkdown](https://github.com/Wysie/tumblr2hugomarkdown) - Exporte tout votre contenu de Tumblr en fichiers Markdown Hugo avec un format original conservé.
- [Tumblr to Hugo](https://github.com/jipiboily/tumblr-to-hugo) - Un outil de migration qui convertit chacun de vos messages de Tumblr en un fichier de contenu avec un titre et un chemin approprié. En outre, "Tumblr to Hugo" crée un fichier CSV avec l'URL originale et le nouveau chemin sur Hugo, pour vous aider à configurer les redirections.

## Drupal

- [drupal2hugo](https://github.com/danapsimer/drupal2hugo) - Convertissez un site Drupal en Hugo.


## Joomla

- [Hugojoomla](https://github.com/davetcc/hugojoomla) - Cet utilitaire écrit en Java prend une base de données Joomla et convertit tout le contenu en fichiers Markdown. Il modifie toutes les URL qui sont dans le format interne de Joomla et les convertit en une forme appropriée.

## Blogger

- [blogimport](https://github.com/natefinch/blogimport) - Un outil pour importer les publications de Blogger vers Hugo.

## Contentful

- [contentful2hugo](https://github.com/ArnoNuyts/contentful2hugo) - Un outil pour créer des fichiers de contenu pour Hugo à partir de contenus sur [Contentful](https://www.contentful.com/).
