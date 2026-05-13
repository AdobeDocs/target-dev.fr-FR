---
title: Envoyez des notifications d’affichage ou de clic à à  [!DNL Adobe Target] ’aide de .NET SDK
description: Découvrez comment utiliser sendNotifications() pour envoyer des notifications d’affichage ou de clic à des  [!DNL Adobe Target]  de mesure et de création de rapports.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
TQID: https://experienceleague.adobe.com/4lJvfqWv6vDehZ-CmO7xj61-ZFS9-3nOAcA7vlbg-3c
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 1%

---

# Envoyer des notifications (.NET)

## Description

`SendNotifications()` sert à envoyer des notifications d’affichage ou de clic aux [!DNL Adobe Target] pour la mesure et le compte rendu des performances.

>[!NOTE]
>
>Lorsqu’un objet `Execute` avec les paramètres requis se trouve dans la requête elle-même, l’impression est incrémentée automatiquement pour les activités de qualification.

Les méthodes SDK qui incrémentent automatiquement une impression sont les suivantes :

* `GetOffers()`
* `GetAttributes()`

Lorsqu’un objet `Prefetch` est transmis dans la requête, l’impression n’est pas automatiquement incrémentée pour les activités comportant des mbox au sein de l’objet `Prefetch`. `SendNotifications()` doit être utilisé pour les expériences prérécupérées afin d’incrémenter les impressions et les conversions.

## Méthode

### Créer

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## Exemple

Tout d’abord, nous allons créer la requête [!UICONTROL Target Delivery API] pour la prérécupération du contenu des mbox `home` et `product1`.

### \.NET

```dotnet {line-numbers="true"}
var mboxRequests = new List<MboxRequest>
    {
        new (index: 1, name: "home"),
        new (index: 2, name: "product1"),
    };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetPrefetch(new PrefetchRequest(mboxes: mboxRequests))
    .Build();

// Next, we fetch the offers via Target .NET SDK GetOffers() API
var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```

Une réponse réussie contient un objet de réponse [!DNL Target Delivery API], qui contient du contenu prérécupéré pour les mbox demandées. Un exemple d’objet `targetResponse.Response` peut se présenter comme suit :

### \.NET

```dotnet {line-numbers="true"}
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

Notez le nom du `mbox` et les champs `state`, ainsi que le champ `eventToken`, dans chacune des options de contenu [!DNL Target]. Ils doivent être fournis dans la requête `SendNotifications()`, dès que chaque option de contenu est affichée. Supposons que la mbox `product1` ait été affichée sur un appareil qui n’est pas un navigateur. La demande de notifications se présente comme suit :

### \.NET

```dotnet {line-numbers="true"}
var mboxNotifications = new List<Notification>
{
    new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
        mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
        tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
}; 

var mboxNotificationRequest = new TargetDeliveryRequest.Builder()
    .SetNotifications(mboxNotifications)
    .Build();
```

Notez que nous avons inclus l’état de la mbox et le jeton d’événement correspondant à l’offre [!DNL Target] diffusée dans la réponse de prérécupération. Après avoir créé la requête de notifications, nous pouvons l’envoyer à [!DNL Target] via la méthode de l’API `SendNotifications()` :

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
