---
keywords: implémenter, implémentation, at.js, sdk web adobe experience platform, sdk web aep
description: Découvrez comment mettre en oeuvre  [!DNL Adobe Target] pour le web côté client à l’aide de [!DNL Adobe Experience Platform Web SDK]  (SDK Web AEP) ou de la bibliothèque JavaScript at.js.
title: Comment mettre en oeuvre  [!DNL Target] pour le web côté client
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 2d2a593df661c7e6c6e6384af6042e8aa4575fdb
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# Présentation : implémentation de [!DNL Target] pour le web côté client

Dans une implémentation côté client de [!DNL Adobe Target], [!DNL Target] fournit les expériences associées directement à une activité dans le navigateur client. Le navigateur décide de l’expérience à afficher et l’affiche. Avec une implémentation côté client, vous pouvez utiliser un éditeur WYSIWYG, le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=fr) (VEC) ou une interface non visuelle, le [compositeur d’expérience basé sur les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=fr), pour créer vos expériences d’activité et de personnalisation.

Pour implémenter [!DNL Target] côté client, vous devez utiliser l’une des bibliothèques JavaScript suivantes :

* [SDK Web Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)

  Le [!UICONTROL Adobe Experience Platform Web SDK] vous permet d’interagir avec les différents services de l’ [!DNL Adobe Experience Cloud] (dont [!DNL Target]) par l’intermédiaire de l’ [!UICONTROL Adobe Experience Edge Network]. Si vous choisissez de migrer vers le [!UICONTROL Adobe Experience Platform Web SDK], voir [Qu&#39;est-ce que [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md) ?

* [[!DNL Target] Bibliothèque JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  La bibliothèque JavaScript at.js réduit les délais de chargement des pages pour les implémentations web, renforce la sécurité et offre des options d’implémentation optimisées pour les applications d’une seule page. Si vous choisissez de migrer vers at.js, reportez-vous aux sections [Fonctionnement d’at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) et [[!DNL Adobe Target] Skill Builder : Chat du développeur, mbox.js d’Adobe Target vers at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Voir [Comparaison de la bibliothèque at.js avec le SDK Web](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} pour en savoir plus sur les différences entre les deux approches d’implémentation.