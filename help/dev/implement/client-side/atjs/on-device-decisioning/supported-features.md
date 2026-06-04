---
keywords: implémentation, bibliothèque javascript, js, atjs, prise de décision sur l’appareil, prise de décision sur l’appareil, fonctionnalités prises en charge, 8 $
description: Découvrez les fonctionnalités prises en charge pour la [!UICONTROL prise de décision sur l’appareil].
title: Les fonctionnalités prises en charge dans la prise de décision sur l’appareil
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
TQID: https://experienceleague.adobe.com/ummFURb6WnrNCbiQNDtzWmtZq05am9CMn9UXL0SPaXo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 747
ht-degree: 8%

---

# Fonctionnalités prises en charge pour la [!UICONTROL prise de décision sur l’appareil]

Le SDK JS [!DNL Adobe Target] offre aux clients et aux clientes la possibilité de choisir entre les performances et la fraîcheur des données pour les décisions. En d’autres termes, si la diffusion du contenu personnalisé le plus pertinent et le plus attrayant via le machine learning est la plus importante pour vous, un appel au serveur en direct doit être effectué. Mais lorsque les performances sont plus critiques, une décision doit être prise sur l’appareil et en mémoire. Pour que la [!UICONTROL prise de décision sur l’appareil] fonctionne, reportez-vous aux sections suivantes qui répertorient les fonctionnalités prises en charge.

## Types d’activité pris en charge

Le tableau suivant indique les [types d’activité](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) créés par le [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) ou le [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) qui sont pris en charge ou non pour la [!UICONTROL prise de décision sur l’appareil].

| Type d’activité | Pris en charge ? |
| --- | --- |
| [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Oui |
| [affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Non |
| [Ciblage automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | Non |
| [Test multivarié](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Non |
| [Ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Oui |
| [](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | Non |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | Non |
| [Activités utilisant Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html ?) (A4T) | Oui |

## Ciblage des audiences

Le tableau suivant indique les règles d’audience prises ou non en charge pour la [!UICONTROL prise de décision sur l’appareil].

| Règle d’audience | Pris en charge ? |
| --- | --- |
| [Géo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Oui<P>Lors de l’utilisation de la prise de décision sur l’appareil, les attributs géographiques suivants sont pris en charge :<ul><li>Pays/zone géographique</li><li>Ville</li><li>Latitude</li><li>Longitude</li></ul> |
| [Réseau](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Non |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Non |
| [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Oui |
| [Système d’exploitation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Oui |
| [Pages du site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Oui |
| [Navigateur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Oui |
| [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Non |
| [Sources de trafic](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Non |
| [Période](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Oui |
| Audiences Adobe Experience Cloud<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager] et [!DNL Adobe Experience Manager]) | Non |

### Ciblage géographique pour la prise de décision [!UICONTROL  sur l’appareil]

Pour maintenir une latence minimale pour les activités [!UICONTROL prise de décision sur l’appareil] avec des audiences basées sur la zone géographique, Adobe vous recommande de fournir vous-même les valeurs géographiques dans l’appel à [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Définissez l’objet géographique dans le contexte de la requête. Cela signifie qu’à partir du navigateur, il est possible de déterminer l’emplacement de chaque visiteur. Par exemple, vous pouvez effectuer une recherche IP/zone géographique à l’aide d’un service que vous configurez. Certains fournisseurs d’hébergement, tels que Google Cloud, proposent cette fonctionnalité via des en-têtes personnalisés dans chaque `HttpServletRequest`.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                city: "SAN FRANCISCO", 
                countryCode: "US", 
                stateCode: "CA", 
                latitude: 37.75, 
                longitude: -122.4 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

Cependant, si vous ne parvenez pas à effectuer des recherches IP/géolocalisation sur votre serveur, mais que vous souhaitez toujours effectuer une [!UICONTROL prise de décision sur l’appareil] pour les requêtes [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) qui contiennent des audiences géolocalisées, cela est également pris en charge. L’inconvénient de cette approche est qu’elle utilise une recherche IP/géolocalisation à distance, ce qui ajoute de la latence à chaque appel `getOffers`. Cette latence doit être inférieure à un appel `getOffers` avec prise de décision côté serveur, car elle atteint un réseau CDN situé près de votre serveur. Indiquez uniquement le champ « ipAddress » dans l’objet Geo dans le contexte de votre demande pour que le SDK récupère la géolocalisation de l’adresse IP du visiteur. Si un autre champ en plus de l’adresse IP est fourni, le SDK [!DNL Target] ne récupère pas les métadonnées de géolocalisation pour la résolution.

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                ipAddress: "127.0.0.1" 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

### Méthode d&#39;allocation

Le tableau suivant indique les méthodes d’attribution prises en charge ou non pour la [!UICONTROL prise de décision sur l’appareil].

| Méthode d&#39;allocation | Pris en charge ? |
| --- | --- |
| Manuel | Oui |
| [ Affectation automatique à la meilleure expérience ](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Non |
| [Ciblage automatique pour les expériences personnalisées](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Non |
