---
title: Initialisation du SDK Java à l’aide de la méthode create
description: Découvrez comment utiliser la méthode create pour initialiser le SDK Java et instancier le [!UICONTROL TargetClient] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: 1d080b5e402e5d55039bf06611b44678cc6c36de
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 18%

---

# Initialiser le SDK Java

## Description

Utilisez la variable `create` pour initialiser le SDK Java et instancier la méthode [!UICONTROL Client Target] pour effectuer des appels vers [!DNL Adobe Target] pour des expériences et des expériences personnalisées.

## Méthode

[!UICONTROL TargetClient] est créé à l’aide de `TargetClient.create`.

### create

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig est créé à l’aide de `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Paramètres

`ClientConfigBuilder` possède la structure suivante :

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| client | Chaîne | Oui | None | [!UICONTROL Identifiant du client Target] |
| organizationId | Chaîne | Oui | None | [!UICONTROL ID d’organisation Experience Cloud] |
| connectTimeout | Nombre | Non | 10000 | Délai de connexion pour toutes les requêtes en millisecondes |
| socketTimeout | Nombre | Non | 10000 | Délai d’expiration du socket pour toutes les requêtes en millisecondes |
| maxConnectionsPerHost | Nombre | Non | 100 | Nombre max. de connexions par [!DNL Target] hôte |
| maxConnectionsTotal | Nombre | Non | 200 | Nombre max. de connexions incluant toutes les [!DNL Target] hosts |
| connectionTtlMs | Nombre | Non | -1 | La durée de vie totale (TTL) définit la durée de vie maximale des connexions persistantes en millisecondes. Par défaut, les connexions resteront actives indéfiniment. |
| idleConnectionValidationMs | Nombre | Non | 1000 | Période d’inactivité en millisecondes après laquelle les connexions persistantes sont revalidées avant d’être réutilisées |
| evrapporteIdleConnectionsAfterSecs | Nombre | Non | 20 | Durée en secondes d’exclusion des connexions inactives du pool de connexions |
| enableRetries | Booléen | Non | true | Tentatives automatiques pour les délais de socket (max 4) |
| logRequests | Booléen | Non | false | Journal [!DNL Target] requêtes et réponses dans debug |
| logRequestStatus | Booléen | Non | false | Journal [!DNL Target] temps de réponse, état et URL |
| serverDomain | Chaîne | Non | `*client*.tt.omtrdc.net` | Remplace le nom d’hôte par défaut |
| secure | Booléen | Non | true | Non défini pour appliquer le schéma HTTP |
| requestInterceptor | HttpRequestInterceptor | Non | Valeur nulle | Ajout d’un intercepteur de requête personnalisé |
| defaultPropertyToken | Chaîne | Non | None | Définit le jeton de propriété par défaut pour chaque `getOffers` appelez . **Pour la prise de décision sur appareil**, le SDK ne télécharge que l’artefact qui contient les activités qualifiées pour le jeton de propriété défini dans `defaultPropertyToken` |
| defaultDecisioningMethod | Enum DecisioningMethod | Non | SERVER_SIDE | Doit être défini sur ON_DEVICE ou HYBRID pour activer la prise de décision sur l’appareil. |
| telemetryEnabled | Booléen | Non | true | Permet aux clients de se désinscrire de la collecte de données supplémentaire lors des demandes à [!DNL Target] serveurs |
| proxyConfig | ClientProxyConfig | Non | None | Permet au client de fournir ses propres détails de proxy. |
| exceptionHandler | TargetExceptionHandler | Non | None | Peut être utilisé pour implémenter une gestion des exceptions personnalisée lors du traitement des règles |
| httpClient | HttpClient | Non | None | Permet aux utilisateurs de remplacer la variable [!DNL Target] Client HTTP avec client HTTP personnalisé |
| onDeviceEnvironment | Chaîne | Non | production | Peut être utilisé pour spécifier un autre environnement sur l’appareil, tel que l’évaluation |
| onDeviceConfigHostname | Chaîne | Non | `assets.adobetarget.com` | Peut être utilisé pour spécifier un autre hôte à utiliser pour télécharger le fichier d’artefact de prise de décision sur l’appareil |
| onDeviceDecisioningPollingIntSecs | int | Non | 300 (5 minutes) | Nombre de secondes entre les récupérations du fichier d’artefact de prise de décision sur l’appareil |
| onDeviceArtifactPayload | octet[] | Non | None | Fournit une prise de décision sur l’appareil avec la charge utile d’artefact précédente pour permettre une exécution immédiate |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | Non | None | Enregistre les rappels pour les événements de prise de décision sur l’appareil |
| onDeviceAllMatchingRulesMboxes | Liste\&lt;string> | Non | None | Permet aux utilisateurs de spécifier des mbox pour lesquelles tout le contenu de règle correspondant sera renvoyé lors de la prise de décision sur l’appareil. |

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
