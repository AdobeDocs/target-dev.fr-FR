---
title: Mettez en oeuvre la configuration du proxy dans la variable [!DNL Adobe Target] SDK Java
description: Découvrez comment configurer la configuration du proxy TargetClient dans le [!DNL Adobe Target] SDK Java.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 1%

---

# Configuration du proxy (Java)

## Proxy de base

Si l’application exécutant le SDK nécessite un proxy pour accéder à Internet, la variable `TargetClient` doit être configuré avec une configuration proxy comme suit.

### Configuration de base du proxy

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Authentification

Si une authentification proxy est requise, les informations d’identification peuvent être transmises en tant que paramètres à la variable `ClientProxyConfig` constructeur, selon l’exemple ci-dessous. Notez que cela ne fonctionne que pour une authentification par proxy simple nom d’utilisateur/mot de passe.

### Authentification de proxy de base

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
