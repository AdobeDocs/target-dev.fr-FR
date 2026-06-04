---
keywords: implémentation, implémentation, configuration, fournisseurs de données
description: Transférez des données dans à l [!DNL Target] aide des fournisseurs de données.
title: Comment puis-je intégrer des données dans  [!DNL Target]  à l’aide des fournisseurs de données ?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
TQID: https://experienceleague.adobe.com/e8uMaGcACjHiaIT4WSlbKry82mhLHUDTSKmCuuhoWgw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 314
ht-degree: 50%

---

# Fournisseurs de données

Les fournisseurs de données sont une fonctionnalité qui vous permet de transmettre facilement des données de tiers à [!DNL Adobe Target].

>[!NOTE]
>
>Les fournisseurs de données nécessitent at.js version 1.3 ou ultérieure.

## Format

Le paramètre `window.targetGlobalSettings.dataProviders` est un tableau de fournisseurs de données.

Pour plus d’informations sur la structure de chaque fournisseur de données, voir [Fournisseurs de données](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Exemples de cas d’utilisation

Collectez des données auprès d’un tiers (par exemple, un service météorologique, une plateforme de gestion des données, ou même votre propre service Web). Vous pouvez ensuite utiliser ces données pour créer des audiences, cibler du contenu et enrichir le profil du visiteur.

## Avantages de la méthode

Ce paramètre permet aux clients de collecter des données auprès de fournisseurs de données tiers, tels que Demandbase, BlueKai et des services personnalisés, et de transmettre les données à [!DNL Target] en tant que paramètres de mbox dans la requête de mbox globale.

Cette fonction prend en charge la collecte des données en provenance de fournisseurs multiples via des requêtes synchrones et asynchrones.

Cette approche permet de gérer aisément le scintillement du contenu de la page par défaut, tout en incluant des délais d’attente indépendants pour chaque fournisseur afin de limiter l’impact sur les performances de la page

## Avertissements

Si les fournisseurs de données ajoutés à `window.targetGlobalSettings.dataProviders` sont asynchrones, ils sont exécutés en parallèle. La requête de l’API visiteur est exécutée en parallèle des fonctions ajoutées à `window.targetGlobalSettings.dataProviders` pour permettre un temps d’attente minimum.

at.js ne tente pas de mettre les données en cache. Si le fournisseur de données extrait les données en une seule fois, il doit s’assurer que les données sont mises en cache et que, lorsque la fonction du fournisseur est appelée, les données du cache sont envoyées pour le second appel.

## Exemples de code

Vous trouverez plusieurs exemples dans la section [Fournisseurs de données](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Liens vers des informations pertinentes

Documentation : [Fournisseurs de données](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Vidéos de formation :

* [Utilisation des fournisseurs de données dans Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Implémenter les fournisseurs de données dans Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
