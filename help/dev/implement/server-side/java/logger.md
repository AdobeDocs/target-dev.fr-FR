---
title: Initialisez le SDK Java  [!DNL Adobe Target]  consigner les requêtes.
description: Découvrez comment consigner les requêtes dans le SDK Java [!DNL Adobe Target] .
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
TQID: https://experienceleague.adobe.com/xvduuV6cjVJu-yIoaxCvbPE-ZttfEViuM8B7sVczAC0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 4%

---

# Enregistreur (Java)

## Description

Lors de l’initialisation [du SDK](initialize-sdk.md), plusieurs options s’offrent à vous sur l’objet `ClientConfig`, qui peut être défini pour consigner les requêtes.

| Option | Description |
| --- | --- |
| `logRequests` | Consigne l’ensemble du corps de la requête ainsi que le corps de la réponse. |
| `logRequestStatus` | Enregistre l’URL de la requête, le statut et le temps de réponse. |

[!DNL Target] Java SDK utilise la journalisation `slf4j`. Vous devez fournir votre implémentation de l’enregistreur, telle que `java.util.logging`, `logback` et `log4j`. Pour plus d&#39;informations, voir [&#128279;](https://www.slf4j.org/manual.html). Tous les journaux seront imprimés en `debug`.

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
