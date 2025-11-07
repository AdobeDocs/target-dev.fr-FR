---
title: Abonnement aux événements dans le SDK  [!DNL Adobe Target]  Python
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK Python à l’aide de l’objet [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 3%

---

# Événements SDK (Python)

## Description

Lors de l’initialisation [&#x200B; du SDK](initialize-sdk.md), le dictionnaire de `options["events"]` est un objet facultatif avec des clés de nom d’événement et des valeurs de fonction de rappel. Il peut être utilisé pour vous abonner à divers événements qui se produisent dans le SDK. Par exemple, l’événement `client_ready` peut être utilisé avec une fonction de rappel appelée lorsque le SDK est prêt pour les appels de méthode.

Lorsque la fonction `callback` est appelée, un objet événement est transmis. Chaque événement possède un `type` correspondant au nom de l’événement, et certains événements incluent des propriétés supplémentaires avec des informations pertinentes.

## Requête 

| Nom de l’événement (type) | Description | Propriétés d’événement supplémentaires |
| --- | --- | --- |
| client_ready | Émis lorsque l’artefact a été téléchargé et que le SDK est prêt pour les appels get_offers. Recommandé lors de l’utilisation de la méthode de prise de décision sur l’appareil. | None |
| artifact_download_success | Émis chaque fois qu’un nouvel artefact est téléchargé. | artifact_payload, artifact_location |
| artifact_download_failed | Émis chaque fois qu’un artefact ne parvient pas à être téléchargé. | artifact_location, error |

## Exemple

### Python

```python {line-numbers="true"}
def client_ready_callback():
    # make get_offers requests

def artifact_download_succeeded(event):
    print("The artifact was successfully downloaded from {}".format(event.artifact_location))
    # optionally do something with event.artifact_payload, like persist it

def artifact_download_failed(event):
    print("The artifact failed to download from {} with the following error: {}"
          .format(event.artifact_location, str(event.error)))

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback,
        "artifact_download_succeeded": artifact_download_succeeded,
        "artifact_download_failed": artifact_download_failed
    }
}
target_client = target_client.create(client_options)
```
