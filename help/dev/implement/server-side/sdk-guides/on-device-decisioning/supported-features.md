---
title: Quelles fonctionnalités sont prises en charge dans la prise de décision sur l’appareil ?
description: Découvrez comment diffuser du contenu personnalisé attrayant et pertinent à l’aide du machine learning à l’aide d’un appel au serveur en direct.
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
TQID: https://experienceleague.adobe.com/Fgwu8Nh90i-tS1aCUVmQReGz6DYBP2GHdcNM7z17BSk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 710
ht-degree: 9%

---

# Présentation des fonctionnalités prises en charge

Les SDK côté serveur d’[!DNL Adobe Target] offrent aux développeurs et aux développeuses la possibilité de choisir entre les performances et la fraîcheur des données pour prendre des décisions. En d’autres termes, si la diffusion du contenu personnalisé le plus pertinent et le plus attrayant via le machine learning est la plus importante pour vous, un appel au serveur en direct doit être effectué. Mais lorsque les performances sont plus critiques, une décision doit être prise sur l’appareil. Pour [!UICONTROL on-device decisioning] à fonctionner, reportez-vous à la liste suivante des fonctionnalités prises en charge :

* Types d’activité
* Ciblage d’audience
* Méthode d&#39;allocation

## Types d’activités

Le tableau suivant indique quels [types d’activité](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) créés à l’aide du [compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html ?) sont pris en charge ou non pour les [!UICONTROL on-device decisioning].

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


## Ciblage des audiences

Le tableau suivant indique les règles d’audience prises en charge ou non pour [!UICONTROL on-device decisioning].

| Règle d’audience | Prise de décision sur l’appareil |
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
| [Audiences &#x200B;](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (audiences de Adobe Audience Manager, Adobe Analytics et Adobe Experience Manager) | Non |

### Ciblage géographique pour les [!UICONTROL on-device decisioning]

Afin de maintenir une latence proche de zéro pour [!UICONTROL on-device decisioning] activités avec des audiences basées sur la zone géographique, Adobe vous recommande de fournir vous-même les valeurs géographiques dans l’appel à l’`getOffers`. Pour ce faire, définissez l’objet `Geo` dans le `Context` de la requête. Cela signifie que votre serveur doit pouvoir déterminer l’emplacement de chaque utilisateur final. Par exemple, votre serveur peut effectuer une recherche IP/zone géographique à l’aide d’un service que vous configurez. Certains fournisseurs d’hébergement, tels que Google Cloud, proposent cette fonctionnalité via des en-têtes personnalisés dans chaque `HttpServletRequest`.

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

>[!TAB Java]

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

Cependant, si vous ne pouvez pas effectuer de recherches IP à géolocalisation sur votre serveur, mais que vous souhaitez quand même effectuer des [!UICONTROL on-device decisioning] pour les requêtes `getOffers` qui contiennent des audiences géolocalisées, cela est également pris en charge. L’inconvénient de cette approche est qu’elle utilisera une recherche IP/géolocalisation à distance, ce qui ajoutera de la latence à chaque appel `getOffers`. Cette latence doit être inférieure à un appel de `getOffers` à distance, car elle atteint un réseau CDN situé près de votre serveur. Vous ne devez fournir le champ `ipAddress` que dans l’objet `Geo` dans la `Context` de votre requête, afin que le SDK récupère la géolocalisation de l’adresse IP de votre utilisateur. Si un autre champ en plus du `ipAddress` est fourni, le SDK [!DNL Target] ne récupère pas les métadonnées de géolocalisation pour la résolution.


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

>[!TAB Java]

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

## Méthode d&#39;allocation

Le tableau suivant indique les méthodes d’attribution prises en charge ou non pour [!UICONTROL on-device decisioning].

| Méthode d&#39;allocation | Pris en charge |
| --- | --- |
| Manuel | Oui |
| [&#x200B; Affectation automatique à la meilleure expérience &#x200B;](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | Non |
| [Ciblage automatique pour les expériences personnalisées](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | Non |
