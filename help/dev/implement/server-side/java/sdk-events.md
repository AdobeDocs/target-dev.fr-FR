---
title: 'Abonnement aux événements dans le SDK Java [!DNL Adobe Target] '
description: Découvrez comment vous abonner à divers événements qui se produisent dans Java SDK à l’aide de l’objet [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
TQID: https://experienceleague.adobe.com/x3aig-jM-GXzmLNcUNclZUK9Y49tuSF9-sdkxzJFtiM
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 134
ht-degree: 5%

---

# Événements SDK (Java)

## Description

Lors de l’initialisation [ du SDK](initialize-sdk.md), un objet `OnDeviceDecisioningHandler` facultatif peut être fourni sur l’objet `ClientConfig`. Il peut être utilisé pour vous abonner à divers événements qui se produisent dans le SDK. Par exemple, l’événement `onDeviceDecisioningReady` peut être utilisé avec une fonction de rappel appelée lorsque le SDK est prêt pour les appels de méthode.

## Requête

L’objet `OnDeviceDecisioningHandler` contient les rappels suivants, qui sont appelés pour certains événements :

| Nom | Arguments | Description |
| --- | --- | --- |
| onDeviceDecisioningReady | None | Appelé une seule fois la première fois que le client est prêt pour la [!UICONTROL on-device decisioning] |
| artifactDownloadSuccessfully | byte [] contenu du fichier d&#39;artefact | Appelé à chaque téléchargement d’un artefact [!UICONTROL on-device decisioning] |
| artifactDownloadFailed | Exception | Appelé chaque fois qu’un artefact de [!UICONTROL on-device decisioning] ne parvient pas à être téléchargé |

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
