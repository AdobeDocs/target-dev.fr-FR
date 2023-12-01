---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil par lot api
description: Obtenir des données dans [!DNL Target] en utilisant la variable [!UICONTROL API de mise à jour des profils en masse].
title: Comment obtenir des données dans [!DNL Target] En utilisant la variable [!UICONTROL API de mise à jour des profils en masse]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 43f4fb8345a77ccb0e112fe196e7e0944cc468c9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 4%

---

# API de mise à jour des profils en masse

La variable [!DNL Adobe Target] [!UICONTROL API de mise à jour des profils en masse] permet de mettre à jour les profils utilisateur de plusieurs visiteurs d’un site web en masse à l’aide d’un fichier de commandes.

En utilisant la variable [!UICONTROL API de mise à jour des profils en masse], vous pouvez facilement envoyer des données détaillées sur le profil du visiteur sous la forme de paramètres de profil à de nombreux utilisateurs. [!DNL Target] de n’importe quelle source externe. Les sources externes peuvent inclure des systèmes de gestion de la relation client (CRM) ou de point de vente (POS), qui ne sont généralement pas disponibles sur une page web.

## [!UICONTROL Attributs du client] versus [!UICONTROL API de mise à jour des profils en masse]

Cette option est similaire à [!UICONTROL attributs du client] avec quelques différences :

* [!UICONTROL Attributs du client] utilisez un transfert FTP. La variable [!UICONTROL API de mise à jour du profil Target en bloc] utilise une API de POST HTTP.
* [!UICONTROL Attribut du client] les données peuvent être partagées avec [!DNL Analytics]. La variable [!UICONTROL Mise à jour du profil en bloc] est utilisable uniquement dans [!DNL Target].
* [!UICONTROL Attributs du client] prise en charge de la création d’un profil pour un utilisateur [!DNL Target] n&#39;a pas encore vu.
   * [!UICONTROL API de mise à jour des profils en masse] v2 : vous n’avez pas besoin de spécifier toutes les valeurs de paramètre pour chaque `pcId`. Les profils sont créés pour tous les `pcId` ou `mbox3rdPartyId` qui est introuvable dans [!DNL Target].
   * [!UICONTROL API de mise à jour des profils en masse] v1 : la variable [!UICONTROL API de mise à jour des profils en masse] mises à jour existantes [!DNL Target] profils uniquement. Si vous utilisez la version 1, les profils ne sont pas créés pour manquants. `pcIds` ou `mbox3rdPartyIds`.
* [!UICONTROL Attributs du client] nécessite l’utilisation de la fonction [!UICONTROL Identifiant Experience Cloud] (ECID) et l’utilisation d’un ID source, tel que l’ID de gestion de la relation client ou l’ID de fidélité.
* La variable [!UICONTROL API de mise à jour des profils en masse] nécessite soit l’identifiant TNT, soit le `mbox3rdPartyId`.
* Vous ne pouvez pas envoyer les caractères suivants dans `mbox3rdPartyID` : signe plus (+) et barre oblique (/).

## Ressources

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)