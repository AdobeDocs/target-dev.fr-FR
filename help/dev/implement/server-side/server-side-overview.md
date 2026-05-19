---
keywords: côté serveur, côté serveur, api, sdk, node.js, nodejs, node js, api recommendations, api, api, api, côté serveur1
description: Découvrez les API  [!DNL Adobe Target]  diffusion côté serveur, les SDK et les API  [!DNL Target Recommendations] .
title: Où puis [!DNL Target] je en savoir plus sur les API et les SDK de diffusion côté serveur ?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
TQID: https://experienceleague.adobe.com/x5WKb9Eenz2bw-idOnxlpWdtiivTx05n38sNXEt3DNc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a6cc21b9-1a36-4fa6-9c61-4acd04d9c88c
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 603
ht-degree: 12%

---

# Implémentation de [!DNL Target] côté serveur

Informations sur [!DNL Adobe Target] API de diffusion côté serveur, les SDK et les API [!DNL Target Recommendations].

>[!NOTE]
>
>Si votre implémentation utilise at.js et [!DNL AppMeasurement] côté client, vous devez utiliser les SDK [!UICONTROL Target Delivery API] et côté serveur décrits ci-dessous.
>
>Si votre implémentation utilise le [!UICONTROL Adobe Experience Platform Web SDK] , vous devez utiliser le [!UICONTROL Edge Network Server API][&#128279;](https://experienceleague.adobe.com/fr/docs/experience-platform/edge-network-server-api/overview){target=_blank} [!UICONTROL Adobe Experience Platform] .

Le processus suivant se produit dans une implémentation côté serveur de [!DNL Target] :

1. Un appareil client émet une demande d’expérience via votre serveur.
1. Votre serveur envoie cette demande à [!DNL Target].
1. [!DNL Target] envoie la réponse à votre serveur.
1. Votre serveur décide de l’expérience à diffuser à l’appareil client pour qu’il la restitue.

L’expérience n’a pas besoin de s’afficher dans un navigateur. L’expérience peut s’afficher dans un e-mail ou kiosque, par l’intermédiaire d’un assistant vocal ou d’une autre expérience non visuelle ou sur un appareil non basé sur un navigateur. Étant donné que votre serveur se trouve entre le client et [!DNL Target], ce type d’implémentation est également idéal si vous avez besoin de plus de contrôle et de sécurité ou si vous avez des processus complexes de serveur principal, que vous souhaitez exécuter sur votre serveur.

>[!NOTE]
>
>Un nouveau visiteur ne peut être initialisé que côté client. Un nouveau visiteur *impossible* ne peut pas être initialisé côté serveur. Cela est dû à l’ECID, qui dépend du cookie demdex tiers et doit donc être initialisé via Visitor API.js sur une implémentation où le navigateur est impliqué.

Les sections suivantes apportent des informations supplémentaires sur les différents SDK et API côté serveur :

## API de diffusion côté serveur

Lien : [API de diffusion côté serveur](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Grâce à l’API de diffusion [!DNL Target], vous pouvez :

* Diffusez des expériences sur le web, y compris les SPA et les canaux mobiles, ainsi que sur les appareils IoT non basés sur un navigateur, tels que les télévisions connectées, les kiosques ou les écrans numériques en magasin.
* Diffusez des expériences à partir de n’importe quelle plateforme ou application côté serveur pouvant effectuer des appels HTTP/s.
* Proposez des expériences cohérentes et personnalisées à un visiteur, quel que soit le ou les canaux utilisés pour interagir avec votre entreprise.
* Mettez en cache des expériences pour un visiteur au cours d’une session sur votre serveur afin d’éviter plusieurs appels d’API, ce qui offre de meilleures performances.
* Intégrez facilement aux produits Adobe Experience Cloud, tels qu’Adobe Analytics, Adobe Audience Manager (AAM) et le service Experience Cloud ID du côté serveur.

## SDK côté serveur

La documentation SDK côté serveur [!DNL Adobe Target] vous aide à implémenter [!DNL Target] sur vos serveurs dans la langue de votre choix.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Grâce aux SDK côté serveur d’[!DNL Adobe Target], vous pouvez :

* Exécutez et exécutez **indicateurs de fonctionnalité**, **déploiements** et **expériences A/B** à **latence quasi nulle**.
* Diffusez des expériences sur **web**, y compris les **SPA** et **canaux mobiles**, ainsi que sur des appareils **Internet des objets (IoT) non basés sur un navigateur** tels qu’une télévision connectée, un kiosque ou un écran numérique en magasin.
* **Proposez des expériences personnalisées basées sur le machine learning (ML** à un utilisateur, quel que soit le canal ou l’appareil qu’il a utilisé pour interagir avec votre entreprise.
* **Intégrez facilement des produits Adobe Experience Cloud** tels que **Adobe Analytics**, **Adobe Audience Manager** et le **service Experience Cloud ID** côté serveur.

Consultez la page [Prise en main](sdk-guides/getting-started/getting-started.md) pour savoir comment exécuter un cas d’utilisation simple de marquage des fonctionnalités via [la prise de décision sur l’appareil](sdk-guides/on-device-decisioning/overview.md).

Consultez notre [Sample Apps](sdk-guides/sample-apps/sample-apps.md) pour vous amuser et jouer !

## [!DNL Target Recommendations] API

Lien : [API Target Recommendations](https://developers.adobetarget.com/api/recommendations) et [Présentation de l’API Adobe Recommendations](../../before-administer/recs-api/overview.md).

Les API Recommendations vous permettent d’interagir par programmation avec [!DNL Target] serveurs de recommandations. Ces API peuvent être intégrées à une plage de piles d’applications pour exécuter des fonctions que vous exécuteriez normalement via l’interface utilisateur d’[!DNL Target].
