---
title: Abonnez-vous aux événements dans la variable [!DNL Adobe Target] SDK Node.js
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK Node.js à l’aide du [!UICONTROL OnDeviceDecisioningHandler] .
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 2%

---

# Événements SDK (Node.js)

## Description

When [initialisation du SDK](initialize-sdk.md), la variable `options.events` est un objet facultatif avec des clés de nom d’événement et des valeurs de fonction de rappel. Il peut être utilisé pour s’abonner à divers événements qui se produisent dans le SDK. Par exemple, la fonction `clientReady` peut être utilisé avec une fonction de rappel qui sera appelée lorsque le SDK est prêt pour les appels de méthode.

Lorsque la fonction de rappel est appelée, un objet d’événement est transmis. Chaque événement comporte une `type` correspondant au nom de l’événement. Certains événements incluent des propriétés supplémentaires avec des informations pertinentes.

## Requête 

| Nom de l’événement (type) | Description | Propriétés d’événement supplémentaires |
| --- | --- | --- |
| clientReady | Émis lorsque l’artefact a été téléchargé et que le SDK est prêt pour `getOffers` appels . Recommandé lors de l’utilisation de la méthode de prise de décision sur l’appareil. |
| artifactDownloadSucceeded | Émis à chaque téléchargement d’un nouvel artefact. | artifactPayload, artifactLocation |
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
