---
title: Utilisation de getAttributes dans [!DNL Adobe Target] avec Java SDK
description: Découvrez comment utiliser getAttributes() pour récupérer des expériences d’expérimentation et des expériences personnalisées depuis et extraire  [!DNL Target]  valeurs d’attribut.
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
TQID: https://experienceleague.adobe.com/ZZy9nUXiyR-qwBmOgv-TPS6ZuilvAuW850gH1Doqquo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 169
ht-degree: 13%

---

# Obtenir Les Attributs (Java)

## Description

`getAttributes()` est utilisé pour récupérer des expériences et des expériences personnalisées à partir de [!DNL Target] et extraire des valeurs d’attribut.

## Méthode

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## Paramètres

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Oui | None | La même requête cible que celle utilisée pour [Obtenir les offres&#x200B;](get-offers.md) |
| mboxNames | tableau var-args | Non | None | Tableau var-args de noms de mbox |


## Résultats

Un objet `Attributes` est renvoyé par `TargetClient.getAttributes()` qui possède les méthodes suivantes :

| Nom | Type | Description |
| --- | --- | --- |
| getBoolean(mboxName, key) | Booléen | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| getString(mboxName, key) | Chaîne | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| getInteger(mboxName, key) | Entier | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| getDouble(mboxName, key) | Double | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| toMboxMap(mboxName) | Carte | Renvoie un mappage simple avec des paires clé-valeur |
| getResponse() | TargetDeliveryResponse | Renvoie l&#39;objet de réponse normalement renvoyé par getOffers |

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
