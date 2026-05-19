---
title: Implémenter la configuration du proxy dans le SDK  [!DNL Adobe Target]  Java
description: Découvrez comment configurer la configuration du proxy TargetClient dans le SDK Java [!DNL Adobe Target] .
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
TQID: https://experienceleague.adobe.com/Vo8KrM-3AGIvoO-E-iAQcAPqzXE24BM30LX7ji5E2Nk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 2%

---

# Configuration Du Proxy (Java)

## Proxy de base

Si l’application exécutant SDK nécessite un proxy pour accéder à Internet, le `TargetClient` doit être configuré avec une configuration de proxy comme suit.

### Configuration de proxy de base

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Authentification

Si une authentification proxy est requise, les informations d’identification peuvent être transmises en tant que paramètres au constructeur `ClientProxyConfig`, comme indiqué dans l’exemple ci-dessous. Notez que cela ne fonctionne que pour une authentification simple par nom d’utilisateur/mot de passe proxy.

### Authentification de base du proxy

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Prise de décision sur l’appareil

Pour les requêtes de récupération de l’artefact de règles, votre proxy doit être configuré pour ne pas mettre la réponse en cache. Cependant, s’il n’est pas possible de configurer le mécanisme de mise en cache du proxy pour cette requête, utilisez une option de configuration comme solution de contournement pour contourner le cache au niveau du proxy. Cette solution de contournement ajoute l’en-tête `Authorization` avec une valeur de chaîne vide à la requête de règles, qui doit indiquer au proxy que la réponse ne doit pas être mise en cache.

Pour activer cette solution de contournement, définissez les éléments suivants :

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


