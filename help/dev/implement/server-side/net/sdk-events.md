---
title: Abonnez-vous aux événements dans le SDK [!DNL Adobe Target] .NET
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK .NET à l’aide de l’objet [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Événements SDK (.NET)

## Description

Lorsque [ initialise le SDK ](initialize-sdk.md), un délégué facultatif `OnDeviceDecisioningReady` peut être fourni sur l’objet `TargetClientConfig`, qui sera appelé lorsque le SDK est prêt pour les appels de méthode sur l’appareil. Quelques autres délégués sont également disponibles pour gérer le téléchargement d’artefact [!UICONTROL on-device decisioning].

## Requête 

Les délégués suivants peuvent être configurés pour certains événements :

| Nom | Arguments | Description |
| --- | --- | --- |
| OnDeviceDecisioningReady | None | Appelé une seule fois que le client est prêt pour [!UICONTROL on-device decisioning] |
| ArtifactDownloadSucceeded | contenu de chaîne du fichier d’artefact | Appelé à chaque téléchargement d’un artefact [!UICONTROL on-device decisioning] |
| ArtifactDownloadFailed | Exception | Appelé chaque fois qu’il y a un échec de téléchargement d’un artefact [!UICONTROL on-device decisioning] |

## Exemple

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
