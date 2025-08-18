---
title: Intégration aux rapports A4T Experience Cloud
description: Intégration à Experience Cloud, rapports A4T, intégration d’Analytics for Target
keywords: api de diffusion, côté serveur, côté serveur, intégration, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: cbae0f1758fb0dee4837e8c237f8617ecb46eb25
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 6%

---

# Rapports [!UICONTROL Analytics for Target] (A4T)

[!DNL Adobe Target] prend en charge les rapports A4T pour les activités de prise de décision sur l’appareil et de [!DNL Target] côté serveur. Il existe deux options de configuration pour activer les rapports A4T :

* [!DNL Adobe Target] transfère automatiquement la payload d’analytics vers [!DNL Adobe Analytics], ou
* L’utilisateur demande la payload d’analyse à [!DNL Adobe Target]. ([!DNL Adobe Target] renvoie la payload [!DNL Adobe Analytics] à l’appelant.)

>[!NOTE]
>
>La prise de décision sur l’appareil ne prend en charge que les rapports A4T, dont [!DNL Adobe Target] transfère automatiquement la payload Analytics vers [!DNL Adobe Analytics]. La récupération de la payload d’analyse de [!DNL Adobe Target] n’est pas prise en charge.

## Conditions requises

1. Configurez l’activité dans l’interface utilisateur de [!DNL Adobe Target] avec [!DNL Adobe Analytics] comme source de création de rapports et assurez-vous que les comptes sont activés pour A4T.
1. L’utilisateur de l’API génère la [!UICONTROL Marketing Cloud Visitor ID] Adobe et s’assure que cet identifiant est disponible lors de l’exécution de la requête [!DNL Target].

## [!DNL Adobe Target] transfère automatiquement la payload [!DNL Analytics]

[!DNL Adobe Target] pouvez transférer automatiquement la payload d’analyse vers [!DNL Adobe Analytics] si les identifiants suivants sont fournis :

1. `supplementalDataId` : ID utilisé pour regrouper les [!DNL Adobe Analytics] et les [!DNL Adobe Target]. Pour que [!DNL Adobe Target] et [!DNL Adobe Analytics] assemblent correctement les données, le même `supplementalDataId` doit être transmis à la fois à [!DNL Adobe Target] et à [!DNL Adobe Analytics].
1. `trackingServer` : le serveur [!DNL Adobe Analytics].

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## L’utilisateur récupère la payload d’analyse de [!DNL Adobe Target]

Un utilisateur peut récupérer la payload de [!DNL Adobe Analytics] pour une mbox donnée, puis l’envoyer à [!DNL Adobe Analytics] via l’[API Data Insertion](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Lorsqu’une requête [!DNL Adobe Target] est déclenchée, transmettez le `client_side` au champ `logging` de la requête. Cette requête renvoie une payload si la mbox spécifiée est présente dans une activité qui utilise [!DNL Analytics] comme source de création de rapports.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const targetClient = TargetClient.create(CONFIG);
targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Une fois que vous avez spécifié `logging = client_side`, vous recevez la payload dans le champ mbox .

Si la réponse de [!DNL Target] contient des éléments dans la propriété `analytics -> payload` , transférez-la telle quelle à [!DNL Adobe Analytics]. [!DNL Adobe Analytics] sait comment traiter cette payload. Cette opération peut être effectuée dans une requête GET à l’aide du format suivant :

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/{content_type_num}/{code_ver}/{session}?pe=tnt&tnta={payload}&c.&a.&target.&sessionId={sessionId}&.target&.a&.c&mid={mid}
```

### Paramètres de chaîne de requête et variables

| Nom du champ | Requis | Description |
| --- | --- | --- |
| `rsid` | Oui | Identifiant de la suite de rapports |
| `content_type_num` | Oui | Toujours définie sur « 0 » |
| `code_ver` | Oui | Toujours définie sur « MOBILE-1.0 » |
| `session` | Oui | Toujours définie sur « 0 » |
| `pe` | Oui | Événement de page. Toujours définie sur `tnt` |
| `tnta` | Oui | Payload [!DNL Analytics] renvoyée par [!DNL Target] serveur dans `analytics -> payload -> tnta` |
| `sessionId` | Oui | ID de session [!DNL Target] de la session en cours |
| `mid` | Oui | Identifiant visiteur Marketing Cloud |

### Valeurs d’en-tête obligatoires

| Nom de l’en-tête | Valeur de l’en-tête |
| --- | --- |
| Hôte | Serveur de collecte de données Analytics (par exemple : `adobeags421.sc.omtrdc.net`) |

### Exemple d’appel HTTP Get d’insertion de données A4T

Version non encodée en URL pour la lisibilité (format à ne pas utiliser pour les appels API) :

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236:0:0|0,253236:0:0|2,253236:0:0|1,253613:0:0|0,253613:0:0|2,253613:0:0|1&c.&a.&target.&sessionId=45c08980-f4b9-4e11-96db-067d58e49f74&.target&.a&.c&pe=tnt&mid=69170113867710665996968872592584719577
```

Version encodée en URL (format à utiliser pour les appels API) :

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236%3A0%3A0%7C0%2C253236%3A0%3A0%7C2%2C253236%3A0%3A0%7C1%2C253613%3A0%3A0%7C0%2C253613%3A0%3A0%7C2%2C253613%3A0%3A0%7C1&c.%26a.%26target.%26sessionId=45c08980-f4b9-4e11-96db-067d58e49f74%26.target%26.a%26.c&pe=tnt&mid=69170113867710665996968872592584719577 
```
