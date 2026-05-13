---
title: Abonnement aux événements dans le SDK Node [!DNL Adobe Target] js
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK Node.js à l’aide de l’objet [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
TQID: https://experienceleague.adobe.com/KWuJT-p-Er-1mx766Y-itlFn7REZnqkUksdHKCy-2-U
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 163
ht-degree: 2%

---

# Événements SDK (Node.js)

## Description

Lors de l’initialisation [ du SDK](initialize-sdk.md), l’objet `options.events` est un objet facultatif avec des clés de nom d’événement et des valeurs de fonction de rappel. Il peut être utilisé pour vous abonner à divers événements qui se produisent dans le SDK. Par exemple, l’événement `clientReady` peut être utilisé avec une fonction de rappel appelée lorsque le SDK est prêt pour les appels de méthode.

Lorsque la fonction de rappel est appelée, un objet d’événement est transmis. Chaque événement possède un `type` correspondant au nom de l’événement. Certains événements incluent des propriétés supplémentaires avec des informations pertinentes.

## Requête

| Nom de l’événement (type) | Description | Propriétés d’événement supplémentaires |
| --- | --- | --- |
| clientReady | Émis lorsque l’artefact a été téléchargé et que le SDK est prêt pour les appels `getOffers`. Recommandé lors de l’utilisation de la méthode de prise de décision sur l’appareil. |  |
| artifactDownloadSuccessfully | Émis chaque fois qu’un nouvel artefact est téléchargé. | artifactPayload, artifactLocation |
| artifactDownloadFailed | Émis chaque fois qu’un artefact ne parvient pas à être téléchargé. | artifactLocation, erreur |

## Exemple

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
