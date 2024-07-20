---
title: Abonnez-vous aux événements dans le kit SDK Java [!DNL Adobe Target]
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK Java à l’aide de l’objet [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# Événements SDK (Java)

## Description

Lorsque [ initialise le SDK ](initialize-sdk.md), un objet `OnDeviceDecisioningHandler` facultatif peut être fourni sur l’objet `ClientConfig`. Il peut être utilisé pour s’abonner à divers événements qui se produisent dans le SDK. Par exemple, l’événement `onDeviceDecisioningReady` peut être utilisé avec une fonction de rappel qui sera appelée lorsque le SDK est prêt pour les appels de méthode.

## Requête 

L’objet `OnDeviceDecisioningHandler` contient les rappels suivants, qui sont appelés pour certains événements :

| Nom | Arguments | Description |
| --- | --- | --- |
| onDeviceDecisioningReady | None | Appelé une seule fois que le client est prêt pour [!UICONTROL on-device decisioning] |
| artifactDownloadSucceeded | contenu byte[] du fichier d’artefact | Appelé à chaque téléchargement d’un artefact [!UICONTROL on-device decisioning] |
| artifactDownloadFailed | Exception | Appelé chaque fois qu’il y a un échec de téléchargement d’un artefact [!UICONTROL on-device decisioning] |

## Exemple

### Événements SDK

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```
