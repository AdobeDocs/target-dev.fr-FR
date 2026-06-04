---
title: Indications du client de l’API de diffusion Adobe Target
description: Comment utiliser les Client Hints dans l’API  [!DNL Adobe Target]  diffusion ?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/ijbOsWitZdNHpjNduh8xtPyEYdw2tsWz2rB6jZ5JbQA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094id: ff2b9b37-92e0-45fc-b853-379d44c08c89
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 282
ht-degree: 0%

---

# Client Hints et [!UICONTROL API de diffusion ]

Les Client Hints doivent être envoyés à [!DNL Adobe Target] lors de la demande d’offres.

En règle générale, il est recommandé d’envoyer tous les Client Hints disponibles à [!DNL Target]. Pour plus d’informations, voir [User-agent et Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) dans la section [Implémentation côté client](../../implement/client-side/overview.md).

## Appels directs à l’API de diffusion

### À partir du navigateur

Dans ce cas, le navigateur envoie automatiquement des Client Hints à faible entropie à [!DNL Target] via des en-têtes de requête. Cette implémentation présente toutefois quelques limites au niveau du navigateur. Tout d’abord, aucun en-tête Client Hints ne sera envoyé à partir du navigateur, sauf si la requête est effectuée via https. Deuxième : les Client Hints ne seront pas envoyés lors de la première demande de [!DNL Target] sur la page. Les en-têtes de Client Hints ne seront envoyés que lors de la deuxième requête et toutes les requêtes suivantes. Cela signifie que la segmentation et la personnalisation de l’audience ne peuvent pas être effectuées par [!DNL Target] lors de la première visite de la page. Pour contourner ces deux limitations, il est vivement recommandé d’utiliser l’API User Agent Client Hints dans le navigateur pour collecter directement les Client Hints et les envoyer sur la payload de la requête.

### À partir d’un serveur

Dans ce cas, les Client Hints doivent être transférés manuellement du navigateur à [!DNL Target] sur la requête de l’API de diffusion.

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## Formatage

Les en-têtes Sec-CH-UA et Sec-CH-UA-Full-Version-List de Client Hints ont un format différent de celui des résultats de l’API du navigateur de Client Hints (navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). Ces deux formats sont acceptés par l’API de diffusion. L’API de diffusion normalisera les valeurs au format utilisé dans les en-têtes de requête, ce qui est important de garder à l’esprit lors de l’accès aux Client Hints dans les scripts de profil.
