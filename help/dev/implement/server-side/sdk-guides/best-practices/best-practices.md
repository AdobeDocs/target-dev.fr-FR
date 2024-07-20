---
title: Bonnes pratiques relatives à l’utilisation de la prise de décision sur l’appareil
description: Découvrez les bonnes pratiques lors de l’utilisation de [!UICONTROL on-device decisioning] dans [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Bonnes pratiques

[!DNL Adobe] recommande les bonnes pratiques suivantes lors de l&#39;utilisation de [!UICONTROL on-device decisioning] :

## Bonnes pratiques lorsque la méthode de prise de décision est &quot;sur appareil&quot;

Lors de l’utilisation de la méthode de prise de décision &quot;sur l’appareil&quot;, l’artefact est téléchargé lorsque le visiteur charge la page web pour la première fois. Toute qualification d’activité qui doit se produire au premier chargement de page (sans cache) n’a lieu qu’après le téléchargement complet de l’artefact. Vous pouvez suivre certaines bonnes pratiques pour vous assurer que les qualifications d’activité se produisent rapidement pour un nouveau visiteur anonyme.

* Désactivez les activités compatibles &quot;On-Device&quot; qui ne sont pas destinées à être dans l’artefact.
* Si vous disposez de Target Premium, vous pouvez utiliser [properties/workspaces](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=fr) pour créer différents fichiers d’artefacts pour différents espaces de travail.
* Si vos fichiers d’artefact deviennent très volumineux pour des raisons légitimes, vous pouvez utiliser la méthode de prise de décision &quot;hybride&quot;. Cette méthode vous permet de télécharger l’artefact en parallèle et tous les appels de l’API Target passent par le fil jusqu’à ce que l’artefact ait été téléchargé. Pour en savoir plus sur cette approche, consultez la section des bonnes pratiques sur le mode de prise de décision &quot;hybride&quot; ci-dessous.
* Si vous disposez d’une application d’une seule page (SPA), [!DNL Adobe] vous recommande de charger et d’initialiser at.js avant de charger le fichier JavaScript principal de votre application lors du premier chargement de la page. Cette approche lance le téléchargement de l’artefact beaucoup plus tôt, ce qui accélère le rendu de l’expérience.

## Bonnes pratiques lorsque la méthode de prise de décision est &quot;hybride&quot;

Lorsque vous utilisez la méthode de prise de décision &quot;hybride&quot;, l’artefact est téléchargé en parallèle. Tant que l’artefact n’est pas téléchargé, tout appel d’API [!DNL Target] passe par le réseau même si les &quot;emplacements&quot; sont compatibles avec l’appareil. Ce comportement est la valeur par défaut de tous les appels `getOffers()` et fournit les meilleures performances dans la plupart des situations. Si vous modifiez le comportement par défaut de `getOffers()` en définissant `decisioningMethod` sur `on-device`, suivez ces bonnes pratiques pour éviter les erreurs et assurer les meilleures performances.

* Si vous décidez d’appeler `getOffers()` avec `decisioningMethod` comme `on-device` lorsque la page se charge pour la première fois, vous devez le faire dans le gestionnaire d’événements at.js &quot;ARTIFACT_DOWNLOAD_SUCCEEDED&quot; pour éviter les erreurs. Si votre artefact est très volumineux, les &quot;emplacements&quot; utilisant cette approche ne sont rendus qu’après son téléchargement complet, ce qui peut retarder le rendu de l’expérience. [!DNL Adobe] recommande d’utiliser rarement cette approche. Suivez les bonnes pratiques pour réduire la taille des artefacts dans la section des bonnes pratiques &quot;On Device&quot; ci-dessus lors de l’utilisation de cette approche.
