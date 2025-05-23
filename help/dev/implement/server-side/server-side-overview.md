---
keywords: côté serveur, api, sdk, node.js, nodejs, node js, api de recommandations, api, api, api, server side1
description: Découvrez les  [!DNL Adobe Target]  API de diffusion côté serveur, SDK et  [!DNL Target Recommendations]  API.
title: Où puis-je en savoir plus sur les  [!DNL Target] API de diffusion côté serveur et les SDK ?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: 75af30045684b95d5989b0a1f877ba95bb8cd883
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# Côté serveur : implémentation de [!DNL Target]

Informations sur [!DNL Adobe Target] API de diffusion côté serveur, SDK et [!DNL Target Recommendations] API.

>[!NOTE]
>
>Si votre mise en oeuvre utilise at.js et [!DNL AppMeasurement] côté client, vous devez utiliser les SDK [!UICONTROL Target Delivery API] et côté serveur décrits ci-dessous.
>
>Si votre mise en oeuvre utilise le [!UICONTROL Adobe Experience Platform Web SDK], vous devez utiliser le [[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network Server API]](https://experienceleague.adobe.com/fr/docs/experience-platform/edge-network-server-api/overview){target=_blank}.

Le processus suivant se produit dans une implémentation côté serveur de [!DNL Target] :

1. Un appareil client émet une demande d’expérience via votre serveur.
1. Votre serveur envoie cette demande à [!DNL Target].
1. [!DNL Target] envoie la réponse à votre serveur.
1. Votre serveur décide de l’expérience à diffuser sur l’appareil client pour qu’elle soit rendue.

L’expérience ne doit pas s’afficher dans un navigateur. L’expérience peut s’afficher dans un e-mail ou un kiosque, par le biais d’un assistant vocal ou par le biais d’une autre expérience non visuelle ou d’un périphérique non basé sur un navigateur. Étant donné que votre serveur se trouve entre le client et [!DNL Target], ce type d’implémentation est également idéal si vous avez besoin de plus de contrôle et de sécurité ou si vous avez des processus complexes de serveur principal, que vous souhaitez exécuter sur votre serveur.

>[!NOTE]
>
>Un nouveau visiteur ne peut être initialisé que côté client. Un nouveau visiteur *ne peut pas* être initialisé côté serveur. Cela est dû à l’ECID, qui dépend du cookie demdex tiers et qui doit donc être initialisé via Visitor API.js sur une implémentation dans laquelle le navigateur est impliqué.

Les sections suivantes apportent des informations supplémentaires sur les différentes API et SDK côté serveur :

## API de diffusion côté serveur

Lien : [API de remise côté serveur](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Grâce à l’API de diffusion [!DNL Target], vous pouvez :

* diffuser des expériences sur le web, y compris les canaux SPA et mobiles, ainsi que sur des appareils IoT hors navigateur, tels que des télévisions connectées, des kiosques ou des écrans numériques en magasin ;
* diffuser des expériences à partir de n’importe quelle plateforme ou application côté serveur pouvant effectuer des appels HTTP/s ;
* diffuser des expériences cohérentes et personnalisées à un visiteur quel que soit le canal ou les appareils utilisés par le visiteur pour interagir avec votre entreprise ;
* Mettez en cache les expériences d’un visiteur au cours d’une session sur votre serveur afin d’éviter plusieurs appels d’API, ce qui améliore les performances.
* S’intégrer de manière transparente avec les produits Adobe Experience Cloud, tels qu’Adobe Analytics, Adobe Audience Manager (AAM) et le service d’ID d’Experience Cloud du côté serveur.

## SDK côté serveur

La documentation du SDK côté serveur [!DNL Adobe Target] vous aide à mettre en oeuvre [!DNL Target] sur vos serveurs dans la langue de votre choix.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Grâce aux SDK côté serveur de [!DNL Adobe Target], vous pouvez :

* Exécutez et exécutez **le marquage de fonctionnalités**, **les déploiements** et **les expériences A/B** à **la latence proche de zéro**.
* Diffusez des expériences sur **web**, y compris **SPA**, et des **canaux mobiles**, ainsi que sur des périphériques **Internet of Things (IoT) basés sur un navigateur** comme une télévision connectée, un kiosque ou un écran numérique en magasin.
* Diffusez des **expériences personnalisées basées sur l’apprentissage automatique** à un utilisateur, quel que soit le canal ou l’appareil utilisé par l’utilisateur pour vos activités.
* **Intégrez en toute simplicité aux produits Adobe Experience Cloud** tels que **Adobe Analytics**, **Adobe Audience Manager** et le **service d&#39;ID d&#39;Experience Cloud** du côté serveur.

Consultez la page [Prise en main](sdk-guides/getting-started/getting-started.md) pour savoir comment exécuter une fonction simple signalant un cas d’utilisation par le biais de la [prise de décision sur l’appareil](sdk-guides/on-device-decisioning/overview.md).

Consultez nos [exemples d’applications](sdk-guides/sample-apps/sample-apps.md) pour vous amuser et jouer !

## [!DNL Target Recommendations] API

Lien : [API Target Recommendations](https://developers.adobetarget.com/api/recommendations) et [API Adobe Recommendations](../../before-administer/recs-api/overview.md) - Aperçu

Les API Recommendations vous permettent d’interagir par programmation avec les serveurs de recommandations [!DNL Target]. Ces API peuvent être intégrées à une série de piles d’applications pour exécuter des fonctions que vous exécuteriez généralement via l’interface utilisateur [!DNL Target].
