---
title: Utilisez getAttributes dans [!DNL Adobe Target] avec le SDK .NET
description: Découvrez comment utiliser getAttributes() pour récupérer des expériences d’expérimentation et des expériences personnalisées depuis et extraire  [!DNL Target]  valeurs d’attribut.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
TQID: https://experienceleague.adobe.com/aflHPozCwJ-6fB7X-2jLaBvs42Ohz6OzwZ7AvkahCE8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 209
ht-degree: 10%

---

# Obtenir les attributs (.NET)

## Description

`GetAttributes()` est utilisé pour récupérer des expériences et des expériences personnalisées à partir de [!DNL Target] et extraire des valeurs d’attribut.

## Méthode

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## Paramètres

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Non | valeur nulle | La même requête [!DNL Target] que celle utilisée pour [Obtenir les offres&#x200B;](get-offers.md) |
| mboxNames | params string[] | Non | valeur nulle | Tableau de paramètres de noms de mbox |

## Résultats

Un objet `TargetAttributes` est renvoyé par `TargetClient.GetAttributes()` qui possède les propriétés et méthodes suivantes :

| Propriété/Méthode | Type de retour | Description |
| --- | --- | --- |
| Réponse | TargetDeliveryResponse | Renvoie l’objet de réponse normalement renvoyé par [Get Offers](get-offers.md) |
| ToDictionary | IReadOnlyDictionary | Renvoie un dictionnaire de dictionnaires avec des paires clé-valeur regroupées par noms de mbox |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | Renvoie un dictionnaire avec des paires clé-valeur pour la mbox fournie |
| GetBoolean(mboxName, key, defaultValue) | booléen | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| GetString(mboxName, key, defaultValue) | string | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| GetInteger(mboxName, key, defaultValue) | int | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| GetDouble(mboxName, key, defaultValue) | Double | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |
| GetValue(mboxName, key, defaultValue) | T | Renvoie la valeur du nom de mbox et de la clé d’attribut spécifiés |

## Exemple

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
