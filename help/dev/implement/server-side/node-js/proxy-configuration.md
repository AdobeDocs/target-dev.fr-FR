---
title: Implémenter la configuration du proxy dans le SDK  [!DNL Adobe Target] Node.js
description: Découvrez comment configurer la configuration du proxy [!UICONTROL TargetClient] dans le SDK  [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
TQID: https://experienceleague.adobe.com/kaE-ZEOTteaVp5kWSHiVYCvEiHuQHSMqeWRq6r-mJaA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 84
ht-degree: 0%

---

# Configuration du proxy (Node.js)

Pour configurer un proxy pour les requêtes HTTP Node SDK, remplacez l’API de récupération utilisée par SDK lors de l’initialisation.

Voici un exemple de base montrant comment remplacer `fetchApi` pendant l’initialisation du `TargetClient` pour ajouter un proxy :

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

Notez que cela ne fonctionne que pour les versions de nœud 18.2+, dans lesquelles `undici.fetch` est la `fetch` par défaut pour le nœud .
Consultez le référentiel d’exemples [Node SDK](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
pour obtenir des exemples de configuration du proxy pour des versions plus anciennes du nœud et plus d’informations.
