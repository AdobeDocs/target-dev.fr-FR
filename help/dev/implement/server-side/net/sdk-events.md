---
title: Abonnement aux événements dans le [!DNL Adobe Target] .NET SDK
description: Découvrez comment vous abonner à divers événements qui se produisent dans le SDK .NET à l’aide de l’objet [!UICONTROL OnDeviceDecisioningHandler].
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
TQID: 'https://experienceleague.adobe.com/oeGknU-pW1-XjVrxn8JNEPoFBF8Gntt-vaVnqjdyTC8'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 5%
---
# Événements SDK (.NET)

## Description

Lors de l’initialisation [&#x200B; du SDK](initialize-sdk.md), un délégué `OnDeviceDecisioningReady` facultatif peut être fourni sur l’objet `TargetClientConfig`, qui sera appelé lorsque le SDK est prêt pour les appels de méthode sur l’appareil. D’autres délégués sont également disponibles pour gérer le téléchargement des artefacts [!UICONTROL prise de décision sur l’appareil].

## Requête

Les délégués suivants peuvent être configurés pour certains événements :

| Nom | Arguments | Description |
| --- | --- | --- |
| OnDeviceDecisioningReady | None | Appelé uniquement la première fois que le client est prêt pour la [!UICONTROL prise de décision sur l’appareil] |
| ArtifactDownloadSuccefully | contenu de chaîne du fichier d’artefact | Appelé à chaque téléchargement d’un artefact [!UICONTROL on-device decisioning] |
| ArtifactDownloadFailed | Exception | Appelé chaque fois qu’un artefact [!UICONTROL prise de décision sur l’appareil] ne peut pas être téléchargé |

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
