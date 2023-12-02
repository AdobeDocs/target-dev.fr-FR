---
title: API de profil Adobe Target - Aperçu
description: Découvrez comment utiliser les API de profil Adobe Target pour envoyer des données de visiteur à [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 1a1c3d96cf6ef5c337a63fdec8c700da695ff5d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!DNL Adobe Target Profile APIs overview]

Un profil utilisateur contient des informations démographiques et comportementales sur un visiteur de page web, telles que l’âge, le sexe, les produits achetés, la dernière heure de la visite, etc. [!DNL Adobe Target] utilise ces informations pour personnaliser le contenu qu’elles diffusent à chaque visiteur.

Les informations de profil de chaque visiteur sont stockées dans des cookies ou dans des applications tierces.

Si votre page web met en oeuvre la variable [!DNL Target] code ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) ou le [SDK Web Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)), les informations de profil des cookies sont transmises à [!DNL Target] à l’aide des paramètres de profil. [!DNL Target] identifie chaque visiteur de manière unique au moyen d’une `pcID` qu’elle génère dans les cookies du visiteur. Cependant, vous pouvez transmettre des paramètres de profil depuis une application externe par le biais d’appels de mbox à l’aide de `mbox3rdPartyIds`.

Utilisez la variable [!DNL Adobe Target] API de profil lorsque vous disposez de données de profil sur vos visiteurs à envoyer à [!DNL Target] que vous ne pouvez pas ou ne souhaitez pas envoyer dans le cadre de votre intégration basée sur les pages avec [!DNL Target]. Il peut s’agir de données provenant d’un système de gestion de la relation client (CRM) ou de point de vente (POS) qui n’est pas disponible sur la page. Ou ces données peuvent être d’une nature plus sensible qui n’a pas de sens à transmettre sur la page.

Il existe deux manières de mettre à jour les profils via l’API :

* [API de mise à jour de profil individuel](/help/dev/administer/profile-api/profile-single-api.md)
* [Mise à jour du profil en masse par lot](/help/dev/administer/profile-api/profile-bulk-api.md)

La documentation héritée de l’API Profiles se trouve ici : [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}
