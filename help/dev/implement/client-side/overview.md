---
keywords: implémentation, implémentation, at.js, sdk web adobe experience platform, sdk web aep
description: Découvrez comment implémenter pour  [!DNL Adobe Target]  web côté client à l’aide de la bibliothèque JavaScript at [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) ou at.js.
title: Comment mettre en œuvre  [!DNL Target]  pour le web côté client ?
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
TQID: https://experienceleague.adobe.com/KgJyhvTguS8EXbwELaApI1mcs5egnEKHKpnxVYGqT4I
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 233
ht-degree: 28%

---

# Présentation : implémentation de [!DNL Target] pour le web côté client

Dans une implémentation côté client de [!DNL Adobe Target], [!DNL Target] fournit les expériences associées directement à une activité dans le navigateur client. Le navigateur décide de l’expérience à afficher et l’affiche. Avec une implémentation côté client, vous pouvez utiliser un éditeur WYSIWYG, le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou une interface non visuelle, le [compositeur d’expérience basé sur les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), pour créer vos expériences d’activité et de personnalisation.

Pour implémenter [!DNL Target] côté client, vous devez utiliser l’une des bibliothèques JavaScript suivantes :

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  Le [!UICONTROL Adobe Experience Platform Web SDK] vous permet d’interagir avec les différents services du [!DNL Adobe Experience Cloud] (y compris [!DNL Target]) via le [!UICONTROL Adobe Experience Edge Network]. Si vous choisissez de migrer vers le [!UICONTROL Adobe Experience Platform Web SDK], voir [Qu’est-ce qui est [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) ?

* [Bibliothèque JavaScript at.js [!DNL Target]](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  La bibliothèque JavaScript at.js réduit les temps de chargement des pages pour les implémentations web, améliore la sécurité et fournit de meilleures options d’implémentation pour les applications d’une seule page. Si vous choisissez de migrer vers at.js, voir [Fonctionnement d’At.js &#x200B;](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) et [[!DNL Adobe Target] Développement des compétences : conversations avec les développeurs, migrez mbox.js Adobe Target vers at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Voir [Comparaison de la bibliothèque at.js à la SDK Web](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) pour en savoir plus sur les différences entre les deux approches d’implémentation.
