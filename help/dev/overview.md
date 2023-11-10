---
keywords: guide de développement de target ; présentation ; accueil
title: Guide de développement d’Adobe Target
description: Comment mettre en œuvre et administrer  [!DNL Adobe Target]  et utiliser ses API et SDK ?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: d98c7b890f7456de0676cadce5d6c70bc62d6140
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 14%

---

# Guide du développeur [!DNL Adobe Target]

**([Affichage [!DNL Target] mises à jour de la documentation](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

Ceci *[!DNL Adobe Target]Guide du développeur* fournit des ressources et des guides pour [!DNL Target] développeurs, y compris la documentation sur l’API et le SDK pour implémenter et administrer [!DNL Target].

>[!NOTE]
>
>En plus de ce guide, les guides [!DNL Adobe Target] suivants sont également disponibles :
>
>* [*[!DNL Adobe Target] Guide du praticien professionnel *](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=fr){target=_blank}
>
>Pour plus d’informations sur la version, voir [Notes de mise à jour de Target (actualisées)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} dans le *[!DNL Adobe Target]Guide du praticien professionnel*.

## Prise en main de la mise en oeuvre

**[](/help/dev/before-implement/considerations-before-you-implement-target.md)** Avant l’implémentation : considérations à prendre en compte avant d’implémenter [!DNL Adobe Target].

## Implémentation côté client

[**SDK Web Adobe Experience Platform**](/help/dev/implement/client-side/aep-web-sdk.md): la variable [!DNL Adobe Experience Platform Web SDK] permet d’interagir avec les différents services de la variable [!DNL Experience Cloud] (y compris [!DNL Target]) par l’intermédiaire de la variable [!UICONTROL Adobe Experience Edge Network].

[**Bibliothèque JavaScript at.js de Target**](/help/dev/implement/client-side/overview.md): la bibliothèque JavaScript at.js réduit les délais de chargement des pages pour les implémentations web, renforce la sécurité et offre des options d’implémentation optimisées pour les applications d’une seule page.

## Mise en oeuvre côté serveur

[**Présentation du SDK Target**](implement/server-side/server-side-overview.md): Prise en main de [!DNL Adobe Target] SDK, y compris la prise de décision sur l’appareil.

[**SDK Node.js**](implement/server-side/node-js/overview.md): comment utiliser la variable [!DNL Target] SDK Node.js.

[**SDK Java**](implement/server-side/java/overview.md): comment utiliser la variable [!DNL Target] SDK Java.

[**SDK .NET**](implement/server-side/net/overview.md): comment utiliser la variable [!DNL Target] SDK .NET.

[**SDK Python**](implement/server-side/python/overview.md): comment utiliser la variable [!DNL Target] SDK Python.

## Implémentation hybride

[**Déploiement hybride**](implement/hybrid/hybrid-overview.md): implémentation [!DNL Target] en utilisant une combinaison de mise en oeuvre côté client et côté serveur.

## Implémentation Recommendations

[**Implémentation Recommendations**](implement/recommendations/recommendations.md): Planifier et mettre en oeuvre [!DNL Adobe Target Recommendations].

## Mise en oeuvre des applications mobiles

[**Présentation du SDK AEP Mobile**](implement/mobile/overview.md): présentation de la mise en oeuvre [!DNL Adobe Target] avec [!DNL Adobe Experience Platform] SDK mobiles.

[**Référence du SDK AEP Mobile**](https://developer.adobe.com/client-sdks/documentation/): implémentation [!DNL Adobe Target] avec [!DNL Adobe Experience Platform] SDK mobiles.

## Implémentation par e-mail

[**Présentation des emails**](implement/email/overview.md): présentation de la mise en oeuvre [!DNL Adobe Target] dans les emails.

## Guides d’API

[**Introduction**](before-administer/target-api-overview.md): Présentation de [!DNL Adobe Target] API.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): utilisez la variable [!DNL Adobe Target] API de diffusion permettant de diffuser des expériences sur les canaux web et mobiles ainsi que sur des appareils IoT hors navigateur, tels qu’une télévision connectée, un kiosque ou un écran numérique en magasin.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): utilisez la variable [!DNL Adobe Target] API d’administration pour gérer les propriétés, les activités, les audiences, les offres, les propriétés, les rapports, les mbox, les hôtes, les environnements, etc.

[**[!DNL Target Profile API]**](https://developers.adobetarget.com/api/#profiles): Récupération [!DNL Adobe Target] informations de profil utilisateur.

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): Récupération [!UICONTROL Test A/B] et [!UICONTROL Automated Personalization] données du rapport d’activité.

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/): utilisez la variable [!DNL Target Recommendations] API.

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md): gérez les listes bloquées pour définir les fonctionnalités utilisées dans [!DNL Target] modèles d’apprentissage automatique.

[**API de Admin Console**](https://developer.adobe.com/umapi/): gérez les utilisateurs et les droits des produits par le biais des API User Management et de synchronisation des utilisateurs Adobe.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html): utilisez la variable [!DNL Adobe Experience Platform Edge Network Server] API pour divers cas d’utilisation de la collecte, de la personnalisation, de la publicité et du marketing.

## Ressources

* [Adobe du référentiel open source](https://github.com/adobe)
* [Source du SDK JS du noeud cible](https://github.com/adobe/target-nodejs-sdk)
* [Référentiel d’exemples de SDK JS pour le noeud cible](https://github.com/adobe/target-nodejs-sdk-samples)
* [Source du SDK Java pour Target](https://github.com/adobe/target-java-sdk)
* [Exemple de référentiel pour SDK Java pour Target](https://github.com/adobe/target-java-sdk-samples)
* [Implémentation de Target](./before-implement/prepare-to-implement-target.md)
* [Administration de Target](./before-administer/target-api-overview.md)
* [Documents de développement Adobe Target : référentiel GitHub](https://github.com/AdobeDocs/target-developers)
* [Notes de mise à jour d’Adobe Target](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Guide de l’utilisateur d’Adobe Target Business](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=fr)

