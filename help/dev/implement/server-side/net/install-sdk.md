---
title: Installation du SDK .NET
description: Découvrez comment installer le [!DNL Adobe Target] SDK .NET.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Installation du SDK .NET

Le SDK .NET est distribué par [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). Pour commencer, ajoutez-la en tant que dépendance en installant via `Package Manage` ou `.NET CLI`:

## Gestionnaire de modules

>[!BEGINTABS]

>[!TAB Gestionnaire de modules]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB CLI .NET]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

Le code open source se trouve à l’adresse [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
