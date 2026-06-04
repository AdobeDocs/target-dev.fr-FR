---
title: Intégration avec Experience Cloud
description: Intégration avec Experience Cloud
keywords: API de diffusion
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 7%

---

<!-- The content on this page was originally pulled from the legacy Delivery API doc site, and was subsequently found to be an outdated version of information now found on [Implement > Server-side > Integration > A4T Reporting](../../implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md) and [Implement > Server-side > Integration > AAM Segments](../../implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md). Therefore sunsetting this page, but not deleting it from the repo immediately, pending a more thorough examination to avoid inadvertently deleting relevant content. -->


# Intégration avec Experience Cloud

## Adobe Analytics for Target (A4T)

Lorsqu’un appel de l’API Target Delivery est déclenché à partir du serveur, Adobe Target renvoie l’expérience de cet utilisateur et, en outre, Adobe Target renvoie la payload Adobe Analytics à l’appelant ou la transfère automatiquement à Adobe Analytics. Pour envoyer des informations sur l’activité de Target à Adobe Analytics côté serveur, certaines conditions préalables doivent être remplies :

1. L’activité est configurée dans l’interface utilisateur d’Adobe Target avec Adobe Analytics comme source des rapports et les comptes sont activés pour A4T
1. L’identifiant visiteur Adobe Marketing Cloud est généré par l’utilisateur de l’API et est disponible lorsque l’appel de l’API de diffusion Target est déclenché

### Adobe Target transfère automatiquement la payload Analytics

Adobe Target peut transférer automatiquement la payload d’analyse vers Adobe Analytics par le biais du serveur si les identifiants suivants sont fournis :

1. `supplementalDataId` - Identifiant utilisé pour regrouper Adobe Analytics et Adobe Target
1. `trackingServer` - Serveur Adobe Analytics Pour qu’Adobe Target et Adobe Analytics assemblent correctement les données, les mêmes `supplementalDataId` doivent être transmises à la fois à Adobe Target et à Adobe Analytics.

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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
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

### Récupération de la payload Analytics d’Adobe Target

Les clients de l’API de diffusion Adobe Target peuvent récupérer la payload Adobe Analytics pour une mbox correspondante afin qu’elle soit envoyée à Adobe Analytics via l’[API Data Insertion](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). Lorsqu’un appel Adobe Target côté serveur est déclenché, transmettez le `client_side` au champ `logging` dans la requête. Une payload est alors renvoyée si la mbox est présente dans une activité utilisant Analytics comme source de création de rapports.

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
      "experienceCloud": {
        "analytics": {
          "logging": "client_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          },
          {
            "name" : "SummerShoesOffer",
            "index" : 2       
          },
          {
            "name" : "SummerDressOffer",
            "index" : 3       
          }      
        ]
      }
    }'
```

Une fois que vous avez spécifié `logging` = `client_side`, vous recevrez la payload dans le champ `mbox` comme illustré ci-dessous.

```
{
    "status": 200,
    "requestId": "4b8855a5-8354-4ac4-8ae7-c551f7c0bb8a",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",

                    }
                ],
                "analytics": {
                    "payload": {
                        "pe": "tnt",
                        "tnta": "285408:0:0|2"
                    }
                }
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                        "type": "html",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                        "type": "html",
                    }
                ]
            }
        ]
    }
}
```

Si la réponse de Target contient des éléments dans la propriété `analytics` -> `payload` , transférez-la telle quelle à Adobe Analytics. Analytics sait comment traiter cette payload. Cette opération peut être effectuée dans une requête GET au format suivant :

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Paramètres et variables de chaîne de requête

| Nom du champ | Requis | Description |
| --- | --- | --- |
| `rsid` | Oui | Identifiant de la suite de rapports |
| `pe` | Oui | Événement de page. Toujours définie sur `tnt` |
| `tnta` | Oui | Payload Analytics renvoyée par le serveur Target dans `analytics` -> `payload` -> `tnta` |
| `mid` | Identifiant visiteur Marketing Cloud |  |

### Valeurs d’en-tête obligatoires

| Nom de l’en-tête | Valeur de l’en-tête |
| --- | --- |
| Hôte | Serveur de collecte de données Analytics (par exemple : adobeags421.sc.omtrdc.net) |

### Exemple d’appel HTTP Get à l’insertion de données A4T

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```

## Adobe Audience Manager

Les segments Adobe Audience Manager (AAM) peuvent également être utilisés via les API de diffusion Adobe Target. Pour exploiter les segments AAM, les champs suivants doivent être fournis :

| Nom du champ | Requis | Description |
| --- | --- | --- |
| `locationHint` | Oui | L’indicateur d’emplacement du serveur de collecte de données est utilisé pour déterminer le point d’entrée du serveur de collecte de données AAM à atteindre afin de récupérer le profil. Doit être >= 1. |
| `marketingCloudVisitorId` | Oui | Identifiant visiteur Marketing Cloud |
| `blob` | Oui | L’objet Blob d’AAM est utilisé pour envoyer des données supplémentaires à AAM. Ne doit pas être vide et la taille &lt;= 1024. |

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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "audienceManager": {
          "locationHint": 9,
          "blob": "32fdghkjh34kj5h43"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          },
          {
            "name" : "SummerShoesOffer",
            "index" : 2       
          },
          {
            "name" : "SummerDressOffer",
            "index" : 3       
          }      
        ]
      }
    }'
```
