---
title: Utilisation de requêtes asynchrones dans le kit SDK  [!DNL Adobe Target] Python
description: Découvrez comment le SDK Python  [!DNL Target] prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 16%

---

# Obtenir des attributs (Python)

## Description

`get_attributes()` est utilisé pour récupérer l’expérimentation et les expériences personnalisées de [!DNL Target] et extraire des valeurs d’attribut.


## Méthode

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## Paramètres

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| mbox_names | list[str] | Oui | None | Liste des noms de mbox |
| Options | dict | Non | None | Les mêmes options que pour [Obtenir des offres](get-offers.md) |

## AttributesProvider

L’ `AttributesProvider` renvoyé par `target_client.get_attributes()` possède les méthodes suivantes :

| Méthode | Type de retour | Description |
| --- | --- | --- |
| get_value(mbox_name, key) | any | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| as_object(mbox_name) | dict | Renvoie un objet json simple avec des paires clé-valeur |
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
