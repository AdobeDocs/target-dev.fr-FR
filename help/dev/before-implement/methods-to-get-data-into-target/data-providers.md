---
keywords: implémentation, implémentation, configuration, configuration, fournisseurs de données
description: Récupérez des données dans  [!DNL Target]  à l’aide des fournisseurs de données.
title: Comment obtenir des données dans  [!DNL Target] à l’aide de fournisseurs de données ?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 55%

---

# Fournisseurs de données

Les fournisseurs de données sont une fonctionnalité qui vous permet de transmettre facilement des données provenant de tiers à [!DNL Adobe Target].

>[!NOTE]
>
>Les fournisseurs de données requièrent at.js 1.3 ou version ultérieure.

## Format

Le paramètre `window.targetGlobalSettings.dataProviders` est un tableau de fournisseurs de données.

Pour plus d’informations sur la structure de chaque fournisseur de données, voir [Fournisseurs de données](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Exemples de cas d’utilisation

Collectez des données auprès d’un tiers (par exemple, un service météorologique, une plateforme de gestion des données, ou même votre propre service Web). Vous pouvez ensuite utiliser ces données pour créer des audiences, cibler du contenu et enrichir le profil du visiteur.

## Avantages de la méthode

Ce paramètre permet aux clients de collecter des données auprès de fournisseurs de données tiers, tels que Demandbase, BlueKai et les services personnalisés, et de transmettre les données à [!DNL Target] en tant que paramètres mbox dans la requête de mbox globale.

Cette fonction prend en charge la collecte des données en provenance de fournisseurs multiples via des requêtes synchrones et asynchrones.

Cette approche permet de gérer aisément le scintillement du contenu de la page par défaut, tout en incluant des délais d’attente indépendants pour chaque fournisseur afin de limiter l’impact sur les performances de la page

## Avertissements

Si les fournisseurs de données ajoutés à `window.targetGlobalSettings.dataProviders` sont asynchrones, ils sont exécutés en parallèle. La requête de l’API visiteur est exécutée en parallèle avec des fonctions ajoutées à `window.targetGlobalSettings.dataProviders` pour permettre un temps d’attente minimal.

at.js ne tente pas de mettre en cache les données. Si le fournisseur de données extrait les données en une seule fois, il doit s’assurer que les données sont mises en cache et que, lorsque la fonction du fournisseur est appelée, les données du cache sont envoyées pour le second appel.

## Exemples de code

Vous trouverez plusieurs exemples dans la section [Fournisseurs de données](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Liens vers les informations pertinentes

Documentation : [Fournisseurs de données](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Vidéos de formation :

* [Utilisation des fournisseurs de données dans Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Implémenter les fournisseurs de données dans Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
