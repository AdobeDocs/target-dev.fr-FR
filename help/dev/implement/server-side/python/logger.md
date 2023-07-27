---
title: Initialisez la [!DNL Adobe Target] SDK Python pour consigner les requêtes
description: Découvrez comment consigner des requêtes dans le [!DNL Adobe Target] SDK Python.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Enregistreur (Python)

## Description

When [initialisation du SDK](initialize-sdk.md), la variable `options["logger"]` est un objet facultatif. Par défaut, un enregistreur de niveau INFO sera créé sous la variable `adobe.target` espace de noms. Toutefois, pour personnaliser efficacement le niveau de journalisation ou le débogage en cas de problème, une `logger` peut être fourni lors de l’initialisation du SDK.

La variable `logger` doit comporter un objet `debug()` et un `error()` . Lorsqu’un enregistreur approprié est fourni, [!DNL Target] les demandes et réponses seront consignées.

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

Vous devriez voir les requêtes et les réponses imprimées dans la console.
