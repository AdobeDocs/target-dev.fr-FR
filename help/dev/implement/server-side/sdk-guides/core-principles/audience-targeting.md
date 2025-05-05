---
title: Ciblage de l’audience
description: Les audiences peuvent être utilisées pour cibler vos activités d’expérimentation et de personnalisation. [!DNL Adobe Target]  prend en charge une myriade de puissantes fonctionnalités de ciblage d’audience prêtes à l’emploi.
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 26%

---

# Ciblage de l’audience

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

Pour plus d’informations, voir [Geo](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=fr).
&#x200B; &#x200B;
* Pays/zone géographique
* État
* Ville
* Code postal
* Latitude
* Longitude
* Zone desservie (DMA)
* Opérateur de téléphonie mobile

### Réseau

Pour plus d’informations, voir [Network](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=fr).

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

### Personnalisé

Pour plus d’informations, voir [Paramètres personnalisés](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=fr).

* n’importe quelle paire clé/valeur

### Système d’exploitation

Pour plus d’informations, voir [Système d’exploitation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=fr).

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

* toute paire clé/valeur qui est conservée.

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

## Conseils au client

[!DNL Adobe Target] nécessite des conseils client pour une segmentation correcte des attributs de navigateur, système d’exploitation et audience mobile, ainsi que certaines instances de scripts de profil. Pour plus d’informations, voir [Agent utilisateur et conseils client](../../../client-side/atjs/user-agent-and-client-hints.md).

### Comment transmettre des conseils au client à [!DNL Adobe Target]

À partir du SDK Node.js v2.4.0 et du SDK Java v2.3.0, les conseils client peuvent être envoyés à [!DNL Target] via des appels `getOffers()`. Les conseils client doivent être inclus dans l’objet `request.context`, avec l’agent utilisateur.

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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

Le tableau suivant indique les règles d’audience prises en charge ou non pour la prise de décision sur les appareils.

| Règle d’audience | Prise de décision sur appareil |
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
| [Audiences Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=fr) (audiences de Adobe Audience Manager, Adobe Analytics et Adobe Experience Manager) | Non |

### Ciblage géographique pour la prise de décision sur les appareils

Afin de maintenir une latence proche de zéro pour les activités de prise de décision sur l’appareil avec des audiences basées sur la géolocalisation, Adobe vous recommande de fournir les valeurs géographiques vous-même dans l’appel à `getOffers`. Pour ce faire, définissez l’objet `Geo` dans le `Context` de la requête. Cela signifie que votre serveur aura besoin d’un moyen de déterminer l’emplacement de chaque utilisateur final. Par exemple, votre serveur peut effectuer une recherche IP/géo à l’aide d’un service que vous configurez. Certains fournisseurs d’hébergement, tels que Google Cloud, fournissent cette fonctionnalité par le biais d’en-têtes personnalisés dans chaque `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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

Cependant, si vous ne pouvez pas effectuer de recherches IP vers géo sur votre serveur, mais que vous souhaitez toujours effectuer une prise de décision sur l’appareil pour les demandes `getOffers` contenant des audiences basées sur la géographie, cette prise en charge est également effectuée. L’inconvénient de cette approche est qu’elle utilise une recherche IP/géo distante, ce qui ajoute une latence à chaque appel `getOffers`. Cette latence doit être inférieure à un appel `getOffers` distant, puisqu’elle atteint un réseau de diffusion de contenu situé près de votre serveur. Vous devez **uniquement** fournir le champ `ipAddress` dans l’objet `Geo` dans l’objet `Context` de votre requête, afin que le SDK puisse récupérer la géolocalisation de l’adresse IP de votre utilisateur. Si un autre champ en plus de `ipAddress` est fourni, le SDK [!DNL Target] ne récupérera pas les métadonnées de géolocalisation pour la résolution.

>[!BEGINTABS]

>[!TAB SDK Node.js]

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

>[!TAB SDK Java]

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
| [Audiences Experience Cloud](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=fr) (audiences de Adobe Audience Manager, Adobe Analytics et Adobe Experience Manager) | Oui |
