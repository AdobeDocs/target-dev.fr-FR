---
title: Utilisation de getAttributes dans  [!DNL Adobe Target]  avec le SDK Java
description: Découvrez comment utiliser getAttributes() pour récupérer des expériences d’expérimentation et personnalisées à partir de [!DNL Target]  et extraire des valeurs d’attribut.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 13%

---

# Obtenir des attributs (Java)

## Description

`getAttributes()` est utilisé pour récupérer l’expérimentation et les expériences personnalisées de [!DNL Target] et extraire des valeurs d’attribut.

## Méthode

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Paramètres

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Oui | None | Même requête cible que celle utilisée pour [Obtenir des offres &#x200B;](get-offers.md) |
| mboxNames | tableau var-args | Non | None | Tableau var-args de noms de mbox |


## Résultats

Un objet `Attributes` est renvoyé par `TargetClient.getAttributes()` avec les méthodes suivantes :

| Nom | Type | Description |
| --- | --- | --- |
| getBoolean(mboxName, key) | Booléen | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| getString(mboxName, key) | Chaîne | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| getInteger(mboxName, key) | Entier | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| getDouble(mboxName, key) | Double | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| toMboxMap(mboxName) | Carte | Renvoie une carte simple avec des paires clé-valeur |
| getResponse() | TargetDeliveryResponse | Renvoie l’objet de réponse normalement renvoyé par getOffers |

## Exemple

### Java

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .build();

Attributes offerAttributes = targetJavaClient.getAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
String searchProviderId = offerAttributes.getString("demo-engineering-flags", "searchProviderId");

//returns a simple Map representing the mbox offer
Map<String, Object> engineeringFlags = offerAttributes.toMboxMap("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

String assetUrl = "http://" + engineeringFlags.cdnHostname + "/path/to/asset";
```
