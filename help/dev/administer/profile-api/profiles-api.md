---
title: API Profils Adobe Target
description: Découvrez comment utiliser les API de profil Adobe Target pour envoyer des données de visiteur à [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] aperçu

[!DNL Adobe Target] crée et conserve un profil pour chaque utilisateur individuel. Ce profil est stocké dans la variable [!DNL Target] grappe Edge et est mise à jour en temps réel après chaque visite.

## Profils [!DNL Postman] collection

[!DNL Postman] est une application qui permet de déclencher facilement des appels API. Ceci [!DNL Postman] contient toutes les [!DNL Profile API] appels . Cliquez sur [Exécuter dans Postman](https://www.getpostman.com/collections/ec7376f9028977ccaa99){target=_blank} pour importer la collection d’API Profile.

## Documentation de l’API Profiles héritée.

La documentation héritée de l’API Profiles se trouve ici : [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}

## Structure d’une [!DNL Target] profile

Un profil Target se compose des objets suivants :

| Objet | Détails |
| --- | --- |
| `clientcode` | La variable [!DNL Target] code client auquel le profil est associé. |
| `visitorId` | Identifiant du profil. Cela peut être une `tntid`, `thirdpartyid`, ou `marketingcloudvisitorid`. |
| `modifiedAt` | Horodatage de la dernière mise à jour du profil. |
| `profileAttributes` | Liste de tous les attributs de profil stockés en tant que paires clé-valeur sur ce profil individuel. |

### Exemple de structure de profil

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```
