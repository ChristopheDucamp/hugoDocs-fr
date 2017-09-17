---
title: "HTTP/2 Server Push in Hugo"
date: 2017-07-24T18:36:00+02:00
description: Comme chaque page de Hugo peut être diffusée en plusieurs formats, il est facile de créer  à la volée les fichiers _redirects et _headers de Netlify.
categories: [blog]
#tags: []
slug: "http2-server-push-in-hugo"
aliases: []
author: bep
images:
- images/gohugoio-card-1.png
---

**Netlify** a annoncé récemment la prise en charge de [HTTP/2 server push](https://www.netlify.com/blog/2017/07/18/http/2-server-push-on-netlify/), et nous l'avons maintenant ajouté aux **sites gohugo.io** pour les principaux bundles `CSS` et` JS`, ainsi que le support de redirection du serveur 301.

Si vous naviguez vers <https://gohugo.io> et regardez dans la console de développement Chrome, vous devriez maintenant voir `Push` comme la nouvelle source (" Initiateur ") pour `CSS` et `JSS` :

{{< figure src="/images/blog/hugo-http2-push.png" caption="Network log for https://gohugo.io" >}}

**Régler ça dans Hugo a été facile :**

## 1. Configurer les Formats Output Netlify

Ajouter un nouveau type media personnalisé et deux nouveaux formats outpout dans `config.toml`. Pour en savoir plus sur les formats output dans Hugo, voir [Formats Output Personnalisés](/templates/output-formats/).
```bash
[outputs]
home = [ "HTML", "RSS", "REDIR", "HEADERS" ]

[mediaTypes]
[mediaTypes."text/netlify"]
suffix = ""
delimiter = ""

[outputFormats]
[outputFormats.REDIR]
mediatype = "text/netlify"
baseName = "_redirects"
isPlainText = true
notAlternative = true
[outputFormats.HEADERS]
mediatype = "text/netlify"
baseName = "_headers"
isPlainText = true
notAlternative = true
```
## 2. Ajouter un Template Pour le Fichier _headers

Ajout `layouts/index.headers` :

```bash
/*
  X-Frame-Options: DENY
  X-XSS-Protection: 1; mode=block
  X-Content-Type-Options: nosniff
  Referrer-Policy: origin-when-cross-origin
*/
  Link: <{{ "dist/app.bundle.js" | relURL }}>; rel=preload; as=script
  Link: <{{ "dist/main.css" | relURL }}>; rel=preload; as=style
```
Le template au-dessus crée à la fois une défintion de header de sécurité et une configuration HTTP/2 server push.

Remarquez aussi que c'est un modèle pour la page d'accueil, aussi regardez la totalité de la `Page` avec son `Site` et beaucoup d'autres variables sont disponibles. Vous pouvez utiliser un `partial` pour inclure d'autres modèles.




## 3. Ajout d'un Template pour le Fichier _redirects  
Ajout d'un `layouts/index.redirects`:
```bash
# Netlify redirects. Voir https://www.netlify.com/docs/redirects/
{{  range $p := .Site.Pages -}}
{{ range .Aliases }}
{{  . | printf "%-35s" }}	{{ $p.RelPermalink -}}
{{ end -}}
{{- end -}}
```
Le modèle au-dessus crée des redirections 301 pour vos [aliases](/content-management/urls/#aliases), par conséquent vous voudrez probablement désactiver vos alias dans votre fichier  `config.toml`: `disableAliases = true`.

