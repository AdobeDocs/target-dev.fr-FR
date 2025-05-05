---
title: Utilisez getOffers() dans [!DNL Adobe Target] lors de l’utilisation du SDK Python
description: Découvrez comment utiliser getOffers() pour exécuter une décision et récupérer une expérience de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

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

Le dict `options` a la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| events | DeliveryRequest | Oui | None | Se conforme à la requête [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | str | non | None | cookie [!DNL Target] |
| target_location_hint | str | non | None | [!DNL Target] indicateur d’emplacement |
| consumer_id | str | non | None | Lors de la combinaison de plusieurs appels, différents identifiants de consommateur doivent être fournis. |
| customer_ids | list[CustomerId] | non | None | Liste des ID de client au format compatible avec VisitorId |
| session_id | str | non | None | Utilisé pour lier plusieurs requêtes |
| callback | callable | non | None | Si vous gérez la requête de manière asynchrone, le rappel est appelé lorsque la réponse est prête. |
| err_callback | callable | non | None | Si vous gérez la requête de manière asynchrone, le rappel d’erreur est appelé lorsque l’exception est levée. |

## Retours

Renvoie un `TargetDeliveryResponse` appelé de manière synchrone (par défaut) ou `AsyncResult` appelé avec un rappel. `TargetDeliveryResponse` a la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| response | DeliveryResponse | Se conforme à la réponse [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) |
| target_cookie | dict | cookie [!DNL Target] |
| target_location_hint_cookie | dict | cookie d’indicateur d’emplacement [!DNL Target] |
| analytics_details | list[AnalyticsResponse] | Charge utile Analytics, en cas d’utilisation d’Analytics côté client |
| trace | list[dict] | Données de suivi agrégées pour toutes les mbox/vues de requête |
| response_tokens | list[dict] | Liste des &#x200B; [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr) |
| meta | dict | Métadonnées de prise de décision supplémentaires à utiliser avec la prise de décision sur appareil |

Les objets `target_cookie` et `target_location_hint_cookie` utilisés pour renvoyer les données au navigateur ont la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| name | str | Nom du cookie |
| value | any | Valeur du cookie, la valeur sera convertie en chaîne |
| max_age | int | Le `max_age option` est pratique pour définir les expirations par rapport à l’heure actuelle en secondes. |

L’objet `meta` utilisé pour indiquer l’état de la réponse cible possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| decisioning_method | str | Quelle méthode de prise de décision a été utilisée : sur appareil ou côté serveur ? |
| remote_mboxes | list`[str]` | Lorsque la méthode de prise de décision est `on-device`, un tableau de noms de mbox qui n’ont pas pu être entièrement décidés sur l’appareil est donné. En d’autres termes, une requête [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |
| remote_views | list`[str]` | Lorsque la méthode de prise de décision est sur l’appareil, un tableau de noms d’affichage qui n’ont pas pu être entièrement décidés sur l’appareil est fourni. En d’autres termes, une requête [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |

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
