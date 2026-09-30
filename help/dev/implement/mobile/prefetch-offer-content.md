---
keywords: offre, prérécupération, iOS, android, sdk, mobile, sdk mobile, 8 $
description: Utilisez la fonction de prérécupération [!DNL Adobe Target] dans les SDK iOS et Android Mobile pour récupérer le contenu de l’offre le moins de fois possible en mettant en cache les réponses du serveur.
title: Puis-je prérécupérer du contenu d’offre pour les applications mobiles ?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: d051910f-2bda-47ea-a969-6ade9fcd71f1
    internal-label: Implement mobile
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 5d119ccf18b09b3ba864a69642458597f65c754f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 37%
---
# Prérécupération du contenu des offres

La fonctionnalité de prérécupération [!DNL Target] utilise les SDK iOS et Android Mobile pour prévisualiser, autant de fois que possible, le contenu des offres, en mettant en cache les réponses du serveur.

>[!IMPORTANT]
>
>La prise en charge des SDK [!DNL Adobe Mobile] version 4.*x* a pris fin le 31 août 2021 et n’est plus recommandée pour les utilisateurs d’[!DNL Adobe Target] mobile.
>
>[Adobe Experience Platform SDK pour les applications mobiles](https://developer.adobe.com/client-sdks/documentation/){target=_blank} est la solution recommandée pour alimenter les solutions et services [!DNL Adobe Experience Cloud] dans vos applications mobiles.

Ce processus réduit le délai de chargement, évite la multiplication des appels réseau et permet à [!DNL Target] d’être informé de quelle mbox l’utilisateur de l’application mobile a visité. L’ensemble du contenu est récupéré et mis en cache lors de l’appel de prérécupération. Ce contenu sera ensuite récupéré du cache pour tous les appels futurs contenant le contenu mis en cache pour cette mbox spécifique.

Tenez compte des restrictions suivantes lors de l’utilisation de la méthode de prérécupération avec les SDK iOS et Android Mobile :

* Le contenu de la prérécupération n’est pas conservé d’une exécution à l’autre. Il reste dans le cache tant que l’application est active ou jusqu’à ce que la méthode `clearPrefetchCache()` soit invoquée.
* La fonctionnalité de prérécupération n’est pas prise en charge pour les méthodes d’affectation de trafic [!UICONTROL Affectation automatique] et [!UICONTROL Ciblage automatique], pour les types d’activité [!UICONTROL Automated Personalization] ou [!UICONTROL Recommendations], ou pour les offres [Recommendations dans une activité A/B ou XT](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html).

Pour plus d’informations, notamment sur les méthodes de prérécupération, les classes publiques et les échantillons de code, voir :

* **iOS:** [Prérécupération du contenu d’offre dans iOS](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) dans l’*Aide d’iOS SDK pour Mobile Services*.
* **Android:** [Prérécupération du contenu d’offre dans Android](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) dans l’*Aide d’Android SDK pour Mobile Services*.
