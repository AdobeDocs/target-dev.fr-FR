---
title: Utilisation [!UICONTROL getOffers()] in [!DNL Adobe Target] lors de l’utilisation du SDK Node.js
description: Découvrez comment utiliser [!UICONTROL getOffers()] pour exécuter une décision et récupérer une expérience d’ [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 22%

---

# [!UICONTROL Obtention d’offres] (Node.js)

## Description

`[!UICONTROL getOffers()]` est utilisé pour exécuter une décision et récupérer une expérience de [!DNL Adobe Target].


## Méthode

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Paramètres

La variable `options` possède la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- |--- | --- | --- | --- |
| Demande | Objet | Oui | None | Se conforme à la variable [[!DNL Target] API de diffusion](/help/dev/implement/delivery-api/overview.md) requête |
| visitorCookie | Chaîne | Non | None | Cookie ECID (VisitorId) |
| targetCookie | Chaîne | Non | None | [!DNL Target] cookie |
| targetLocationHint | Chaîne | Non | None | [!DNL Target] indicateur de location |
| consumerId | Chaîne | Non | None | consumerIds pour [!UICONTROL Analytics pour Target] (A4T) assemblage |
| CustomerIds | Tableau | Non | None | ID de client au format compatible avec VisitorId |
| sessionId | Chaîne | Non | None | Utilisé pour lier plusieurs [!DNL Target] requests |
| visiteur | Objet | Non | new VisitorId | Fournir une instance VisitorId externe |

## Promesse

`Promise` La valeur renvoyée présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| events | Objet | [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) requête |
| response | Objet | [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) response |
| visitorState | Objet | Objet qui doit être transmis à l’API visiteur `getInstance()` |
| targetCookie | Objet | [!DNL Target] cookie |
| targetLocationHintCookie | Objet | [!DNL Target] cookie d’indicateur d’emplacement |
| analyticsDetails | Tableau | Charge utile Analytics, en cas d’utilisation d’Analytics côté client |
| responseTokens | Tableau | Une liste de [Jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trace | Tableau | Données de suivi agrégées pour toutes les mbox/vues de requête |
| status | Objet | Objet contenant l’état de la réponse. |
| decisioningMethod | Chaîne | Détermine la méthode de prise de décision à utiliser ([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), côté serveur, hybride) |

`targetCookie` et `targetLocationHintCookie` les objets utilisés pour renvoyer les données au navigateur présentent la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| name | Chaîne | Nom du cookie |
| value | Quelconque | Valeur du cookie, qui sera convertie en chaîne |
| maxAge | Nombre | La variable `maxAge` est pratique pour définir les expirations par rapport à l’heure actuelle en secondes. |

La variable `status` L’objet utilisé pour indiquer l’état de la réponse cible présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| status | Nombre | Code d’état HTTP |
| message | Chaîne | Un message à propos de la réponse. Par exemple, il peut indiquer si la réponse a été décidée. [on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) ou côté serveur |
| remoteMboxes | Tableau | Lorsque la méthode de prise de décision est `on-device`, un tableau de noms de mbox qui n’ont pas pu être entièrement décidés sur l’appareil est fourni. En d’autres termes, une [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |

## Exemple

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
