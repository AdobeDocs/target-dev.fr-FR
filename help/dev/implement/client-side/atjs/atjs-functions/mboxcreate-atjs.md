---
keywords: mboxCreate, mboxcreate, mbox create, at.js, fonctions, fonction
description: Utilisez la variable [!UICONTROL mboxCreate()] pour la fonction [!DNL Adobe Target] Bibliothèque JavaScript at.js pour appliquer les offres au DIV le plus proche avec le nom de classe mboxDefault . (at.js 1.x)
title: Comment utiliser la variable [!UICONTROL mboxCreate()] Fonction ?
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 55%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

Exécute une requête et applique l’offre au DIV le plus proche avec le nom de la classe mboxDefault.

>[!NOTE]
>
>Cette fonction est disponible pour at.js versions 1.*x* uniquement. Cette fonction a été abandonnée avec la version d’at.js 2.x. Cette fonction renvoie le contenu par défaut s’il est utilisé avec at.js 2.x.

Cette fonction est intégrée à at.js pour faciliter principalement la transition de mbox.js (désormais obsolète) vers at.js. `[!UICONTROL adobe.target.getOffer()]`, `[!UICONTROL adobe.target.applyOffer()]` ou la directive angulaire sont de nouvelles options de remplacement de `[!UICONTROL mboxCreate()]`.

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

* Veillez à avoir une `<div class="mboxDefault"></div>`avant d’appeler `[!UICONTROL mboxCreate()]`, car at.js n’en ajoute pas pour vous.

* Les fonctions `[!UICONTROL mboxCreate()]` vides en haut de page ne sont pas recommandées en tant mbox globale.

  La mbox globale créée automatiquement dans at.js est une meilleure option, car elle se déclenche à partir de la fonction `<head>` et peut renvoyer du contenu plus tôt.
