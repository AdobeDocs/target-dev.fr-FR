---
title: Utilisation de requêtes asynchrones dans la variable [!DNL Adobe Target] SDK .NET
description: Découvrez comment [!DNL Target] Le SDK Java prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.
feature: APIs/SDKs
exl-id: fd36cc7b-a884-4e57-93c2-8aff8256109a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 4%

---

# Requêtes asynchrones (.NET)

## Description

L’un des avantages de l’intégration côté serveur réside dans le fait que l’on peut exploiter l’énorme bande passante et les ressources informatiques disponibles côté serveur en utilisant le parallélisme. [!DNL Target] Le SDK .NET prend en charge les requêtes asynchrones, ce qui facilite l’intégration. [!DNL Target] dans le processus asynchrone existant d’une application.

## Méthodes prises en charge

### \.NET

```dotnet {line-numbers="true"}
Task<TargetDeliveryResponse> GetOffersAsync(TargetDeliveryRequest request);
Task<TargetDeliveryResponse> SendNotificationsAsync(TargetDeliveryRequest request);
Task<TargetAttributes> GetAttributesAsync(TargetDeliveryRequest request, params string[] mboxes);
```

## Exemple

Voici un exemple d’utilisation de l’API SDK asynchrone :

### \.NET

```dotnet {line-numbers="true"}
var deliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { new MboxRequest(index: 1, name: "a1-serverside-ab") }))
    .Build();

var response = await this.targetClient.GetOffersAsync(deliveryRequest);

var notificationRequest = new TargetDeliveryRequest.Builder()
    .SetSessionId(response.Request.SessionId)
    .SetTntId(response.Response?.Id?.TntId)
    .SetNotifications(new List<Notification>
        {
            new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
                mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
                tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
        })
    .Build();

var notificationResponse = await this.targetClient.SendNotificationsAsync(notificationRequest);
```

Cet exemple suppose que vous avez [initialisation du SDK](initialize-sdk.md).
