---
title: Abonnez-vous aux événements dans la variable [!DNL Adobe Target] SDK .NET
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK .NET à l’aide de la variable [!UICONTROL OnDeviceDecisioningHandler] .
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# Événements SDK (.NET)

## Description

When [initialisation du SDK](initialize-sdk.md), facultatif `OnDeviceDecisioningReady` Le délégué peut être fourni dans la variable `TargetClientConfig` qui sera appelée lorsque le SDK est prêt pour les appels de méthode sur l’appareil. Deux autres délégués sont également disponibles pour gérer la [!UICONTROL prise de décision sur appareil] téléchargement d’artefact.

## Requête 

Les délégués suivants peuvent être configurés pour certains événements :

| Nom | Arguments | Description |
| --- | --- | --- |
| OnDeviceDecisioningReady | None | Appelé une seule fois que le client est prêt pour la première fois [!UICONTROL prise de décision sur appareil] |
| ArtifactDownloadSucceeded | contenu de chaîne du fichier d’artefact | Appelé chaque fois qu’un [!UICONTROL prise de décision sur appareil] artifact est téléchargé |
| ArtifactDownloadFailed | Exception | Appelé chaque fois qu’il y a un échec de téléchargement d’une [!UICONTROL prise de décision sur appareil] artifact |

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
