---
keywords: mboxDefine, mboxdefine, mboxUpdate, mboxUpdate, mise à jour de mbox, at.js, fonctions, fonction, mboxDefine0
description: Utilisez la variable [!UICONTROL mboxDefine()] et [!UICONTROL mboxUpdate()] pour la fonction [!DNL Adobe Target] Bibliothèque JavaScript at.js pour définir ou mettre à jour une mbox. (at.js 1.x)
title: Comment utiliser la variable [!UICONTROL mboxDefine()] Et [!UICONTROL mboxUpdate()] Fonctions ?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 52%

---

# [!UICONTROL mboxDefine()] et [!UICONTROL mboxUpdate()] - at.js 1.x

Définir et mettre à jour une mbox dans [!DNL Adobe Target].

>[!NOTE]
>
>Ces fonctions sont disponibles pour at.js versions 1.*x* uniquement. Ces fonctions ont été abandonnées avec la version d’at.js 2.*x*. Ces fonctions renvoient le contenu par défaut si elles sont utilisées avec at.js 2.*x*.

Les fonctions `[!UICONTROL mboxDefine()]` et `[!UICONTROL mboxCreate()]` sont liées aux éléments HTML DIV dans lesquels l’offre doit s’afficher. Ces éléments HTML DIV doivent avoir la classe `mboxDefault`. Si cette classe n’est pas attachée aux éléments HTML, un scintillement peut être visible.

## mboxDefine

Crée un mappage interne entre un nodeId et le nom d’une mbox, mais n’exécute pas la demande. Cette fonction est utilisée avec `[!UICONTROL mboxUpdate()]`. Intégrée à at.js pour faciliter principalement la transition de mbox.js (désormais obsolète) vers at.js.

## mboxUpdate

Exécute la demande et applique l’offre à l’élément identifié par le `nodeId` dans la fonction `mboxDefine()`. Cette fonction peut être également utilisée pour mettre à jour une mbox initiée par `[!UICONTROL mboxCreate]`. Intégrée à at.js pour faciliter principalement la transition de mbox.js (désormais obsolète) vers at.js. `mboxDefine()`/ `mboxUpdate()` peut être remplacé par [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) et [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) à l’aide de l’option de sélecteur.

## Exemple

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
