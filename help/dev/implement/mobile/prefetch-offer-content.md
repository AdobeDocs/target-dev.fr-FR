---
keywords: offre, prérécupération, iOS, android, sdk, mobile, sdk mobile, 8 $
description: Utilisez la fonction de prérécupération  [!DNL Adobe Target] dans les SDK iOS et Android Mobile pour récupérer le contenu des offres aussi peu de fois que possible en mettant en cache les réponses du serveur.
title: Puis-je prérécupérer le contenu des offres pour les applications mobiles ?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 43%

---

# Prérécupération du contenu des offres

La fonctionnalité de prérécupération [!DNL Target] utilise les SDK iOS et Android Mobile pour prévisualiser, autant de fois que possible, le contenu des offres, en mettant en cache les réponses du serveur.

>[!IMPORTANT]
>
>Prise en charge de la version 4 de [!DNL Adobe Mobile].Les SDK *x* ont pris fin le 31 août 2021 et ne sont plus recommandés pour les utilisateurs mobiles [!DNL Adobe Target].
>
>Le [SDK Adobe Experience Platform pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les services et solutions [!DNL Adobe Experience Cloud] de vos applications mobiles.

Ce processus réduit le délai de chargement, évite la multiplication des appels réseau et permet à [!DNL Target] d’être informé de quelle mbox l’utilisateur de l’application mobile a visité. L’ensemble du contenu est récupéré et mis en cache lors de l’appel de prérécupération. Ce contenu sera ensuite récupéré du cache pour tous les appels futurs contenant le contenu mis en cache pour cette mbox spécifique.

Tenez compte des restrictions suivantes lors de l’utilisation de la méthode de prérécupération avec les SDK mobiles iOS et Android :

* Le contenu de la prérécupération n’est pas conservé d’une exécution à l’autre. Il reste dans le cache tant que l’application est active ou jusqu’à ce que la méthode `clearPrefetchCache()` soit invoquée.
* La fonctionnalité de prérécupération n’est pas prise en charge pour les méthodes d’affectation du trafic [!UICONTROL Auto-Allocate] et [!UICONTROL Auto-Target], pour les types d’activité [!UICONTROL Automated Personalization] ou [!UICONTROL Recommendations], ou pour les offres [recommandations dans une activité A/B ou XT](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html).

Pour plus d’informations, notamment sur les méthodes de prérécupération, les classes publiques et les échantillons de code, voir :

* **iOS :** [ Prérécupération du contenu des offres dans iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) dans l’ *aide du SDK iOS Mobile Services*.
* **Android :** [ Prérécupération du contenu des offres dans Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) dans l’ *aide du SDK Android Mobile Services*.
