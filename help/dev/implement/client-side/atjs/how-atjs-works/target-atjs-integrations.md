---
keywords: intégration d’at.js, intégrations prises en charge, intégrations non prises en charge, intégrations tierces
description: Voir les intégrations prises en charge (et non prises en charge) par [!DNL Adobe Target] at.js, y compris [!UICONTROL Analytics pour Target] (A4T), la variable [!UICONTROL Service d’ID d’Experience Cloud], etc.
title: Quelles intégrations at.js prend-il en charge ?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 64%

---

# Intégrations d’at.js

Informations sur les intégrations courantes de [!DNL Adobe Target] et la prise en charge avec at.js.

Si vous sentez le besoin irrépressible d’une intégration, mais qu’elle n’est pas prise en charge, ni même mentionnée ici, veuillez contacter votre gestionnaire de compte ou votre consultant.

## Intégrations prises en charge

| Intégration | Détails |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | Voir [Adobe Analytics comme source de création de rapports pour Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) |
| [!UICONTROL Profils et audiences] (P&amp;A) | Voir [Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=fr) dans le *Guide de l’utilisateur des services principaux*. |
| [!UICONTROL Service Experience Cloud ID] | Voir la [documentation du Service Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| [!UICONTROL Balises dans Adobe Experience Platform] | [!UICONTROL Balises dans Adobe Experience Platform] représente la nouvelle génération des fonctionnalités de gestion des balises de [!DNL Adobe]. [!UICONTROL Les balises offrent aux clients un moyen simple de déployer et gérer les balises d’analyse, de marketing et de publicité nécessaires pour proposer des expériences client pertinentes. ] Voir [Mise en oeuvre [!DNL Target] Utilisation de Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md). |
| [!UICONTROL Adobe Experience Manager] (AEM) Cloud Service | La variable [!UICONTROL AEM Cloud Service] permet la création de [!UICONTROL Test A/B] et [!UICONTROL Ciblage d’expérience] activités dans le workflow AEM. Prend en charge at.js avec [!UICONTROL Adobe Experience Manager] 6.2 avec FP-11577 (ou version ultérieure). Pour plus d’informations, voir [Intégration à  [!DNL Adobe Target] et sélectionnez votre version d’AEM.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr) |
| [!UICONTROL Fragments d’expérience AEM] | Fragments d’expérience créés dans AEM dans [!DNL Target] Les activités vous permettent de combiner la facilité d’utilisation et la puissance de l’AEM avec de puissantes fonctionnalités d’intelligence automatisée (AI) et d’apprentissage automatique (ML) dans [!DNL Target] pour tester et personnaliser des expériences à grande échelle.  AEM rassemble tous vos contenus et ressources dans un emplacement central pour alimenter votre stratégie de personnalisation. AEM permet de créer facilement du contenu pour les ordinateurs de bureau, les tablettes et les appareils mobiles dans un emplacement sans avoir à écrire de code. Il n’est pas nécessaire de créer des pages pour chaque appareil : AEM ajuste automatiquement chaque expérience à l’aide de votre contenu.  Voir [fragments d’expérience AEM](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html). |

## Intégrations non prises en charge

| Intégration | Détails |
|--- |--- |
| Hérité [!DNL Target] to [!DNL SiteCatalyst] Intégration | Il s’agit de l’intégration qui envoyait des ID de recette et de campagne à [!DNL SiteCatalyst] via l’appel de page pour que vous puissiez créer des rapports dans l’interface utilisateur de [!DNL SiteCatalyst]. Cette fonctionnalité est remplacée par A4T. |
| Hérité [!DNL Target] to [!DNL SiteCatalyst] Intégration | Il s’agit de l’intégration qui effectuait des appels de mbox appelés `"SiteCatalyst: Event"` et `"SiteCatalyst: Purchase"` qui vous permettaient de créer des mesures de succès et des profils d’utilisateur basés sur les evar et les prop. Cette fonctionnalité est remplacée par A4T et Profils et audiences. |
| Hérité [!DNL Audience Manager] (AAM) à [!DNL Target] Intégration | Il s’agit de l’intégration qui effectuait un appel d’API principal pour récupérer des segments AAM et les envoyer ensuite en tant que paramètres de mbox à chaque appel de mbox sur la page. |

## Intégrations tierces

| Intégration | Détails |
|--- |--- |
| Autres gestionnaires de balises | at.js doit fonctionner avec des plates-formes de gestion de balises autres qu’Adobe. Soyez toutefois prudent lorsque vous utilisez des fonctionnalités d’intégration développées par d’autres éditeurs. Leur intégration peut être dépendante de fonctions mbox.js internes qui n’existent plus dans at.js. |
| Fournisseurs de données tiers (Demandbase, BlueKai, API de météo, par exemple) | De nombreux fournisseurs de données tiers habitués à compléter la création de profils utilisateur de Target peuvent être intégrés grâce à l’utilisation de la fonctionnalité d’at.js [Fournisseurs de données.](../atjs-functions/targetglobalsettings.md#data-providers). |
