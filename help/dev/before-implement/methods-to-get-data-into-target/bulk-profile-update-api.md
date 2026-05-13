---
keywords: implémentation, implémentation, configuration, configuration, api de mise à jour de profil en masse
description: Insérez des données dans à l [!DNL Target] aide de l’[!UICONTROL Bulk Profile Update API] .
title: Comment puis-je intégrer des données dans  [!DNL Target]  à l’aide de l’[!UICONTROL Bulk Profile Update API] ?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
TQID: https://experienceleague.adobe.com/vBcIsBR6wwYr7MbRh7UJvt71ULDEq6iXVZ5spZlif-0
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
source-wordcount: 221
ht-degree: 7%

---

# API de mise à jour des profils en masse

Le [!UICONTROL Bulk Profile Update API] [!DNL Adobe Target] vous permet de mettre à jour en bloc les profils utilisateur de plusieurs visiteurs d’un site web à l’aide d’un fichier de commandes.

À l’aide de l’[!UICONTROL Bulk Profile Update API] , vous pouvez envoyer des données de profil de visiteur détaillées sous la forme de paramètres de profil à de nombreux utilisateurs à [!DNL Target] de n’importe quelle source externe. Les sources externes peuvent inclure les systèmes de gestion de la relation client (CRM) ou de point de vente (POS), qui ne sont généralement pas disponibles sur une page web.

Mettez le [!UICONTROL Bulk Profile Update API] en contraste avec le [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] contre la [!UICONTROL Bulk Profile Update API]

Cette option est similaire à [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md), à quelques différences près :

* [!UICONTROL Customer attributes] utiliser un chargement FTP. Le [!UICONTROL Target Bulk Profile Update API] utilise une API HTTP POST.
* [!UICONTROL Customer attribute] données peuvent être partagées avec [!DNL Analytics]. L’[!UICONTROL Bulk Profile Update] n’est utilisable qu’en [!DNL Target].
* [!UICONTROL Customer attributes] prise en charge de la création d’un profil pour un utilisateur [!DNL Target] n’a pas encore vu.
   * [!UICONTROL Bulk Profile Update API] v2 : il n’est pas nécessaire de spécifier toutes les valeurs de paramètre pour chaque `pcId`. Les profils sont créés pour tout `pcId` ou `mbox3rdPartyId` introuvable dans [!DNL Target].
   * [!UICONTROL Bulk Profile Update API] v1 : l’[!UICONTROL Bulk Profile Update API] met uniquement à jour les profils de [!DNL Target] existants. Si vous utilisez v1, les profils ne sont pas créés pour les `pcIds` ou les `mbox3rdPartyIds` manquants.
* [!UICONTROL Customer attributes] nécessitent l’utilisation de l’[!UICONTROL Experience Cloud ID] (ECID) et d’un identifiant source, tel que l’identifiant CRM ou l’identifiant de fidélité.
* Le [!UICONTROL Bulk Profile Update API] nécessite l’identifiant TNT ou l’`mbox3rdPartyId` .
* Vous ne pouvez pas envoyer les caractères suivants dans `mbox3rdPartyID` : signe plus (+) et barre oblique (/).

## Ressources

Pour obtenir plus d’informations, voir :

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)