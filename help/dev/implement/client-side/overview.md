---
keywords: implémenter, implémentation, at.js, sdk web adobe experience platform, sdk web aep
description: Découvrez comment implémenter [!DNL Adobe Target] pour le web côté client à l’aide de la variable [!DNL Adobe Experience Platform Web SDK] (SDK Web AEP) ou la bibliothèque JavaScript at.js.
title: Comment mettre en oeuvre [!DNL Target] pour le Web côté client
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 2d2a593df661c7e6c6e6384af6042e8aa4575fdb
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# Présentation : implémentation [!DNL Target] pour le web côté client

Dans une implémentation côté client de [!DNL Adobe Target], [!DNL Target] fournit les expériences associées directement à une activité dans le navigateur client. Le navigateur décide de l’expérience à afficher et l’affiche. Avec une implémentation côté client, vous pouvez utiliser un éditeur WYSIWYG, le [compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) ou une interface non visuelle, le [compositeur d’expérience basé sur les formulaires](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), pour créer vos expériences d’activité et de personnalisation.

Pour mettre en oeuvre [!DNL Target] côté client, vous devez utiliser l’une des bibliothèques JavaScript suivantes :

* [SDK Web Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)

  La variable [!UICONTROL Adobe Experience Platform Web SDK] permet d’interagir avec les différents services de la variable [!DNL Adobe Experience Cloud] (y compris [!DNL Target]) par l’intermédiaire de la variable [!UICONTROL Adobe Experience Edge Network]. Si vous choisissez de migrer vers le [!UICONTROL Adobe Experience Platform Web SDK], voir [Présentation [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk.md).

* [[!DNL Target] Bibliothèque JavaScript at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  La bibliothèque JavaScript at.js réduit les délais de chargement des pages pour les implémentations web, renforce la sécurité et offre des options d’implémentation optimisées pour les applications d’une seule page. Si vous choisissez de migrer vers at.js, voir [Fonctionnement d’at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) et [[!DNL Adobe Target] Skill Builder : Chat du développeur, migrez le fichier mbox.js Adobe Target vers at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).


Voir [Comparaison de la bibliothèque at.js avec le SDK Web](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank} pour en savoir plus sur les différences entre les deux approches de mise en oeuvre.