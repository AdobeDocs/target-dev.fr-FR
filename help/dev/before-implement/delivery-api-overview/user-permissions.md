---
title: Autorisations utilisateur de l’API de diffusion Adobe Target
description: Autorisations utilisateur de l’API de diffusion Adobe Target
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=fr#premium newtab=true" tooltip="Voir ce qui est inclus dans Target Premium."
keywords: API de diffusion
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/V7F8WjDNUMJJySyep0nVCg0wMK05ZfdV4XPtMjXOBvM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 184
ht-degree: 1%

---

# Autorisations utilisateur (Premium)

[!DNL Adobe] permet aux clients de gérer les autorisations de leurs utilisateurs lorsqu’ils utilisent Adobe Target. Pour réussir un appel API de diffusion , un jeton disposant des autorisations appropriées doit être transmis dans l’appel API. Pour en savoir plus sur les autorisations des utilisateurs et la récupération du jeton, consultez [cette documentation](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=fr).

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

Une fois que vous disposez du jeton correspondant, transmettez-le dans `property` -> `token` pour chaque appel API effectué. Si la `property` -> `token` n’est pas transmise dans chaque appel API, vous ne recevrez aucune `content` en retour d’Adobe Target.

```
{
    "status": 200,
    "requestId": "07ce783d-58b9-461c-9f4c-6873aeb00c01",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage"
            }
        ]
    }
}
```

Comme vous pouvez le voir ci-dessus, sans transmettre le `property` -> `token`, vous ne récupérerez aucun contenu. Si vous attendez du contenu de votre appel API mais que vous n’en récupérez aucun à partir de la réponse, cela est probablement dû au fait que le `token` `property` -> n’est pas fourni ou qu’il est transmis sans les autorisations appropriées.
