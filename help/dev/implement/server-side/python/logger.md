---
title: Initialisez le SDK  [!DNL Adobe Target]  Python pour consigner les requêtes
description: Découvrez comment consigner des requêtes dans le SDK  [!DNL Adobe Target]  Python.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
TQID: https://experienceleague.adobe.com/9LSln8V3QIG9GTok2yTTnKvhlpQhaed3a-qJyA4jErg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 97
ht-degree: 3%

---

# Enregistreur (Python)

## Description

Lors de [initialisation du SDK](initialize-sdk.md), l’objet `options["logger"]` est un objet facultatif. Par défaut, un enregistreur de niveau INFO est créé sous l’espace de noms `adobe.target`. Cependant, pour personnaliser efficacement le niveau de journal ou le débogage en cas de problème, un objet `logger` peut être fourni lors de l’initialisation du SDK.

L’objet `logger` doit comporter un `debug()` et une méthode `error()`. Lorsqu’un enregistreur approprié est fourni, [!DNL Target] requêtes et réponses sont consignées.

## Exemple

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

Les requêtes et les réponses doivent s’afficher en cours d’impression dans la console.
