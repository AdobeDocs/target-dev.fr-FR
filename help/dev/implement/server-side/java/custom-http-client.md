---
title: Découvrez comment configurer le client HTTP personnalisé
description: Découvrez comment configurer TargetClient à l’aide de ClientConfig.builder().httpClient().
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
TQID: https://experienceleague.adobe.com/SwijRIrhqSG4Mlij4sBH9Kx8tRB-6Bo7eyMoUZREOW8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 108
ht-degree: 0%

---

# Configuration personnalisée du client HTTP (Java)

Si l’application exécutant SDK nécessite un client HTTP personnalisé, pour activer des fonctionnalités telles que la configuration de SSL ou l’ajout d’en-têtes par défaut aux requêtes, le `TargetClient` doit être configuré à l’aide de `ClientConfig.builder().httpClient()` :

## Configuration de base d’un client HTTP personnalisé

Le SDK prend actuellement en charge les clients HTTP qui mettent en œuvre l’interface `org.apache.http.client.HttpClient`.

### Implémentation de base

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Configuration de client HTTP personnalisé avec configuration SSL

Voici un exemple de configuration de SSL dans le `TargetClient` en personnalisant les `HttpClient` transmises dans le `ClientConfig`. Le fragment de code suivant utilise des classes du package `org.apache.http.conn.ssl` pour la configuration SSL.

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
