---
title: Utilisation des requêtes asynchrones dans le SDK  [!DNL Adobe Target]  Python
description: Découvrez comment  [!DNL Target]  SDK Python prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
TQID: https://experienceleague.adobe.com/ZWRw2OlSbuEHorY0MXPOaBw3uePIW5dzpsuqho0Jtqk
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 142
ht-degree: 4%

---

# Requêtes Asynchrones (Python)

## Description

L’un des avantages de l’intégration côté serveur est que vous pouvez tirer parti de l’énorme bande passante et des ressources informatiques disponibles côté serveur en utilisant le parallélisme. [!DNL Target] Python SDK prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.

## Méthodes prises en charge

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## Exemple

Voici à quoi pourrait ressembler un exemple d&#39;application qui utilise la fonction async/await du module `asyncio` dans Python 3.9+ :

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

Cet exemple suppose que vous utilisez Python 3.9+. Si vous utilisez une ancienne version de Python, vous pouvez toujours envoyer des requêtes asynchrones en transmettant des `options.callback` à `get_offers`. Consultez l’exemple d’application Flask pour plus d’informations sur l’exécution asynchrone à l’aide de rappels ou async/await, [ici](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py).
