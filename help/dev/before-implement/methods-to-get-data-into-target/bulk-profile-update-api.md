---
keywords: implémentation, implémentation, configuration, configuration, api de mise à jour de profil en masse
description: Transférez des données dans à l [!DNL Target] aide de l’API [!UICONTROL Bulk Profile Update].
title: Comment puis-je importer des données dans à l [!DNL Target] aide de l’API [!UICONTROL Bulk Profile Update] ?
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
source-wordcount: 284
ht-degree: 5%

---

# API de mise à jour des profils en masse

L’[!DNL Adobe Target] [!UICONTROL API de mise à jour de profil en bloc] vous permet de mettre à jour en bloc les profils d’utilisateurs de plusieurs visiteurs sur un site web à l’aide d’un fichier par lots.

Grâce à l’[!UICONTROL API de mise à jour de profil en bloc], vous pouvez envoyer des données de profil de visiteur détaillées sous la forme de paramètres de profil à de nombreux utilisateurs à [!DNL Target] de n’importe quelle source externe. Les sources externes peuvent inclure les systèmes de gestion de la relation client (CRM) ou de point de vente (POS), qui ne sont généralement pas disponibles sur une page web.

Comparez l’[!UICONTROL API de mise à jour de profil en bloc] à l’[[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Attributs du client] par rapport à l’[!UICONTROL API de mise à jour de profil en bloc]

Cette option est similaire aux [[!UICONTROL attributs du client]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) avec quelques différences :

* [!UICONTROL Attributs du client] utilisez un chargement FTP. L’API [!UICONTROL Target Bulk Profile Update] utilise une API HTTP POST.
* [!UICONTROL Attributs du client] les données peuvent être partagées avec [!DNL Analytics]. La [!UICONTROL &#x200B; Mise à jour de profil en bloc &#x200B;] n’est utilisable que dans [!DNL Target].
* [!UICONTROL Attributs du client] prise en charge de la création d’un profil pour un utilisateur [!DNL Target] n’a pas encore vu.
   * [!UICONTROL API de mise à jour de profil en masse] v2 : vous n’avez pas besoin de spécifier toutes les valeurs de paramètre pour chaque `pcId`. Les profils sont créés pour tout `pcId` ou `mbox3rdPartyId` introuvable dans [!DNL Target].
   * [!UICONTROL API de mise à jour de profil en masse] v1 : l’[!UICONTROL API de mise à jour de profil en masse] met uniquement à jour les profils [!DNL Target] existants. Si vous utilisez v1, les profils ne sont pas créés pour les `pcIds` ou les `mbox3rdPartyIds` manquants.
* Les [!UICONTROL attributs du client] nécessitent l’utilisation du [!UICONTROL Experience Cloud ID] (ECID) et d’un identifiant source, tel que l’identifiant CRM ou l’identifiant de fidélité.
* L’[!UICONTROL API de mise à jour de profil en masse] nécessite l’identifiant TNT ou le `mbox3rdPartyId` .
* Vous ne pouvez pas envoyer les caractères suivants dans `mbox3rdPartyID` : signe plus (+) et barre oblique (/).

## Ressources

Pour obtenir plus d’informations, voir :

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)