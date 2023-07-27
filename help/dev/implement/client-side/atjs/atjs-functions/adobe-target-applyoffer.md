---
keywords: adobe.target.applyOffer, applyOffer, apply offer, at.js, fonctions, fonction, $8
description: Utilisez la variable [!UICONTROL adobe.target.applyOffer()] pour la fonction [!DNL Adobe Target] Bibliothèque JavaScript at.js pour appliquer le contenu de la réponse.
title: Comment utiliser la variable [!UICONTROL adobe.target.applyOffer()] Fonction ?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 69%

---

# [!UICONTROL adobe.target.applyOffer(options)]

Cette fonction permet d’appliquer le contenu de la réponse avec [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` nécessite le paramètre `mbox`. Si le nom de mbox n’est pas spécifié, une erreur se produit.

Le paramètre options est obligatoire et possède la structure suivante :

| Clé | Type | Requis | Description |
|--- |--- |--- |--- |
| mbox | Chaîne | Oui | Nom de mbox<br /> avec at.js 1.3.0 (et versions ultérieures), Target applique impérativement l’utilisation de la clé mbox. Cette clé était obligatoire par le passé, mais Target force désormais son application de manière à garantir sa validation et l’utilisation correcte de la fonction par les clients. |
| selector | Chaîne ou élément DOM | Non | Élément HTML ou sélecteur CSS utilisé pour identifier l’élément HTML dans lequel Target doit placer le contenu de l’offre. Si le sélecteur n’est pas fourni, Target suppose que l’élément de HTML doit utiliser l’HEAD de HTML. |
| Offre | Tableau | Oui | Les actions d’un tableau devant être appliquées à l’élément. |

## Exemple

L’exemple suivant illustre l’utilisation conjointe de `[!UICONTROL getOffer]` et d’`[!UICONTROL applyOffer]` :

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```
