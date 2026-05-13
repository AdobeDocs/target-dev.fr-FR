---
keywords: guide du développeur de target ; présentation;accueil
title: Guide du développeur d’Adobe Target
description: Comment mettre en œuvre et administrer  [!DNL Adobe Target]  et utiliser ses API et SDK ?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
TQID: https://experienceleague.adobe.com/lTn4veG9PKL-ZXohH3qv1UH7lpyLfn80nwuxgehXSy0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
  - id: c011fe9c-b94b-4a88-93d8-f2acece55112
  - id: c5abb976-5170-45d6-bcac-66d15d10a4d4
  - id: cd7b6938-5837-4ee0-9790-5840997133d9
  - id: e22d67ea-317b-44f8-abd1-52e07f636ca8
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 501
ht-degree: 11%

---

# Guide de developpement [!DNL Adobe Target]

**([Afficher [!DNL Target] mises à jour de la documentation](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

Ce guide du développeur *[!DNL Adobe Target]* fournit des ressources et des guides pour les développeurs [!DNL Target], y compris la documentation sur l’API et SDK pour implémenter et administrer [!DNL Target].

>[!NOTE]
>
>En plus de ce guide, les guides [!DNL Adobe Target] suivants sont également disponibles :
>
>* Guide [*[!DNL Adobe Target] professionnel *](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr){target=_blank}
>
>* [*[!DNL Adobe Target] Tutoriels *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=fr){target=_blank}
>
>Pour plus d’informations sur les versions, voir [Notes de mise à jour de Target (actualisées)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} dans le Guide *[!DNL Adobe Target]destiné aux professionnels et professionnelles*.

## Prise en main de l’implémentation

**[Avant l’implémentation](/help/dev/before-implement/considerations-before-you-implement-target.md)** : considérations à prendre en compte avant d’implémenter [!DNL Adobe Target].

## Implémentation côté client

[**Adobe Experience Platform Web SDK**](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) : le [!DNL Adobe Experience Platform Web SDK] permet d&#39;interagir avec les différents services de la [!DNL Experience Cloud] ([!DNL Target] compris) à travers le [!UICONTROL Adobe Experience Edge Network].

[**Bibliothèque JavaScript at.js Target**](/help/dev/implement/client-side/overview.md) : la bibliothèque JavaScript at.js réduit les temps de chargement des pages pour les implémentations web, améliore la sécurité et fournit de meilleures options d’implémentation pour les applications d’une seule page.

## Implémentation côté serveur

[**Présentation de Target SDK**](implement/server-side/server-side-overview.md) : prise en main des SDK [!DNL Adobe Target], y compris la prise de décision sur l’appareil.

[**Node.js SDK**](implement/server-side/node-js/overview.md) : utilisation du SDK Node.js [!DNL Target].

[**Java SDK**](implement/server-side/java/overview.md) : utilisation du SDK Java [!DNL Target].

[**.NET SDK**](implement/server-side/net/overview.md) : Utilisation du SDK .NET [!DNL Target].

[**Python SDK**](implement/server-side/python/overview.md) : Utilisation du SDK Python [!DNL Target].

## Implémentation hybride

[**Déploiement hybride**](implement/hybrid/hybrid-overview.md) : implémentez des [!DNL Target] à l’aide d’une combinaison d’implémentation côté client et côté serveur.

## Implémentation de Recommendations

[**Implémentation des recommandations**](implement/recommendations/recommendations.md) : planifiez et implémentez des [!DNL Adobe Target Recommendations].

## Implémentation des applications mobiles

[**Présentation d’AEP Mobile SDK**](implement/mobile/overview.md) : présentation de l’implémentation de [!DNL Adobe Target] avec les SDK mobiles [!DNL Adobe Experience Platform].

[**Référence AEP Mobile SDK**](https://developer.adobe.com/client-sdks/documentation/) : Implémentez [!DNL Adobe Target] avec les SDK mobiles [!DNL Adobe Experience Platform].

## Implémentation par e-mail

[**Présentation des e-mails**](implement/email/overview.md) : présentation de la mise en œuvre de la [!DNL Adobe Target] dans les e-mails.

## Guides d’API

[**Introduction**](before-administer/target-api-overview.md) : présentation des API [!DNL Adobe Target].

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md) : utilisez les API de diffusion [!DNL Adobe Target] pour diffuser des expériences sur des canaux web et mobiles, ainsi que sur des appareils IoT non basés sur un navigateur, tels qu’une télévision connectée, un kiosque ou un écran numérique en magasin.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md) : utilisez l’API [!DNL Adobe Target] Admin pour gérer les propriétés, les activités, les audiences, les offres, les propriétés, les rapports, les mbox, les hôtes, les environnements, etc.

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profiles-api.md) : récupération des informations de profil utilisateur [!DNL Adobe Target].

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports) : récupérez les données des rapports d’activité [!UICONTROL A/B Test] et [!UICONTROL Automated Personalization].

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/) : utiliser l’API [!DNL Target Recommendations].

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md) : gérez les places sur la liste bloquée pour définir les fonctionnalités utilisées dans les modèles de machine learning [!DNL Target].

[**API Admin Console**](https://developer.adobe.com/umapi/) : gérez les utilisateurs et les droits sur les produits via les API Adobe User Management et User Sync.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html) : utilisez l’API [!DNL Adobe Experience Platform Edge Network Server] pour divers cas d’utilisation de la collecte de données, de la personnalisation, de la publicité et du marketing.

## Ressources

* [Référentiel open source Adobe](https://github.com/adobe)
* [Nœud cible JS SDK Source](https://github.com/adobe/target-nodejs-sdk)
* [Référentiel d’exemples JS SDK pour le nœud cible](https://github.com/adobe/target-nodejs-sdk-samples)
* [Source Target Java SDK](https://github.com/adobe/target-java-sdk)
* [Exemple De Référentiel SDK Target](https://github.com/adobe/target-java-sdk-samples)
* [Implémentation de Target](./before-implement/prepare-to-implement-target.md)
* [Administration de Target](./before-administer/target-api-overview.md)
* [Référentiel GitHub des documents de développement Adobe Target](https://github.com/AdobeDocs/target-developers)
* [Notes de mise à jour d’Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Guide de l’utilisateur professionnel d’Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr)

