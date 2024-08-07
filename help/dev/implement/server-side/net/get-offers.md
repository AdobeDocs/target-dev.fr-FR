---
title: Utilisez getOffers() dans [!DNL Adobe Target] lors de l’utilisation du SDK .NET
description: Découvrez comment utiliser getOffers() pour exécuter une décision et récupérer une expérience de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 14%

---

# Obtention d’offres (.NET)

## Description

`GetOffers()` est utilisé pour exécuter une décision et récupérer une expérience de [!DNL Adobe Target].

## Méthode

signature de la méthode `TargetClient.GetOffers`.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest` est créé en utilisant `TargetDeliveryRequest.Builder`.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## Paramètres

L’objet `TargetDeliveryRequest.Builder` possède la structure suivante :

| Nom | Type | Requis | Description |
| --- | --- | --- | --- |
| contexte | Contexte | Oui | Spécifie le contexte de la requête. |
| sessionId | Chaîne | Non | Utilisé pour lier plusieurs requêtes [!DNL Target] |
| thirdPartyId | Chaîne | Non | Identifiant de votre société pour l’utilisateur que vous pouvez envoyer avec chaque appel |
| cookies | Liste | Non | Liste des cookies renvoyés dans la requête [!DNL Target] précédente du même utilisateur. |
| customerIds | Carte | Non | ID de client au format compatible avec VisitorId |
| execute | ExecuteRequest | Non | Requête PageLoad ou mbox à exécuter. Est évalué immédiatement côté serveur |
| prefetch | PrefetchRequest | Non | Requête Vues, PageLoad ou mbox à prérécupérer. Renvoie avec jeton de notification à renvoyer lors de la conversion. |
| notifications | Liste | Non | Utilisé pour envoyer des notifications concernant le contenu prérécupéré affiché |
| requestId | Chaîne | Non | Identifiant de requête qui sera renvoyé dans la réponse. Généré automatiquement s’il n’est pas présent. |
| impressionId | Chaîne | Non | Si elles sont présentes, les deuxième requêtes et les requêtes suivantes avec le même ID n’incrémentent pas les impressions aux activités/mesures. Généré automatiquement s’il n’est pas présent. |
| environmentId | Long | Non | ID d’environnement client valide. Si l’hôte n’est pas spécifié, il est déterminé en fonction de l’hôte fourni. |
| property | Propriété | Non | Spécifie la propriété at_property via le champ de jeton. Il peut être utilisé pour contrôler la portée de la diffusion. |
| trace | Trace | Non | Active la trace pour l’API de diffusion. |
| qaMode | QAMode | Non | Utilisez cet objet pour activer le mode AQ dans la requête. |
| locationHint | Chaîne | Non | [!DNL Target] Conseil d’emplacement du cluster Edge. Utilisé pour cibler un cluster Edge donné pour cette requête. |
| visiteur | Visitor | Non | Utilisé pour fournir un objet API visiteur personnalisé. |
| l’id | VisitorId | Non | Objet contenant les identifiants du visiteur. Par exemple. tntId, thirdParyId, mcId, customerIds. |
| experienceCloud | ExperienceCloud | Non | Spécifie les intégrations avec Audience Manager et Analytics. Automatiquement renseignée à l’aide de cookies, le cas échéant. |
| tntId | Chaîne | Non | Identifiant de Principal dans [!DNL Target] pour un utilisateur. Récupéré de targetCookies. Génération automatique si elle n’est pas fournie. |
| mcId | Chaîne | Non | Utilisé pour fusionner et partager des données entre différentes solutions Adobe (ECID). Récupéré de targetCookies. Génération automatique si elle n’est pas fournie. |
| trackingServer | Chaîne | Non | Le serveur Adobe Analytics afin que [!DNL Adobe Target] et [!DNL Adobe Analytics] relient correctement les données. |
| trackingServerSecure | Chaîne | Non | [!UICONTROL Adobe Analytics Secure Server] afin que [!DNL Adobe Target] et [!DNL Adobe Analytics] relient correctement les données. |
| decisioningMethod | DecisioningMethod | Non | Peut être utilisé pour définir explicitement la méthode de prise de décision ON_DEVICE ou HYBRID pour la prise de décision sur l’appareil |

Les valeurs de chaque champ doivent être conformes à la spécification de requête [API de diffusion cible](/help/dev/implement/delivery-api/overview.md) .

## Réponse

La `TargetDeliveryResponse` renvoyée par `TargetClient.GetOffers()` possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| Demande | &#x200B; TargetDeliveryRequest | Requête [API de diffusion cible](/help/dev/implement/delivery-api/overview.md) |
| Réponse | &#x200B; DeliveryResponse | Réponse [API de diffusion cible](/help/dev/implement/delivery-api/overview.md)* |
| État | HttpStatusCode | Code d’état HTTP de réponse |
| Message | string | Message d’état de la réponse ou message d’erreur |
| Emplacements | Emplacements | [!DNL Target] noms d’emplacement, y compris le nom de mbox globale et les mbox/vues pour lesquelles seule la prise de décision à distance est disponible |
| GetCookies | Dictionnaire | Renvoie un dictionnaire de métadonnées de session pour cet utilisateur. Cela doit être transmis dans la requête [!DNL Target] suivante pour cet utilisateur. |
| VisitorState | IDictionary | État du visiteur à définir côté client pour l’initialisation de la bibliothèque JavaScript de l’API visiteur |

L’objet `TargetCookie` utilisé pour enregistrer des données pour une session utilisateur présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| Nom | string | Nom du cookie |
| Valeur | string | Valeur du cookie |
| MaxAge | int | L’option `MaxAge` est pratique pour définir Expires par rapport à l’heure actuelle en secondes. |

Vous n’avez pas à vous soucier de l’expiration des cookies. [!DNL Target] gère `MaxAge` à l’intérieur du SDK.

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
