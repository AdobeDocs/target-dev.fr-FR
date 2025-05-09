---
keywords: adobe.target.trackEvent, trackEvent, trackevent, track event, at.js, fonctions, function, protectDefault, preventdefault, empêcher la valeur par défaut, adobe.target.trackEvent
description: Utilisez la fonction [!UICONTROL adobe.target.trackEvent()] de la bibliothèque JavaScript  [!DNL Adobe Target] at.js pour déclencher une requête de création de rapports sur les actions des utilisateurs, telles que les clics et les conversions sur votre site.
title: Comment utiliser la fonction [!UICONTROL adobe.target.trackEvent()] ?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 59%

---

# [!UICONTROL adobe.target.trackEvent(options)]

Cette fonction déclenche une demande pour signaler les actions de l’utilisateur, telles que les clics et les conversions. Elle ne déclenche pas la diffusion d’activités dans le cadre de la réponse.

Ces appels de mbox de suivi d’événement peuvent servir à définir des mesures dans les activités. Pour plus d’informations, voir [Mesures de succès](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=fr) et [Suivi des conversions](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Voici les détails de l’API :

| Clé | Type | Requis | Description |
|--- |--- |--- |--- |
| mbox | Chaîne | Oui | Nom de mbox<P>**Remarque** : Si un appel [!UICONTROL trackEvent()] est déclenché avec un nom de mbox qui a déjà été déclenché sur la page, le SDID de [!UICONTROL trackEvent()] est réinitialisé et sera différent des appels [!DNL Target] de la page. Cependant, le déclenchement d’un appel [!UICONTROL trackEvent()] avec un nom de mbox différent conserve le SDID de l’appel [!UICONTROL trackEvent()] cohérent avec les appels [!UICONTROL Page Load Request]/[!UICONTROL triggerView()] sur la page. |
| selector | Chaîne | Non | Sélecteurs CSS utilisés pour rechercher les éléments HTML. Les écouteurs d’événement seront attachés aux éléments trouvés. |
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
