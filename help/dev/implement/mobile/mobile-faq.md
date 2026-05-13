---
keywords: application mobile, questions fréquentes, faq, application mobile target
description: Consultez les questions fréquentes et leurs réponses sur pour  [!DNL Adobe Target]  applications mobiles.
title: Quelles sont les questions fréquentes relatives  [!DNL About Target]  applications mobiles ?
feature: Implement Mobile
exl-id: 06cae3de-83a4-4018-a832-66fb292a1d0f
TQID: https://experienceleague.adobe.com/DvyEuK-o-3qAJDKVI3tSe9ZirSQa0my6vbIhJQP9EU4
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: d051910f-2bda-47ea-a969-6ade9fcd71f1
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 310
ht-degree: 3%

---

# FAQ sur [!DNL Target] pour les applications mobiles

Liste des questions fréquentes sur [!DNL Target] pour les applications mobiles.

## Dois-je utiliser les balises dans [!DNL Adobe Experience Platform] pour déployer le SDK ou puis-je déployer le SDK sans utiliser Launch ?

Le SDK est disponible sur le git [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud/acp-sdks/){target=_blank}. Si vous n’utilisez pas de balises [ dans Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr){target=_blank}, vous devez gérer votre propre fichier de paramètres et le gérer dans votre application.

## Quels SDK sont disponibles aujourd’hui ?

Les SDK mobiles Adobe Experience Platform prennent actuellement en charge iOS, Android et React. Pour plus d’informations, consultez le guide des SDK mobiles de Adobe Experience Cloud Platform [](https://experienceleague.adobe.com/docs/mobile.html?lang=fr){target=_blank}.

## Quelle est la fréquence de la fonction de localisation, en termes de vérification de la latitude et de la longitude ?

Pour plus d’informations](https://experienceleague.adobe.com/docs/places/using/home.html){target=_blank} consultez la documentation sur Adobe Places [.

## Ai-je besoin d’at.js pour que les SDK mobiles Adobe Experience Platform fonctionnent ?

Non, vous n’avez pas besoin d’at.js pour utiliser les SDK mobiles. at.js est la bibliothèque JavaScript [!DNL Target] pour les sites web. Les SDK Adobe Experience Platform Mobile sont destinés aux applications mobiles.

## [!DNL Target] Mobile est-il une fonctionnalité [!DNL Adobe Target] SKU du produit Premium uniquement ?

Non. Pour les clients [!DNL Adobe Target Standard], vous pouvez utiliser nos SDK Mobile pour les activités [!UICONTROL A/B Test] et [!UICONTROL Experience Targeting] (XT) uniquement avec le module complémentaire de l’application mobile [!DNL Target Standard]. Si vous souhaitez utiliser des fonctionnalités [!UICONTROL Recommendations] ou basées sur l’IA dans l’application mobile, vous avez besoin d’une licence [Adobe Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium).

## Existe-t-il une intégration d’application mobile entre les activités [!DNL Adobe Experience Manager] (AEM) et [!DNL Target] ?

Actuellement, vous pouvez partager des JSON [fragments d’expérience](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html){target=_blank} d’AEM vers [!DNL Target] et il est possible de les utiliser ensuite dans une activité d’application mobile.
