+++
title = "mermaid"
description = "mermaid est ici un raccourci-code pour intégrer des diagrammes de séquence, flowcharts ou Gantt "
+++

[mermaid](https://knsv.github.io/mermaid/) est un éditeur pour créer des diagrammes pouvant être utilisés en raccourci-code pour intégrer de jolis diagrammes dans les pages web d'une doc ou d'un projet.

## Exemple de Flowchart

{{%expand "Afficher le code ..."%}}
	{{</*mermaid align="left"*/>}}
	graph LR;
		A[Bords carrés] -->|Lien texte| B(Bords Rounds)
    	B --> C{Décision}
    	C -->|Un| D[Résultat un]
    	C -->|Deux| E[Résultat deux]
    {{</* /mermaid */>}}
{{%/expand%}}

{{<mermaid align="left">}}
graph LR;
	A[Bords carrés] -->|Lien texte| B(Bords Rounds)    
	B --> C{Décision}
   C -->|Un| D[Résultat un]
   C -->|Deux| E[Résultat deux]
{{< /mermaid >}}

## Exemples de diagramme séquence

### Transaction croisées
{{<mermaid>}}
sequenceDiagram
    participant Barbara
    participant Christophe
    Barbara->>Christophe: Salut Christophe, comment va ?
    Christophe-->>Barbara: Génial !
{{< /mermaid>}}
### Diagramme à raffiner 

{{%expand "Afficher le code ..."%}}
	{{</*mermaid*/>}}
	sequenceDiagram
	    participant Alice
	    participant Bruno
	    Alice->>Jean: Salut Jean, comment vas-tu ?
	    loop Healthcheck
	        Jean->Jean: Je lutte contre l'hypocondrie
	    end
	    Note right of John: Rational thoughts <br/>prevail...
	    John-->Alice: Great!
	    John->Bob: How about you?
	    Bob-->John: Jolly good!
	{{</* /mermaid */>}}
{{%/expand%}}

{{<mermaid>}}
sequenceDiagram
    participant Alice
    participant Bruno
    Alice->> Christophe: Salut Christophe, ça va ?
    loop santé mentale
        Christophe->Christophe: Lutte contre hypochondrie
    end
    Note right of Christophe: Les pensées rationnelles reprennent le dessus...
    Christophe--> Alice: Génial !
    Christophe-> Bruno: Et toi ?
    Bruno-->Christophe: Vraiment super et toi!
{{< /mermaid >}}



## Exemple diagramme de GANTT
{{%expand "Afficher le code ..."%}}
	{{</*mermaid*/>}}
	gantt
	        dateFormat  YYYY-MM-DD
	        title Ajouter une fonctionnalité de diagramme de GANTT à mermaid
	        section A section
	        Completed task            :done,    des1, 2014-01-06,2014-01-08
	        Active task               :active,  des2, 2014-01-09, 3d
	        Future task               :         des3, after des2, 5d
	        Future task2               :         des4, after des3, 5d
	        section Critical tasks
	        Completed task in the critical line :crit, done, 2014-01-06,24h
	        Implement parser and jison          :crit, done, after des1, 2d
	        Create tests for parser             :crit, active, 3d
	        Future task in critical line        :crit, 5d
	        Create tests for renderer           :2d
	        Add to mermaid                      :1d
	{{</* /mermaid */>}}
{{%/expand%}}

{{<mermaid>}}
gantt
        dateFormat  YYYY-MM-DD
        title Ajouter une fonctionnalité de diagramme de GANTT à mermaid
        section section A
        Tâche terminée            :done,    des1, 2018-01-06,2018-01-08
        Tâche en cours               :active,  des2, 2018-01-09, 3d
        Faire le ménage               :         des3, after des2, 5d
        Trouver autres idées               :         des4, after des3, 5d
        section Tâches critiques
        Tâches complétées dans la ligne critique :crit, done, 2018-01-06,24h
        Impl. parseur et json          :crit, done, after des1, 2d
        Tests parseurs             :crit, active, 3d
        Future tâche ligne critique          :crit, 5d
        Tests rendu            :2d
        Ajout mermaid                      :1d
{{</mermaid>}}



