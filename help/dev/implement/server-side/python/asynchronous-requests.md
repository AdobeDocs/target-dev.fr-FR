---
title: Utilisation de requêtes asynchrones dans la variable [!DNL Adobe Target] SDK Python
description: Découvrez comment [!DNL Target] Le SDK Python prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# Requêtes asynchrones (Python)

## Description

L’un des avantages de l’intégration côté serveur est que vous pouvez exploiter l’énorme bande passante et les ressources informatiques disponibles côté serveur en utilisant le parallélisme. [!DNL Target] Le SDK Python prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.

## Méthodes prises en charge

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## Exemple

Un exemple d’application qui utilise la méthode `asyncio` async/attente du module en Python 3.9+ pourrait ressembler à ceci :

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

Cet exemple suppose que vous utilisez Python 3.9+. Si vous utilisez une ancienne version de Python, vous pouvez toujours envoyer des requêtes asynchrones en transmettant `options.callback` to `get_offers`. Consultez l’exemple d’application Flask pour plus d’informations sur l’exécution asynchrone à l’aide de rappels ou async/attente, [here](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
