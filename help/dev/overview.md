---
keywords: guide de développement de target ; présentation ; accueil
title: Guide du développeur d’Adobe Target
description: Comment mettre en oeuvre et administrer  [!DNL Adobe Target] et utiliser ses API et SDK ?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: dadc3804da4592dba4ad88b8c5c9f804c56e232b
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 5%

---

# [!DNL Adobe Target] Guide du développeur

**([Afficher [!DNL Target] mises à jour de la documentation](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html?lang=fr){target=_blank})**

Ce *[!DNL Adobe Target]Guide du développeur* fournit des ressources et des guides à l&#39;intention des développeurs [!DNL Target], y compris la documentation sur les API et le SDK pour la mise en oeuvre et l&#39;administration de [!DNL Target].

>[!NOTE]
>
>En plus de ce guide, les guides [!DNL Adobe Target] suivants sont également disponibles :
>
>* [*[!DNL Adobe Target] Guide du professionnel *](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=fr){target=_blank}
>
>Pour plus d’informations sur la version, voir [Notes de mise à jour de Target (en cours)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=fr){target=_blank} dans le *[!DNL Adobe Target]Guide du praticien de l’entreprise*.

## Prise en main de la mise en oeuvre

**[Avant de mettre en oeuvre](/help/dev/before-implement/considerations-before-you-implement-target.md)** : observations à prendre en compte avant de mettre en oeuvre [!DNL Adobe Target].

## Implémentation côté client

[**SDK Web Adobe Experience Platform**](/help/dev/implement/client-side/aep-web-sdk.md) : [!DNL Adobe Experience Platform Web SDK] permet d’interagir avec les différents services de l’ [!DNL Experience Cloud] (y compris [!DNL Target]) par le [!UICONTROL Adobe Experience Edge Network].

[**Bibliothèque JavaScript at.js**](/help/dev/implement/client-side/overview.md) : la bibliothèque JavaScript at.js réduit les délais de chargement des pages pour les implémentations web, renforce la sécurité et offre de meilleures options d’implémentation pour les applications d’une seule page.

## Mise en oeuvre côté serveur

[**Présentation du SDK Target**](implement/server-side/server-side-overview.md) : commencez avec [!DNL Adobe Target] SDK, y compris la prise de décision sur l’appareil.

[**SDK Node.js**](implement/server-side/node-js/overview.md) : utilisation du SDK [!DNL Target] Node.js.

[**SDK Java**](implement/server-side/java/overview.md) : utilisation du SDK Java [!DNL Target].

[**.NET SDK**](implement/server-side/net/overview.md) : utilisation du SDK .NET [!DNL Target].

[**SDK Python**](implement/server-side/python/overview.md) : utilisation du [!DNL Target] SDK Python.

## Implémentation hybride

[**Déploiement hybride**](implement/hybrid/hybrid-overview.md) : implémentez [!DNL Target] en combinant l’implémentation côté client et l’implémentation côté serveur.

## Implémentation Recommendations

[**Implémentation de Recommendations**](implement/recommendations/recommendations.md) : planifiez et implémentez [!DNL Adobe Target Recommendations].

## Mise en oeuvre des applications mobiles

[**Présentation du SDK AEP Mobile**](implement/mobile/overview.md) : vue d’ensemble de la mise en oeuvre de [!DNL Adobe Target] avec [!DNL Adobe Experience Platform] SDK mobiles.

[**Référence du SDK AEP Mobile**](https://developer.adobe.com/client-sdks/documentation/) : implémentation de [!DNL Adobe Target] avec [!DNL Adobe Experience Platform] SDK mobiles.

## Implémentation par e-mail

[**Présentation des emails**](implement/email/overview.md) : vue d’ensemble de l’implémentation de [!DNL Adobe Target] dans les emails.

## Guides d’API

[**Introduction**](before-administer/target-api-overview.md) : présentation des [!DNL Adobe Target] API.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md) : utilisez les API de diffusion [!DNL Adobe Target] pour diffuser des expériences sur les canaux web et mobiles ainsi que sur des appareils IoT hors navigateur tels qu’une télévision connectée, un kiosque ou un écran numérique en magasin.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md) : utilisez l’API d’administration [!DNL Adobe Target] pour gérer les propriétés, les activités, les audiences, les offres, les propriétés, les rapports, les mbox, les hôtes, les environnements, etc.

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profiles-api.md) : récupérez les informations de profil utilisateur [!DNL Adobe Target].

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports) : récupérez les données des rapports d’activité [!UICONTROL A/B Test] et [!UICONTROL Automated Personalization].

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/) : utilisez l’API [!DNL Target Recommendations].

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md) : gérez les listes bloquées pour définir les fonctionnalités utilisées dans les modèles d’apprentissage automatique [!DNL Target].

[**API Admin Console**](https://developer.adobe.com/umapi/) : gérez les utilisateurs et les droits sur les produits par le biais des API User Management et User Sync Adobe.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=fr) : utilisez l’API [!DNL Adobe Experience Platform Edge Network Server] pour divers cas d’utilisation de la collecte, de la personnalisation, de la publicité et du marketing.

## Ressources

* [Adobe du référentiel open source](https://github.com/adobe)
* [Target Node JS SDK Source](https://github.com/adobe/target-nodejs-sdk)
* [Exemples de SDK JS de noeud Target Repo](https://github.com/adobe/target-nodejs-sdk-samples)
* [Target Java SDK Source](https://github.com/adobe/target-java-sdk)
* [ Exemple de référentiel avec SDK Java Target ](https://github.com/adobe/target-java-sdk-samples)
* [Implémentation de Target](./before-implement/prepare-to-implement-target.md)
* [Administration de Target](./before-administer/target-api-overview.md)
* [Adobe Target Dev Docs GitHub Repo](https://github.com/AdobeDocs/target-developers)
* [Notes de mise à jour d’Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=fr)
* [Guide de l’utilisateur professionnel Adobe Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr)

