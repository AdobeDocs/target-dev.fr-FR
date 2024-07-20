---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil par lot api
description: Récupérez des données dans  [!DNL Target] à l’aide de [!UICONTROL Bulk Profile Update API].
title: Comment obtenir des données dans  [!DNL Target] à l’aide de [!UICONTROL Bulk Profile Update API] ?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 7%

---

# API de mise à jour des profils en masse

Le [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API] permet de mettre à jour en masse les profils utilisateur de plusieurs visiteurs d’un site web à l’aide d’un fichier de commandes.

Grâce à [!UICONTROL Bulk Profile Update API], vous pouvez facilement envoyer des données détaillées sur le profil du visiteur sous la forme de paramètres de profil pour de nombreux utilisateurs à [!DNL Target] à partir de n’importe quelle source externe. Les sources externes peuvent inclure des systèmes de gestion de la relation client (CRM) ou de point de vente (POS), qui ne sont généralement pas disponibles sur une page web.

Comparez le [!UICONTROL Bulk Profile Update API] à [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL Customer attributes] et [!UICONTROL Bulk Profile Update API]

Cette option est similaire à [[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) avec quelques différences :

* [!UICONTROL Customer attributes] utilisez un transfert FTP. [!UICONTROL Target Bulk Profile Update API] utilise une API de POST HTTP.
* [!UICONTROL Customer attribute] les données peuvent être partagées avec [!DNL Analytics]. [!UICONTROL Bulk Profile Update] ne peut être utilisé que dans [!DNL Target].
* [!UICONTROL Customer attributes] La prise en charge de la création d&#39;un profil pour un utilisateur [!DNL Target] n&#39;a pas encore été vue.
   * [!UICONTROL Bulk Profile Update API] v2 : vous n’avez pas besoin de spécifier toutes les valeurs de paramètre pour chaque `pcId`. Les profils sont créés pour tout `pcId` ou `mbox3rdPartyId` introuvable dans [!DNL Target].
   * [!UICONTROL Bulk Profile Update API] v1 : [!UICONTROL Bulk Profile Update API] met à jour les profils [!DNL Target] existants uniquement. Si vous utilisez la version 1, les profils ne sont pas créés pour `pcIds` ou `mbox3rdPartyIds` manquants.
* [!UICONTROL Customer attributes] nécessite l’utilisation de [!UICONTROL Experience Cloud ID] (ECID) et d’un ID source, tel que l’ID de gestion de la relation client ou l’ID de fidélité.
* [!UICONTROL Bulk Profile Update API] nécessite l&#39;identifiant TNT ou `mbox3rdPartyId`.
* Vous ne pouvez pas envoyer les caractères suivants dans `mbox3rdPartyID` : signe plus (+) et barre oblique (/).

## Ressources

Pour obtenir plus d’informations, voir :

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)