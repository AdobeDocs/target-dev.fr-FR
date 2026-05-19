---
title: Utilisation des requêtes asynchrones dans le SDK Node [!DNL Adobe Target] js
description: Découvrez comment  [!DNL Target]  Node.js SDK prend en charge les requêtes asynchrones, ce qui peut réduire à zéro le temps cible effectif.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
TQID: https://experienceleague.adobe.com/cIoEnAinSLl-TO2vunG164i97Y2h-9NdE487ZyXJSzs
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 116
ht-degree: 18%

---

# Obtenir les attributs (Node.js)

## Description

`[!UICONTROL getAttributes()]` est utilisé pour récupérer des expériences et des expériences personnalisées à partir de [!DNL Target] et extraire des valeurs d’attribut.

## Méthode

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## Paramètres

| Nom | Type | Requis | Par défaut |
| --- | --- | --- |--- |
| mboxNames | Tableau | Oui | None |
| Options | Objet | Non | None |

## Promesse

Le `Promise` renvoyé par `TargetClient.getAttributes()` résout un objet avec les méthodes suivantes :

| Méthode | Type de retour | Description |
| --- | --- | --- |
| getValue(mboxName, key) | Quelconque | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| asObject(mboxName) | Objet | Renvoie un objet json simple avec des paires clé-valeur |
| getResponse() | [getOffers Response](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Renvoie l’objet de réponse normalement renvoyé par `getOffers` |

## Exemple

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
