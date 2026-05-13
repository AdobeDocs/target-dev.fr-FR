---
title: Utilisez getOffers() in [!DNL Adobe Target] lors de l’utilisation du SDK .NET
description: Découvrez comment utiliser getOffers() pour exécuter une décision et récupérer une expérience depuis  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
TQID: https://experienceleague.adobe.com/T-oUyDgCJZ8hqQZgCb3-Z-d9WeMaffwq8krMHhGvYlI
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 572
ht-degree: 14%

---

# Obtenir les offres (.NET)

## Description

`GetOffers()` est utilisé pour exécuter une décision et récupérer une expérience à partir de [!DNL Adobe Target].

## Méthode

Signature de méthode `TargetClient.GetOffers`.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest` est créé à l’aide de `TargetDeliveryRequest.Builder`.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## Paramètres

L’objet `TargetDeliveryRequest.Builder` présente la structure suivante :

| Nom | Type | Requis | Description |
| --- | --- | --- | --- |
| contexte | Contexte | Oui | Indique le contexte de la demande |
| sessionId | Chaîne | Non | Utilisé pour lier plusieurs requêtes [!DNL Target] |
| thirdPartyId | Chaîne | Non | Identifiant de votre société pour l’utilisateur que vous pouvez envoyer avec chaque appel |
| cookies | Liste | Non | Liste des cookies renvoyés dans la demande de [!DNL Target] précédente du même utilisateur. |
| customerIds | Carte | Non | ID de client au format compatible avec les VisitorId |
| exécuter | ExecuteRequest | Non | Requête PageLoad ou mbox à exécuter. Sera évalué immédiatement côté serveur |
| prérécupération | PrefetchRequest | Non | Requête de prérécupération des vues, du chargement de page ou des mbox. Renvoie avec jeton de notification à renvoyer lors de la conversion. |
| notifications | Liste | Non | Utilisé pour envoyer des notifications concernant le contenu prérécupéré affiché |
| requestId | Chaîne | Non | L’identifiant de requête qui sera renvoyé dans la réponse. Généré automatiquement s’il est absent. |
| impressionId | Chaîne | Non | Si elles sont présentes, les deuxièmes requêtes et les requêtes suivantes avec le même id n’incrémenteront pas les impressions en activités/mesures. Généré automatiquement s’il est absent. |
| environmentId | Long | Non | Identifiant d’environnement client valide. Si aucun hôte n’est spécifié, il est déterminé en fonction de l’hôte fourni. |
| propriété | Propriété | Non | Indique la propriété at_property via le champ Jeton . Il peut être utilisé pour contrôler la portée de la diffusion. |
| trace | Trace | Non | Active la trace pour l’API de diffusion. |
| qaMode | QAMode | Non | Utilisez cet objet pour activer le mode assurance qualité dans la requête. |
| locationHint | Chaîne | Non | [!DNL Target] indicateur d’emplacement du cluster Edge. Utilisé pour cibler un cluster Edge donné pour cette requête. |
| visiteur | Visitor | Non | Utilisé pour fournir un objet API visiteur personnalisé. |
| l’id | VisitorId | Non | Objet contenant les identifiants du visiteur. Par ex. tntId, thirdPartyId, mcId, customerIds. |
| experienceCloud | Experience Cloud | Non | Indique les intégrations avec Audience Manager et Analytics. Automatiquement renseigné à l’aide de cookies, si non fourni. |
| tntId | Chaîne | Non | Identifiant de Principal en [!DNL Target] pour un utilisateur. Récupéré à partir de targetCookies. Généré automatiquement s’il n’est pas fourni. |
| mcId | Chaîne | Non | Utilisé pour fusionner et partager des données entre différentes solutions Adobe (ECID). Récupéré à partir de targetCookies. Généré automatiquement s’il n’est pas fourni. |
| trackingServer | Chaîne | Non | Le serveur Adobe Analytics afin que [!DNL Adobe Target] et [!DNL Adobe Analytics] assemblent correctement les données. |
| trackingServerSecure | Chaîne | Non | La [!UICONTROL Adobe Analytics Secure Server] pour que [!DNL Adobe Target] et [!DNL Adobe Analytics] assemblent correctement les données. |
| decisioningMethod | DecisioningMethod | Non | Peut être utilisé pour définir explicitement la méthode de prise de décision ON_DEVICE ou HYBRID pour la prise de décision sur l’appareil |

Les valeurs de chaque champ doivent être conformes à la spécification de requête [API de diffusion Target](/help/dev/implement/delivery-api/overview.md).

## Réponse

La `TargetDeliveryResponse` renvoyée par `TargetClient.GetOffers()` présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| Demande | TargetDeliveryRequest&#x200B; | Requête [API de diffusion Target](/help/dev/implement/delivery-api/overview.md) |
| Réponse | DeliveryResponse &#x200B; | Réponse [API de diffusion Target](/help/dev/implement/delivery-api/overview.md)* |
| État | HttpStatusCode | Code d’état HTTP de réponse |
| Message | string | Message d’état de réponse ou message d’erreur |
| Emplacements | Emplacements | [!DNL Target] les noms d’emplacement, y compris le nom global de la mbox et les mbox/vues pour lesquelles seule la prise de décision à distance est disponible |
| GetCookies | Dictionnaire | Renvoie un dictionnaire de métadonnées de session pour cet utilisateur. Elle doit être transmise dans la requête de [!DNL Target] suivante pour cet utilisateur. |
| VisitorState | IDictionary | État du visiteur à définir côté client pour l’initialisation de la bibliothèque JavaScript de l’API visiteur |

L’objet `TargetCookie` utilisé pour enregistrer des données pour une session utilisateur possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| Nom | string | Nom du cookie |
| Valeur | string | Valeur du cookie |
| MaxAge | int | L’option `MaxAge` permet de définir facilement la valeur Expire par rapport à l’heure actuelle en secondes |

Vous n’avez pas à vous soucier de l’expiration des cookies. [!DNL Target] gère les `MaxAge` à l’intérieur du SDK.

## Exemple

## \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
    .Build();

var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```
