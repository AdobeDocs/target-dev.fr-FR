---
keywords: implémentation, bibliothèque javascript, js, atjs, prise de décision sur les appareils, prise de décision sur les appareils, fonctionnalités prises en charge, 8 $
description: Découvrez les fonctionnalités prises en charge pour [!UICONTROL prise de décision sur appareil].
title: Quelles fonctionnalités sont prises en charge dans la prise de décision sur les périphériques ?
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 10%

---

# Fonctionnalités prises en charge pour [!UICONTROL prise de décision sur appareil]

La variable [!DNL Adobe Target] Le SDK JS offre aux clients la possibilité de choisir entre les performances et l’actualisation des données pour les décisions. En d’autres termes, si la diffusion de contenu personnalisé le plus pertinent et attrayant par le biais de l’apprentissage automatique est la plus importante pour vous, un appel au serveur en direct doit être effectué. Mais lorsque les performances sont plus critiques, une décision doit être prise sur l’appareil et en mémoire. Pour [!UICONTROL prise de décision sur appareil] pour travailler, reportez-vous aux sections suivantes qui répertorient les fonctionnalités prises en charge.

## Types d’activité pris en charge

Le tableau suivant indique laquelle [types d’activités](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) créé par la fonction [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) ou [Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) sont pris en charge ou non par [!UICONTROL prise de décision sur appareil].

| Type d’activité | Pris en charge ? |
| --- | --- |
| [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Oui |
| [affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Non |
| [ciblage automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | Non |
| [Test multivarié](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Non |
| [Ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Oui |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | Non |
| [Recommandations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | Non |
| [Activités utilisant Analytics pour Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | Oui |

## Ciblage de l’audience

Le tableau suivant indique les règles d’audience prises en charge ou non par [!UICONTROL prise de décision sur appareil].

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
| Audiences Adobe Experience Cloud<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager], et [!DNL Adobe Experience Manager]) | Non |

### Ciblage géographique pour [!UICONTROL prise de décision sur appareil]

Pour maintenir une latence minimale pour [!UICONTROL prise de décision sur appareil] activités avec des audiences basées sur la géographie, Adobe vous recommande de fournir les valeurs géographiques vous-même dans l’appel à la fonction [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). Définissez l’objet Geo dans le contexte de la requête. Cela signifie, à partir du navigateur, un moyen de déterminer l’emplacement de chaque visiteur. Par exemple, vous pouvez effectuer une recherche IP/géo à l’aide d’un service que vous configurez. Certains fournisseurs d’hébergement, tels que Google Cloud, fournissent cette fonctionnalité par le biais d’en-têtes personnalisés dans chaque `HttpServletRequest`.

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

Cependant, si vous ne parvenez pas à effectuer des recherches IP vers géo sur votre serveur, mais que vous souhaitez toujours effectuer des recherches [!UICONTROL prise de décision sur appareil] pour [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) requêtes contenant des audiences basées sur la géographie, cette fonctionnalité est également prise en charge. L’inconvénient de cette approche est qu’elle utilise une recherche distante IP/géo, ce qui ajoute une latence à chaque `getOffers` appelez . Cette latence doit être inférieure à une `getOffers` appel avec prise de décision côté serveur, car il atteint un réseau de diffusion de contenu situé près de votre serveur. Indiquez uniquement le champ &quot;ipAddress&quot; dans l’objet Geo dans le contexte de votre requête pour que le SDK récupère la géolocalisation de l’adresse IP de votre visiteur. Si un autre champ en plus de &quot;ipAddress&quot; est fourni, la variable [!DNL Target] Le SDK ne récupère pas les métadonnées de géolocalisation pour la résolution.

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

Le tableau suivant indique les méthodes d’attribution prises en charge ou non par [!UICONTROL prise de décision sur appareil].

| Méthode d’affectation | Pris en charge ? |
| --- | --- |
| Manuel | Oui |
| [Auto affecter à la meilleure expérience](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Non |
| [Ciblage automatique pour les expériences personnalisées](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Non |
