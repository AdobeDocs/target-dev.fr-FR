---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil unique
description: Transférez des données dans  [!DNL Target]  à l’aide de l’API de mise à jour de profil unique.
title: Comment puis-je importer des données dans  [!DNL Target]  à l’aide de l’[!UICONTROL API de mise à jour de profil unique] ?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
TQID: https://experienceleague.adobe.com/tkh7YEJ9Vr5eMynNYYxYKZZDOXZTVJNxwUSCxiwPfzI
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 160
ht-degree: 3%

---

# [!UICONTROL API de mise à jour de profil individuel]

L’[!DNL Adobe Target] [!UICONTROL API de mise à jour de profil individuel] vous permet d’envoyer une mise à jour de profil à un seul utilisateur. L’API [!UICONTROL Single Profile Update API] est presque identique à l’API [!UICONTROL Bulk Profile Update API], mais un profil de visiteur est mis à jour à la fois, en ligne avec l’appel API plutôt qu’avec un fichier .cvs.

L’API [!UICONTROL Single Profile Update API] et est généralement utilisée lorsqu’une mise à jour doit se produire en relation avec une transaction se produisant dans un canal qui n’a pas implémenté [!DNL Target]. Par exemple, vous souhaitez mettre à jour le profil d’un seul visiteur qui effectue une action hors ligne. Il peut s’agir de contacter un centre d’appel, d’obtenir un prêt, d’utiliser une carte de fidélité en magasin, d’accéder à un kiosque, etc.

Comparez l’[!UICONTROL API de mise à jour de profil unique] à l’[[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## Ressources

Pour obtenir plus d’informations, voir :

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
