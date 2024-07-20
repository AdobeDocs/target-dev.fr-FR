---
title: Mise en oeuvre de la configuration du proxy dans le kit SDK  [!DNL Adobe Target] Node.js
description: Découvrez comment configurer la configuration du proxy [!UICONTROL TargetClient] dans le kit SDK  [!DNL Adobe Target] Node.js.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Configuration du proxy (Node.js)

Pour configurer un proxy pour les requêtes HTTP du SDK Node, remplacez l’API de récupération utilisée par le SDK lors de l’initialisation.

Voici un exemple de base montrant comment remplacer `fetchApi` lors de l’initialisation de `TargetClient` pour ajouter un proxy :

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

Notez que cela ne fonctionne que pour Node versions 18.2+, dans laquelle `undici.fetch` est le `fetch` par défaut pour le noeud.
Veuillez consulter le [référentiel d’exemples de SDK de noeud](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
pour obtenir des exemples de configuration de proxy pour les anciennes versions du noeud et plus d’informations.
