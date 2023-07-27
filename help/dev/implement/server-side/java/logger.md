---
title: Initialisez la [!DNL Adobe Target] SDK Java pour consigner les requêtes
description: Découvrez comment consigner des requêtes dans le [!DNL Adobe Target] SDK Java.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# Enregistreur (Java)

## Description

When [initialisation du SDK](initialize-sdk.md), plusieurs options de la variable `ClientConfig` , qui peut être défini sur des requêtes de journal.

| Option | Description |
| --- | --- |
| `logRequests` | Consigne tout le corps de la requête ainsi que le corps de la réponse. |
| `logRequestStatus` | Consigne l’URL de la requête, l’état ainsi que le temps de réponse. |

[!DNL Target] Utilisation du SDK Java `slf4j` journalisation. Vous devez fournir votre implémentation de l’enregistreur, comme `java.util.logging`, `logback`, et `log4j`. Voir [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) pour plus d’informations. Tous les journaux seront imprimés dans `debug`.

## Exemple

Ajoutez la variable `slf4j` dépendance.

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

Activez la variable `DEBUG` se connectent en fonction de votre implémentation et marquent les indicateurs de journalisation des requêtes.

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
