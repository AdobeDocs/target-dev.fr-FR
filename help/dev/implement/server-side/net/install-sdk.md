---
title: Installation du SDK .NET
description: Découvrez comment installer le SDK  [!DNL Adobe Target] .NET.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
TQID: https://experienceleague.adobe.com/438ax3dEUclYIa42EvOLyBBuRngsZLHRDXabumxp0F8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 63
ht-degree: 9%

---

# Installation du SDK .NET

.NET SDK est distribué par [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). Pour commencer, ajoutez-le en tant que dépendance en installant via `Package Manage` ou `.NET CLI` :

## Gestionnaire de packages

>[!BEGINTABS]

>[!TAB Gestionnaire de packages]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB .NET CLI]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

Le code open source se trouve à l’adresse [](https://github.com/adobe/target-dotnet-sdk).
