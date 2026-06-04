---
keywords: intégration d’at.js, intégrations prises en charge, intégrations non prises en charge, intégrations tierces
description: Consultez les intégrations prises en charge (et non prises en charge) par [!DNL Adobe Target] at.js, y compris [!UICONTROL Analytics for Target] (A4T), le [!UICONTROL service Experience Cloud ID], etc.
title: Quelles intégrations at.js prend-il en charge ?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
TQID: https://experienceleague.adobe.com/RdcxcIGufo2O5aKPqIAJVINkCzZ1Brcv8EXiX1n4buc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e6ff21d3-dec6-4298-8590-7c749fffaf78
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 530
ht-degree: 50%

---

# Intégrations d’at.js

Informations sur les intégrations courantes de [!DNL Adobe Target] et la prise en charge avec at.js.

Si vous sentez le besoin irrépressible d’une intégration, mais qu’elle n’est pas prise en charge, ni même mentionnée ici, veuillez contacter votre gestionnaire de compte ou votre consultant.

## Intégrations prises en charge

| Intégration | Détails |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | [Adobe Analytics comme source de création de rapports pour Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=fr) |
| [!UICONTROL Profils Et Audiences] (P&amp;A) | Voir [Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=fr) dans le *Guide de l’utilisateur des services principaux*. |
| [!UICONTROL Service Experience Cloud ID] | Voir la [documentation du Service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr). |
| [!UICONTROL &#x200B; Balises dans Adobe Experience Platform &#x200B;] | [!UICONTROL Les balises dans Adobe Experience Platform] représentent la nouvelle génération des fonctionnalités de gestion des balises de [!DNL Adobe]. Les [!UICONTROL &#x200B; Balises &#x200B;] offrent aux clients un moyen simple de déployer et de gérer les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Voir [Implémentation [!DNL Target] à l’aide de Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
|  (AEM) Cloud Service | Le [!UICONTROL Cloud Service AEM] permet la création d’activités [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] dans le workflow AEM. Prend en charge at.js avec  6.2 avec FP-11577 (ou version ultérieure). Pour plus d’informations, voir [Intégration à [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr) et sélectionnez votre version d’AEM. |
| [!UICONTROL Fragments d’expérience AEM] | Les fragments d’expérience créés dans AEM dans les activités [!DNL Target] vous permettent d’associer la facilité d’utilisation et la puissance d’AEM à de puissantes fonctionnalités d’intelligence artificielle (IA) et de machine learning (ML) dans le [!DNL Target] de tester et de personnaliser des expériences à grande échelle.  AEM rassemble tous vos contenus et ressources dans un emplacement central pour alimenter votre stratégie de personnalisation. AEM permet de créer facilement du contenu pour les ordinateurs de bureau, les tablettes et les appareils mobiles dans un emplacement sans avoir à écrire de code. Il n’est pas nécessaire de créer des pages pour chaque appareil : AEM ajuste automatiquement chaque expérience à l’aide de votre contenu.  Voir [fragments d’expérience AEM](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=fr). |

## Intégrations non prises en charge

| Intégration | Détails |
|--- |--- |
| [!DNL Target] hérités de l’intégration [!DNL SiteCatalyst] | Il s’agit de l’intégration qui a envoyé des identifiants de campagne et de recette à [!DNL SiteCatalyst] via l’appel de page afin que vous puissiez créer des rapports dans l’interface utilisateur de [!DNL SiteCatalyst]. Cette fonctionnalité est remplacée par A4T. |
| [!DNL Target] hérités de l’intégration [!DNL SiteCatalyst] | Il s’agit de l’intégration qui effectuait des appels de mbox appelés `"SiteCatalyst: Event"` et `"SiteCatalyst: Purchase"` qui vous permettaient de créer des mesures de succès et des profils d’utilisateur basés sur les evar et les prop. Cette fonctionnalité est remplacée par A4T et Profils et audiences. |
| Intégration des [!DNL Audience Manager] hérités (AAM) à [!DNL Target] | Il s’agit de l’intégration qui effectuait un appel d’API front-end pour récupérer des segments AAM et les envoyer ensuite en tant que paramètres de mbox à chaque appel de mbox sur la page. |

## Intégrations tierces

| Intégration | Détails |
|--- |--- |
| Autres gestionnaires de balises | at.js doit fonctionner avec des plates-formes de gestion de balises autres qu’Adobe. Soyez toutefois prudent lorsque vous utilisez des fonctionnalités d’intégration développées par d’autres éditeurs. Leur intégration peut être dépendante de fonctions mbox.js internes qui n’existent plus dans at.js. |
| Fournisseurs de données tiers (Demandbase, BlueKai, API de météo, par exemple) | De nombreux fournisseurs de données tiers utilisés pour compléter le profilage des utilisateurs de Target peuvent être intégrés à l’aide de la fonctionnalité at.js [Fournisseurs de données](../atjs-functions/targetglobalsettings.md#data-providers). |
