---
title: Mettre à jour les profils
description: Découvrez comment utiliser les API de profil Adobe Target pour envoyer des données de visiteur à  [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---

# Mettre à jour les profils

Un profil utilisateur contient des informations démographiques et comportementales sur un visiteur de page web, telles que l’âge, le sexe, les produits achetés, la dernière heure de la visite, etc. [!DNL Adobe Target] utilise ces informations pour personnaliser le contenu qu’il diffuse à chaque visiteur.

Les informations de profil de chaque visiteur sont stockées dans des cookies ou dans des applications tierces.

Si votre page web implémente le code [!DNL Target] ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) ou le [SDK web Adobe Experience Platform](/help/dev/implement/client-side/aep-web-sdk.md)), les informations de profil des cookies sont transmises à [!DNL Target] à l’aide de paramètres de profil. [!DNL Target] identifie chaque visiteur de manière unique via un `pcID` généré dans les cookies du visiteur. Cependant, vous pouvez transmettre des paramètres de profil à partir d’une application externe par le biais d’appels de mbox à l’aide de `mbox3rdPartyIds`.

Utilisez les API de profil [!DNL Adobe Target] lorsque vous disposez de données de profil sur vos visiteurs à envoyer à [!DNL Target] que vous ne pouvez pas ou ne souhaitez pas envoyer dans le cadre de votre intégration basée sur les pages avec [!DNL Target]. Il peut s’agir de données provenant d’un système de gestion de la relation client (CRM) ou de point de vente (POS) qui n’est pas disponible sur la page. Ou ces données peuvent être d’une nature plus sensible qui n’a pas de sens à transmettre sur la page.

Il existe deux manières de mettre à jour les profils via l’API :

* [API de mise à jour de profil individuel](/help/dev/administer/profile-api/profile-single-api.md)
* [Mise à jour du profil en masse par lot](/help/dev/administer/profile-api/profile-bulk-api.md)
