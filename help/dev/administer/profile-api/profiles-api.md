---
title: API de profils Adobe Target
description: Découvrez comment utiliser les API de profil Adobe Target pour envoyer des données de visiteur à  [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 480cbbbe-4822-48c3-80d4-53628dee57b0
TQID: https://experienceleague.adobe.com/zmA1vGqBRL8gD-cFjJC0idogx7UF1e22iLEfNT9OHZ4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 105
ht-degree: 2%

---

# Vue d’ensemble des [!DNL Adobe Target Profiles API]

[!DNL Adobe Target] crée et conserve un profil pour chaque utilisateur. Ce profil est stocké sur le cluster Edge de [!DNL Target] et est mis à jour en temps réel après chaque visite.

## Structure d’un profil de [!DNL Target]

Un profil Target se compose des objets suivants :

| Objet | Détails |
| --- | --- |
| `clientcode` | Code client [!DNL Target] auquel le profil est associé. |
| `visitorId` | Identifiant du profil. Il peut s’agir d’un `tntid`, d’un `thirdpartyid` ou d’un `marketingcloudvisitorid`. |
| `modifiedAt` | Date et heure de la dernière mise à jour du profil. |
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
