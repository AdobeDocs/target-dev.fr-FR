---
title: Envoyez des notifications d’affichage ou de clic à  [!DNL Adobe Target] ’aide du SDK Node.js.
description: Découvrez comment utiliser sendNotifications() pour envoyer des notifications d’affichage ou de clic à des  [!DNL Adobe Target]  de mesure et de création de rapports.
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
TQID: https://experienceleague.adobe.com/-YiepZ5Rqm7JFTUuYKxQc2ISL5EZ9nvW-K0M-aoaleU
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 246
ht-degree: 4%

---

# Envoi de notifications (Node.js)

## Description

`[!UICONTROL sendNotifications()]` sert à envoyer des notifications d’affichage ou de clic aux [!DNL Adobe Target] pour la mesure et le compte rendu des performances.

>[!NOTE]
>
>Lorsqu’un objet `execute` avec les paramètres requis se trouve dans la requête elle-même, l’impression est incrémentée automatiquement pour les activités de qualification.

Les méthodes SDK qui incrémentent automatiquement une impression sont les suivantes :

* `getOffers()`
* `getAttributes()`

Lorsqu’un objet `prefetch` est transmis dans la requête, l’impression n’est pas automatiquement incrémentée pour les activités comportant des mbox au sein de l’objet `prefetch`. `sendNotifications()` doit être utilisé pour les expériences prérécupérées afin d’incrémenter les impressions et les conversions.

## Méthode

### créer

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

### Paramètres

`options` présente la structure suivante :

| Nom | Type | Requis | Par défaut |
| --- | --- | --- | --- |
| events | Objet | Oui | None |

## Exemple

Tout d’abord, nous allons créer la requête dAPI de diffusion Target pour prérécupérer du contenu pour les mbox `home` et `product1`.

### Node.js

```js {line-numbers="true"}
const prefetchMboxesRequest = {
  prefetch: {
    mboxes: [
      { name: "home" },
      { name: "product1" }
    ]
  }
};
// Next, we fetch the offers via Target Node.js SDK getOffers() API
const targetResponse = await targetClient.getOffers({ request: prefetchMboxesRequest });
```

Une réponse réussie contient un objet de réponse [!UICONTROL Target Delivery API], qui contient du contenu prérécupéré pour les mbox demandées. Un exemple d’objet `targetResponse.response` peut se présenter comme suit :

### Node.js

```js {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

Notez les champs `name` et `state` de la mbox, ainsi que le champ `eventToken`, dans chacune des options de contenu [!DNL Target]. Ils doivent être fournis dans la requête `sendNotifications()`, dès que chaque option de contenu est affichée. Supposons que la mbox `product1` ait été affichée sur un appareil qui n’est pas un navigateur. La demande de notifications se présente comme suit :

### Node.js

```js {line-numbers="true"}
const mboxNotificationRequest = {
  notifications: [{
    id: "1",
    timestamp: Date.now(),
    type: "display",
    mbox: {
      name: "product1",
      state: "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    },
    tokens: [ "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" ]
  }]
};
```

Notez que nous avons inclus l’état de la mbox et le jeton d’événement correspondant à l’offre [!DNL Target] diffusée dans la réponse de prérécupération. Après avoir créé la requête de notifications, nous pouvons l’envoyer à [!DNL Target] via la méthode de l’API `sendNotifications()` :

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
