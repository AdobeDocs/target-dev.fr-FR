---
title: Prérécupération de l’API de diffusion Adobe Target
description: Comment utiliser la prérécupération dans [!UICONTROL Adobe Target Delivery API] ?
keywords: api de diffusion
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 4ff2746b8b485fe3d845337f06b5b0c1c8d411ad
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# Prérécupération

La prérécupération permet aux clients tels que les applications mobiles et les serveurs de récupérer du contenu pour plusieurs mbox ou vues dans une requête, de le mettre en cache localement et par la suite de notifier [!DNL Target] lorsque le visiteur visite ces mbox ou vues.

Lors de l’utilisation de la prérécupération, il est important de connaître les termes suivants :

| Nom du champ | Description |
| --- | --- |
| `prefetch` | Liste des mbox et des vues qui doivent être récupérées, mais qui ne doivent pas être marquées comme visitées. L’Edge [!DNL Target] renvoie un `eventToken` pour chaque mbox ou vue existant dans le tableau de prérécupération. |
| `notifications` | Liste des mbox et des vues précédemment prérécupérées et qui doivent être marquées comme visitées. |
| `eventToken` | Jeton chiffré haché renvoyé lors de la prérécupération du contenu. Ce jeton doit être renvoyé à [!DNL Target] dans le tableau `notifications`. |

## Prérécupération des mbox

Les clients, tels que les applications mobiles et les serveurs, peuvent prérécupérer plusieurs mbox pour un visiteur donné au cours d’une session et les mettre en cache afin d’éviter plusieurs appels vers le [!UICONTROL Adobe Target Delivery API].

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

Dans le champ `prefetch` , ajoutez un ou plusieurs `mboxes` que vous souhaitez prérécupérer au moins une fois pour un visiteur au cours d’une session. Après avoir prérécupéré pour ces `mboxes`, vous recevez la réponse suivante :

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

Dans la réponse, vous voyez le champ `content` contenant l’expérience à présenter au visiteur pour un `mbox` particulier. Cela s’avère très utile lorsqu’il est mis en cache sur votre serveur, de sorte que lorsqu’un visiteur interagit avec votre application web ou mobile au cours d’une session et visite un `mbox` sur une page spécifique de votre application, l’expérience peut être diffusée à partir du cache au lieu d’effectuer un autre appel [!UICONTROL Adobe Target Delivery API]. Cependant, lorsqu’une expérience est fournie au visiteur à partir de `mbox`, un `notification` est envoyé via un appel API de diffusion pour que la journalisation des impressions se produise. En effet, la réponse des appels `prefetch` est mise en cache, ce qui signifie que le visiteur n’a pas vu les expériences au moment de l’appel `prefetch`. Pour en savoir plus sur le processus `notification`, voir [Notifications](notifications.md).

## Prérécupération des mbox avec des mesures `clickTrack` lors de l’utilisation de [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics for Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr){target=_blank} (A4T) est une intégration intersolutions qui vous permet de créer des activités basées sur [!DNL Analytics] mesures de conversion et segments d’audience.

Le fragment de code suivant est une réponse d’une prérécupération d’une mbox contenant des mesures `clickTrack` pour informer [!DNL Analytics] qu’un utilisateur a cliqué sur une offre :

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
>La prérécupération d’une mbox contient la charge utile [!DNL Analytics] pour les activités qualifiées uniquement. La prérécupération des mesures de succès pour les activités non encore qualifiées entraîne des incohérences dans les rapports.

## Prérécupération des vues

Les vues prennent en charge les applications d’une seule page (SPA) et les applications mobiles de manière plus transparente. Les vues peuvent être considérées comme un groupe logique d’éléments visuels qui, ensemble, constituent une expérience SPA ou mobile. Désormais, grâce à l’API de diffusion, les activités [[!UICONTROL A/B Test]](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=fr){target=_blank} et [[!UICONTROL Experience Targeting]](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html?lang=fr){target=_blank} (X)T créées par le VEC avec des modifications sur les [vues pour SPA](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) peuvent être prérécupérées.

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

L’exemple d’appel ci-dessus prérécupère toutes les vues créées via le SPA VEC pour [!UICONTROL A/B Test] et les activités XT à afficher pour le web `channel`. Notez que l’appel prérécupère toutes les vues des activités [!UICONTROL A/B Test] ou XT auxquelles un visiteur avec `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` qui visite `url`:`https://target.enablementadobe.com/react/demo/#/` est admissible.

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

Dans les champs `content` de la réponse, notez les métadonnées telles que `type`, `selector`, `cssSelector` et `content`, qui sont utilisées pour rendre l’expérience à votre visiteur lorsqu’un utilisateur visite votre page. Notez que le contenu `prefetched` peut être mis en cache et rendu à l’utilisateur si nécessaire.
