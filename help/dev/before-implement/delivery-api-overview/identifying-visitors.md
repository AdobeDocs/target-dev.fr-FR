---
title: API de diffusion Adobe Target Identification des visiteurs
description: Comment identifier un utilisateur dans  [!DNL Adobe Target] ?
keywords: API de diffusion
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/ciTxaPn8odyuyHzrnqhPWzdmpcU2bknOATGCt-ZtAZw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: f7c7de77-382f-4f48-8b36-61a170f06d3d
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 797
ht-degree: 9%

---

# Identification des visiteurs

Il existe plusieurs façons d’identifier un visiteur dans [!DNL Adobe Target].

Target utilise trois identifiants :

| Nom du champ | Description |
| --- | --- |
| `tntId` | L’`tntId` est l’identifiant principal dans [!DNL Target] pour un utilisateur. Vous pouvez fournir cet identifiant ou [!DNL Target] le générera automatiquement si la requête n’en contient pas. |
| `thirdPartyId` | Le `thirdPartyId` est l’identifiant de votre société pour l’utilisateur que vous pouvez envoyer à chaque appel. Lorsqu’un utilisateur se connecte au site d’une entreprise, l’entreprise crée généralement un identifiant lié au compte du visiteur, à la carte de fidélité, au numéro d’abonnement ou à d’autres identifiants applicables de cette entreprise. |
| `marketingCloudVisitorId` | Le `marketingCloudVisitorId` est utilisé pour fusionner et partager des données entre différentes solutions Adobe. Le `marketingCloudVisitorId` est requis pour les intégrations avec Adobe Analytics et Adobe Audience Manager. |
| `customerIds` | Outre l’identifiant visiteur Experience Cloud, il est possible d’utiliser des [ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) supplémentaires et un statut d’authentification pour chaque visiteur. |

## [!DNL Target] ID

L’ID [!DNL Target] ou le `tntId` peut être vu comme un ID d’appareil. Cette `tntId` est générée automatiquement par [!DNL Target] si elle n’est pas fournie dans la requête. Par la suite, les requêtes suivantes doivent inclure ce `tntId` pour que le contenu approprié soit diffusé sur un appareil utilisé par l’utilisateur ou l’utilisatrice.

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

L’exemple d’appel ci-dessus montre qu’un `tntId` n’a pas besoin d’être transmis. Dans ce scénario, [!DNL Target] génère un `tntId` et le fournit dans la réponse, comme illustré ici :

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

La `tntId` générée est `10abf6304b2714215b1fd39a870f01afc.28_20`. Notez que ce `tntId` doit être utilisé lors de l’appel de l’API de diffusion [!UICONTROL Adobe Target] pour le même utilisateur entre les sessions.

## Identifiant visiteur Marketing Cloud

Le `marketingCloudVisitorId` est un identifiant universel et persistant qui identifie vos visiteurs dans toutes les solutions Experience Cloud. Lorsque votre organisation met en œuvre le service d’ID, cet identifiant permet d’identifier un même visiteur et ses données dans différentes solutions Experience Cloud telles qu’Adobe Target, Adobe Analytics ou Adobe Audience Manager. Notez que la `marketingCloudVisitorId` est requise lors de l’utilisation et de l’intégration d’Analytics et d’Audience Manager.

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

L’exemple d’appel ci-dessus montre comment un `marketingCloudVisitorId` récupéré à partir du service Experience Cloud ID est transmis à Adobe Target. Dans ce scénario, [!DNL Target] génère un `tntId`, car il n’a pas été transmis à l’appel d’origine qui sera mappé au `marketingCloudVisitorId` fourni, comme illustré dans la réponse ci-dessous.

## ID tiers

Si votre organisation utilise un identifiant pour identifier votre visiteur, vous pouvez utiliser `thirdPartyID` pour diffuser du contenu. Cependant, vous devez fournir le `thirdPartyID` pour chaque appel de l’API de diffusion [!UICONTROL Adobe Target] que vous effectuez.

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

L’exemple d’appel ci-dessus montre un `thirdPartyId`, qui est un identifiant persistant que votre entreprise utilise pour identifier un utilisateur final, qu’il interagisse avec votre entreprise à partir de canaux web, mobiles ou IoT. En d’autres termes, le `thirdPartyId` référencera les données de profil utilisateur qui peuvent être utilisées sur plusieurs canaux. Dans ce scénario, [!DNL Target] génère un `tntId`, puisqu’il n’a pas été transmis à l’appel d’origine, qui sera mappé au `thirdPartyId` fourni, comme illustré dans la réponse ci-dessous.

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

[Les ID de client](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) peuvent être ajoutés et associés à un ID de visiteur Experience Cloud. Lors de l’envoi de `customerIds`, le `marketingCloudVisitorId` doit également être fourni. De plus, un statut d’authentification peut être fourni avec chaque `customerId` pour chaque visiteur. Le statut d’authentification suivant peut être pris en compte :

| État d’authentification | État d’utilisateur |
| --- | --- |
| `unknown` | Inconnu ou jamais authentifié. Cet état peut être utilisé dans des scénarios tels qu’un visiteur qui a atterri sur votre site en cliquant sur une publicité display. |
| `authenticated` | L’utilisateur est actuellement authentifié dans une session active sur votre site web ou votre application. |
| `logged_out` | L’utilisateur était authentifié, mais actuellement déconnecté. Celui-ci a eu l’intention de se déconnecter de l’état d’authentification. Il ne souhaite plus être considéré comme authentifié. |

Notez que ce n’est que lorsque l’ID de client est à l’état `authenticated` que Target référencera les données de profil utilisateur stockées et liées à l’ID de client. Si l’ID de client est à l’état `unknown` ou `logged_out`, il est ignoré et les données de profil utilisateur éventuellement associées ne sont pas utilisées pour le ciblage d’audience.

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

L’exemple d’appel ci-dessus montre comment envoyer un `customerId` avec un `authenticatedState`. Lors de l’envoi d’un `customerId`, les `integrationCode`, `id` et `authenticatedState` ainsi que les `marketingCloudVisitorId` sont requis. Le `integrationCode` est l’alias du fichier [attributs du client](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=fr) que vous avez fourni via CRS.

## Profil fusionné

Vous pouvez combiner `tntId`, `thirdPartyID` et `marketingCloudVisitorId` dans la même requête. Dans ce scénario, Adobe Target conserve le mappage de tous ces identifiants et les épingle à un visiteur. Découvrez comment les profils sont [fusionnés et synchronisés en temps réel](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) à l’aide des différents identifiants.

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

L’exemple d’appel ci-dessus montre comment combiner `tntId`, `thirdPartyID` et `marketingCloudVisitorId` dans la même requête. Les trois ID sont également renvoyés dans la réponse.
