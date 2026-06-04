---
title: Prérécupération de l’API de diffusion Adobe Target
description: Comment utiliser la prérécupération dans l’API de diffusion [!UICONTROL Adobe Target &#x200B;] ?
keywords: API de diffusion
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/gthn2vJrIjEkmQdpsf4J818OrzFiLpeRvXXRAUp2SiY
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c18d9e03-ac7d-4811-9c92-3e92ddc70ade
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 578
ht-degree: 0%

---

# Prérécupération

La prérécupération permet aux clients tels que les applications mobiles et les serveurs de récupérer du contenu pour plusieurs mbox ou vues en une seule requête, de le mettre en cache localement et de [!DNL Target] informer ultérieurement lorsque le visiteur visite ces mbox ou vues.

Lors de l’utilisation de la prérécupération, il est important de connaître les termes suivants :

| Nom du champ | Description |
| --- | --- |
| `prefetch` | Liste des mbox et des vues qui doivent être récupérées, mais ne doivent pas être marquées comme visitées. L’Edge [!DNL Target] renvoie un `eventToken` pour chaque mbox ou vue existant dans le tableau de prérécupération. |
| `notifications` | Liste des mbox et des vues qui ont été précédemment prérécupérées et qui doivent être marquées comme visitées. |
| `eventToken` | Jeton chiffré haché renvoyé lorsque le contenu est prérécupéré. Ce jeton doit être renvoyé à [!DNL Target] dans le tableau `notifications`. |

## Prérécupération des mbox

Les clients, tels que les applications mobiles et les serveurs, peuvent prérécupérer plusieurs mbox pour un visiteur donné au cours d’une session et les mettre en cache pour éviter plusieurs appels à l’API de diffusion .

```shell shell-session
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
  "id": {
    "tntId": "abcdefghijkl00023.1_1"
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
    "prefetch": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
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

Dans le champ `prefetch` , ajoutez une ou plusieurs `mboxes` que vous souhaitez prérécupérer au moins une fois pour un visiteur au cours d’une session. Après la prérécupération de ces `mboxes`, vous recevez la réponse suivante :

```JSON {line-numbers="true"}
{
    "status": 200,
    "requestId": "5efee0d8-3779-4b12-a74e-e04848faf191",
    "client": "demo",
    "id": {
        "tntId": "abcdefghijkl00023.1_1"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "mboxes": [
            {
                "index": 1,
                "name": "SummerOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            }
        ]
    }
}
```

Dans la réponse, vous voyez le champ `content` contenant l’expérience à afficher au visiteur pour une `mbox` particulière. Cette méthode est très utile lorsque vous la mettez en cache sur votre serveur. Ainsi, lorsqu’un visiteur interagit avec votre application web ou mobile au cours d’une session et visite une `mbox` sur une page particulière de votre application, l’expérience peut être diffusée à partir du cache au lieu d’effectuer un autre appel de l’API de diffusion Adobe Target. Cependant, lorsqu’une expérience est diffusée au visiteur à partir du `mbox`, un `notification` est envoyé via un appel d’API de diffusion pour que la journalisation des impressions se produise. Cela est dû au fait que la réponse des appels `prefetch` est mise en cache, ce qui signifie que le visiteur n’a pas vu les expériences au moment où l’appel `prefetch` se produit. Pour en savoir plus sur le processus de `notification`, voir [Notifications](notifications.md).

## Prérécupération des mbox avec des mesures `clickTrack` lors de l’utilisation d’[!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics for Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html){target=_blank} (A4T) est une intégration intersolutions qui vous permet de créer des activités basées sur des mesures de conversion [!DNL Analytics] et des segments d’audience.

Le fragment de code suivant est une réponse d’une prérécupération d’une mbox contenant des mesures `clickTrack` pour [!DNL Analytics] informer qu’un utilisateur a cliqué sur une offre :

```JSON {line-numbers="true"}
{
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "<mboxName>",
        "options": [
           ...
        ],
        "metrics": [
          {
            "type": "click",
            "eventToken": "<eventToken>",
             "analytics": {
               "payload": {
                 "pe": "tnt",
                 "tnta": "..."
               }
             }
          },
          }
        ],
        "analytics": {
          "payload": {
            "pe": "tnt",
            "tnta": "347565:1:0|2,347565:1:0|1"
          }
        }
      }
    ]
  }
}
```

>[!NOTE]
>
>La prérécupération d’une mbox contient la payload [!DNL Analytics] pour les activités qualifiées uniquement. La prérécupération des mesures de succès pour les activités non encore qualifiées entraîne des incohérences dans les rapports.

## Prérécupération des vues

Les vues prennent en charge les applications sur une seule page (SPA) et les applications mobiles de manière plus transparente. Les vues peuvent être considérées comme un groupe logique d’éléments visuels qui, ensemble, constituent une SPA ou une expérience mobile. Désormais, grâce à l’API de diffusion, les activités [[!UICONTROL Test A/B]](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html){target=_blank} et [[!UICONTROL Ciblage d’expérience]](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html){target=_blank} (X)T créées par le VEC et comportant des modifications sur [Vues pour SPA](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) peuvent être prérécupérées.

```shell  {line-numbers="true"}
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=a3e7368c62d944c0855d424cd7a03ab0' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "prefetch": {
    "views": [{}]
  }
}'
```

L’exemple d’appel ci-dessus prérécupère toutes les vues créées par le biais du VEC SPA pour les activités [!UICONTROL Test A/B] et XT à afficher pour le `channel` web. Notez que l’appel prérécupère toutes les vues des activités [!UICONTROL Test A/B] ou XT pour lesquelles un visiteur avec `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` qui visite le `url`:`https://target.enablementadobe.com/react/demo/#/` est éligible.

```JSON  {line-numbers="true"}
{
    "status": 200,
    "requestId": "14ce028e-d2d2-4504-b3da-32740fa8dd61",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "views": [
            {
                "id": 228,
                "name": "checkout-express",
                "key": "checkout-express",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV:nth-of-type(1) > DIV.mb-3:eq(2)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > FORM:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(3)",
                                "content": "<span style=\"color:#000080;\"><strong>*We charge an additional fee of $12.34 for faster delivery. If you choose express delivery get 15% off on your next order.</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 5,
                "name": "home",
                "key": "home",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
                                "content": "<span style=\"color:#800000;\"><strong>Trending Items</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 6,
                "name": "products",
                "key": "products",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setStyle",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > DIV.heading:eq(0) > BUTTON.btn:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > BUTTON:nth-of-type(1)",
                                "content": {
                                    "background-color": "rgba(191,0,0,1)",
                                    "priority": "important"
                                }
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            }
        ]
    }
}
```

Dans les champs `content` de la réponse, notez les métadonnées telles que `type`, `selector`, `cssSelector` et `content`, qui sont utilisées pour effectuer le rendu de l’expérience pour votre visiteur lorsqu’un utilisateur visite votre page. Notez que le contenu `prefetched` peut être mis en cache et rendu à l’utilisateur ou à l’utilisatrice si nécessaire.
