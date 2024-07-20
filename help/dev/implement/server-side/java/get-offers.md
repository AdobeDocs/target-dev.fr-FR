---
title: Utilisez getOffers() dans [!DNL Adobe Target] lors de l’utilisation du SDK Java
description: Découvrez comment utiliser getOffers() pour exécuter une décision et récupérer une expérience de [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 13%

---

# Obtention d’offres (Java)

## Description

`getOffers()` est utilisé pour exécuter une décision et récupérer une expérience de [!DNL Adobe Target].

## Méthode

### getOffers

La signature de la méthode `TargetClient.getOffers` s’affiche comme suit.

**Demande**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest est créé à l’aide de `TargetDeliveryRequest.builder`.

**Réponse**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## Paramètres

L’objet `[!UICONTROL TargetDeliveryRequestBuilder]` possède la structure suivante :

| Nom | Type | Requis | Description |
| --- | --- | --- | --- |
| contexte | Contexte | Oui | Spécifie le contexte de la requête. |
| sessionId |  | Chaîne | Non | Utilisé pour lier plusieurs requêtes [!DNL Target] |
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
| mcId | Chaîne | Non | Utilisé pour fusionner et partager des données entre différentes [!DNL Adobe] solutions (ECID). Récupéré de targetCookies. Génération automatique si elle n’est pas fournie. |
| trackingServer | Chaîne | Non | Le serveur Adobe Analytics afin que [!DNL Adobe Target] et [!DNL Adobe Analytics] relient correctement les données. |
| trackingServerSecure | Chaîne | Non | [!UICONTROL Adobe Analytics Secure Server] afin que [!DNL Adobe Target] et [!DNL Adobe Analytics] relient correctement les données. |
| decisioningMethod | DecisioningMethod | Non | Peut être utilisé pour définir explicitement la méthode de prise de décision ON_DEVICE ou HYBRID pour la prise de décision sur l’appareil |

Les valeurs de chaque champ doivent être conformes à la spécification de requête *[!UICONTROL Target View Delivery API]*. Pour en savoir plus sur *[!UICONTROL Target View Delivery API]*, voir [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## Réponse

La `TargetDeliveryResponse` renvoyée par `TargetClient.getOffers(` a la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| events | &#x200B; TargetDeliveryRequest | requête *[!DNL Target]* |
| response | DeliveryResponse | Réponse *[!DNL Target]* |
| cookies | Liste | Liste des métadonnées de session pour cet utilisateur. Doit être transmis dans la requête cible suivante pour cet utilisateur. |
| visitorState | Carte | État du visiteur à définir côté client pour être utilisé par l’API visiteur |
| responseStatus | ResponseStatus | Objet représentant l’état de la réponse |

Le `ResponseStatus` de la réponse contient les champs suivants :

| Nom | Type | Description |
| --- | --- | --- |
| status | int | État HTTP renvoyé par [!DNL Target] |
| message | Chaîne | Message d’état au cas où l’état HTTP ne serait pas 200 |
| remoteMboxes | Liste de chaînes | Utilisé pour la prise de décision sur l’appareil. Contient une liste des mbox comportant des activités distantes qui ne peuvent pas être décidées entièrement sur l’appareil. |
| remoteViews | Liste de chaînes | Utilisé pour la prise de décision sur l’appareil. Contient une liste des vues comportant des activités distantes qui ne peuvent pas être décidées entièrement sur l’appareil. |

L’objet `TargetCookie` utilisé pour enregistrer des données pour une session utilisateur présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| name | Chaîne | Nom du cookie |
| value | Chaîne | Valeur du cookie, la valeur sera convertie en chaîne |
| maxAge | Nombre | L’option maxAge est pratique pour définir les expirations par rapport à l’heure actuelle en secondes. |

Vous n’avez pas à vous soucier de l’expiration des cookies. Target gère maxAge dans le SDK.

## Exemple

**Demande**

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().setMboxes(mboxRequests))
        .build();
```

**Réponse**

```javascript {line-numbers="true"}
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```
