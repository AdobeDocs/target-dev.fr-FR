---
keywords: mboxDefine, mboxdefine, mbox define, mboxUpdate, mboxupdate, mbox update, at.js, fonctions, fonction, mboxDefine0
description: Utilisez les fonctions [!UICONTROL mboxDefine()] et [!UICONTROL mboxUpdate()] de la bibliothèque JavaScript at [!DNL Adobe Target] js pour définir ou mettre à jour une mbox. (at.js 1.x)
title: Comment utiliser les fonctions [!UICONTROL mboxDefine()] et [!UICONTROL mboxUpdate()] ?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
TQID: https://experienceleague.adobe.com/Fn-Ej8jk2AMEn79tOtRoP9GQc36Ugy6FtXyn6x7jkmA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 208
ht-degree: 46%

---

# [!UICONTROL mboxDefine()] et [!UICONTROL mboxUpdate()] - at.js 1.x

Définissez et mettez à jour une mbox dans [!DNL Adobe Target].

>[!NOTE]
>
>Ces fonctions sont disponibles uniquement pour les versions 1.*x* d’at.js. Ces fonctions ont été abandonnées avec la version 2.*x* d’at.js. Ces fonctions renvoient le contenu par défaut si elles sont utilisées avec at.js 2.*x*.

Les fonctions `[!UICONTROL mboxDefine()]` et `[!UICONTROL mboxCreate()]` sont liées aux éléments HTML DIV dans lesquels l’offre doit s’afficher. Ces éléments HTML DIV doivent avoir la classe `mboxDefault`. Si cette classe n’est pas attachée aux éléments HTML, un scintillement peut être visible.

## mboxDefine

Crée un mappage interne entre un nodeId et le nom d’une mbox, mais n’exécute pas la demande. Cette fonction est utilisée avec `[!UICONTROL mboxUpdate()]`. Intégré à at.js principalement pour faciliter la transition de mbox.js (désormais obsolète) vers at.js.

## mboxUpdate

Exécute la demande et applique l’offre à l’élément identifié par le `nodeId` dans la fonction `mboxDefine()`. Cette fonction peut être également utilisée pour mettre à jour une mbox initiée par `[!UICONTROL mboxCreate]`. Intégré à at.js principalement pour faciliter la transition de mbox.js (désormais obsolète) vers at.js. `mboxDefine()`/ `mboxUpdate()` peut être remplacé par [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) et [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) à l’aide de l’option de sélecteur.

## Exemple

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
