---
title: API de diffusion Adobe Target identifiant les visiteurs
description: Comment identifier un utilisateur dans [!DNL Adobe Target]?
keywords: api de diffusion
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 9%

---

# Identification des visiteurs

Il existe plusieurs façons d’identifier un visiteur dans [!DNL Adobe Target].

Target utilise trois identifiants :

| Nom du champ | Description |
| --- | --- |
| `tntId` | La variable `tntId` est l’identifiant Principal dans [!DNL Target] pour un utilisateur. Vous pouvez fournir cet identifiant ou [!DNL Target] la génère automatiquement si la requête ne contient pas. |
| `thirdPartyId` | La variable `thirdPartyId` est l’identifiant de votre société pour l’utilisateur que vous pouvez envoyer avec chaque appel . Lorsqu’un utilisateur se connecte au site d’une entreprise, celle-ci crée généralement un identifiant lié au compte du visiteur, à sa carte de fidélité, à son numéro de membre ou à tout autre identifiant applicable de l’entreprise. |
| `marketingCloudVisitorId` | La variable `marketingCloudVisitorId` est utilisé pour fusionner et partager des données entre différentes solutions d’Adobe. La variable `marketingCloudVisitorId` est requis pour les intégrations avec Adobe Analytics et Adobe Audience Manager. |
| `customerIds` | Outre l’identifiant visiteur Experience Cloud, d’autres [ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) et un état authentifié pour chaque visiteur peut être utilisé. |

## [!DNL Target] ID

La variable [!DNL Target] ID ou `tntId` peut être considéré comme un identifiant d’appareil. Ceci `tntId` est généré automatiquement par [!DNL Target] s’il n’est pas fourni dans la requête. Par la suite, les demandes suivantes doivent inclure ceci : `tntId` pour que le contenu approprié soit diffusé sur un appareil utilisé par l’utilisateur.

```http {line-numbers="true"}
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

L’exemple d’appel ci-dessus montre qu’une `tntId` ne doit pas être transmis. Dans ce scénario, [!DNL Target]  génère une `tntId` et fournissez-le dans la réponse, comme illustré ici :

```URI {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "demo",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  ...
}
```

La variable `tntId` is `10abf6304b2714215b1fd39a870f01afc.28_20`. Veuillez noter que `tntId` doit être utilisé lors de l’appel de la variable [!UICONTROL API de diffusion Adobe Target] pour le même utilisateur sur plusieurs sessions.

## Identifiant visiteur Marketing Cloud

La variable `marketingCloudVisitorId` est un identifiant universel et permanent qui identifie vos visiteurs dans toutes les solutions de l’Experience Cloud. Lorsque votre organisation met en oeuvre le service d’ID, cet ID vous permet d’identifier un même visiteur du site et ses données dans différentes solutions Experience Cloud telles qu’Adobe Target, Adobe Analytics ou Adobe Audience Manager. Veuillez noter que la variable `marketingCloudVisitorId` est requis lors de l’utilisation et de l’intégration avec Analytics et Audience Manager.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "marketingCloudVisitorId": "10527837386392355901041112038610706884"
  },
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

L’exemple d’appel ci-dessus illustre comment un appel `marketingCloudVisitorId` qui a été récupéré du service d’ID d’Experience Cloud est transmis à Adobe Target. Dans ce scénario, [!DNL Target] génère une `tntId` puisqu’il n’a pas été transmis à l’appel d’origine qui sera mappé à la variable fournie `marketingCloudVisitorId` comme illustré dans la réponse ci-dessous.

## ID tiers

Si votre organisation utilise un ID pour identifier votre visiteur, vous pouvez utiliser `thirdPartyID` pour diffuser du contenu. Cependant, vous devez fournir la variable `thirdPartyID` pour chaque [!UICONTROL API de diffusion Adobe Target] appelle-toi à faire.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "thirdPartyId": "B234A029348"
  },
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

L’exemple d’appel ci-dessus illustre une `thirdPartyId`, qui est un identifiant persistant utilisé par votre entreprise pour identifier un utilisateur final, qu’il interagisse avec votre entreprise à partir de canaux web, mobiles ou IoT. En d’autres termes, la variable `thirdPartyId` fera référence aux données de profil utilisateur qui peuvent être utilisées sur plusieurs canaux. Dans ce scénario, [!DNL Target] génère une `tntId`, puisqu’il n’a pas été transmis à l’appel d’origine, qui sera mappé à la variable fournie `thirdPartyId` comme illustré dans la réponse ci-dessous.

```
{
    "status": 200,
    "requestId": "55de9886-bd14-4dee-819c-7d1633b79b90",
    "client": "demo",
    "id": {
        "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20",
        "thirdPartyId": "B234A029348"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    ...
}
```

## Customer ID

[ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) peut être ajouté et associé à un identifiant visiteur Experience Cloud. Lors de l’envoi `customerIds` la valeur `marketingCloudVisitorId` doit également être fourni. En outre, un état d’authentification peut être fourni avec chaque `customerId` pour chaque visiteur. L’état d’authentification suivant peut être pris en compte :

| État d’authentification | État d’utilisateur |
| --- | --- |
| `unknown` | Inconnu ou jamais authentifié. Cet état peut être utilisé pour des scénarios tels qu’un visiteur qui a accédé à votre site en cliquant sur une annonce publicitaire. |
| `authenticated` | L’utilisateur est actuellement authentifié dans une session active sur votre site web ou votre application. |
| `logged_out` | L’utilisateur était authentifié, mais actuellement déconnecté. Celui-ci a eu l’intention de se déconnecter de l’état d’authentification. Il ne souhaite plus être considéré comme authentifié. |

Veuillez noter que uniquement lorsque l’ID de client se trouve dans `authenticated` L’état de Target référence les données de profil utilisateur stockées et liées à l’ID de client. Si l’ID de client se trouve dans `unknown` ou `logged_out` , l’ID de client sera ignoré et les données de profil utilisateur qui peuvent lui être associées ne seront pas utilisées pour le ciblage de l’audience.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
      "id": {
        "marketingCloudVisitorId" : "2304820394812039",
        "customerIds": [{
          "id": "134325423",
          "integrationCode" : "crm_data",
          "authenticatedState" : "authenticated"
        }]
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

L’exemple d’appel ci-dessus montre comment envoyer une `customerId` avec un `authenticatedState`. Lors de l’envoi d’un `customerId`, la variable `integrationCode`, `id`, et `authenticatedState` ainsi que la variable `marketingCloudVisitorId` sont obligatoires. La variable `integrationCode` est l’alias de la variable [fichier d’attributs du client](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=fr) vous avez fourni via CRS.

## Profil fusionné

Vous pouvez combiner des `tntId`, `thirdPartyID`, et `marketingCloudVisitorId` dans la même requête. Dans ce scénario, Adobe Target conserve le mappage de tous ces identifiants et les épingle à un visiteur. Découvrez comment les profils [fusionné et synchronisé en temps réel](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) en utilisant les différents identifiants.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
      "id": {
        "marketingCloudVisitorId" : "2304820394812039",
        "tntId": "d359234570e044f14e1faeeba02d6ab23439914e.28_78",
        "thirdPartyId":"23423432"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
        }
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

L’exemple d’appel ci-dessus montre comment combiner des `tntId`, `thirdPartyID`, et `marketingCloudVisitorId` dans la même requête. Les trois identifiants sont également renvoyés dans la réponse.
