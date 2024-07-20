---
title: Initialisation du kit SDK  [!DNL Adobe Target] Node.js pour consigner les requêtes
description: Découvrez comment consigner des requêtes dans le kit SDK  [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# Enregistreur (Node.js)

## Description

Lorsque [ initialise le SDK ](initialize-sdk.md), l’objet `options.logger` est un objet facultatif. Cependant, pour déboguer efficacement en cas de problème, un objet `logger` doit être fourni lors de l’initialisation du SDK.

L’objet `logger` doit avoir une méthode `debug()` et une méthode `error()`. Lorsqu’un journal approprié est fourni, par exemple `console`, les requêtes et réponses [!DNL Target] seront consignées.

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
