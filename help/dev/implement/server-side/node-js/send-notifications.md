---
title: Envoi de notifications d’affichage ou de clic sur [!DNL Adobe Target] utilisation du SDK Node.js
description: Découvrez comment utiliser sendNotifications() pour envoyer des notifications d’affichage ou de clic à [!DNL Adobe Target] pour les mesures et les rapports.
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 4%

---

# Envoi de notifications (Node.js)

## Description

`[!UICONTROL sendNotifications()]` est utilisé pour envoyer des notifications d’affichage ou de clic à [!DNL Adobe Target] pour les mesures et les rapports.

>[!NOTE]
>
>Lorsqu’une `execute` avec les paramètres requis se trouve dans la requête elle-même, l’impression sera incrémentée automatiquement pour les activités admissibles.

Les méthodes du SDK qui incrémenteront automatiquement une impression sont les suivantes :

* `getOffers()`
* `getAttributes()`

Lorsqu’une `prefetch` est transmis dans la requête, l’impression n’est pas automatiquement incrémentée pour les activités comportant des mbox dans la `prefetch` . `sendNotifications()` doit être utilisé pour les expériences prérécupérées afin d’incrémenter les impressions et les conversions.

## Méthode

### create

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

### Paramètres

`options` possède la structure suivante :

| Nom | Type | Requis | Par défaut |
| --- | --- | --- | --- |
| events | Objet | Oui | None |

## Exemple

Commençons par créer le D cible.Requête d’API de diffusion pour la prérécupération de contenu pour la variable `home` et `product1` mbox.

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

Une réponse réussie contient une [!UICONTROL API de diffusion Target] objet de réponse, qui contient du contenu prérécupéré pour les mbox demandées. Un exemple `targetResponse.response` peut se présenter comme suit :

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

Notez la mbox `name` et `state` , ainsi que la variable `eventToken` , dans chacun des [!DNL Target] options de contenu. Elles doivent être fournies dans la variable `sendNotifications()` dès que chaque option de contenu est affichée. Supposons que la variable `product1` mbox s’affiche sur un périphérique autre que le navigateur. La demande de notification s’affiche comme suit :

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

Notez que nous avons inclus à la fois l’état de mbox et le jeton d’événement correspondant au [!DNL Target] offre fournie dans la réponse de prérécupération. Une fois la requête de notification créée, nous pouvons l’envoyer à [!DNL Target] via le `sendNotifications()` Méthode d’API :

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
