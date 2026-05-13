---
title: Ciblage des audiences
description: Les audiences peuvent être utilisées pour cibler vos activités d’expérimentation et de personnalisation.  [!DNL Adobe Target]  prend en charge une myriade de puissantes fonctionnalités de ciblage d’audience prêtes à l’emploi.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
TQID: https://experienceleague.adobe.com/BmKrCmWIkEkNHiipZ-DqDlhzOT7bVmKHl9de5uXhJQU
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1069
ht-degree: 18%

---

# Ciblage des audiences

## Aperçu

Les audiences peuvent être utilisées pour cibler vos activités d’expérimentation et de personnalisation. [!DNL Adobe Target] prend en charge une myriade de puissantes fonctionnalités de ciblage d’audience prêtes à l’emploi. Les attributs suivants sont disponibles pour le [ciblage d’audience](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html?lang=fr) :

### Bibliothèque [!DNL Target]

Pour plus d’informations, voir [[!DNL Target] Bibliothèque](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html?lang=fr).
&#x200B;
* Provenant de Bing
* Navigateur Chrome
* Navigateur Firefox
* Provenant de Google
* Internet Explorer
* Système d’exploitation Linux
* Système d’exploitation Mac OS
* Nouveaux visiteurs
* Visiteurs récurrents
* Navigateur Safari
* Tablette
* Système d’exploitation Windows
* Provenant de Yahoo

### Géo

Pour plus d’informations, voir [Géo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=fr).
&#x200B;
* Pays/zone géographique
* État
* Ville
* Code postal
* Latitude
* Longitude
* Zone desservie (DMA)
* Opérateur de téléphonie mobile

### Réseau

Pour plus d’informations, voir [Réseau](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=fr).

* Fournisseur de services Internet
* Nom de domaine
* Vitesse de connexion

### Mobile

Pour plus d’informations, voir [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=fr).

* Nom marketing du périphérique
* Modèle de périphérique
* Fournisseur de périphérique
* Appareil mobile
* Téléphone mobile
* Tablette
* Système d’exploitation
* Hauteur de l’écran (px)
* Largeur de l’écran (px)

### Valeur personnalisée

Pour plus d’informations, voir [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=fr).

* toute paire clé/valeur

### Système d’exploitation

