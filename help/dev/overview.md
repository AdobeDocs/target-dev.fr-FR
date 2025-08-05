---
keywords: guide du développeur de target ; présentation;accueil
title: Guide du développeur d’Adobe Target
description: Comment mettre en œuvre et administrer  [!DNL Adobe Target]  et utiliser ses API et SDK ?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: 599aa4c965e331bb2681523d50708a03fc933875
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

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

* [référentiel open source Adobe](https://github.com/adobe)
* [Source SDK du nœud Target](https://github.com/adobe/target-nodejs-sdk)
* [Référentiel d’exemples de SDK JS du nœud Target](https://github.com/adobe/target-nodejs-sdk-samples)
* [Source Target Java SDK](https://github.com/adobe/target-java-sdk)
* [Exemple de référentiel Target Java SDK](https://github.com/adobe/target-java-sdk-samples)
* [Implémentation de Target](./before-implement/prepare-to-implement-target.md)
* [Administration de Target](./before-administer/target-api-overview.md)
* [Référentiel GitHub des documents de développement Adobe Target](https://github.com/AdobeDocs/target-developers)
* [Notes De Mise À Jour D’Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Guide de l’utilisateur professionnel d’Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr)

