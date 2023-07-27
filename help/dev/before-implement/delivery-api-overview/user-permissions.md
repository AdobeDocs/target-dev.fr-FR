---
title: Autorisations utilisateur de l’API de diffusion Adobe Target
description: Autorisations utilisateur de l’API de diffusion Adobe Target
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="Découvrez les fonctionnalités incluses dans Target Premium."
keywords: api de diffusion
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Autorisations utilisateur (Premium)

[!DNL Adobe] permet aux clients de gérer les autorisations de leurs utilisateurs lors de l’utilisation d’Adobe Target. Pour réussir une [!UICONTROL API de diffusion Adobe Target] , un jeton avec les autorisations appropriées doit être transmis dans l’appel API . Pour en savoir plus sur l’autorisation des utilisateurs et sur la récupération de la visite du jeton [cette documentation](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html).

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

Une fois que vous disposez du jeton correspondant, transmettez-le dans `property` -> `token` pour chaque appel d’API effectué. Si la variable `property` -> `token` n’est pas transmis dans chaque appel d’API, vous n’obtiendrez aucune `content` de retour depuis Adobe Target.

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

Comme vous pouvez le voir ci-dessus, sans transmettre la variable `property` -> `token`, vous ne récupérerez aucun contenu. Si vous attendez du contenu de votre appel API, mais que vous ne récupérez aucun contenu de la réponse, c’est probablement parce que la variable  `property` -> `token` n’est pas fourni ou est transmis sans les autorisations appropriées.