Pour plus d’informations, voir [&#x200B; Système d’exploitation &#x200B;](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=fr).

* Linux
* Macintosh
* Windows

### Pages du site

Pour plus d’informations, voir [Pages du site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=fr).

* Page actuelle
* Page précédente
* Page de destination
* En-tête HTTP

### Navigateur

Pour plus d’informations, voir [Navigateur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=fr).

* Type
* Langue
* Version

### Profil du visiteur

Pour plus d’informations, voir [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=fr).

* toute paire clé/valeur, qui est conservée

### Sources de trafic

Pour plus d’informations, voir [Sources de trafic](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=fr).

* Depuis Baidu
* Depuis Bing
* Google
* Yahoo
* Page d’entrée de référence : URL
* Page d’entrée de référence : Domaine
* Page d’entrée de référence : Requête

### Période

Pour plus d’informations, voir [Période](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=fr).

* Date de début / Date de fin

## Client Hints

[!DNL Adobe Target] nécessite des Client Hints pour la segmentation correcte des attributs de navigateur, de système d’exploitation et d’audience mobile, ainsi que de certaines instances de scripts de profil. Pour plus d’informations d’arrière-plan, voir [&#x200B; Agent utilisateur et Client Hints](../../../client-side/atjs/user-agent-and-client-hints.md).

### Comment transmettre des Client Hints à [!DNL Adobe Target]

À partir de Node.js SDK v2.4.0 et Java SDK v2.3.0, les Client Hints peuvent être envoyés à [!DNL Target] via des appels `getOffers()`. Les Client Hints doivent être inclus dans l’objet `request.context`, ainsi que l’agent utilisateur.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
targetClient.getOffers({ 
    request: { 
        context: { 
            channel: "mobile" 
            userAgent: "Mozilla/5.0 (Linux; Android 12; Pixel 4a) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36", 
            clientHints: { 
                mobile: "true", 
                platform: "Linux", 
                platformVersion: "12.1", 
                model: "Pixel 4a", 
                browserUAWithMajorVersion: "\"Not A;Brand\";v=\"98\", \"Chromium\";v=\"98\", \"Google Chrome\";v=\"98\"", 
                browserUAWithFullVersion: "\" Not A;Brand\";v=\"98.0.0.0\", \"Chromium\";v=\"98.0.4844.83\", \"Google Chrome\";v=\"98.0.4758.101\"", 
                bitness: "64", 
                architecture: "x86" 
            } 
        }, 
        execute: { 
            mboxes: [{ 
                name: "home", 
                index: 1 
            }] 
        } 
    } 
});
```

>[!TAB Java SDK]

```javascript {line-numbers="true"}
import com.adobe.target.delivery.v1.model.ClientHints; 
import com.adobe.target.delivery.v1.model.Context; 
import com.adobe.target.delivery.v1.model.ExecuteRequest; 
import com.adobe.target.edge.client.model.TargetDeliveryRequest; 

 
ClientHints clientHints = new ClientHints(); 
clientHints.setMobile(true); 
clientHints.setPlatform("macOS"); 
clientHints.setArchitecture("x86"); 
clientHints.setPlatformVersion("11.3.1"); 
clientHints.setBrowserUAWithMajorVersion( 
  "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"99\", \"Google Chrome\";v=\"99\""); 
String userAgent = 
  "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36"; 

 
TargetDeliveryRequest request = TargetDeliveryRequest.builder() 
        .execute(new ExecuteRequest().pageLoad(pageLoad)) 
        .context(new Context().clientHints(clientHints).userAgent(userAgent)) 
        .build(); 
```

>[!ENDTABS]

## Prise de décision sur l’appareil

Le tableau suivant indique les règles d’audience prises en charge ou non pour la prise de décision sur l’appareil.

| Règle d’audience | Prise de décision sur l’appareil |
| --- | --- |
| [Géo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=fr) | Oui |
| [Réseau](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=fr) | Non |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=fr) | Non |
| [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=fr) | Oui |
| [Système d’exploitation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=fr) | Oui |
| [Pages du site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=fr) | Oui |
| [Navigateur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=fr) | Oui |
| [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=fr) | Non |
| [Sources de trafic](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=fr) | Non |
| [Période](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=fr) | Oui |
| [Audiences &#x200B;](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=fr) (audiences de Adobe Audience Manager, Adobe Analytics et Adobe Experience Manager) | Non |

### Ciblage géographique pour la prise de décision sur l’appareil

Afin de maintenir une latence proche de zéro pour les activités de prise de décision sur l’appareil avec des audiences basées sur la zone géographique, Adobe vous recommande de fournir vous-même les valeurs géographiques dans l’appel à l’`getOffers`. Pour ce faire, définissez l’objet `Geo` dans le `Context` de la requête. Cela signifie que votre serveur doit pouvoir déterminer l’emplacement de chaque utilisateur final. Par exemple, votre serveur peut effectuer une recherche IP/zone géographique à l’aide d’un service que vous configurez. Certains fournisseurs d’hébergement, tels que Google Cloud, proposent cette fonctionnalité via des en-têtes personnalisés dans chaque `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

Cependant, si vous ne pouvez pas effectuer de recherches IP à géolocalisation sur votre serveur, mais que vous souhaitez toujours effectuer une prise de décision sur l’appareil pour les requêtes `getOffers` contenant des audiences géolocalisées, cela est également pris en charge. L’inconvénient de cette approche est qu’elle utilisera une recherche IP/géolocalisation à distance, ce qui ajoutera de la latence à chaque appel `getOffers`. Cette latence doit être inférieure à un appel de `getOffers` à distance, car elle atteint un réseau CDN situé près de votre serveur. Vous devez **uniquement** fournir le champ `ipAddress` dans l’objet `Geo` dans le `Context` de votre requête, afin que le SDK récupère la géolocalisation de l’adresse IP de votre utilisateur. Si un autre champ en plus du `ipAddress` est fourni, le SDK [!DNL Target] ne récupère pas les métadonnées de géolocalisation pour la résolution.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

## Prise de décision côté serveur

Le tableau suivant indique les règles d’audience prises en charge ou non pour la prise de décision côté serveur.

| Règle d’audience | Prise de décision côté serveur |
| --- | --- |
| [Géo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=fr) | Oui |
| [Réseau](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=fr) | Oui |
| [Mobile](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=fr) | Oui |
| [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=fr) | Oui |
| [Système d’exploitation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=fr) | Oui |
| [Pages du site](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=fr) | Oui |
| [Navigateur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=fr) | Oui |
| [Profil du visiteur](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=fr) | Oui |
| [Sources de trafic](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=fr) | Oui |
| [Période](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=fr) | Oui |
| [Audiences &#x200B;](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=fr) (audiences de Adobe Audience Manager, Adobe Analytics et Adobe Experience Manager) | Oui |
