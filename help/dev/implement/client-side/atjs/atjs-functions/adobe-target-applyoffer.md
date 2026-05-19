---
keywords: adobe.target.applyOffer, applyOffer, applyoffer, applyOffer, at.js, fonctions, fonction, 8 $
description: Utilisez la fonction [!UICONTROL adobe.target.applyOffer()] pour que la bibliothèque JavaScript at [!DNL Adobe Target] js applique le contenu de la réponse.
title: Comment utiliser la fonction [!UICONTROL adobe.target.applyOffer()] ?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
TQID: https://experienceleague.adobe.com/lrjsIl-gKu1SnrZapxYcoDObvUCGG2ht58QtWbQkYts
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 169
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
| selector | Chaîne ou élément DOM | Non | Élément HTML ou sélecteur CSS utilisé pour identifier l’élément HTML dans lequel Target doit placer le contenu de l’offre. Si le sélecteur n’est pas fourni, Target suppose que l’élément HTML doit utiliser HTML HEAD. |
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
