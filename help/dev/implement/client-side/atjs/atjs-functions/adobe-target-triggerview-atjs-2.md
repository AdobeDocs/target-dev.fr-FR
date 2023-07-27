---
keywords: adobe.target.triggerView, triggerView, déclencheur vue, at.js, fonctions, fonction, viewName, nom de la vue, adobe.target.triggerView1
description: Utilisez la fonction adobe.target.triggerView() pour la fonction [!DNL Adobe Target] Bibliothèque JavaScript at.js à utiliser dans les applications d’une seule page (SPA). (at.js 2.x)
title: Comment utiliser la fonction adobe.target.triggerView() ?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 37%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Cette fonction peut être appelée à chaque chargement d’une nouvelle page ou lorsqu’un composant fait l’objet d’un nouveau rendu sur une page. `adobe.target.triggerView()` doit être implémenté pour les applications d’une seule page (SPA) afin d’utiliser la variable [!UICONTROL Compositeur d’expérience visuelle] (VEC) à créer [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] (XT). If `[!UICONTROL adobe.target.triggerView()]` n’est pas implémenté sur le site, le compositeur d’expérience visuelle ne peut pas être utilisé pour SPA. Pour plus d’informations, voir [Implémentation d’application monopage](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Cette fonction a été introduite avec at.js 2.*x*. Cette fonction n’est pas disponible pour at.js version 1.*x*.

| Paramètre | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| viewName | Chaîne | Oui | Transmettez n’importe quel nom en tant que type de chaîne que vous souhaitez représenter votre vue. Ce nom d’affichage apparaît dans la variable [!UICONTROL Modifications] du compositeur d’expérience visuelle pour que les marketeurs puissent créer des actions et exécuter leurs [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] Activités XT. |
| Options | Objet | Non |  |
| options > page | Booléen | Non | **TRUE :** La valeur par défaut de la page est vrai. Lorsque page = vrai, les notifications sont envoyées au serveur principal [!DNL Target] pour incrémenter le nombre d’impressions.<P>Une notification est toujours envoyée par défaut lorsqu’une `[!UICONTROL triggerView]` est appelée, sauf si options > page est défini sur false.<P>**FALSE :** lorsque page = false, les notifications sont envoyées pour incrémenter le nombre d’impressions. Cette approche doit être utilisée lorsque vous souhaitez uniquement effectuer le rendu d’un composant sur une page avec une offre.<P>**Remarque**: les offres de code personnalisé dans le compositeur d’expérience visuelle ne sont pas rendues à nouveau lors de la `[!UICONTROL triggerView()]` est appelé avec `{page: false}` comme option. |

## Exemple : True

Appel `[!UICONTROL triggerView()]`[!DNL Target] pour envoyer une notification au serveur principal pour incrémenter les impressions d’activité et d’autres mesures.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Exemple : False

Appel `[!UICONTROL triggerView()]`[!DNL Target] pour ne pas envoyer de notifications au serveur principal pour le comptage d’impression.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Exemple : promesse d’un chaînage avec `getoffers()` et `applyOffers()`

Pour exécuter `triggerView()` lorsque la variable `getOffers()` la promesse est résolue, il est important d’exécuter `triggerView()` sur le bloc final, comme illustré dans l&#39;exemple ci-dessous. Cela est nécessaire pour que le VEC détecte `Views` en mode création.

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```
