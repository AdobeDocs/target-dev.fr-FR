---
keywords: implémentation, implémentation, at.js, sdk web adobe experience platform, sdk web aep
description: Découvrez comment implémenter pour  [!DNL Adobe Target]  web côté client à l’aide de la bibliothèque JavaScript at [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) ou at.js.
title: Comment mettre en œuvre  [!DNL Target]  pour le web côté client ?
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 315e8fbe67938588c3c9a0135e0cd85fa1f12187
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# Présentation : implémentation de [!DNL Target] pour le web côté client

Dans une implémentation côté client de [!DNL Adobe Target], [!DNL Target] fournit les expériences associées directement à une activité dans le navigateur client. Le navigateur décide de l’expérience à afficher et l’affiche. Avec une implémentation côté client, vous pouvez utiliser un éditeur WYSIWYG, le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou une interface non visuelle, le [compositeur d’expérience basé sur les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), pour créer vos expériences d’activité et de personnalisation.

Pour implémenter [!DNL Target] côté client, vous devez utiliser l’une des bibliothèques JavaScript suivantes :

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  Le [!UICONTROL Adobe Experience Platform Web SDK] vous permet d’interagir avec les différents services du [!DNL Adobe Experience Cloud] (y compris [!DNL Target]) via le [!UICONTROL Adobe Experience Edge Network]. Si vous choisissez de migrer vers le [!UICONTROL Adobe Experience Platform Web SDK], voir [Qu’est-ce qui est [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) ?

* [Bibliothèque JavaScript at.js [!DNL Target]](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  La bibliothèque JavaScript at.js réduit les temps de chargement des pages pour les implémentations web, améliore la sécurité et fournit de meilleures options d’implémentation pour les applications d’une seule page. Si vous choisissez de migrer vers at.js, voir [Fonctionnement d’At.js ](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) et [[!DNL Adobe Target] Développement des compétences : conversations avec les développeurs, migrez mbox.js Adobe Target vers at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Voir [Comparaison de la bibliothèque at.js à la SDK Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} pour en savoir plus sur les différences entre les deux approches d’implémentation.