---
title: Utilisez [!UICONTROL getOffers()] in [!DNL Adobe Target] lors de l’utilisation du SDK Node.js.
description: Découvrez comment utiliser [!UICONTROL getOffers()] pour exécuter une décision et récupérer une expérience depuis  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
TQID: https://experienceleague.adobe.com/WRGy74F1kUobRl1Pakse0VnXt3cT3-ntCljm4bHtiZ4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 20%

---

# [!UICONTROL Obtenir les offres] (Node.js)

## Description

`[!UICONTROL getOffers()]` est utilisé pour exécuter une décision et récupérer une expérience à partir de [!DNL Adobe Target].


## Méthode

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Paramètres

L’objet `options` présente la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- |--- | --- | --- | --- |
| Demande | Objet | Oui | None | Conforme à la requête [[!DNL Target] API de diffusion](/help/dev/implement/delivery-api/overview.md) |
| visitorCookie | Chaîne | Non | None | Cookie ECID (VisitorId) |
| targetCookie | Chaîne | Non | None | cookie [!DNL Target] |
| targetLocationHint | Chaîne | Non | None | [!DNL Target] l’indicateur d’emplacement |
| consumerId | Chaîne | Non | None | assemblage de consumerIds pour [!UICONTROL &#x200B; Analytics for Target &#x200B;] (A4T) |
| CustomerIds | Tableau | Non | None | ID de client au format compatible avec les VisitorId |
| sessionId | Chaîne | Non | None | Utilisé pour lier plusieurs requêtes [!DNL Target] |
| visiteur | Objet | Non | new VisitorId | Fournir une instance externe VisitorId |

## Promesse

`Promise` renvoyé présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| events | Objet | Requête [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) |
| réponse | Objet | Réponse [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) |
| visitorState | Objet | Objet qui doit être transmis à l’API visiteur `getInstance()` |
| targetCookie | Objet | cookie [!DNL Target] |
| targetLocationHintCookie | Objet | [!DNL Target] cookie d’indice d’emplacement |
| analyticsDetails | Tableau | Payload Analytics, en cas d’utilisation d’Analytics côté client |
| responseTokens | Tableau | Une liste de [jetons de réponse](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=fr ?). |
| trace | Tableau | Données de suivi agrégées pour toutes les mbox/vues de requête |
| status | Objet | Objet contenant le statut de la réponse. |
| decisioningMethod | Chaîne | Détermine la méthode de prise de décision à utiliser ([sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), côté serveur, hybride). |

Les objets `targetCookie` et `targetLocationHintCookie` utilisés pour transmettre des données au navigateur ont la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| name | Chaîne | Nom du cookie |
| value | Quelconque | Valeur du cookie, le sera converti en chaîne |
| maxAge | Nombre | L’option `maxAge` est pratique pour définir les expirations par rapport à l’heure actuelle en secondes |

L’objet `status` utilisé pour indiquer le statut de la réponse cible possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| status | Nombre | Code d’état HTTP |
| message | Chaîne | Un message sur la réponse. Par exemple, il peut indiquer si la réponse a été décidée [sur l’appareil](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) ou côté serveur |
| remoteMboxes | Tableau | Lorsque la méthode de prise de décision est `on-device`, un tableau de noms de mbox qui n’ont pas pu être entièrement décidés sur l’appareil est fourni. En d’autres termes, une requête [[!UICONTROL API de diffusion Target]](/help/dev/implement/delivery-api/overview.md) est nécessaire. |

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
