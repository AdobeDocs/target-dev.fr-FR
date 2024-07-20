---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil unique
description: Récupérez des données dans  [!DNL Target]  à l’aide de l’API de mise à jour de profil unique.
title: Comment obtenir des données dans  [!DNL Target] à l’aide de [!UICONTROL Single Profile Update API] ?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 3%

---

# [!UICONTROL Single Profile Update API]

[!DNL Adobe Target] [!UICONTROL Single Profile Update API] permet d&#39;envoyer une mise à jour de profil pour un utilisateur unique. [!UICONTROL Single Profile Update API] est presque identique à [!UICONTROL Bulk Profile Update API], mais un profil du visiteur est mis à jour à la fois, en ligne avec l’appel API au lieu d’un fichier .cvs.

Le [!UICONTROL Single Profile Update API] et est généralement utilisé lorsqu’une mise à jour doit se produire par rapport à une transaction survenant dans un canal qui n’a pas implémenté [!DNL Target]. Par exemple, vous souhaitez mettre à jour le profil d’un visiteur unique qui effectue une action hors ligne. Les actions peuvent inclure l’accès à un centre d’appel, le financement d’un prêt, l’utilisation d’une carte de fidélité en magasin, l’accès à un kiosque, etc.

Comparez le [!UICONTROL Single Profile Update API] à [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## Ressources

Pour obtenir plus d’informations, voir :

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
