---
title: API Profils Adobe Target
description: Découvrez comment utiliser les API de profil Adobe Target pour envoyer des données de visiteur à  [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 480cbbbe-4822-48c3-80d4-53628dee57b0
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] - Aperçu

[!DNL Adobe Target] crée et conserve un profil pour chaque utilisateur individuel. Ce profil est stocké sur la grappe [!DNL Target] Edge et est mis à jour en temps réel après chaque visite.

## Structure d’un profil [!DNL Target]

Un profil Target se compose des objets suivants :

| Objet | Détails |
| --- | --- |
| `clientcode` | Code client [!DNL Target] auquel le profil est associé. |
| `visitorId` | Identifiant du profil. Il peut s’agir d’un `tntid`, d’un `thirdpartyid` ou d’un `marketingcloudvisitorid`. |
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
