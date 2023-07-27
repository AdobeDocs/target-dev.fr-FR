---
title: Utilisez getOffers() dans [!DNL Adobe Target] lorsque vous utilisez le SDK Python
description: Découvrez comment utiliser getOffers() pour exécuter une décision et récupérer une expérience à partir de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 13%

---

# Obtention d’offres (Python)

## Description

`get_offers()` est utilisé pour exécuter une décision et récupérer une expérience de [!DNL Adobe Target].


## Méthode

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## Paramètres

La variable `options` dict a la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| events | DeliveryRequest | Oui | None | Se conforme à la variable [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) requête |
| target_cookie | str | non | None | [!DNL Target] cookie |
| target_location_hint | str | non | None | [!DNL Target] indicateur de location |
| consumer_id | str | non | None | Lors de la combinaison de plusieurs appels, différents identifiants de consommateur doivent être fournis. |
| customer_ids | list[CustomerId] | non | None | Liste des ID de client au format compatible avec VisitorId |
| session_id | str | non | None | Utilisé pour lier plusieurs requêtes |
| callback | callable | non | None | Si vous gérez la requête de manière asynchrone, le rappel est appelé lorsque la réponse est prête. |
| err_callback | callable | non | None | Si vous gérez la requête de manière asynchrone, le rappel d’erreur est appelé lorsque l’exception est levée. |

## Retours

Renvoie un `TargetDeliveryResponse` s’il est appelé de manière synchrone (par défaut), ou un `AsyncResult` s’il est appelé avec un rappel . `TargetDeliveryResponse` possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| response | DeliveryResponse | Se conforme à la variable [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) response |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | [!DNL Target] cookie d’indicateur d’emplacement |
| analytics_details | list[AnalyticsResponse] | Charge utile Analytics, en cas d’utilisation d’Analytics côté client |
| trace | list[dict] | Données de suivi agrégées pour toutes les mbox/vues de requête |
| response_tokens | list[dict] | Une liste de &#x200B;[Jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | dict | Métadonnées de prise de décision supplémentaires à utiliser avec la prise de décision sur appareil |

`target_cookie` et `target_location_hint_cookie` les objets utilisés pour renvoyer les données au navigateur présentent la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| name | str | Nom du cookie |
| value | any | Valeur du cookie, la valeur sera convertie en chaîne |
| max_age | int | La variable `max_age option` est pratique pour définir les expirations par rapport à l’heure actuelle en secondes. |

La variable `meta` L’objet utilisé pour indiquer l’état de la réponse cible présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| decisioning_method | str | Quelle méthode de prise de décision a été utilisée : sur appareil ou côté serveur ? |
| remote_mboxes | list`[str]` | Lorsque la méthode de prise de décision est `on-device`, un tableau de noms de mbox qui n’ont pas pu être entièrement décidés sur l’appareil est fourni. En d’autres termes, une [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |
| remote_views | list`[str]` | Lorsque la méthode de prise de décision est sur l’appareil, un tableau de noms d’affichage qui n’ont pas pu être entièrement décidés sur l’appareil est fourni. En d’autres termes, une [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |

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
