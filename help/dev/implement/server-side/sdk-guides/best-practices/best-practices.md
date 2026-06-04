---
title: Bonnes pratiques relatives à l’utilisation de la prise de décision sur l’appareil
description: Découvrez les bonnes pratiques d’utilisation de la [!UICONTROL prise de décision sur l’appareil] dans  [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
TQID: https://experienceleague.adobe.com/GgVJaAal4uS1RqpCK3wNCVwPjAOaXzjXNV7EoqWhwcY
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 399
ht-degree: 3%

---

# Bonnes pratiques

[!DNL Adobe] recommande les bonnes pratiques suivantes lors de l’utilisation de la [!UICONTROL prise de décision sur l’appareil] :

## Bonnes pratiques lorsque la méthode de prise de décision est « sur l’appareil »

Lorsque vous utilisez « sur l’appareil » comme méthode de prise de décision, l’artefact est téléchargé lorsque le visiteur charge la page web pour la première fois. Toute qualification d’activité qui doit se produire au premier chargement de page (pas de cache) se produit uniquement après le téléchargement complet de l’artefact. Vous pouvez suivre certaines bonnes pratiques pour vous assurer que les qualifications d’activité se produisent rapidement pour un nouveau visiteur anonyme.

* Désactivez les activités compatibles avec « Sur l’appareil » qui ne sont pas censées se trouver dans l’artefact.
* Si vous disposez de Target Premium, vous pouvez utiliser [properties/workspaces](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=fr) pour créer différents fichiers d’artefacts pour différents espaces de travail.
* Si vos fichiers d’artefact deviennent très volumineux pour des raisons légitimes, vous pouvez utiliser la méthode de prise de décision « hybride ». Cette méthode vous permet de télécharger l’artefact en parallèle et tous les appels de l’API Target passent par le câble jusqu’à ce que l’artefact ait été téléchargé. Lisez la section des bonnes pratiques sur le mode de prise de décision « hybride » ci-dessous pour en savoir plus sur cette approche.
* Si vous disposez d’une application d’une seule page (SPA), [!DNL Adobe] vous recommande de charger et d’initialiser at.js avant de charger le fichier JavaScript principal de votre application lors du chargement de la première page. Cette approche démarre le téléchargement de l’artefact beaucoup plus tôt, offrant ainsi un rendu d’expérience plus rapide.

## Bonnes pratiques lorsque la méthode de prise de décision est « hybride »

Lorsque vous utilisez « hybride » comme méthode de prise de décision, l’artefact est téléchargé en parallèle. Jusqu’à ce que l’artefact soit téléchargé, tous les appels d’API [!DNL Target] passent par le réseau même si les « emplacements » sont compatibles avec l’appareil. Ce comportement est le comportement par défaut pour tous les appels `getOffers()` et offre les meilleures performances dans la plupart des situations. Si vous modifiez le comportement par défaut d’`getOffers()` en définissant la `decisioningMethod` sur `on-device`, suivez ces bonnes pratiques pour éviter les erreurs et garantir des performances optimales.

* Si vous décidez d’appeler `getOffers()` avec des `decisioningMethod` telles que `on-device` lors du premier chargement de la page, vous devez le faire dans le gestionnaire d’événements at.js « ARTIFACT_DOWNLOAD_SUCCEEDED » pour éviter les erreurs. Si votre artefact est très volumineux, tous les « emplacements » utilisant cette approche sont rendus uniquement après le téléchargement complet de l’artefact, ce qui peut retarder le rendu de l’expérience. [!DNL Adobe] vous recommande d’utiliser rarement cette approche. Suivez les bonnes pratiques pour réduire la taille des artefacts dans la section « Bonnes pratiques sur l’appareil » ci-dessus lors de l’utilisation de cette approche.
