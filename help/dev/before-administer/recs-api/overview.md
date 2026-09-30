---
title: Qu’est-ce que l’API Adobe Recommendations ?
description: Ce guide explique aux développeurs la pratique de l’utilisation des API Recommendations d’Adobe Target pour configurer et gérer les catalogues de recommandations et les critères personnalisés, ainsi que l’utilisation de l’API de diffusion pour récupérer le contenu des recommandations.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail:
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
TQID: 'https://experienceleague.adobe.com/-bWsxWNZK7LXp0VvKZmsZc68jXcit57v7Wki9hR3wH4'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
  - id: f69bc5f1-ebdb-4306-a281-f2e77daf734c
    internal-label: Activities and tests
subfeature_v2:
  - id: ed58f4a1-16eb-4c8c-b505-be9da766a9ec
    internal-label: Recommendations
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 3%
---
# Présentation de l’API Adobe Recommendations

Les API pertinentes pour Recommendations incluent les [API d’administration](../../before-administer/target-api-overview.md) qui vous permettent d’effectuer les opérations suivantes :

* Gérer votre catalogue de produits ou de contenu recommandés
* Gestion des algorithmes et des activités Recommendations

À l’aide de l’[API de diffusion](../../implement/delivery-api/overview.md) Target avec Recommendations, vous pouvez également :

* Récupérez les recommandations dans les objets JSON, HTML ou XML afin qu’elles puissent être affichées sur le web, les appareils mobiles, les e-mails, l’Internet des objets (IOT) et d’autres canaux.

## Description

Ce guide relatif aux API Recommendations explique aux développeurs la pratique de l’utilisation des API Recommendations pour configurer et gérer les catalogues de recommandations et les critères personnalisés, ainsi que l’utilisation de l’API de diffusion pour récupérer le contenu des recommandations. À la fin, vous pourrez :

* Configuration et gestion des entités à l’aide de l’API Recommendations
* Configurer et gérer des critères personnalisés à l’aide de l’API Recommendations
* Découvrez comment utiliser Recommendations avec l’API de diffusion pour utiliser les résultats des recommandations sur les appareils non HTML

## Audience

Ce guide est destiné aux développeurs qui découvrent les API Target ou Recommendations.

## Conditions préalables {#prerequisites}

Les API d’administration Target nécessitent la configuration de l’authentification [](../configure-authentication.md). Assurez-vous que cette configuration est terminée avant d’utiliser l’API Recommendations.

## Ressources

Notez les ressources suivantes, qui sont nécessaires pour comprendre ce guide et le suivre avec succès :

| Ressource | Détails |
| --- | --- |
| Postman | Obtenez l&#39;application [](https://www.postman.com/downloads/) pour votre système d&#39;exploitation. Postman basic est gratuit avec la création de compte. Bien que cela ne soit pas nécessaire pour utiliser les API Adobe Target en général, Postman facilite les workflows d’API et Adobe Target fournit plusieurs collections Postman pour l’aider à exécuter ses API et à apprendre à les utiliser. Le reste de ce guide suppose une connaissance pratique de Postman. Pour obtenir de l’aide, consultez la documentation de [](https://learning.getpostman.com/). |
| Références | Tout au long du reste de ce guide, les ressources suivantes doivent être connues :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation de l’API Target Admin et Profile](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentation de l’API Recommendations](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
