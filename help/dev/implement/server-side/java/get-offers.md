---
title: Utilisez getOffers() in [!DNL Adobe Target] lors de l’utilisation de Java SDK.
description: Découvrez comment utiliser getOffers() pour exécuter une décision et récupérer une expérience depuis  [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
TQID: https://experienceleague.adobe.com/2oYkwezf-GkZnybeQUKUbCE6sPAHNQkg3Z1KH8s2a-g
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
source-wordcount: 664
ht-degree: 13%

---

# Obtenir Des Offres (Java)

## Description

`getOffers()` est utilisé pour exécuter une décision et récupérer une expérience à partir de [!DNL Adobe Target].

## Méthode

### getOffers

La signature de la méthode `TargetClient.getOffers` s’affiche comme suit.

**Demande**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest est créé à l&#39;aide de `TargetDeliveryRequest.builder`.

**Réponse**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## Paramètres

L’objet `[!UICONTROL TargetDeliveryRequestBuilder]` présente la structure suivante :

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
| mcId | Chaîne | Non | Utilisé pour fusionner et partager des données entre différentes solutions [!DNL Adobe] (ECID). Récupéré à partir de targetCookies. Généré automatiquement s’il n’est pas fourni. |
| trackingServer | Chaîne | Non | Le serveur Adobe Analytics afin que [!DNL Adobe Target] et [!DNL Adobe Analytics] assemblent correctement les données. |
| trackingServerSecure | Chaîne | Non | Le [!UICONTROL serveur sécurisé &#x200B;] pour que [!DNL Adobe Target] et [!DNL Adobe Analytics] assemblent correctement les données. |
| decisioningMethod | DecisioningMethod | Non | Peut être utilisé pour définir explicitement la méthode de prise de décision ON_DEVICE ou HYBRID pour la prise de décision sur l’appareil |

Les valeurs de chaque champ doivent être conformes à la spécification de requête *[!UICONTROL API de diffusion de la vue cible]*. Pour en savoir plus sur l’*[!UICONTROL API de diffusion de la vue Target]*, consultez [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## Réponse

La `TargetDeliveryResponse` renvoyée par `TargetClient.getOffers(`) présente la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| events | TargetDeliveryRequest&#x200B; | *[!DNL Target]* la demande |
| réponse | DeliveryResponse | *[!DNL Target]* réponse |
| cookies | Liste | Liste des métadonnées de session pour cet utilisateur. Doit être transmis dans la prochaine requête cible pour cet utilisateur. |
| visitorState | Carte | État du visiteur à définir côté client à utiliser par l’API visiteur |
| responseStatus | ResponseStatus | Objet représentant le statut de la réponse |

Le `ResponseStatus` de la réponse contient les champs suivants :

| Nom | Type | Description |
| --- | --- | --- |
| status | int | Statut HTTP renvoyé par [!DNL Target] |
| message | Chaîne | Message de statut au cas où le statut HTTP n’est pas 200 |
| remoteMboxes | Liste de chaînes | Utilisé pour la prise de décision sur l’appareil. Contient une liste de mbox ayant des activités distantes qui ne peuvent pas être décidées entièrement sur l’appareil. |
| remoteViews | Liste de chaînes | Utilisé pour la prise de décision sur l’appareil. Contient une liste de vues ayant des activités distantes qui ne peuvent pas être décidées entièrement sur l’appareil. |

L’objet `TargetCookie` utilisé pour enregistrer des données pour une session utilisateur possède la structure suivante :

| Nom | Type | Description |
| --- | --- | --- |
| name | Chaîne | Nom du cookie |
| value | Chaîne | Valeur du cookie. La valeur sera convertie en chaîne. |
| maxAge | Nombre | L’option maxAge est pratique pour définir les expirations par rapport à l’heure actuelle en secondes |

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
