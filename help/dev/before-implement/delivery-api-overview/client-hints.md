---
title: Conseils sur le client de l’API de diffusion Adobe Target
description: Comment utiliser les conseils aux clients dans l'API de diffusion  [!DNL Adobe Target] ?
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Conseils au client et [!UICONTROL Adobe Target Delivery API]

Les conseils client doivent être envoyés à [!DNL Adobe Target] sur la demande d’offres.

En règle générale, il est recommandé d&#39;envoyer tous les conseils client disponibles à [!DNL Target]. Pour plus d’informations, voir [User-agent and Client Hints](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md) dans la section [Mise en oeuvre côté client](../../implement/client-side/overview.md) .

## Appels directs de l’API de diffusion

### À partir du navigateur

Dans ce cas, le navigateur enverra automatiquement des conseils à la clientèle à faible entropie vers [!DNL Target] via des en-têtes de requête. Cette mise en oeuvre présente toutefois quelques limites au niveau du navigateur. Tout d’abord, aucun en-tête de conseils client ne sera envoyé à partir du navigateur, sauf si la demande est effectuée via https. Deuxièmement : les conseils client ne seront pas envoyés à la première requête vers [!DNL Target] sur la page. Les en-têtes de conseils client ne sont envoyés que lors de la deuxième requête et toutes les requêtes suivantes. Cela signifie que la segmentation et la personnalisation de l’audience ne peuvent pas être effectuées par [!DNL Target] lors de la première visite de la page. Pour contourner ces deux restrictions, nous vous recommandons vivement d’utiliser l’API User Agent Client Hints dans le navigateur afin de collecter directement les conseils client et de les envoyer sur la payload de la requête.

### Depuis un serveur

Dans ce cas, les conseils client doivent être transférés manuellement du navigateur vers [!DNL Target] à la demande d’API de diffusion.

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

Les en-têtes Sec-CH-UA et Sec-CH-UA-Full-Version-List des conseils client ont un format différent des résultats de l’API du navigateur de conseils client (navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues). Ces deux formats sont acceptés par l&#39;API de diffusion. L’API de diffusion normalise les valeurs au format utilisé dans les en-têtes de requête, ce qui est important à garder à l’esprit lors de l’accès aux conseils du client dans les scripts de profil.
