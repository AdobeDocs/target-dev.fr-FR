---
keywords: paramètres de mbox globale, targetPageParams, chaîne de requête, tableau, json, dtm
description: Découvrez comment utiliser la fonction [!UICONTROL targetPageParams] pour transmettre des informations de ciblage ou de contexte supplémentaires à la mbox globale  [!DNL Adobe Target] .
title: Comment transférer des paramètres à une mbox globale ?
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 61%

---

# Transfert de paramètres à une mbox globale

La fonction JavaScript `targetPageParams` est utilisée pour transmettre des paramètres à la mbox globale dans [!DNL Adobe Target]. Cela est nécessaire dans tout scénario où des informations de ciblage/contexte supplémentaires doivent être transmises à [!DNL Target].

Par exemple, dans une activité de recommandations, utilisez les paramètres pour représenter le produit ou la catégorie actuelle qui est consultée.

Le code permettant d’appeler la fonction JavaScript doit être placé avant la mbox globale sur la page, que la mbox globale soit déclenchée dans le cadre d’at.js ou qu’elle soit incluse manuellement dans le code de page.

>[!NOTE]
>
>Si vous souhaitez ajouter des paramètres à toutes les mbox de la page et pas seulement à la mbox globale, utilisez la fonction [targetPageParamsAll()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) .

Vous pouvez transférer des paramètres à `target-global-mbox` à l’aide de la fonction `targetPageParams()` de l’une des façons suivantes :

* Un tableau
* Un objet JSON
* Une liste délimitée par des esperluettes

Utilisez ces trois méthodes pour vérifier que les paramètres sont transférés correctement. Vous pouvez également être en mesure de vérifier le transfert des paramètres en utilisant le [Débogueur d’Adobe Experience Cloud](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html).

Vous devez définir la fonction JavaScript avant d’ajouter la mbox globale à la page. Le nom doit être `targetPageParams`.

## Chaîne de requête

```
p1=v1&p2=v2&p3=hello%20world
```

* Nom : `targetPageParams`
* Valeur de renvoi : des paramètres délimités « &amp; » avec des valeurs de paramètre codées en URL

  Exemple :

  Dans cet exemple, p3 a la valeur `hello world`, qui est codée en URL.

Examinez l’exemple de code de page suivant :

```html {line-numbers="true"}
<html> 
  <head> 
    <title>Title here..</title> 
    <script type="text/javascript"> 
        function targetPageParams() { 
          return "p1=v1&p2=v2&p3=hello%20world";
        } 
    </script> 
    <script src="mbox.js" type="text/javascript"></script> 
  </head> 
  <body>Body here... 
  </body> 
</html>
```

Cet exemple envoie les données suivantes dans le bord de mbox :

* p1=v1
* p2=v2
* p3=hello world

## Tableau

```javascript {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return ["a=1", "b=2", "c=hello world"]; 
}; 
```

Il n’est pas nécessaire que les valeurs soient encodées en URL. Par exemple, si une valeur comporte un espace, il n’est pas nécessaire d’encoder l’espace.

Cet exemple envoie les données suivantes dans le bord de mbox :

* a=1
* b=2
* c=hello world

## JSON

JSON est un moyen puissant de transférer des paramètres. [!DNL Target] utilise les clés d’objet JSON pour aplatir les structures complexes en paramètres simples.

```json {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
                  "memberStatus": Gold, 
                  "country": { 
                                "city": "San Francisco" 
                            } 
              } 
  }; 
}; 
```

Il n’est pas nécessaire que les valeurs soient encodées en URL. Par exemple, « San Francisco » ne nécessite pas d’espace pour être encodé. Un espace suffit.

Cet exemple envoie les données suivantes dans le bord de mbox :

* a=1
* b=2
* `profile.memberStatus`=Gold
* `profile.country.city`=San Francisco
