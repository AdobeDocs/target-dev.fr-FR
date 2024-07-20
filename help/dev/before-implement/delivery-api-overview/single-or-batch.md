---
title: API de diffusion Adobe Target Diffusion unique ou par lots
description: Comment utiliser les appels de [!UICONTROL Adobe Target Delivery API] de diffusion unique ou par lots ?
keywords: api de diffusion
exl-id: 525cd1f2-616a-486c-8f49-8117615500bb
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Diffusion unique ou par lots

[!UICONTROL Adobe Target Delivery API] prend en charge un appel de remise unique ou par lots. Vous pouvez envoyer une requête de serveur pour du contenu pour une ou plusieurs mbox.

Pesez les coûts de performance lorsque vous décidez d’effectuer un appel unique par rapport à un appel par lot. Si vous connaissez tout le contenu qui doit être affiché pour un utilisateur, la bonne pratique consiste à récupérer le contenu de toutes les mbox avec un seul appel de diffusion par lot, afin d’éviter d’effectuer plusieurs appels de diffusion uniques.

## Appel de diffusion unique

Vous pouvez récupérer une expérience à afficher à l’utilisateur pour une mbox via [!UICONTROL Adobe Target Delivery API]. Notez que si vous effectuez un seul appel de diffusion, vous devez lancer un autre appel de serveur pour récupérer du contenu supplémentaire pour une mbox pour un utilisateur. Cela peut devenir très coûteux au fil du temps. Par conséquent, veillez à évaluer votre approche lors de l’utilisation d’un seul appel de l’API de diffusion.

```
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

Dans l’exemple d’appel de diffusion unique ci-dessus, l’expérience est récupérée pour s’afficher pour l’utilisateur avec `tntId`: `abcdefghijkl00023.1_1` pour un `mbox`:`SummerOffer` sur le canal web. Cet appel de diffusion unique génère la réponse suivante :

```
{
  "status": 200,
  "requestId": "25e0cc42-3d7b-456a-8b49-af60c1fb23d9",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.1_1"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
    }
}
```

Dans la réponse, notez que le champ `content` contient l’HTML qui décrit l’expérience à présenter à l’utilisateur pour le web qui correspond à la mbox SummerOffer.

### Exécuter le chargement de page

Si des expériences doivent être affichées lorsqu’un chargement de page se produit dans le canal web, par exemple un test A/B des polices situées dans le pied de page ou l’en-tête, vous pouvez spécifier `pageLoad` dans le champ `execute` pour récupérer toutes les modifications à appliquer.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
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
  "execute": {
    "pageLoad": {}
  }
}'
```

L’exemple d’appel ci-dessus récupère toutes les expériences pour afficher un utilisateur lors du chargement de la page `https://target.enablementadobe.com/react/demo/#/`.

```
{
      "status": 200,
      "requestId": "355ebc47-edb6-481f-aeae-ae55d71afaca",
      "client": "demo",
      "id": {
          "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
      },
      "edgeHost": "mboxedge28.tt.omtrdc.net",
      "execute": {
          "pageLoad": {
              "options": [
                  {
                      "content": [
                          {
                              "type": "setHtml",
                              "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV.nav:eq(0) > DIV.container:eq(0) > DIV.nav-right:eq(0) > A.nav-item:eq(0)",
                              "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > A:nth-of-type(1)",
                              "content": "Modified Home"
                          }
                      ],
                      "type": "actions"
                  }
              ],
              "metrics": [
                  {
                      "type": "click",
                      "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV.form-group:eq(0) > BUTTON.btn:eq(0)",
                      "eventToken": "QPaLjCeI9qKCBUylkRQKBg=="
                  }
              ]
          }
      }
  }
```

Dans le champ `content` , la modification qui doit être appliquée au chargement d’une page peut être récupérée. Dans l’exemple ci-dessus, notez qu’un lien sur l’en-tête doit être nommé *Modified Home*.

## Appel de diffusion mise en cache

Au lieu d’effectuer plusieurs appels de diffusion avec une seule mbox dans chaque appel, effectuer un appel de diffusion avec un lot de mbox peut réduire les appels de serveur inutiles. Pour être hautement performant, l’appel d’un appel au serveur doit être minimal autant que possible.

```
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
    "execute": {
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

Dans l’exemple d’appel de diffusion par lot ci-dessus, les expériences sont récupérées pour s’afficher pour l’utilisateur avec `tntId`: `abcdefghijkl00023.1_1` pour plusieurs `mbox`:`SummerOffer`, `SummerShoesOffer` et `SummerDressOffer`. Puisque nous savons que nous devons présenter une expérience pour plusieurs mbox pour cet utilisateur, nous pouvons traiter ces requêtes par lots et effectuer un appel au serveur au lieu de trois appels de diffusion individuels.

```
{
  "status": 200,
  "requestId": "fe15286f-effb-434f-85d8-c3db804075ce",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_120"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",

                  }
              ]
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

Dans la réponse ci-dessus, vous pouvez constater que dans le champ `content` de chaque mbox, la représentation par HTML de l’expérience à afficher à l’utilisateur pour chaque mbox peut être récupérée.
