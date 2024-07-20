---
title: Initialisation du kit SDK  [!DNL Adobe Target] Python pour consigner les requêtes
description: Découvrez comment consigner des requêtes dans le kit SDK  [!DNL Adobe Target] Python.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Enregistreur (Python)

## Description

Lorsque [ initialise le SDK ](initialize-sdk.md), l’objet `options["logger"]` est un objet facultatif. Par défaut, un enregistreur de niveau INFO sera créé sous l’espace de noms `adobe.target`. Cependant, pour personnaliser le niveau de journalisation ou déboguer efficacement en cas de problème, un objet `logger` peut être fourni lors de l’initialisation du SDK.

L’objet `logger` doit avoir une méthode `debug()` et une méthode `error()`. Lorsqu’un journal approprié est fourni, [!DNL Target] requêtes et réponses seront consignées.

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
