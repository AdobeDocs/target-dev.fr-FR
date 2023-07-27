---
title: Initialisation du SDK .NET à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Java et instancier le [!UICONTROL TargetClient] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 17%

---

# Initialisation du SDK .NET

## Description

Utilisez la variable `Create` pour initialiser le SDK .NET et instancier la méthode [!UICONTROL Client Target] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.

Lorsque vous utilisez l’injection de dépendance .NET, ajoutez simplement le SDK à l’étape de configuration du service en appelant `services.AddTargetLibrary()`;, puis injecter `ITargetClient targetClient` dans le constructeur de votre application.

Ensuite, utilisez la méthode `Initialize` du SDK pour configurer le SDK, ce qui permet de terminer l’étape d’initialisation.

## Méthode

`TargetClient` est créé à l’aide de `TargetClient.Create`.

## C\
#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` est créé à l’aide de ClientConfig.Builder.

## C\
#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Paramètres

`TargetClientConfig.Builder` possède la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| Code | string | Oui | None | [!UICONTROL Identifiant du client Target] |
| OrganizationId | string | Oui | None | [!UICONTROL ID d’organisation Experience Cloud] |
| Expiration | int | Non | 10000 | Timeout de toutes les requêtes en millisecondes |
| Proxy |  | WebProxy | Non | valeur nulle | Proxy pour tous [!DNL Target] requests |
| RetryPolicy | Stratégie | Non | valeur nulle | Stratégie de reprise pour tous [!DNL Target] requests |
| AsyncRetryPolicy | AsyncPolicy | Non | valeur nulle | Stratégie de reprise asynchrone pour tous [!DNL Target] requests |
| Enregistreur | ILogger | Non | valeur nulle | Utilisé pour la journalisation du débogage de [!DNL Target] requêtes et réponses |
| ServerDomain | string | Non | `client.tt.omtrdc.net` | Remplace le nom d’hôte par défaut |
| Sécurisé | bool | Non | true | Non défini pour appliquer le schéma HTTP |
| DefaultPropertyToken | string | Non | valeur nulle | Définit le jeton de propriété par défaut pour chaque `getOffers` appel |
| TelemetryEnabled | bool | Non | true | Envoi de données de télémétrie pour améliorer l’expérience d’utilisation du SDK |
| DecisioningMethod | Enum DecisioningMethod | Non | ServerSide | Doit être défini sur OnDevice ou hybride pour activer la prise de décision sur l’appareil. |
| OnDeviceDecisioningReady | Action | Non | valeur nulle | Déléguer pour l’événement prêt pour la prise de décision sur les appareils (appelé une fois lorsque la prise de décision sur les appareils est prête) |
| ArtifactDownloadSucceeded | Action | Non | valeur nulle | Déléguer pour la réussite du téléchargement d’artefact de prise de décision sur l’appareil (appelé à chaque téléchargement d’artefact réussi) |
| ArtifactDownloadFailed | Action | Non | valeur nulle | Déléguer pour l’échec du téléchargement d’artefact de prise de décision sur l’appareil (appelé pour chaque téléchargement d’artefact ayant échoué) |
| OnDeviceEnvironment | string | Non | production | Peut être utilisé pour spécifier un autre environnement sur l’appareil, tel que l’évaluation |
| OnDeviceConfigHostname | string | Non | `assets.adobetarget.com` | Peut être utilisé pour spécifier un autre hôte à utiliser pour télécharger le fichier d’artefact de prise de décision sur l’appareil |
| OnDeviceDecisioningPollingIntSecs | int | Non | 300 (5 min) | Nombre de secondes entre les récupérations du fichier d’artefact de prise de décision sur l’appareil |
| OnDeviceArtifactPayload | string | Non | valeur nulle | Fournit une prise de décision sur l’appareil avec une charge utile d’artefact locale pour permettre une exécution immédiate |

## Exemple

## C\
#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
