---
title: Abonnez-vous aux événements dans la variable [!DNL Adobe Target] SDK Java
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK Java à l’aide de la variable [!UICONTROL OnDeviceDecisioningHandler] .
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 4%

---

# Événements SDK (Java)

## Description

When [initialisation du SDK](initialize-sdk.md), facultatif `OnDeviceDecisioningHandler` peut être fourni sur l’objet `ClientConfig` . Il peut être utilisé pour s’abonner à divers événements qui se produisent dans le SDK. Par exemple, la variable `onDeviceDecisioningReady` peut être utilisé avec une fonction de rappel qui sera appelée lorsque le SDK est prêt pour les appels de méthode.

## Requête 

La variable `OnDeviceDecisioningHandler` contient les rappels suivants, qui sont appelés pour certains événements :

| Nom | Arguments | Description |
| --- | --- | --- |
| onDeviceDecisioningReady | None | Appelé une seule fois que le client est prêt pour la première fois [!UICONTROL prise de décision sur appareil] |
| artifactDownloadSucceeded | byte[] contenu du fichier d’artefact | Appelé chaque fois qu’un [!UICONTROL prise de décision sur appareil] artifact est téléchargé |
| artifactDownloadFailed | Exception | Appelé chaque fois qu’il y a un échec de téléchargement d’une [!UICONTROL prise de décision sur appareil] artifact |

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
