---
keywords: implémentation, bibliothèque javascript, js, atjs, prise de décision sur les appareils, prise de décision sur les appareils, fonctionnalités prises en charge, 8 $
description: Découvrez les fonctionnalités prises en charge pour [!UICONTROL on-device decisioning].
title: Quelles fonctionnalités sont prises en charge dans la prise de décision sur les périphériques ?
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 12%

---

# Fonctionnalités prises en charge pour [!UICONTROL on-device decisioning]

Le SDK JS [!DNL Adobe Target] offre aux clients la possibilité de choisir entre les performances et l’actualisation des données pour les décisions. En d’autres termes, si la diffusion de contenu personnalisé le plus pertinent et attrayant par le biais de l’apprentissage automatique est la plus importante pour vous, un appel au serveur en direct doit être effectué. Mais lorsque les performances sont plus critiques, une décision doit être prise sur l’appareil et en mémoire. Pour que [!UICONTROL on-device decisioning] fonctionne, reportez-vous aux sections suivantes qui répertorient les fonctionnalités prises en charge.

## Types d’activité pris en charge

Le tableau suivant indique les [types d’activité](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=fr) créés par le [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr) ou le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr) (VEC) sont pris en charge ou non pour [!UICONTROL on-device decisioning].

| Type d’activité | Pris en charge ? |
| --- | --- |
| [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=fr) | Oui |
| [affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=fr) | Non |
| [Ciblage automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=fr) ![Premium](../../../assets/premium.png) | Non |
| [Test multivarié](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=fr) (MVT) | Non |
| [Ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=fr) (XT) | Oui |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=fr) ![Premium](../../../assets/premium.png) | Non |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=fr) ![Premium](../../../assets/premium.png) | Non |
| [Activités utilisant Analytics pour Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr&) (A4T) | Oui |

## Ciblage de l’audience

Le tableau suivant indique les règles d’audience prises en charge ou non pour [!UICONTROL on-device decisioning].

| Règle d’audience | Pris en charge ? |
| --- | --- |
| [Géo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=fr) | Oui<P>Lors de l’utilisation de la prise de décision sur l’appareil, les attributs géographiques suivants sont pris en charge :<ul><li>Pays/zone géographique</li><li>Ville</li><li>Latitude</li><li>Longitude</li></ul> |
| [Réseau](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=fr) | Non |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=fr) | Non |
| [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=fr) | Oui |
| [Système d’exploitation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=fr) | Oui |
| [Pages du site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=fr) | Oui |
| [Navigateur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=fr) | Oui |
| [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=fr) | Non |
| [Sources de trafic](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=fr) | Non |
| [Période](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=fr) | Oui |
| Audiences Adobe Experience Cloud<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager] et [!DNL Adobe Experience Manager]) | Non |

### Ciblage géographique pour [!UICONTROL on-device decisioning]

Pour maintenir une latence minimale pour les activités [!UICONTROL on-device decisioning] avec des audiences basées sur la géolocalisation, Adobe vous recommande de fournir vous-même les valeurs géographiques dans l’appel à [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Définissez l’objet Geo dans le contexte de la requête. Cela signifie, à partir du navigateur, un moyen de déterminer l’emplacement de chaque visiteur. Par exemple, vous pouvez effectuer une recherche IP/géo à l’aide d’un service que vous configurez. Certains fournisseurs d’hébergement, tels que Google Cloud, fournissent cette fonctionnalité par le biais d’en-têtes personnalisés dans chaque `HttpServletRequest`.

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

Cependant, si vous ne parvenez pas à effectuer des recherches IP vers géo sur votre serveur, mais que vous souhaitez toujours effectuer [!UICONTROL on-device decisioning] pour les demandes [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) qui contiennent des audiences basées sur la géographie, cela est également pris en charge. L’inconvénient de cette approche est qu’elle utilise une recherche IP/géo distante, ce qui ajoute une latence à chaque appel `getOffers`. Cette latence doit être inférieure à un appel `getOffers` avec prise de décision côté serveur, car elle atteint un réseau de diffusion de contenu situé près de votre serveur. Indiquez uniquement le champ &quot;ipAddress&quot; dans l’objet Geo dans le contexte de votre requête pour que le SDK récupère la géolocalisation de l’adresse IP de votre visiteur. Si un autre champ en plus de &quot;ipAddress&quot; est fourni, le SDK [!DNL Target] ne récupérera pas les métadonnées de géolocalisation pour la résolution.

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

### Méthode d’affectation

Le tableau suivant indique les méthodes d’attribution prises en charge ou non pour [!UICONTROL on-device decisioning].

| Méthode d’affectation | Pris en charge ? |
| --- | --- |
| Manuel | Oui |
| [Auto affecter à la meilleure expérience](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=fr) | Non |
| [Ciblage automatique pour les expériences personnalisées](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html?lang=fr) | Non |
