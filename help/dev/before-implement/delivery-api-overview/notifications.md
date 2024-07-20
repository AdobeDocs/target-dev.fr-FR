---
title: Notifications de l’API de diffusion Adobe Target
description: Comment déclencher des notifications à l’aide de [!UICONTROL Adobe Target Delivery API] ?
keywords: api de diffusion
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Notifications

Les notifications doivent être déclenchées lorsqu’une mbox ou une vue prérécupérée a été visitée ou rendue à l’utilisateur final.

Pour que les notifications soient déclenchées pour la mbox ou la vue appropriée, veillez à suivre le `eventToken` correspondant pour chaque mbox ou vue. Les notifications comportant le `eventToken` correct pour les mbox ou vues correspondantes doivent être déclenchées afin que la création de rapports soit correctement reflétée.

## Notifications des mbox prérécupérées

Une ou plusieurs notifications peuvent être envoyées via un seul appel de diffusion. Déterminez si la mesure qui doit faire l’objet d’un suivi est `click` ou `display` pour chaque mbox, de sorte que l’ `type` de la notification puisse être correctement reflétée. Transmettez également un `id` pour chaque notification afin que vous puissiez déterminer si une notification a été correctement envoyée via le [!UICONTROL  Adobe Target Delivery API]. `timestamp` doit également être transféré vers [!DNL Target] pour indiquer le moment où `click` ou `display` s’est produit pour une mbox donnée à des fins de création de rapports.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
    "id": {
      "tntId": "abcdefghijkl00023.1_1"
    },
    "context": {
      "channel": "web",
      "browser" : {
        "host" : "demo"
      },
      "address" : {
        "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
      },
      "screen" : {
        "width" : 1200,
        "height": 1400
      }
    },
      "notifications": [
      {
      "id" : "SummerOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerShoesOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerShoesOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerDressOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerDressOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
    } 
    ]
  }'
```

L’exemple d’appel ci-dessus entraînera une réponse indiquant que la requête `notifications` a été traitée avec succès.

```
{
  "status": 200,
  "requestId": "36014eed-4772-4c48-a9e2-e532762b6a85",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "notifications": [
      {
          "id": "SummerOfferNotification"
      },
      {
          "id": "SummerDressOfferNotification"
      },
      {
          "id": "SummerShoesOfferNotification"
      }
  ]
}
```

Si tous les `notifications` envoyés à [!DNL Target] sont correctement traités, ils apparaîtront dans le tableau `notifications` de la réponse. Cependant, si un `notifications` `id` est manquant, cet `notification` particulier n&#39;a pas été parcouru. Dans ce scénario, une logique de reprise peut être mise en place jusqu’à ce qu’une réponse `notification` réussie soit récupérée. Assurez-vous que le délai d’expiration de la logique de reprise est spécifié afin que l’appel de l’API ne bloque pas et n’entraîne pas de retards en termes de performances.

## Notifications des vues prérécupérées

Une ou plusieurs notifications peuvent être envoyées via un seul appel de diffusion. Déterminez si la mesure qui doit faire l’objet d’un suivi est `click` ou `display` pour chaque mbox afin que le type de notification puisse être correctement reflété. Transmettez également un `id` pour chaque notification afin que vous puissiez déterminer si une notification a été correctement envoyée via le [!UICONTROL Adobe Target Delivery API]. L’horodatage est également important à transférer vers [!DNL Target] pour indiquer quand `click` ou `display` s’est produit pour une vue donnée à des fins de création de rapports.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "notifications": [{
      "id": "228",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "checkout-express",
      }
    },
    {
      "id": "5",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "home",
      }
    },
    {
      "id": "6",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "products",
      }
    }
  ]
}'
```

L’exemple d’appel ci-dessus entraînera une réponse indiquant que la requête `notifications` a été traitée avec succès.

```
{
    "status": 200,
    "requestId": "85cc7394-c19a-4398-9b8b-bbee1e4c4579",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "notifications": [
        {
            "id": "5"
        },
        {
            "id": "6"
        },
        {
            "id": "228"
        }
    ]
}
```

Si tous les `notifications` envoyés à [!DNL Target] sont correctement traités, ils apparaîtront dans le tableau `notifications` de la réponse. Cependant, si un `notifications` `id` est manquant, cette notification particulière n&#39;a pas été envoyée. Dans ce scénario, une logique de reprise peut être mise en place jusqu’à ce qu’une réponse de notification réussie soit récupérée. Assurez-vous que le délai d’expiration de la logique de reprise est spécifié afin que l’appel de l’API ne bloque pas et n’entraîne pas de retards en termes de performances.
