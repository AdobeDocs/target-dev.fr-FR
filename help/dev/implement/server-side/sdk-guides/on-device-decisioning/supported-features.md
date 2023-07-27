---
title: Quelles fonctionnalités sont prises en charge dans la prise de décision sur l’appareil ?
description: Découvrez comment diffuser le contenu personnalisé le plus pertinent et attrayant via l’apprentissage automatique à l’aide d’un appel au serveur en direct.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 10%

---

# Présentation des fonctionnalités prises en charge

[!DNL Adobe Target]Les SDK côté serveur permettent aux développeurs de choisir entre les performances et l’actualisation des données pour les décisions. En d’autres termes, si la diffusion de contenu personnalisé le plus pertinent et attrayant par le biais de l’apprentissage automatique est la plus importante pour vous, un appel au serveur en direct doit être effectué. Mais lorsque les performances sont plus critiques, une décision doit être prise sur l’appareil. Pour [!UICONTROL prise de décision sur appareil] pour travailler, reportez-vous à la liste suivante des fonctionnalités prises en charge :

* Types d’activité
* Ciblage d’audience
* Méthode d’affectation

## Types d’activités

Le tableau suivant indique laquelle [types d’activités](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) créé à l’aide de la fonction [Compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?) sont prises en charge ou non prises en charge pour [!UICONTROL prise de décision sur appareil].

| Type d’activité | Pris en charge |
| --- | --- |
| [Test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | Oui |
| [affectation automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Non |
| [ciblage automatique](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | Non |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) | Oui |
| [Test multivarié](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | Non |
| [Ciblage d’expérience](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | Oui |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) | Non |
| [Recommandations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) | Non |


## Ciblage de l’audience

Le tableau suivant indique les règles d’audience prises en charge ou non par [!UICONTROL prise de décision sur appareil].

| Règle d’audience | Prise de décision sur appareil |
| --- | --- |
| [Géo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | Oui |
| [Réseau](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | Non |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | Non |
| [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | Oui |
| [Système d’exploitation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | Oui |
| [Pages du site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | Oui |
| [Navigateur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | Oui |
| [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | Non |
| [Sources de trafic](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | Non |
| [Période](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | Oui |
| [Audiences Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Audiences de Adobe Audience Manager, Adobe Analytics et Adobe Experience Manager | Non |

### Ciblage géographique pour [!UICONTROL prise de décision sur appareil]

Pour maintenir une latence proche de zéro pour [!UICONTROL prise de décision sur appareil] activités avec des audiences basées sur la géographie, Adobe vous recommande de fournir les valeurs géographiques vous-même dans l’appel à la fonction `getOffers`. Pour ce faire, définissez la variable `Geo` dans le `Context` de la requête. Cela signifie que votre serveur aura besoin d’un moyen de déterminer l’emplacement de chaque utilisateur final. Par exemple, votre serveur peut effectuer une recherche IP/géo à l’aide d’un service que vous configurez. Certains fournisseurs d’hébergement, tels que Google Cloud, fournissent cette fonctionnalité par le biais d’en-têtes personnalisés dans chaque `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java ]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(ipToGeoLookup(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

    public static Geo ipToGeoLookup(String ip) {
        GeoResult geoResult = geoLookupService.lookup(ip);
        return new Geo()
            .city(geoResult.getCity())
            .stateCode(geoResult.getStateCode())
            .countryCode(geoResult.getCountryCode());
    }

}
```

>[!ENDTABS]

Cependant, si vous ne pouvez pas effectuer de recherches IP vers géo sur votre serveur, mais que vous souhaitez toujours effectuer des recherches [!UICONTROL prise de décision sur appareil] pour `getOffers` requêtes contenant des audiences basées sur la géographie, cette fonctionnalité est également prise en charge. L’inconvénient de cette approche est qu’elle utilise une recherche IP/géo distante, ce qui ajoute une latence à chaque `getOffers` appelez . Cette latence doit être inférieure à une valeur distante `getOffers` , puisqu’il atteint un réseau de diffusion de contenu situé près de votre serveur. Vous ne devez fournir que la variable `ipAddress` dans le champ `Geo` dans le `Context` de votre requête, afin que le SDK récupère la géolocalisation de l’adresse IP de votre utilisateur. Si un autre champ s’ajoute à la variable `ipAddress` est fourni, la variable [!DNL Target] Le SDK ne récupère pas les métadonnées de géolocalisation pour la résolution.


>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java ]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(new Geo().ipAddress(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

}
```

>[!ENDTABS]

## Méthode d’affectation

Le tableau suivant indique les méthodes d’attribution prises en charge ou non par [!UICONTROL prise de décision sur appareil].

| Méthode d’affectation | Pris en charge |
| --- | --- |
| Manuel | Oui |
| [Auto affecter à la meilleure expérience](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Non |
| [Ciblage automatique pour les expériences personnalisées](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | Non |
