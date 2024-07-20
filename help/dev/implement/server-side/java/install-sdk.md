---
title: Installation du SDK Java
description: Découvrez comment installer le  [!DNL Adobe Target] SDK Java.
feature: APIs/SDKs
exl-id: 5828d5b3-c487-49bf-9458-7ef94374e32d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Installation du SDK Java

Le SDK Java est distribué par [Maven Central](https://search.maven.org/artifact/com.adobe.target/target-java-sdk). Pour commencer, ajoutez-la en tant que dépendance en l’installant dans `gradle` ou `maven` :

>[!BEGINTABS]

>[!TAB Gradle]

```javascript {line-numbers="true"}
compile 'com.adobe.target:java-sdk:1.0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>2.0</version>
</dependency>
```

>[!ENDTABS]

Le code open source se trouve à l’adresse <https://github.com/adobe/target-java-sdk>.
