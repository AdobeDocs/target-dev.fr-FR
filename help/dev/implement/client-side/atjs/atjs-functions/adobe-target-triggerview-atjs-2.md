---
keywords: adobe.target.triggerView, triggerView, trigger view, trigger view, at.js, functions, function, viewName, viewname, nom de la vue, adobe.target.triggerView1
description: Utilisez la fonction adobe.target.triggerView() pour la bibliothèque JavaScript at [!DNL Adobe Target] js à utiliser dans les applications d’une seule page (SPA). (at.js 2.x)
title: Comment utiliser la fonction adobe.target.triggerView() ?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
TQID: https://experienceleague.adobe.com/pBC1GRKG0mxeaZ1hfaByKv2tu-XScrSJfm7lUw-3yKw
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
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 19%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

Cette fonction peut être appelée à chaque chargement d’une nouvelle page ou lorsqu’un composant fait l’objet d’un nouveau rendu sur une page. `adobe.target.triggerView()` doit être implémenté pour que les applications monopages (SPA) utilisent le [!UICONTROL compositeur d’expérience visuelle] (VEC) afin de créer des activités [!UICONTROL test A/B] et [!UICONTROL ciblage d’expérience] (XT). Si `[!UICONTROL adobe.target.triggerView()]` n’est pas implémenté sur le site, le compositeur d’expérience visuelle ne peut pas être utilisé pour les SPA. Pour plus d’informations, voir [Implémentation d’application monopage](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>Cette fonction a été introduite avec at.js 2.*x*. Cette fonction n’est pas disponible pour at.js version 1.*x*.

| Paramètre | Type | Obligatoire ? | Description |
| --- | --- | --- | --- |
| viewName | Chaîne | Oui | Transmettez n’importe quel nom en tant que type de chaîne que vous souhaitez représenter votre vue. Le nom de cette vue s’affiche dans le panneau [!UICONTROL Modifications] du compositeur d’expérience visuelle pour que les marketeurs puissent créer des actions et exécuter leurs activités [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] XT. |
| Options | Objet | Non |  |
| options > page | Booléen | Non | **TRUE :** La valeur par défaut de la page est vrai. Lorsque page = vrai, les notifications sont envoyées au serveur principal [!DNL Target] pour incrémenter le nombre d’impressions.<P>Une notification est toujours envoyée par défaut lorsqu’une `[!UICONTROL triggerView]` est appelée, sauf lorsque options > page est défini sur false.<P>**FALSE :** lorsque page=false, les notifications ne sont pas envoyées pour incrémenter le nombre d’impressions. Cette approche doit être utilisée lorsque vous souhaitez effectuer uniquement le rendu d’un composant sur une page avec une offre.<P>**Remarque** : les offres de code personnalisé dans le VEC ne sont pas rendues de nouveau lorsque `[!UICONTROL triggerView()]` est appelé avec `{page: false}` comme option. |

## Exemple : True

`[!UICONTROL triggerView()]` appel pour envoyer une notification au serveur principal [!DNL Target] afin d’incrémenter les impressions d’activité et d’autres mesures.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Exemple : False

`[!UICONTROL triggerView()]` appel pour que les notifications ne soient pas envoyées au serveur principal [!DNL Target] pour le comptage d’impressions.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Exemple : Chaînage de promesses avec `getoffers()` et `applyOffers()`

Pour exécuter `triggerView()` lorsque la promesse de `getOffers()` est résolue, il est important d’exécuter `triggerView()` sur le bloc final, comme illustré dans l’exemple ci-dessous. Cela est nécessaire pour que le compositeur d’expérience visuelle détecte les `Views` en mode création.

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

## Exemple : meilleure compatibilité pour `triggerView()` avec l’extension Visual Editing Helper d’Adobe 

Tenez compte des points suivants lors de l’utilisation de l’extension Visual Editing Helper d’Adobe [&#128279;](https://experienceleague.adobe.com/fr/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank} :

En raison des nouvelles politiques de manifeste V3 de [!DNL Googl]e pour les extensions [!DNL Chrome], l’extension [!UICONTROL &#x200B; Visual Editing Helper &#x200B;] doit attendre l’événement `DOMContentLoaded` avant de charger les bibliothèques [!DNL Target] dans le VEC. Ce délai peut entraîner le déclenchement de l’appel `triggerView()` aux pages web avant que les bibliothèques de création ne soient prêtes, ce qui fait que la vue n’est pas renseignée au chargement.

Pour atténuer ce problème, utilisez un écouteur pour l’événement de `load` de page.

Voici un exemple d’implémentation :

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```



