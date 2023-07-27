---
title: Qu’est-ce que l’API Adobe Recommendations ?
description: Ce guide permet aux développeurs de suivre des pratiques pratiques pratiques à l’aide des API Recommendations d’Adobe Target pour configurer et gérer des catalogues Recommendations et des critères personnalisés, ainsi que d’utiliser l’API de diffusion pour récupérer le contenu des recommandations.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# API Adobe Recommendations - Aperçu

Les API pertinentes pour Recommendations incluent [API d’administration](../../before-administer/target-api-overview.md) qui vous permettent d’effectuer les opérations suivantes :

* Gestion de votre catalogue de produits ou de contenu recommandables
* Gestion des algorithmes et activités Recommendations

Utilisation de Target [API de diffusion](../../implement/delivery-api/overview.md) avec Recommendations, vous pouvez également :

* Récupérez les recommandations dans les objets JSON, HTML ou XML afin qu’elles puissent être affichées sur le web, les appareils mobiles, les e-mails, l’Internet des objets (IOT) et sur d’autres canaux.

## Description

Ce guide concernant les API Recommendations guide les développeurs à travers les pratiques pratiques à l’aide des API Recommendations pour configurer et gérer des catalogues Recommendations et des critères personnalisés, ainsi que l’utilisation de l’API de diffusion pour récupérer le contenu des recommandations. D’ici la fin, vous pourrez :

* Configuration et gestion des entités à l’aide de l’API Recommendations
* Configuration et gestion de critères personnalisés à l’aide de l’API Recommendations
* Comprendre comment utiliser Recommendations avec l’API de diffusion pour utiliser les résultats de recommandations sur les périphériques non HTMLS

## Public

Ce guide est destiné aux développeurs qui découvrent les API de Target ou de Recommendations.

## Conditions préalables {#prerequisites}

Les API d’administration de Target requièrent [Configuration de l’authentification des Adobes](../configure-authentication.md). Assurez-vous d’avoir configuré cette configuration avant d’utiliser l’API Recommendations.

## Ressources

Notez les ressources suivantes, qui sont nécessaires pour comprendre ce guide et le suivre avec succès :

| Ressource | Détails |
| --- | --- |
| Postman | Obtenez la variable [application Postman](https://www.postman.com/downloads/) pour votre système d’exploitation. Postman basic est gratuit avec la création de compte. Bien qu’elles ne soient pas requises pour utiliser les API Adobe Target en général, Postman facilite les processus d’API et Adobe Target fournit plusieurs collections Postman pour aider à exécuter ses API et apprendre à les utiliser. Le reste de ce guide suppose des connaissances opérationnelles de Postman. Pour obtenir de l’aide, reportez-vous au [Documentation Postman](https://learning.getpostman.com/). |
| Références | Le reste de ce guide se familiarisera avec les ressources suivantes :<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentation sur l’API d’administration et de profil de Target](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Documentation de l’API Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></UL> |
