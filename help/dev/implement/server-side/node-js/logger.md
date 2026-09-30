---
title: Initialisez le SDK Node.js [!DNL Adobe Target] pour consigner les requêtes
description: Découvrez comment consigner les requêtes dans le SDK Node.js [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
TQID: 'https://experienceleague.adobe.com/tC6xT-eAHOO17h1BK-PwWTBmwg3Dy0Wj8KYrV3W-VR4'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%
---
# Enregistreur (Node.js)

## Description

Lors de [initialisation du SDK](initialize-sdk.md), l’objet `options.logger` est un objet facultatif. Cependant, pour un débogage efficace en cas de problème, un objet `logger` doit être fourni lors de l’initialisation du SDK.

L’objet `logger` doit comporter un `debug()` et une méthode `error()`. Lorsqu’un enregistreur approprié est fourni, tel que `console`, [!DNL Target] requêtes et réponses sont consignées.

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

Les requêtes et les réponses doivent s’afficher en cours d’impression dans la console.
