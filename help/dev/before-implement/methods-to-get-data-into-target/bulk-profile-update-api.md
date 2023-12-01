---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil par lot api
description: Obtenir des données dans [!DNL Target] en utilisant la variable [!UICONTROL API de mise à jour des profils en masse].
title: Comment obtenir des données dans [!DNL Target] En utilisant la variable [!UICONTROL API de mise à jour des profils en masse]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 24%

---

# API de mise à jour des profils en masse

Via l’API, envoyez un fichier .csv à [!DNL Adobe Target] avec des mises à jour du profil du visiteur pour de nombreux visiteurs. Chaque profil du visiteur peut être mis à jour avec plusieurs attributs de profil internes à la page en un seul appel.

Cette option est similaire à [!UICONTROL attributs du client] avec quelques différences :

* [!UICONTROL Attributs du client] utilisez un transfert FTP. La variable [!UICONTROL API de mise à jour du profil Target en bloc] utilise une API de POST HTTP.
* [!UICONTROL Attribut du client] les données peuvent être partagées avec [!DNL Analytics]. La mise à jour des profils en masse peut uniquement être utilisée dans [!DNL Target].
* [!UICONTROL Attributs du client] prise en charge de la création d’un profil pour un utilisateur [!DNL Target] n&#39;a pas encore vu.
   * [!UICONTROL API de mise à jour des profils en masse] v2 : vous n’avez pas besoin de spécifier toutes les valeurs de paramètre pour chaque `pcId`. Les profils sont créés pour tous les `pcId` ou `mbox3rdPartyId` qui est introuvable dans [!DNL Target].
   * [!UICONTROL API de mise à jour des profils en masse] v1 : la variable [!UICONTROL API de mise à jour des profils en masse] mises à jour existantes [!DNL Target] profils uniquement. Si vous utilisez la version 1, les profils ne sont pas créés pour manquants. `pcIds` ou `mbox3rdPartyIds`.
* [!UICONTROL Attributs du client] nécessite l’utilisation de la fonction [!UICONTROL Identifiant Experience Cloud] (ECID) et l’utilisation d’un ID source, tel que l’ID de gestion de la relation client ou l’ID de fidélité.
* La variable [!UICONTROL API de mise à jour des profils en masse] nécessite soit l’identifiant TNT, soit le `mbox3rdPartyId`.
* Vous ne pouvez pas envoyer les caractères suivants dans `mbox3rdPartyID` : signe plus (+) et barre oblique (/).

## Format

Le fichier .csv doit faire référence à chaque visiteur par l’intermédiaire de son [!DNL Target] PCID ou `mbox3rdPartyId`. La variable [!UICONTROL Identifiant Experience Cloud] (ECID) n’est pas pris en charge. Tous les attributs/valeurs de profil sont créés et mis à jour via l’API. Les détails relatifs au format sont disponibles dans la documentation de l’API.

## Exemples de cas d’utilisation

Votre système de gestion de la relation client ou autre système interne stocke des données importantes sur vos visiteurs que vous souhaitez mettre à jour de manière cohérente dans [!DNL Target], sans exposer les données de profil dans l’implémentation de votre page.

## Avantages de la méthode

* Nombre d’attributs de profil illimité.
* Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et de la manière inverse.

## Avertissements

* La taille du fichier de traitement par lot doit être inférieure à 50 Mo. En outre, le nombre total de lignes ne doit pas dépasser 500 000 lignes par téléchargement.
* Les mises à jour surviennent généralement en moins d’une heure, mais peuvent prendre jusqu’à 24 heures pour être répercutées.
* Le nombre de lignes que vous pouvez transférer sur une période de 24 heures dans les lots suivants n’est pas limité. Cependant, le processus d’assimilation peut être ralenti pendant les heures ouvrables pour s’assurer que les autres processus s’exécutent efficacement.
* Appels de mise à jour de lots V2 consécutifs sans appels de mbox intermédiaires pour le même `thirdPartyIds` remplacez les propriétés mises à jour lors du premier appel de mise à jour de lot.

## Ressources

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)