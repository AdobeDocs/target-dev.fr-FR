---
keywords: mboxCreate, mboxcreate, mbox create, at.js, fonctions, fonction
description: Utilisez la fonction [!UICONTROL mboxCreate()] de la bibliothèque JavaScript at [!DNL Adobe Target] js pour appliquer des offres au DIV le plus proche avec le nom de classe mboxDefault. (at.js 1.x)
title: Comment utiliser la fonction [!UICONTROL mboxCreate()] ?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
TQID: https://experienceleague.adobe.com/hCEKL9RPtqIbMVEouzObjU6dc7TKl1hBtKZ1jEdicRE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 211
ht-degree: 41%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Exécute une requête et applique l’offre au DIV le plus proche avec le nom de la classe mboxDefault.

>[!NOTE]
>
>Cette fonction est disponible uniquement pour les versions 1.*x* d’at.js. Cette fonction a été abandonnée avec la publication d’at.js 2.x. Cette fonction renvoie le contenu par défaut s’il est utilisé avec at.js 2.x.

Cette fonction est intégrée à at.js principalement pour faciliter la transition de mbox.js (désormais obsolète) vers at.js. `[!UICONTROL adobe.target.getOffer()]`, `[!UICONTROL adobe.target.applyOffer()]` ou la directive angulaire sont de nouvelles options de remplacement de `[!UICONTROL mboxCreate()]`.

## Exemple

```javascript {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  mboxCreate('mboxName','param1=value1','param2=value2'); 
</script>
```

## Remarques

La fonction `mboxCreate()` utilise désormais le point d’entrée « json » à la place du point d’entrée standard et est déclenchée de manière asynchrone. Pour cette raison :

* [Le débogage](/help/dev/implement/client-side/target-debugging-atjs/target-debugging-atjs.md) est légèrement différent.
* Évitez du code d’offre qui requiert des appels de blocage synchrones,

  comme des offres qui définissent des variables JavaScript qui sont utilisées par le code du site ou d’autres mbox qui sont ajoutées ultérieurement à la page.

* Assurez-vous de disposer d’un `<div class="mboxDefault"></div>`avant d’appeler `[!UICONTROL mboxCreate()]`, car at.js n’en ajoutera pas pour vous.

* Les fonctions `[!UICONTROL mboxCreate()]` vides en haut de page ne sont pas recommandées en tant mbox globale.

  La mbox globale créée automatiquement dans at.js est une meilleure option, car elle se déclenche à partir du `<head>` et peut renvoyer du contenu plus tôt.
