---
title: Implémentez la configuration du proxy dans le SDK Node.js [!DNL Adobe Target]
description: Découvrez comment configurer la configuration du proxy [!UICONTROL TargetClient] dans le SDK Node.js [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
TQID: 'https://experienceleague.adobe.com/kaE-ZEOTteaVp5kWSHiVYCvEiHuQHSMqeWRq6r-mJaA'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '100'
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
Consultez le référentiel d’exemples [Node SDK).](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
pour obtenir des exemples de configuration du proxy pour des versions plus anciennes du nœud et plus d’informations.
