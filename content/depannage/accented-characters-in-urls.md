---
title: Caractères Accentués dans les URLs
linktitle: Caractères Accentués dans les URLs
description: Si vous rencontrez des problèmes avec des caractères spéciaux dans vos taxonomies ou les titres ajoutant des caractères étranges à vos URLs.
date: 2017-02-01
publishdate: 2017-02-01
lastmod: 2017-07-22
#tags: [multilingue,special characters]
categories: [dépannage]
menu:
  docs:
    parent: "depannage"
    weight: 200
weight: 200
sections_weight: 200
draft: false
slug:
aliases: [/troubleshooting/categories-with-accented-characters/]
toc: true
---

## Problème : catégories avec des caractères accentués

> Une de mes catégories s'appelle "Le-Carré", mais le lien finit par être généré comme ceci :
>
> `` `Bash
> Catégories / le-carr% C3% A9
> `` `
>
> Et ne fonctionne pas. Y a-t-il une solution facile pour cela que je domine ?

## Solution

Êtes-vous un utilisateur MacOS ? Si tel est le cas, vous êtes probablement une victime de l'insistance du système de fichiers HFS Plus à stocker le caractère "é" (U+00E9) en mode Décomposition normale (NFD), c'est-à-dire sous "e" + "  ́" (U+0065 U+0301).

`le-carr%C3%A9` est réellement correct,`%C3%A9` étant la version UTF-8 de U+00E9 comme prévu par le serveur web. Le problème est que OS X transforme [U+00E9] en [U+0065 U+0301], et donc `le-carr%C3%A9` ne fonctionne plus. Au lieu de cela, seul `le-carre% CC%81` se termine par `e%CC%81` correspondrait à [U +0065 U+0301] à la fin.

Ceci est unique à OS X. Le reste du monde ne le fait pas, et certainement pas votre serveur Web qui fonctionne très probablement avec Linux. Ce n'est pas non plus un problème spécifique à Hugo. D'autres personnes ont été mordues par cela lorsqu'elles ont des caractères accentués dans leurs fichiers HTML.

Notez que ce problème n'est pas spécifique aux scripts latins. Les utilisateurs japonais de Mac rencontrent souvent le même problème ; par exemple avec `だ` se décomposant en `た` et `&#x3099;`. (Lire l'article [Japanese Perl users article][]).

Rsync 3.x à la rescousse ! À partir d'[une réponse postée sur Server Fault][] :

> Vous pouvez utiliser l'option `--iconv` de rsync pour convertir UTF-8 NFC et NFD, au moins si vous êtes sur un Mac. Il existe un jeu de caractères «utf-8-mac» spécial qui représente UTF-8 NFD. Donc, pour copier des fichiers de votre Mac sur votre serveur Web, vous devriez exécuter quelque chose comme :
>
> `rsync -a --iconv=utf-8-mac, utf-8 localdir/monserveurweb:remotedir/`
>
> Cela convertira tous les noms de fichiers locaux de UTF-8 NFD en UF-8 NFC sur le serveur distant. Le contenu des fichiers ne sera pas affecté. - [Server Fault][]

Assurez-vous d'avoir la dernière version de rsync 3.x installée. Le rsync fourni avec OS X est obsolète. Même la version livrée avec 10.10 (Yosemite) est la version 2.6.9. Le flag `--iconv` est nouveau dans rsync 3.x.

### Références Forum de Discussion

* http://discourse.gohugo.io/t/categories-with-accented-characters/505
* http://wiki.apache.org/subversion/NonNormalizingUnicodeCompositionAwareness
* https://en.wikipedia.org/wiki/Unicode_equivalence#Example
* http://zaiste.net/2012/07/brand_new_rsync_for_osx/
* https://gogo244.wordpress.com/2014/09/17/drived-me-crazy-convert-utf-8-mac-to-utf-8/

[an Answer posted on Server Fault]: http://serverfault.com/questions/397420/converting-utf-8-nfd-filenames-to-utf-8-nfc-in-either-rsync-or-afpd "Converting UTF-8 NFD filenames to UTF-8 NFC in either rsync or afpd, Server Fault Discussion"
[Japanese Perl users article]: http://perl-users.jp/articles/advent-calendar/2010/english/24 "Encode::UTF8Mac makes you happy while handling file names on MacOSX"
[Server Fault]: http://serverfault.com/questions/397420/converting-utf-8-nfd-filenames-to-utf-8-nfc-in-either-rsync-or-afpd "Converting UTF-8 NFD filenames to UTF-8 NFC in either rsync or afpd, Server Fault Discussion"
