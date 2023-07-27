---
title: Initialisez la [!DNL Adobe Target] SDK Node.js pour consigner les requêtes
description: Découvrez comment consigner des requêtes dans le [!DNL Adobe Target] SDK Node.js.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# Enregistreur (Node.js)

## Description

When [initialisation du SDK](initialize-sdk.md), la variable `options.logger` est un objet facultatif. Toutefois, pour déboguer efficacement en cas de problème, une `logger` doit être fourni lors de l’initialisation du SDK.

La variable `logger` doit comporter un objet `debug()` et un `error()` . Lorsqu’un enregistreur approprié est fourni, par exemple `console`, [!DNL Target] les demandes et réponses seront consignées.

## Exemple

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

Vous devriez voir les requêtes et les réponses imprimées dans la console.
