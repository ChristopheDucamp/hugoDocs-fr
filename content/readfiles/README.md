# readdirs Répertoire pour Contenu Réutilisable 

Les fichiers dans ce dossier sont : 

1. Utilisés plus d'une fois dans la doc Hugo
2. Utilisés dans les exemples de readdir (par ex. dans des modèles de fichiers locaux)

Ces fichiers sont appelés en utilisant le shortcode [`readfile` (source)](../layouts/readfile.html).

Vous pouvez appeler ce shortcode dans les docs comme suit : 


<code>{</code><code>{</code>% readfile file="/path/to/file.txt" markdown="true" %<code>}</code><code>}</code>


`markdown="true"` est facultatif (default = `"false"`) et analyse la chaîne à travers le rendu Blacfriday.
