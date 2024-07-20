---
title: Initialisation du kit SDK Java  [!DNL Adobe Target]  pour consigner les requêtes
description: Découvrez comment consigner des requêtes dans le kit SDK Java [!DNL Adobe Target] .
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 4%

---

# Enregistreur (Java)

## Description

Lorsque [ initialise le SDK ](initialize-sdk.md), il existe plusieurs options sur l’objet `ClientConfig`, qui peuvent être définies pour consigner des requêtes.

| Option | Description |
| --- | --- |
| `logRequests` | Consigne tout le corps de la requête ainsi que le corps de la réponse. |
| `logRequestStatus` | Consigne l’URL de la requête, l’état ainsi que le temps de réponse. |

[!DNL Target] Le SDK Java utilise la journalisation `slf4j`. Vous devez fournir votre mise en oeuvre d’un journal tel que `java.util.logging`, `logback` et `log4j`. Pour plus d’informations, voir [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) . Tous les journaux seront imprimés dans `debug`.

## Exemple

Ajoutez la dépendance `slf4j`.

>[!BEGINTABS]

>[!TAB Gradle]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

Activez les journaux `DEBUG` en fonction de votre mise en oeuvre et marquez les indicateurs de journalisation de la requête.

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

Les requêtes, réponses et temps de réponse doivent être imprimés dans la console.
