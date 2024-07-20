---
keywords: targetPageParams, targetpageparams, pageParams, pageparams, pages params, paramètres de page, at.js, fonctions, fonction, targetPageParams0
description: Utilisez la fonction [!UICONTROL targetPageParams()] de la bibliothèque JavaScript  [!DNL Adobe Target] at.js pour joindre des paramètres à la mbox globale depuis l’extérieur du code de requête.
title: Comment utiliser la fonction [!UICONTROL targetPageParams()] ?
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 68%

---

# [!UICONTROL targetPageParams()]

Cette méthode permet de joindre des paramètres à la mbox globale depuis l’extérieur du code de demande.

Elle s’avère très utile pour inclure un même ensemble de paramètres dans plusieurs appels de mbox. La fonction doit être définie par le client. Elle doit renvoyer un tableau de paramètres qui sera transmis uniquement à la demande de la mbox globale. Cette fonction peut être définie avant le chargement du fichier at.js ou dans **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Library Header]**.

Vous pouvez transmettre des paramètres à target-global-mbox à l’aide de la fonction `[!UICONTROL targetPageParams()]` de n’importe quelle façon suivante :

* Une liste délimitée par des esperluettes
* Un tableau
* Un objet JSON

## Exemples

Liste délimitée par des esperluettes (les valeurs doivent être codées dans l’URL) :

```javascript {line-numbers="true"}
function targetPageParams() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

Tableau (les valeurs n’ont pas besoin d’être codées dans l’URL) :

```javascript {line-numbers="true"}
targetPageParams = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

Objet JSON (les valeurs n’ont pas besoin d’être codées dans l’URL) :

```javascript {line-numbers="true"}
targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```
