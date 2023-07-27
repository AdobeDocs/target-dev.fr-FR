---
title: Utilisation de getAttributes dans [!DNL Adobe Target] avec le SDK .NET
description: Découvrez comment utiliser getAttributes() pour récupérer des expériences d’expérimentation et personnalisées à partir de [!DNL Target] et extraire des valeurs d’attribut.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 10%

---

# Obtention des attributs (.NET)

## Description

`GetAttributes()` est utilisé pour récupérer les expériences et les expériences personnalisées d’ [!DNL Target] et extraire des valeurs d’attribut.

## Méthode

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## Paramètres

| Nom | Type | Requis | Par défaut | Description |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | Non | valeur nulle | Identique [!DNL Target] requête utilisée pour [Obtention d’une &#x200B; d’offres](get-offers.md) |
| mboxNames | chaîne params[] | Non | valeur nulle | Tableau de paramètres de noms de mbox |

## Résultats

A `TargetAttributes` est renvoyé par `TargetClient.GetAttributes()` qui possède les propriétés et méthodes suivantes :

| Propriété/méthode | Type de retour | Description |
| --- | --- | --- |
| Réponse | TargetDeliveryResponse | Renvoie l’objet de réponse normalement renvoyé par [Obtention d’offres](get-offers.md) |
| ToDictionary | IReadOnlyDictionary | Renvoie un dictionnaire de dictionnaires avec des paires clé-valeur regroupées par noms de mbox |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | Renvoie un dictionnaire avec des paires clé-valeur pour la mbox fournie |
| GetBoolean(mboxName, key, defaultValue) | bool | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| GetString(mboxName, key, defaultValue) | string | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| GetInteger(mboxName, key, defaultValue) | int | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| GetDouble(mboxName, key, defaultValue) | double | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |
| GetValue(mboxName, key, defaultValue) | T   | Renvoie la valeur d’un nom de mbox et d’une clé d’attribut spécifiés |

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
