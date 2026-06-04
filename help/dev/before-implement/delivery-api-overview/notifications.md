---
title: Notifications de l’API de diffusion Adobe Target
description: Comment déclencher des notifications à l’aide de l’API de diffusion [!UICONTROL Adobe Target &#x200B;] ?
keywords: API de diffusion
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/rooWLG-bh7lu7eBELTQys3KoNtS-6ZicxfHoQcU6TU0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 426
ht-degree: 0%

---

# Notifications

Les notifications doivent être déclenchées lorsqu’une mbox ou une vue prérécupérée a été visitée ou rendue à l’utilisateur final.

Pour que les notifications soient déclenchées pour la mbox ou la vue appropriée, assurez-vous de conserver une trace du `eventToken` correspondant pour chaque mbox ou vue. Les notifications avec le `eventToken` correct pour les mbox ou les vues correspondantes doivent être déclenchées pour que les rapports soient correctement reflétés.

## Notifications pour les mBox prérécupérées

Une ou plusieurs notifications peuvent être envoyées via un seul appel de diffusion. Déterminez si la mesure qui doit être suivie est un `click` ou un `display` pour chaque mbox afin que le `type` de la notification puisse être correctement reflété. Transmettez également un `id` pour chaque notification afin que vous puissiez déterminer si une notification a été envoyée correctement via l’API de diffusion [!UICONTROL &#x200B; Adobe Target]. Il est également important de transmettre le `timestamp` à [!DNL Target] pour indiquer le moment où le `click` ou le `display` s’est produit pour une mbox donnée à des fins de création de rapports.

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

L’exemple d’appel ci-dessus entraîne une réponse indiquant que la demande `notifications` a été traitée avec succès.

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

Si toutes les `notifications` envoyées à [!DNL Target] sont correctement traitées, elles apparaîtront dans le tableau `notifications` dans la réponse. Toutefois, si un `id` de `notifications` est manquant, ce `notification` n&#39;a pas été adopté. Dans ce scénario, une logique de reprise peut être mise en place jusqu’à ce qu’une réponse `notification` réussie soit récupérée. Assurez-vous que la logique de reprise a un délai d’expiration spécifié afin que l’appel API ne se bloque pas et ne provoque pas de retards de performances.

## Notifications pour les vues prérécupérées

Une ou plusieurs notifications peuvent être envoyées via un seul appel de diffusion. Déterminez si la mesure qui doit être suivie est un `click` ou un `display` pour chaque mbox afin que le type de notification puisse être reflété correctement. Transmettez également un `id` pour chaque notification afin que vous puissiez déterminer si une notification a été envoyée correctement via l’API de diffusion [!UICONTROL Adobe Target]. L’horodatage est également important à transmettre à [!DNL Target] pour indiquer le moment où la `click` ou la `display` s’est produite pour une vue donnée à des fins de création de rapports.

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

L’exemple d’appel ci-dessus entraîne une réponse indiquant que la demande `notifications` a été traitée avec succès.

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

Si toutes les `notifications` envoyées à [!DNL Target] sont correctement traitées, elles apparaîtront dans le tableau `notifications` dans la réponse. Toutefois, si un `id` de `notifications` est manquant, cette notification particulière n&#39;a pas été transmise. Dans ce scénario, une logique de reprise peut être mise en place jusqu’à ce qu’une réponse de notification réussie soit récupérée. Assurez-vous que la logique de reprise a un délai d’expiration spécifié afin que l’appel API ne se bloque pas et ne provoque pas de retards de performances.
