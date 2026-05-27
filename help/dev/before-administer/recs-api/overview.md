---
title: Qu’est-ce que l’API Adobe Recommendations ?
description: Ce guide explique aux développeurs la pratique de l’utilisation des API Recommendations d’Adobe Target pour configurer et gérer les catalogues de recommandations et les critères personnalisés, ainsi que l’utilisation de l’API de diffusion pour récupérer le contenu des recommandations.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
TQID: https://experienceleague.adobe.com/-bWsxWNZK7LXp0VvKZmsZc68jXcit57v7Wki9hR3wH4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 343
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

Les API d’administration Target nécessitent la configuration de l’authentification [&#128279;](../configure-authentication.md). Assurez-vous que cette configuration est terminée avant d’utiliser l’API Recommendations.

## Ressources

Notez les ressources suivantes, qui sont nécessaires pour comprendre ce guide et le suivre avec succès :

| Ressource | Détails |
| --- | --- |
| Postman | Obtenez l&#39;application [&#128279;](https://www.postman.com/downloads/) pour votre système d&#39;exploitation. Postman basic est gratuit avec la création de compte. Bien que cela ne soit pas nécessaire pour utiliser les API Adobe Target en général, Postman facilite les workflows d’API et Adobe Target fournit plusieurs collections Postman pour l’aider à exécuter ses API et à apprendre à les utiliser. Le reste de ce guide suppose une connaissance pratique de Postman. Pour obtenir de l’aide, consultez la documentation de [&#128279;](https://learning.getpostman.com/). |
| Références | Tout au long du reste de ce guide, les ressources suivantes doivent être connues :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation de l’API Target Admin et Profile](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentation de l’API Recommendations](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
