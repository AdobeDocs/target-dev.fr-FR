---
title: Initialisez le SDK Java  [!DNL Adobe Target]  consigner les requêtes.
description: Découvrez comment consigner les requêtes dans le SDK Java [!DNL Adobe Target] .
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 4%

---

# Enregistreur (Java)

## Description

Lors de l’initialisation [du SDK](initialize-sdk.md), plusieurs options s’offrent à vous sur l’objet `ClientConfig`, qui peut être défini pour consigner les requêtes.

| Option | Description |
| --- | --- |
| `logRequests` | Consigne l’ensemble du corps de la requête ainsi que le corps de la réponse. |
| `logRequestStatus` | Enregistre l’URL de la requête, le statut et le temps de réponse. |

[!DNL Target] Java SDK utilise la journalisation `slf4j`. Vous devez fournir votre implémentation de l’enregistreur, telle que `java.util.logging`, `logback` et `log4j`. Pour plus d&#39;informations, voir [https://www.slf4j.org/manual.html](https://www.slf4j.org/manual.html). Tous les journaux seront imprimés en `debug`.

## Exemple

Ajoutez la dépendance `slf4j` .

>[!BEGINTABS]

>[!TAB Gradle ]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB  Maven ]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

Activez les journaux `DEBUG` en fonction de votre implémentation et marquez les indicateurs de journalisation des demandes.

### Debug

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

Vous devriez voir les requêtes, les réponses et les temps de réponse imprimés dans la console.
