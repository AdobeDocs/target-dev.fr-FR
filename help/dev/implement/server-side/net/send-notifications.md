---
title: Envoyez des notifications d’affichage ou de clic à  [!DNL Adobe Target] à l’aide du SDK .NET
description: Découvrez comment utiliser sendNotifications() pour envoyer des notifications d’affichage ou de clic à  [!DNL Adobe Target] pour la mesure et la création de rapports.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Envoi de notifications (.NET)

## Description

`SendNotifications()` est utilisé pour envoyer des notifications d’affichage ou de clic à [!DNL Adobe Target] pour la mesure et la création de rapports.

>[!NOTE]
>
>Lorsqu’un objet `Execute` avec les paramètres requis se trouve dans la requête elle-même, l’impression est incrémentée automatiquement pour les activités admissibles.

Les méthodes du SDK qui incrémenteront automatiquement une impression sont les suivantes :

* `GetOffers()`
* `GetAttributes()`

Lorsqu’un objet `Prefetch` est transmis dans la requête, l’impression n’est pas automatiquement incrémentée pour les activités comportant des mbox dans l’objet `Prefetch`. `SendNotifications()` doit être utilisé pour les expériences prérécupérées afin d’incrémenter les impressions et les conversions.

## Méthode

### Créer 

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## Exemple

Commençons par créer la requête [!UICONTROL Target Delivery API] pour la prérécupération de contenu pour les mbox `home` et `product1`.

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

Une réponse réussie contient un objet de réponse [!DNL Target Delivery API], qui contient le contenu prérécupéré pour les mbox demandées. Un exemple d’objet `targetResponse.Response` peut se présenter comme suit :

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

Notez les champs `mbox` name et `state`, ainsi que le champ `eventToken`, dans chacune des options de contenu [!DNL Target]. Elles doivent être fournies dans la requête `SendNotifications()`, dès que chaque option de contenu est affichée. Supposons que la mbox `product1` ait été affichée sur un périphérique autre que le navigateur. La demande de notification s’affiche comme suit :

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

Notez que nous avons inclus à la fois l’état mbox et le jeton d’événement correspondant à l’offre [!DNL Target] fournie dans la réponse de prérécupération. Une fois la requête de notifications créée, nous pouvons l’envoyer à [!DNL Target] via la méthode d’API `SendNotifications()` :

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
