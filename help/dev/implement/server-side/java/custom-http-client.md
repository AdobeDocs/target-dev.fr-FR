---
title: Découvrez comment configurer le client HTTP personnalisé
description: Découvrez comment configurer TargetClient à l’aide de ClientConfig.builder().httpClient().
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Configuration client HTTP personnalisée (Java)

Si l’application exécutant le SDK nécessite un client HTTP personnalisé, pour activer des fonctionnalités telles que la configuration SSL ou l’ajout d’en-têtes par défaut aux requêtes, le `TargetClient` devra être configuré à l’aide de `ClientConfig.builder().httpClient()` :

## Configuration de base du client HTTP

Le SDK prend actuellement en charge les clients HTTP qui implémentent l’interface `org.apache.http.client.HttpClient`.

### Mise en oeuvre de base

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Configuration client HTTP personnalisée avec configuration SSL

Voici un exemple de configuration du protocole SSL dans le `TargetClient` en personnalisant le `HttpClient` transmis dans le `ClientConfig`. Le fragment de code suivant utilise des classes du package `org.apache.http.conn.ssl` pour la configuration SSL.

### Implémentation SSL

```java {line-numbers="true"}
SSLContext context = SSLContextBuilder.create().build();
SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context);
CloseableHttpClient httpClient = HttpClients.custom().setSSLSocketFactory(sslSocketFactory).build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
