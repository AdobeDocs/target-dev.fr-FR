---
keywords: application mobile, questions fréquentes, faq, application mobile target
description: Afficher les questions fréquentes et leurs réponses [!DNL Adobe Target] pour les applications mobiles.
title: Questions fréquentes [!DNL About Target] pour les applications mobiles ?
feature: Implement Mobile
exl-id: 06cae3de-83a4-4018-a832-66fb292a1d0f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---

# [!DNL Target] FAQ pour les applications mobiles

Liste des questions fréquentes sur [!DNL Target] pour les applications mobiles.

## Dois-je utiliser des balises dans [!DNL Adobe Experience Platform] pour déployer le SDK ou puis-je le déployer sans utiliser Launch ?

Le SDK est disponible sur la page [Adobe Marketing Cloud git](https://github.com/Adobe-Marketing-Cloud/acp-sdks/){target=_blank}. If you don't use [tags in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr){target=_blank}, vous devez gérer votre propre fichier de paramètres et le gérer dans votre application.

## Quels SDK sont disponibles aujourd’hui ?

Les SDK Adobe Experience Platform Mobile prennent actuellement en charge iOS, Android et React. Pour plus d’informations, voir [Guide des SDK Mobile Adobe Experience Cloud Platform](https://experienceleague.adobe.com/docs/mobile.html?lang=fr){target=_blank}.

## Quelle est la fréquence de la fonction basée sur l’emplacement, en termes de vérification de la latitude et de la longitude ?

Voir [Documentation sur Adobe Places](https://experienceleague.adobe.com/docs/places/using/home.html){target=_blank} pour plus d’informations.

## Ai-je besoin d’at.js pour que les SDK Adobe Experience Platform Mobile fonctionnent ?

Non, vous n’avez pas besoin d’at.js pour utiliser les SDK mobiles. at.js est la variable [!DNL Target] Bibliothèque JavaScript pour les sites web. Les SDK Adobe Experience Platform Mobile sont destinés aux applications mobiles.

## Is [!DNL Target] Fonctionnalité mobile de [!DNL Adobe Target] SKU du produit Premium uniquement ?

Non. Pour [!DNL Adobe Target Standard] clients, vous pouvez utiliser nos SDK mobiles pour [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] (XT) uniquement avec la fonction [!DNL Target Standard] Module complémentaire Applications mobiles. Si vous souhaitez utiliser [!UICONTROL Recommendations] ou fonctions optimisées par l’IA dans l’application mobile, vous avez besoin d’une [Adobe Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium) licence.

## Existe-t-il une intégration d’application mobile entre [!DNL Adobe Experience Manager] (AEM) et [!DNL Target] activités mobiles ?

Actuellement, vous pouvez partager JSON. [Fragments d’expérience](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html){target=_blank} de l’AEM à [!DNL Target] et il est possible de les utiliser ensuite dans une activité d’application mobile.
