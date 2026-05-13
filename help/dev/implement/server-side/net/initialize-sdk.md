---
title: Initialisez le SDK .NET à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Java et instancier l’[!UICONTROL TargetClient] afin d’effectuer des appels vers  [!DNL Adobe Target]  expériences et des expériences personnalisées.
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
TQID: https://experienceleague.adobe.com/uOEojoWWjXmcDl2yY1UmSRD-EXL0j9p-p-eE8PXa7Rk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 359
ht-degree: 15%

---

# Initialiser le SDK .NET

## Description

Utilisez la méthode `Create` afin d’initialiser le SDK .NET et d’instancier le [!UICONTROL Target Client] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.

Lors de l’utilisation de l’injection de dépendance .NET, ajoutez simplement le SDK à l’étape de configuration du service en appelant `services.AddTargetLibrary()` `ITargetClient targetClient`;, puis injectez-le dans le constructeur de votre application.

Ensuite, utilisez la méthode `Initialize` du SDK pour configurer le SDK et terminer ainsi l’étape d’initialisation.

## Méthode

`TargetClient` est créé à l’aide de `TargetClient.Create`.

## C\
&#x200B;#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig` est créé à l’aide de ClientConfig.Builder.

## C\
&#x200B;#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## Paramètres

`TargetClientConfig.Builder` présente la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| Client ou cliente | string | Oui | None | [!UICONTROL Target Client Id] |
| OrganizationId | string | Oui | None | [!UICONTROL Experience Cloud Organization ID] |
| Délai d’expiration | int | Non | 10000 | Timeout de toutes les requêtes en millisecondes |
| Proxy | WebProxy | Non | valeur nulle | Proxy pour toutes les requêtes [!DNL Target] |
| RetryPolicy | Politiques | Non | valeur nulle | Stratégie de reprise pour toutes les requêtes [!DNL Target] |
| AsyncRetryPolicy | AsyncPolicy | Non | valeur nulle | Stratégie de reprise asynchrone pour toutes les requêtes [!DNL Target] |
| Enregistreur | ILogger | Non | valeur nulle | Utilisé pour la journalisation du débogage des requêtes et réponses [!DNL Target] |
| ServerDomain | string | Non | `client.tt.omtrdc.net` | Remplace le nom d’hôte par défaut |
| Sécurisé | booléen | Non | true | Annuler l’application du schéma HTTP |
| DefaultPropertyToken | string | Non | valeur nulle | Définit le jeton de propriété par défaut pour chaque appel `getOffers` |
| TélémétrieActivée | booléen | Non | true | Envoi de données de télémétrie pour améliorer l’expérience d’utilisation de SDK |
| DecisioningMethod | Énumération de DecisioningMethod | Non | Côté serveur | Doit être défini sur Sur l’appareil ou hybride pour activer la prise de décision sur l’appareil |
| OnDeviceDecisioningReady | Action | Non | valeur nulle | Déléguer pour l’événement Prêt pour la prise de décision sur l’appareil (appelé une fois lorsque la prise de décision sur l’appareil est prête) |
| ArtifactDownloadSuccefully | Action | Non | valeur nulle | Déléguer pour le succès du téléchargement des artefacts de prise de décision sur l’appareil (appelé à chaque téléchargement réussi des artefacts) |
| ArtifactDownloadFailed | Action | Non | valeur nulle | Déléguer pour échec du téléchargement des artefacts de prise de décision sur l’appareil (appelé à chaque échec de téléchargement des artefacts) |
| OnDeviceEnvironment | string | Non | production | Peut être utilisé pour spécifier un autre environnement sur l’appareil, tel que l’évaluation |
| OnDeviceConfigHostname | string | Non | `assets.adobetarget.com` | Peut être utilisé pour spécifier un hôte différent à utiliser pour télécharger le fichier artefact de prise de décision sur l’appareil |
| OnDeviceDecisioningPollingIntSecs | int | Non | 300 (5 min) | Nombre de secondes entre les récupérations du fichier d’artefact de prise de décision sur l’appareil |
| OnDeviceArtifactPayload | string | Non | valeur nulle | Permet la prise de décision sur l’appareil avec une payload d’artefact local pour permettre une exécution immédiate |

## Exemple

## C\
&#x200B;#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
