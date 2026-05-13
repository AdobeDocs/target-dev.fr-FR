---
title: Utilisez getOffers() in [!DNL Adobe Target] when using the Python SDK
description: Découvrez comment utiliser getOffers() pour exécuter une décision et récupérer une expérience depuis  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
TQID: https://experienceleague.adobe.com/b7t1NfE5Gcsj86w4u3Cfl5-Eb7a6HG1Hg8vi6-ViQFg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 357
ht-degree: 12%

---

# Obtenir Des Offres (Python)

## Description

`get_offers()` est utilisé pour exécuter une décision et récupérer une expérience à partir de [!DNL Adobe Target].


## Méthode

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## Paramètres

Le dictionnaire de `options` présente la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| events | DeliveryRequest | Oui | None | Conforme à la requête [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | non | None | cookie [!DNL Target] |
| target_location_hint | str | non | None | [!DNL Target] l’indicateur d’emplacement |
| consumer_id | str | non | None | Lors du regroupement de plusieurs appels, différents ID de client doivent être fournis |
| customer_ids | list[CustomerId] | non | None | Une liste des ID de client au format compatible avec les VisitorId |
| session_id | str | non | None | Utilisé pour lier plusieurs requêtes |
| callback | appelable | non | None | Si vous gérez les requêtes de manière asynchrone, le rappel est appelé lorsque la réponse est prête |
| err_callback | appelable | non | None | Si la requête est traitée de manière asynchrone, le rappel d’erreur est appelé lorsque l’exception est levée |

## Retours

Renvoie un `TargetDeliveryResponse` s’il est appelé de manière synchrone (par défaut) ou un `AsyncResult` s’il est appelé avec un rappel . `TargetDeliveryResponse` présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| réponse | DeliveryResponse | Conforme à la réponse [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | dictionnaire | cookie [!DNL Target] |
| target_location_hint_cookie | dictionnaire | [!DNL Target] cookie d’indice d’emplacement |
| analytics_details | list[AnalyticsResponse] | Payload Analytics, en cas d’utilisation d’Analytics côté client |
| trace | list[dict] | Données de suivi agrégées pour toutes les mbox/vues de requête |
| response_tokens | list[dict] | Une liste de &#x200B;jetons [&#x200B; réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr) |
| méta | dictionnaire | Métadonnées de prise de décision supplémentaires à utiliser avec la prise de décision sur l’appareil |

Les objets `target_cookie` et `target_location_hint_cookie` utilisés pour transmettre des données au navigateur ont la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| name | str | Nom du cookie |
| value | any | Valeur du cookie. La valeur sera convertie en chaîne. |
| max_age | int | L’`max_age option` est pratique pour définir les expirations par rapport à l’heure actuelle en secondes |

L’objet `meta` utilisé pour indiquer le statut de la réponse cible possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| decisioning_method | str | La méthode de prise de décision utilisée : sur l’appareil ou côté serveur |
| remote_mboxes | list`[str]` | Lorsque la méthode de prise de décision est `on-device`, un tableau de noms de mbox qui n’ont pas pu être entièrement décidés sur l’appareil est fourni. En d’autres termes, une requête [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |
| remote_views | list`[str]` | Lorsque la méthode de prise de décision est sur l’appareil, un tableau de noms de vue qui n’ont pas pu être entièrement décidés sur l’appareil est fourni. En d’autres termes, une requête [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |

## Exemple

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }

    target_delivery_response = target_client.get_offers(get_offers_options)


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
