---
title: Utilisation des requêtes asynchrones dans le SDK  [!DNL Adobe Target]  Python
description: Découvrez comment  [!DNL Target]  SDK Python prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
TQID: https://experienceleague.adobe.com/CFfT7Amoca2yqYkkt9AviTmWi-RCjGdABYYuWHxvqC8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 130
ht-degree: 15%

---

# Obtenir Les Attributs (Python)

## Description

`get_attributes()` est utilisé pour récupérer des expériences et des expériences personnalisées à partir de [!DNL Target] et extraire des valeurs d’attribut.


## Méthode

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## Paramètres

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| mbox_names | list[str] | Oui | None | Une liste de noms de mbox |
| Options | dictionnaire | Non | None | Les mêmes options que pour [Obtenir les offres](get-offers.md) |

## AttributesProvider

La `AttributesProvider` renvoyée par `target_client.get_attributes()` comporte les méthodes suivantes :

| Méthode | Type de retour | Description |
| --- | --- | --- |
| get_value(mbox_name, key) | any | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| as_object(mbox_name) | dictionnaire | Renvoie un objet json simple avec des paires clé-valeur |
| get_response() | [TargetDeliveryResponse](https://github.com/adobe/target-python-sdk/blob/main/target_python_sdk/types/target_delivery_response.py) | Renvoie l’objet de réponse normalement renvoyé par `get_offers` |

## Exemple

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_attributes_options = {
      "request": delivery_request
    }

    attributes_provider = target_client.get_attributes(["demo-engineering-flags"], get_attributes_options)
    # returns just the value of searchProviderId from the demo-engineering-flags mbox offer
    search_provider_id = attributes_provider.get_value("demo-engineering-flags", "searchProviderId")

    # returns a simple dict object representing the demo-engineering-flags mbox offer
    engineering_flags = attributes_provider.as_object("demo-engineering-flags")
    """  the value of engineeringFlags looks like this
        {
            "cdnHostname": "cdn.cloud.corp.net",
            "searchProviderId": 143,
            "hasLegacyAccess": false
        }
    """

    asset_url = "http://{}/path/to/asset".format(engineering_flags.get("cdnHostname"))


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
