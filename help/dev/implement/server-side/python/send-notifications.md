---
title: Envoyer des notifications d’affichage ou de clic à à à l [!DNL Adobe Target] aide de Python SDK
description: Découvrez comment utiliser sendNotifications() pour envoyer des notifications d’affichage ou de clic à des  [!DNL Adobe Target]  de mesure et de création de rapports.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
TQID: https://experienceleague.adobe.com/r7j2MaCmcZBEsx7TmTlKL9R-IKlncZJw5DhSfcKmVNU
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 420
ht-degree: 8%

---

# Envoyer Des Notifications (Python)

## Description

`send_notifications()` sert à envoyer des notifications d’affichage ou de clic aux [!DNL Adobe Target] pour la mesure et le compte rendu des performances.

>[!NOTE]
>
>Lorsqu’un objet `execute` avec les paramètres requis se trouve dans la requête elle-même, l’impression est incrémentée automatiquement pour les activités de qualification.

Les méthodes SDK qui incrémentent automatiquement une impression sont les suivantes :

* `get_offers()`
* `get_attributes()`

Lorsqu’un objet `prefetch` est transmis dans la requête, l’impression n’est pas automatiquement incrémentée pour les activités comportant des mbox au sein de l’objet `prefetch`. `Send_notifications()` doit être utilisé pour les expériences prérécupérées afin d’incrémenter les impressions et les conversions.

## Méthode

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## Paramètres

`options` présente la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| events | DeliveryRequest | Oui | None | Conforme à la requête [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | non | None | cookie [!DNL Target] |
| target_location_hint | str | non | None | [!DNL Target] l’indicateur d’emplacement |
| consumer_id | str | non | None | Lors du regroupement de plusieurs appels, différents ID de client doivent être fournis |
| customer_ids | list[CustomerId] | non | None | Une liste des ID de client au format compatible avec les VisitorId |
| session_id | str | non | None | Utilisé pour lier plusieurs requêtes |
| callback | appelable | non | None | Si vous gérez les requêtes de manière asynchrone, le rappel est appelé lorsque la réponse est prête |
| err_callback | appelable | non | None | Si la requête est traitée de manière asynchrone, le rappel d’erreur est appelé lorsque l’exception est levée |

## Retours

`Returns` un `TargetDeliveryResponse` s’il est appelé de manière synchrone (par défaut) ou un `AsyncResult` s’il est appelé avec un rappel . `TargetDeliveryResponse` présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| réponse | DeliveryResponse | Conforme à la réponse [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | dictionnaire | cookie [!DNL Target] |
| target_location_hint_cookie | dictionnaire | [!DNL Target] cookie d’indice d’emplacement |
| analytics_details | list[AnalyticsResponse] | Payload [!DNL Analytics], en cas d’utilisation du [!DNL Analytics] côté client |
| trace | list[dict] | Données de suivi agrégées pour toutes les mbox/vues de requête |
| response_tokens | list[dict] | Une liste de &#x200B;jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)[ |
| méta | dictionnaire | Métadonnées de prise de décision supplémentaires à utiliser avec la prise de décision sur l’appareil |

## Exemple

Tout d’abord, nous allons créer la requête [!UICONTROL API de diffusion Target] pour prérécupérer du contenu pour les mbox `home` et `product1`.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

Une réponse réussie contient un objet de réponse [!UICONTROL API de diffusion Target], qui contient du contenu prérécupéré pour les mbox demandées. Un exemple d’objet `target_response["response"]` (au format dict) peut se présenter comme suit :

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

Notez les champs `name` et `state` de la mbox, ainsi que le champ `eventToken`, dans chacune des options de contenu de Target. Ils doivent être fournis dans la requête `send_notifications()`, dès que chaque option de contenu est affichée. Supposons que la mbox `product1` ait été affichée sur un appareil qui n’est pas un navigateur. La demande de notifications se présente comme suit :

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

Notez que nous avons inclus l’état de la mbox et le jeton d’événement correspondant à l’offre [!DNL Target] diffusée dans la réponse de prérécupération. Après avoir créé la requête de notifications, nous pouvons l’envoyer à [!DNL Target] via la méthode de l’API `send_notifications()` :

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
