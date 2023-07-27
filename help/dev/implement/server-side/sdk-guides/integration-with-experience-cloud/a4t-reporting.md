---
title: Intégration aux rapports A4T Experience Cloud
description: Intégration avec l’intégration Experience Cloud, Rapports A4T, Analytics for Target
keywords: api de diffusion, côté serveur, côté serveur, intégration, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 8%

---

# Rapports Analytics for Target (A4T)

[!DNL Adobe Target] prend en charge les rapports A4T pour la prise de décision sur les appareils et les activités Target côté serveur. Il existe deux options de configuration pour activer les rapports A4T :

* [!DNL Adobe Target] transfère automatiquement la charge utile analytics vers [!DNL Adobe Analytics], ou
* L’utilisateur demande la charge utile Analytics à partir de [!DNL Adobe Target]. ([!DNL Adobe Target] renvoie la variable [!DNL Adobe Analytics] payload vers l’appelant.)

>[!NOTE]
>
>La prise de décision sur les appareils ne prend en charge que les rapports A4T pour lesquels [!DNL Adobe Target] transfère automatiquement la charge utile analytics vers [!DNL Adobe Analytics]. Récupération de la charge utile Analytics depuis [!DNL Adobe Target] n’est pas prise en charge.

## Conditions requises

1. Configurez l’activité dans la [!DNL Adobe Target] Interface utilisateur avec [!DNL Adobe Analytics] comme source de création de rapports et assurez-vous que les comptes sont activés pour A4T.
1. L’utilisateur de l’API génère l’identifiant visiteur Adobe Marketing Cloud et s’assure que cet identifiant est disponible lors de l’exécution de la requête Target.

## [!DNL Adobe Target] transfère automatiquement la charge utile Analytics

[!DNL Adobe Target] peut transférer automatiquement la charge utile analytics vers [!DNL Adobe Analytics] si les identifiants suivants sont fournis :

1. `supplementalDataId`: identifiant utilisé pour se regrouper entre les [!DNL Adobe Analytics] et [!DNL Adobe Target]. Pour [!DNL Adobe Target] et [!DNL Adobe Analytics] pour regrouper correctement les données, la même `supplementalDataId` doit être transmis aux deux [!DNL Adobe Target] et [!DNL Adobe Analytics].
1. `trackingServer`: la variable [!DNL Adobe Analytics] Serveur.

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

>[!TAB Java ]

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

## L’utilisateur récupère la payload d’analyse depuis [!DNL Adobe Target]

Un utilisateur peut récupérer la variable [!DNL Adobe Analytics] charge utile pour une mbox donnée, puis l’envoyer à [!DNL Adobe Analytics] via le [API d’insertion de données](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Lorsqu’une [!DNL Adobe Target] est déclenchée, passe `client_side` à la fonction `logging` dans la requête. Cela renverra un payload si la mbox spécifiée est présente dans une activité qui utilise Analytics comme source de création de rapports.

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

>[!TAB Java ]

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

Une fois que vous avez spécifié `logging = client_side`, vous recevrez la charge utile dans le champ de mbox.

Si la réponse de Target contient quelque chose dans la variable `analytics -> payload` propriété, transférez-la tel qu’il est à [!DNL Adobe Analytics]. [!DNL Adobe Analytics] sait comment traiter cette payload. Vous pouvez le faire dans une requête de GET au format suivant :

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Paramètres et variables de chaîne de requête

| Nom du champ | Requis | Description |
| --- | --- | --- |
| `rsid` | Oui | Identifiant de la suite de rapports |
| `pe` | Oui | Événement de page. Toujours définie sur `tnt` |
| `tnta` | Oui | Charge utile Analytics renvoyée par le serveur Target dans `analytics -> payload -> tnta` |
| `mid` | Oui | Identifiant visiteur Marketing Cloud |

### Valeurs d’en-tête requises

| Nom de l&#39;en-tête | Valeur de l&#39;en-tête |
| --- | --- |
| Hôte | Serveur de collecte de données Analytics (par exemple : `adobeags421.sc.omtrdc.net`) |

### Exemple d’appel de récupération HTTP pour l’insertion de données A4T

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
