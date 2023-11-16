---
keywords: implémentation, implémentation, configuration, configuration, mise à jour de profil par lot
description: Obtenir des données dans [!DNL Target] à l’aide de l’API de mise à jour des profils en masse.
title: Comment obtenir des données dans [!DNL Target] Utilisation de l’API de mise à jour de profil en bloc ?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 3ae2391dea9994c0ddc1df39d74cccf6e067c1a4
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 59%

---

# API de mise à jour des profils en masse

Via l’API, envoyez un fichier .csv à [!DNL Adobe Target] avec des mises à jour du profil du visiteur pour de nombreux visiteurs. Chaque profil du visiteur peut être mis à jour avec plusieurs attributs de profil internes à la page en un seul appel.

Cette option est similaire aux attributs du client avec quelques différences :

* Les attributs du client utilisent un transfert FTP pendant que la variable [!UICONTROL API de mise à jour du profil Target en bloc] utilise une API de POST HTTP.
* Les données d’attributs du client peuvent être partagées avec [!DNL Analytics]. [!UICONTROL La mise à jour des profils en masse peut uniquement être utilisée dans Target.]
* Les attributs du client prennent en charge la création d’un profil pour un utilisateur [!DNL Target] n&#39;a pas encore vu. L’API de mise à jour des profils en masse met à jour les [!DNL Target] profils uniquement.
* Les attributs du client nécessitent l’utilisation de l’identifiant Experience Cloud (ECID) et d’un identifiant source, tel que l’identifiant CRM ou l’identifiant de fidélité.
* L’API de mise à jour des profils en masse requiert soit l’ID TNT, soit l’ID `mbox3rdPartyId`.
* Vous ne pouvez pas envoyer les caractères suivants dans `mbox3rdPartyID` : signe plus (+) et barre oblique (/).

## Format

Le fichier .csv doit faire référence à chaque visiteur par son intermédiaire. [!DNL Target] PCID ou `mbox3rdPartyId`. L’Experience Cloud ID (ECID) n’est pas pris en charge. Tous les attributs/valeurs de profil sont créés et mis à jour via l’API. Les détails relatifs au format sont disponibles dans la documentation de l’API.

## Exemples de cas d’utilisation

Votre logiciel de gestion de la relation client ou autre système interne stocke des données importantes sur vos visiteurs que vous souhaitez constamment mettre à jour dans Target, sans exposer les données du profil dans l’implémentation de votre page.

## Avantages de la méthode

Nombre d’attributs de profil illimité.

Les attributs de profil envoyés via le site peuvent être mis à jour via l’API et vice versa.

## Avertissements

La taille du fichier de traitement par lot doit être inférieure à 50 Mo. En outre, le nombre total de lignes ne doit pas dépasser 500 000 lignes par téléchargement.

Les mises à jour surviennent généralement en moins d’une heure, mais peuvent prendre jusqu’à 24 heures pour être répercutées.

Le nombre de lignes pouvant être téléchargées en lots ultérieurs sur une période de 24 heures est illimité. Cependant, le processus d’assimilation peut être ralenti pendant les heures ouvrables pour s’assurer que les autres processus s’exécutent efficacement.

Les [appels de mise à jour de lots V2](https://developers.adobetarget.com/api/#updating-profiles) consécutifs non espacés par des appels mbox pour le même identifiant tiers remplacent les propriétés mises à jour au premier appel de mise à jour de lots.

## Exemples de code

Voir [Mise à jour des profils](https://developers.adobetarget.com/api/#updating-profiles).

### Liens vers les informations pertinentes

[Mise à jour des profils](https://developers.adobetarget.com/api/#updating-profiles)
