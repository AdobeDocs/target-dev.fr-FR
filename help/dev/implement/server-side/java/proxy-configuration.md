---
title: Mettez en oeuvre la configuration du proxy dans la variable [!DNL Adobe Target] SDK Java
description: Découvrez comment configurer la configuration du proxy TargetClient dans le [!DNL Adobe Target] SDK Java.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: 59ab3f53e2efcbb9f7b1b2073060bbd6a173e380
workflow-type: tm+mt
source-wordcount: '170'
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

## Prise de décision sur l’appareil

Pour les requêtes de récupération de l’artefact de règles, votre proxy doit être configuré pour ne pas mettre en cache la réponse. Cependant, s’il n’est pas possible de configurer le mécanisme de mise en cache du proxy pour cette requête, utilisez une option de configuration comme solution pour contourner le cache au niveau du proxy. Cette solution ajoute la méthode `Authorization` en-tête avec une valeur de chaîne vide pour la requête de règles, qui doit indiquer au proxy que la réponse ne doit pas être mise en cache.

Pour activer cette solution, définissez les options suivantes :

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


