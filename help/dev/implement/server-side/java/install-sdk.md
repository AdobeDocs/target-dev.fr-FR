---
title: Installation de Java SDK
description: Découvrez comment installer le SDK Java  [!DNL Adobe Target] .
feature: APIs/SDKs
exl-id: 5828d5b3-c487-49bf-9458-7ef94374e32d
TQID: https://experienceleague.adobe.com/NJ8oBLe6fuxcU67YGBg8dFFg32YzBX2jB1HNFegcaGk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 51
ht-degree: 0%

---

# Installation de Java SDK

Le SDK Java est distribué par [Maven Central](https://search.maven.org/artifact/com.adobe.target/target-java-sdk). Pour commencer, ajoutez-le en tant que dépendance en l’installant dans `gradle` ou `maven` :

>[!BEGINTABS]

>[!TAB Gradle ]

```javascript {line-numbers="true"}
compile 'com.adobe.target:java-sdk:1.0'
```

>[!TAB  Maven ]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>2.0</version>
</dependency>
```

>[!ENDTABS]

Le code open source se trouve à l’adresse <https://github.com/adobe/target-java-sdk>.
