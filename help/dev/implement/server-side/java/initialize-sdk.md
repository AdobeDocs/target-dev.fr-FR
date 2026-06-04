---
title: Initialisez le SDK Java à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Java et instancier le [!UICONTROL TargetClient] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
TQID: https://experienceleague.adobe.com/B1Ev7NnjlFMg4VoicF6Z4whyqfJYDjCwPeYRKEk2viY
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 471
ht-degree: 16%

---

# Initialiser le SDK Java

## Description

Utilisez la méthode `create` afin d’initialiser Java SDK et d’instancier le [!UICONTROL client Target] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.

## Méthode

[!UICONTROL TargetClient] est créé à l’aide de `TargetClient.create`.

### créer

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig est créé à l’aide de `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Paramètres

`ClientConfigBuilder` présente la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| client | Chaîne | Oui | None | [!UICONTROL Identifiant Client Target] |
| organizationId | Chaîne | Oui | None | [!UICONTROL ID d’organisation Experience Cloud] |
| connectTimeout | Nombre | Non | 10000 | Délai d’expiration de connexion pour toutes les requêtes, en millisecondes |
| socketTimeout | Nombre | Non | 10000 | Délai d’expiration du socket pour toutes les requêtes, en millisecondes |
| maxConnectionsPerHost | Nombre | Non | 100 | Nbre max. de connexions par hôte [!DNL Target] |
| maxConnectionsTotal | Nombre | Non | 200 | Connexions max. incluant tous les hôtes [!DNL Target] |
| connectionTtlMs | Nombre | Non | -1 | La durée de vie totale (TTL) définit la durée de vie maximale des connexions persistantes en millisecondes. Par défaut, les connexions seront maintenues en vie indéfiniment |
| idleConnectionValidationMs | Nombre | Non | 1000 | Période d’inactivité en millisecondes au-delà de laquelle les connexions persistantes sont revalidées avant d’être réutilisées |
| eventIdleConnectionsAfterSecs | Nombre | Non | 20 | Délai en secondes pour éjecter les connexions inactives du pool de connexions |
| enableRetries | Booléen | Non | true | Reprises automatiques pour les dépassements de délai de socket (max. 4) |
| logRequests | Booléen | Non | false | Enregistrer [!DNL Target] requêtes et les réponses dans le débogage |
| logRequestStatus | Booléen | Non | false | Enregistrer [!DNL Target] temps de réponse, le statut et l’URL |
| serverDomain | Chaîne | Non | `*client*.tt.omtrdc.net` | Remplace le nom d’hôte par défaut |
| sécuriser | Booléen | Non | true | Annuler l’application du schéma HTTP |
| requestInterceptor | HttpRequestInterceptor | Non | Null | Ajouter l’intercepteur de requêtes personnalisé |
| defaultPropertyToken | Chaîne | Non | None | Définit le jeton de propriété par défaut pour chaque appel `getOffers`. **Pour la prise de décision sur l’appareil**, le SDK télécharge uniquement l’artefact qui contient les activités qualifiées pour le jeton de propriété défini dans `defaultPropertyToken` |
| defaultDecisioningMethod | Énumération de DecisioningMethod | Non | SERVER_SIDE | Doit être défini sur ON_DEVICE ou HYBRID pour activer la prise de décision sur l’appareil |
| telemetryEnabled | Booléen | Non | true | Permet aux clients de se désabonner de la collecte de données supplémentaires lors des requêtes aux serveurs [!DNL Target] |
| proxyConfig | ClientProxyConfig | Non | None | Permet au client de fournir ses propres détails de proxy |
| exceptionHandler | TargetExceptionHandler | Non | None | Peut être utilisé pour implémenter la gestion des exceptions personnalisées lors du traitement des règles |
| httpClient | HttpClient | Non | None | Permet aux utilisateurs de remplacer le client HTTP [!DNL Target] par un client HTTP personnalisé |
| onDeviceEnvironment | Chaîne | Non | production | Peut être utilisé pour spécifier un autre environnement sur l’appareil, tel que l’évaluation |
| onDeviceConfigHostname | Chaîne | Non | `assets.adobetarget.com` | Peut être utilisé pour spécifier un hôte différent à utiliser pour télécharger le fichier artefact de prise de décision sur l’appareil |
| onDeviceDecisioningPollingIntSecs | int | Non | 300 (5 minutes) | Nombre de secondes entre les récupérations du fichier d’artefact de prise de décision sur l’appareil |
| onDeviceArtifactPayload | byte[] | Non | None | Permet la prise de décision sur l’appareil avec la payload de l’artefact précédent pour permettre une exécution immédiate |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Non | None | Enregistre des rappels pour les événements de prise de décision sur l’appareil |
| onDeviceAllMatchingRulesMboxes | Liste\&lt;Chaîne\> | Non | None | Permet aux utilisateurs de spécifier des mbox pour lesquelles tout le contenu de règle correspondant sera renvoyé lors de la prise de décision sur l’appareil |

## Exemple

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
