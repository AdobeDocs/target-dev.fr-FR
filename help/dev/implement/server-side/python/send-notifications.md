---
title: Envoi de notifications d’affichage ou de clic sur [!DNL Adobe Target] utilisation du SDK Python
description: Découvrez comment utiliser sendNotifications() pour envoyer des notifications d’affichage ou de clic à [!DNL Adobe Target] pour les mesures et les rapports.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 8%

---

# Envoyer des notifications (Python)

## Description

`send_notifications()` est utilisé pour envoyer des notifications d’affichage ou de clic à [!DNL Adobe Target] pour les mesures et les rapports.

>[!NOTE]
>
>Lorsqu’une `execute` avec les paramètres requis se trouve dans la requête elle-même, l’impression sera incrémentée automatiquement pour les activités admissibles.

Les méthodes du SDK qui incrémenteront automatiquement une impression sont les suivantes :

* `get_offers()`
* `get_attributes()`

Lorsqu’une `prefetch` est transmis dans la requête, l’impression n’est pas automatiquement incrémentée pour les activités comportant des mbox dans la `prefetch` . `Send_notifications()` doit être utilisé pour les expériences prérécupérées afin d’incrémenter les impressions et les conversions.

## Méthode

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Paramètres

`options` possède la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| events | DeliveryRequest | Oui | None | Se conforme à la variable [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) requête |
| target_cookie | str | non | None | [!DNL Target] cookie |
| target_location_hint | str | non | None | [!DNL Target] indicateur de location |
| consumer_id | str | non | None | Lors de la combinaison de plusieurs appels, différents identifiants de consommateur doivent être fournis. |
| customer_ids | list[CustomerId] | non | None | Liste des ID de client au format compatible avec VisitorId |
| session_id | str | non | None | Utilisé pour lier plusieurs requêtes |
| callback | callable | non | None | Si vous gérez la requête de manière asynchrone, le rappel est appelé lorsque la réponse est prête. |
| err_callback | callable | non | None | Si vous gérez la requête de manière asynchrone, le rappel d’erreur est appelé lorsque l’exception est levée. |

## Retours

`Returns` a `TargetDeliveryResponse` s’il est appelé de manière synchrone (par défaut), ou un `AsyncResult` s’il est appelé avec un rappel . `TargetDeliveryResponse` possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| response | DeliveryResponse | Se conforme à la variable [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) response |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | [!DNL Target] cookie d’indicateur d’emplacement |
| analytics_details | list[AnalyticsResponse] | [!DNL Analytics] payload, dans le cas d’une requête côté client [!DNL Analytics] usage |
| trace |  | list[dict] | Données de suivi agrégées pour toutes les mbox/vues de requête |
| response_tokens | list[dict] | Une liste de [Jetons de réponse &#x200B;](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | dict | Métadonnées de prise de décision supplémentaires à utiliser avec la prise de décision sur appareil |

## Exemple

Commençons par construire le [!UICONTROL API de diffusion Target] demande de prérécupération de contenu pour la variable `home` et `product1` mbox.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Une réponse réussie contient une [!UICONTROL API de diffusion Target] objet de réponse, qui contient du contenu prérécupéré pour les mbox demandées. Un exemple `target_response["response"]` (au format dict) peut se présenter comme suit :

### Python

```python {line-numbers="true"}
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

Notez la mbox `name` et `state` , ainsi que la variable `eventToken` , dans chacune des options de contenu de Target. Elles doivent être fournies dans la variable `send_notifications()` dès que chaque option de contenu est affichée. Supposons que la variable `product1` mbox s’affiche sur un périphérique autre que le navigateur. La demande de notification s’affiche comme suit :

### Python

```python {line-numbers="true"}
notification_mbox = NotificationMbox(name="product1",
                                     state="J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
notification = Notification(
    id="1",
    type=MetricType.DISPLAY,
    timestamp=1621530726000,  # Epoch time in milliseconds
    mbox=notification_mbox,
    tokens=["t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="]
)
notification_request = DeliveryRequest(notifications=[notification])
```

Notez que nous avons inclus à la fois l’état de mbox et le jeton d’événement correspondant à la variable [!DNL Target] offre fournie dans la réponse de prérécupération. Une fois la requête de notification créée, nous pouvons l’envoyer à [!DNL Target] via le `send_notifications()` Méthode d’API :

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
