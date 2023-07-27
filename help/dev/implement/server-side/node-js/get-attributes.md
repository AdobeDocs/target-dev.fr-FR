---
title: Utilisation de requêtes asynchrones dans la variable [!DNL Adobe Target] SDK Node.js
description: Découvrez comment [!DNL Target] Le SDK Node.js prend en charge les requêtes asynchrones, ce qui peut réduire le temps cible effectif à zéro.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 18%

---

# Obtention d’attributs (Node.js)

## Description

`[!UICONTROL getAttributes()]` est utilisé pour récupérer les expériences et les expériences personnalisées d’ [!DNL Target] et extraire des valeurs d’attribut.

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

La variable `Promise` renvoyé par `TargetClient.getAttributes()` résout un objet avec les méthodes suivantes :

| Méthode | Type de retour | Description |
| --- | --- | --- |
| getValue(mboxName, key) | Quelconque | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| asObject(mboxName) | Objet | Renvoie un objet json simple avec des paires clé-valeur |
| getResponse() | [Réponse getOffers](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | Renvoie l’objet de réponse normalement renvoyé par `getOffers` |

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
