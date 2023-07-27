---
title: Mettez en oeuvre la configuration du proxy dans la variable [!DNL Adobe Target] SDK Node.js
description: Découvrez comment configurer le [!UICONTROL TargetClient] configuration du proxy dans la [!DNL Adobe Target] SDK Node.js.
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Configuration du proxy (Node.js)

Pour configurer un proxy pour les requêtes HTTP du SDK Node, remplacez l’API de récupération utilisée par le SDK lors de l’initialisation.

Voici un exemple de base montrant comment remplacer `fetchApi` pendant la `TargetClient` initialisation pour ajouter un proxy :

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

Notez que cela ne fonctionne que pour les versions 18.2+ de Node dans lesquelles `undici.fetch` est la valeur par défaut `fetch` pour le noeud .
Veuillez consulter le [Référentiel d’exemples de SDK de noeud](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
pour obtenir des exemples de configuration de proxy pour les anciennes versions du noeud et plus d’informations.
