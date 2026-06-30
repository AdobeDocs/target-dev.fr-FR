---
keywords: adobe.target.trackEvent, trackEvent, trackevent, track event, at.js, fonctions, fonction, preventionDefault, preventiondefault, empêcher le défaut, adobe.target.trackEvent
description: Utilisez la fonction [!UICONTROL adobe.target.trackEvent()] de la bibliothèque JavaScript at [!DNL Adobe Target] js pour déclencher une requête afin de signaler les actions des utilisateurs et utilisatrices, telles que les clics et les conversions sur votre site.
title: Comment utiliser la fonction [!UICONTROL adobe.target.trackEvent()] ?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
TQID: https://experienceleague.adobe.com/Jib9C5FvmsgIF6CA-0UbdMdnMiXxQCkU2-O3Zys3vrY
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
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 336
ht-degree: 56%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Cette fonction déclenche une demande pour signaler les actions de l’utilisateur, telles que les clics et les conversions. Elle ne déclenche pas la diffusion d’activités dans le cadre de la réponse.

Ces appels de mbox de suivi d’événement peuvent servir à définir des mesures dans les activités. Pour plus d’informations, voir [Mesures de succès](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=fr) et [Suivi des conversions](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Voici les détails de l’API :

| Clé | Type | Requis | Description |
|--- |--- |--- |--- |
| mbox | Chaîne | Oui | Nom de mbox<P>**Remarque** : si un appel [!UICONTROL trackEvent()] est déclenché avec un nom de mbox déjà déclenché sur la page, le SDID de [!UICONTROL trackEvent()] est réinitialisé et sera différent des appels [!DNL Target] sur la page. Cependant, le déclenchement d’un appel [!UICONTROL trackEvent()] avec un nom de mbox différent maintient le SDID de l’appel [!UICONTROL trackEvent()] cohérent avec les appels [!UICONTROL Page Load Request]/[!UICONTROL triggerView()] sur la page. |
| selector | Chaîne | Non | Sélecteurs CSS utilisés pour rechercher les éléments HTML. Les écouteurs d’événement seront associés aux éléments trouvés. |
| type | Chaîne | Non | Représente un type d’événement enregistré. Il peut s’agir d’événements HTML connus (click, mousedown, etc.) et d’événements HTML personnalisés. |
| preventDefault | Booléen | Non | Indique si `[!UICONTROL event.preventDefault()]` () doit être utilisé dans le rappel des détecteurs d’événements. La valeur par défaut est false.<P>**Remarque** : seuls `[!UICONTROL form[submit]]` et `a[click]` sont pris en charge. D’autres scénarios ne sont pas pris en charge pour des raisons de complexité et parce que le nombre de scénarios possibles est trop élevé. |
| params | Objet | Non | Paramètres mbox. Objet de paires clé-valeur qui possède la structure suivante :<P>`{ "param1": "value1", "param2": "value2"}` |
| timeout | Nombre | Non | Délai d’attente exprimé en secondes.<P>S’il n’est pas spécifié, la valeur par défaut est utilisée :<P>`...timeoutInSeconds: 0.15...}` |
| success | Fonction | Non | Fonction de rappel utilisée pour indiquer que l’événement a été signalé. |
| error | Fonction | Non | Fonction de rappel utilisée pour indiquer que l’événement n’a pas pu être signalé. |

## Exemple

```javascript {line-numbers="true"}
<a href="https://asite.com">click me!</a> 
```

plus le code JavaScript pour affecter `trackEvent` :

```javascript {line-numbers="true"}
<script> 
$('a').click(function(event){ 
  adobe.target.trackEvent({'mbox':'homePageHero'}) 
}); 
</script> 
```

Ou :

```javascript {line-numbers="true"}
adobe.target.trackEvent({ 
    "mbox": "clicked-cta", 
    "params": { 
        "param1": "value1" 
    } 
});
```

>[!WARNING]
>
>Si les champs obligatoires ne sont pas définis, aucune requête n’est exécutée et une erreur est générée.


