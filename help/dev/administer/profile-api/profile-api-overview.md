---
title: Mettre à jour les profils
description: Découvrez comment utiliser les API de profil Adobe Target pour envoyer des données de visiteur à  [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 3b0bc0b67800ed4b1da6ba2bfa05c677147a78ba
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---

# Mettre à jour les profils

Un profil utilisateur contient des informations démographiques et comportementales sur le visiteur d’une page web, telles que son âge, son sexe, les produits achetés, l’heure de sa dernière visite, etc. [!DNL Adobe Target] utilise ces informations pour personnaliser le contenu proposé à chaque visiteur.

Les informations de profil de chaque visiteur sont stockées dans des cookies ou dans des applications tierces.

Si votre page web implémente le code de [!DNL Target] ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md) ou [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)), les informations de profil des cookies sont transmises à [!DNL Target] à l’aide des paramètres de profil. [!DNL Target] identifie chaque visiteur de manière unique par le biais d’un `pcID` qu’il génère dans les cookies du visiteur. Cependant, vous pouvez transmettre des paramètres de profil à partir d’une application externe par le biais d’appels de mbox à l’aide de `mbox3rdPartyIds`.

Utilisez les API de profil [!DNL Adobe Target] lorsque vous disposez de données de profil sur vos visiteurs à envoyer à des [!DNL Target] que vous ne pouvez pas ou ne souhaitez pas envoyer dans le cadre de votre intégration basée sur les pages d’[!DNL Target]. Il peut s’agir de données provenant d’un système de gestion de la relation client (GRC) ou d’un système de point de vente (PDV) qui ne sont pas disponibles sur la page. Il se peut également que ces données soient de nature plus sensible et qu’il ne soit pas logique de les transmettre à la page.

Il existe deux façons de mettre à jour les profils à l’aide de l’API :

* [API de mise à jour de profil individuel](/help/dev/administer/profile-api/profile-single-api.md)
* [Mise à jour des profils en masse par lots](/help/dev/administer/profile-api/profile-bulk-api.md)
