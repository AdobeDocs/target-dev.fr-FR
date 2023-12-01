---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil unique
description: Obtenir des données dans [!DNL Target] à l’aide de l’API de mise à jour de profil unique.
title: Comment obtenir des données dans [!DNL Target] En utilisant la variable [!UICONTROL API de mise à jour de profil unique]?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 81bff85a9d1fe28ca267c471a470da95568fd06d
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 2%

---

# [!UICONTROL API de mise à jour de profil unique]

La variable [!DNL Adobe Target] [!UICONTROL API de mise à jour de profil unique] vous permet d’envoyer une mise à jour de profil pour un utilisateur unique. La variable [!UICONTROL API de mise à jour de profil unique] est presque identique au [!UICONTROL API de mise à jour des profils en masse], mais un profil du visiteur est mis à jour à la fois, en ligne avec l’appel API au lieu d’un fichier .cvs.

La variable [!UICONTROL API de mise à jour de profil unique] et est généralement utilisé lorsqu’une mise à jour doit se produire par rapport à une transaction survenant dans un canal qui n’a pas été implémenté [!DNL Target]. Par exemple, vous souhaitez mettre à jour le profil d’un visiteur unique qui effectue une action hors ligne. Les actions peuvent inclure l’accès à un centre d’appel, le financement d’un prêt, l’utilisation d’une carte de fidélité en magasin, l’accès à un kiosque, etc.

Pour obtenir plus d’informations, voir :

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
